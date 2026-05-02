# Generic Operational Runbook — AI Agent Execution in Cowork / Claude Desktop

> **What this is**: A field-tested reference for AI agents (Claude, Codex, Gemini, etc.) operating inside the Cowork / Claude Desktop environment on this specific Windows host machine.
>
> **What this is NOT**: Theory, documentation, or speculation. Every pattern in this file was empirically verified on this machine (2026-03-12). If a command is listed, it ran successfully. If a limitation is listed, it was hit in production.
>
> **How to use**: Copy this file into any new project's `dev/` directory. Fill in the `[PLACEHOLDERS]` in §1a and §1d with your project's actual values. Everything else is machine-level and works as-is.

> **This project's instance** (`Adam-AI-Instructions`): §1d filled 2026-05-02 (session Claude_20260502_1711). GCP-related rows are NA — this repo is a docs/prompts share, no cloud integration. §5j added 2026-05-02 documents a stale inode cache exception encountered in this project. All other content remains the generic field-tested reference.

---

## 1. Environment Summary

### 1a. Windows Host (via MCP Windows Shell)

| Component | Path / Value |
|---|---|
| Git | `C:\Program Files\Git\cmd\git.exe` (v2.41.0) |
| Python | `C:\Python313\python.exe` (v3.13.1) |
| Node.js | `C:\Program Files\nodejs\node.exe` (v22.14.0) |
| gcloud CLI | `C:\Program Files (x86)\google-cloud-sdk\bin\gcloud.cmd` (v495.0.0) |
| Project root | `[WINDOWS_PROJECT_ROOT]` — e.g. `C:\Users\adam\_claude_desktop\Work_RnD\MyProject` |
| GitHub credentials | Windows Credential Manager (only accessible from Windows side) |
| gcloud credentials | Application Default Credentials (only accessible from Windows side) |

### 1b. Linux VM (Cowork Sandbox)

| Component | Value |
|---|---|
| OS | Ubuntu 22.04 (kernel 6.8) |
| Git | `/usr/bin/git` (v2.34.1) |
| Node.js | `/usr/bin/node` (v22.22.0) |
| npm | `/usr/bin/npm` (v10.9.4) |
| Python | `/usr/bin/python3` (v3.10.12) |
| gcloud | **NOT available** |
| sudo | **NOT available** (no new privileges flag) |
| apt-get | **NOT available** (cannot install system packages) |
| Project mount | `/sessions/<session-name>/mnt/<FolderName>` (FUSE virtiofs, rw) |

> The `<session-name>` changes every Cowork session. Use `pwd` to discover the current mount path at session start.

### 1c. Cross-VM Permission Boundary (CRITICAL)

These are hard facts, not configuration options. They cannot be changed.

| Operation | Linux VM | Windows MCP Shell | Windows FileSystem tool |
|---|---|---|---|
| Read files on mount | ✅ | ✅ | ✅ |
| Create / write files on mount | ✅ | ✅ | ✅ |
| **Delete files on mount** | ❌ `Operation not permitted` | ✅ | ✅ |
| git status / log / diff | ✅ | ✅ (often MCP timeout) | — |
| git add / commit | ✅ (⚠️ lock risk, see §5d) | ✅ | — |
| git push / pull | ❌ No credentials | ✅ (via Node.exe) | — |
| Delete `.git/*.lock` | ❌ | ✅ | ✅ |
| Run `node` / `npm` scripts | ✅ | ✅ | — |
| Run `gcloud` | ❌ Not installed | ✅ | — |
| Run `pip install` | ✅ (`--break-system-packages`) | ✅ | — |

**Key consequences**:
1. Any file created by a failed VM operation (e.g. `.git/index.lock`) **cannot** be cleaned up from the VM — must use Windows.
2. All credential-dependent operations (git push, gcloud, cloud APIs) **must** run from the Windows side.
3. Temp files written by Windows processes take **10-60 seconds** to appear on the VM mount (FUSE sync delay).

### 1d. Project-Specific Values (Fill In Per Project)

```
WINDOWS_PROJECT_ROOT = D:\_Adam_Projects\KnowledgeDB\_Prompt_Template\Adam-AI-Instructions
VM_PROJECT_MOUNT     = /sessions/<session-name>/mnt/Adam-AI-Instructions
GIT_REMOTE_BRANCH    = origin main
GCP_PROJECT_ID       = NA — 本 repo 為 docs/prompts 分享庫,無 GCP 整合
GCS_BUCKET           = NA
AR_REPO              = NA
CLOUD_RUN_JOB        = NA
CLOUD_RUN_REGION     = NA
```

> Filled 2026-05-02 (Claude_20260502_1711). Re-fill GCP rows if cloud integration is added later.

---

## 2. Three-Tier Execution Strategy (MANDATORY)

The MCP Windows Shell has a **hard 60-second timeout** that cannot be extended or configured.
Every command must be classified into a tier before execution.

| Tier | When to use | Method | Timeout risk |
|---|---|---|---|
| **Tier 1: VM Direct** | node/npm scripts, git read/add/commit, file I/O, Python scripts (no cloud) | Linux VM Bash tool | **None** (no MCP involvement) |
| **Tier 2: MCP Node.exe** | git push/pull, short gcloud queries (<30s), short Windows-only commands | `& "C:\Program Files\nodejs\node.exe" -e "..."` in MCP PowerShell | **Low** (Node.exe starts fast, returns within seconds) |
| **Tier 3: MCP Python subprocess** | Long-running operations (>60s): Cloud Build, Cloud Run Job, large GCS transfers | `& "C:\Python313\python.exe" -c "..."` → write result to file → poll | **Expected** (MCP *will* report timeout; read result file afterward) |

### Decision Rules

```
Can the command run entirely on the VM?
  ├─ YES → Tier 1 (VM Direct)
  └─ NO (needs Windows credentials / tools)
       ├─ Will it complete in <30 seconds? → Tier 2 (Node.exe)
       └─ Will it take >60 seconds? → Tier 3 (Python subprocess + file output)
```

### 2a. Tier 1 — VM Direct

```bash
cd /sessions/<session-name>/mnt/<FolderName>
node my-script.js           # run any node script
npm test                     # run tests
npm install                  # install dependencies
git status --short           # check status
git add <files>              # stage files
git commit -m "message"      # commit (⚠️ check for locks first — see §5d)
python3 my-script.py         # run Python scripts (no cloud dependencies)
```

**Limitations**: No gcloud, no GitHub credentials, cannot delete files, cannot delete .git lock files.

### 2b. Tier 2 — MCP Node.exe (Preferred for Short Windows Commands)

Template:
```powershell
& "C:\Program Files\nodejs\node.exe" -e "
const{execSync}=require('child_process');
const r=execSync('<COMMAND>', {
  cwd:'<WINDOWS_PROJECT_ROOT_ESCAPED>',
  encoding:'utf-8',
  timeout:30000
});
console.log(r)
"
```

> Replace `<WINDOWS_PROJECT_ROOT_ESCAPED>` with the Windows path using `\\` separators.

Example — git push:
```powershell
& "C:\Program Files\nodejs\node.exe" -e "const{execSync}=require('child_process');try{const r=execSync('git push origin master',{cwd:'<WINDOWS_PROJECT_ROOT_ESCAPED>',encoding:'utf-8',timeout:120000});console.log('OK:'+r)}catch(e){console.log('ERR:'+e.stderr+e.stdout)}"
```

Example — short gcloud query:
```powershell
& "C:\Program Files\nodejs\node.exe" -e "const{execSync}=require('child_process');const r=execSync('gcloud builds list --limit=3 --format=csv(id,status,createTime,duration) --project=<GCP_PROJECT_ID>',{encoding:'utf8',timeout:30000});console.log(r)"
```

> **Why Node.exe and not Python.exe for short commands?**
> Empirical testing (2026-03-12): `& "python.exe" -c "print('hello')"` almost always exceeds MCP's 60s timeout. `& "node.exe" -e "console.log('hello')"` returns in <1 second. Root cause appears to be Python's startup overhead combined with MCP subprocess management. This is not speculation — it was tested repeatedly.

### 2c. Tier 3 — MCP Python Subprocess (Long-Running Only)

Template:
```powershell
& "C:\Python313\python.exe" -c "
import subprocess, os
cwd = r'<WINDOWS_PROJECT_ROOT>'
r = subprocess.run(
    [<COMMAND_LIST>],
    capture_output=True, text=True, cwd=cwd,
    timeout=<TIMEOUT_SECONDS>,
    encoding='utf-8', errors='replace'
)
open(os.path.join(cwd, '<OUTPUT_FILE>'), 'w', encoding='utf-8').write(
    f'RC:{r.returncode}\n---STDOUT---\n{r.stdout}\n---STDERR---\n{r.stderr}'
)
"
```

Key rules:
1. **Always** write output to a file — MCP will timeout before the command completes
2. **Always** use `encoding='utf-8', errors='replace'` — Windows console codepage issues
3. **Always** use raw strings `r'...'` for Windows paths
4. **Always** set an explicit `timeout` (recommended: 180s node scripts, 300s gcloud queries, 600s deploy/build)
5. After MCP reports timeout, **wait 15-60s** then read the result file (see §2d)

### 2d. Reading Result Files After Tier 3

Files written by Windows processes take **10-60 seconds** to appear on the VM mount.

**Method A — Windows FileSystem tool (preferred, no sync delay):**
```
FileSystem read → <WINDOWS_PROJECT_ROOT>\<output_file>
```

**Method B — VM Bash (needs FUSE sync wait):**
```bash
sleep 15 && cat /sessions/<session-name>/mnt/<FolderName>/<output_file>
```

Method A is preferred because it reads the Windows filesystem directly, bypassing FUSE sync delay entirely.

---

## 3. Common Command Patterns

### 3a. Run Node.js Scripts

**Tier 1 (preferred):**
```bash
cd /sessions/<session-name>/mnt/<FolderName>
node <script>.js
```

**Tier 2 (if the script needs Windows resources, e.g. calls gcloud internally):**
```powershell
& "C:\Program Files\nodejs\node.exe" -e "const{execSync}=require('child_process');console.log(execSync('node <script>.js',{cwd:'<WINDOWS_PROJECT_ROOT_ESCAPED>',encoding:'utf-8',timeout:60000}))"
```

**Tier 3 (if the script takes >60s and needs Windows resources):**
```powershell
& "C:\Python313\python.exe" -c "
import subprocess, os
node = r'C:\Program Files\nodejs\node.exe'
cwd = r'<WINDOWS_PROJECT_ROOT>'
r = subprocess.run(
    [node, '<script>.js'],
    capture_output=True, text=True, cwd=cwd,
    timeout=180, encoding='utf-8', errors='replace'
)
open(os.path.join(cwd, '_output.txt'), 'w', encoding='utf-8').write(
    f'RC:{r.returncode}\n{r.stdout}\n{r.stderr}'
)
"
```

### 3b. gcloud Commands (General)

All gcloud commands run on Windows only. Short queries (<30s) can use Tier 2; longer operations use Tier 3.

**Tier 2 (short gcloud, <30s):**
```powershell
& "C:\Program Files\nodejs\node.exe" -e "const{execSync}=require('child_process');const r=execSync('gcloud <subcommand> <args> --project=<GCP_PROJECT_ID>',{encoding:'utf8',timeout:30000});console.log(r)"
```

**Tier 3 (long gcloud, >60s):**
```powershell
& "C:\Python313\python.exe" -c "
import subprocess, os
gcloud = r'C:\Program Files (x86)\google-cloud-sdk\bin\gcloud.cmd'
cwd = r'<WINDOWS_PROJECT_ROOT>'
r = subprocess.run(
    [gcloud, '<subcommand>', '<arg1>', '<arg2>',
     '--project=<GCP_PROJECT_ID>'],
    capture_output=True, text=True, cwd=cwd,
    timeout=300, encoding='utf-8', errors='replace'
)
open(os.path.join(cwd, '_gcloud_output.txt'), 'w', encoding='utf-8').write(
    f'RC:{r.returncode}\n{r.stdout}\n{r.stderr}'
)
"
```

> **Important**: Never call `gcloud` directly in PowerShell — always use the full `.cmd` path (`gcloud.cmd`). The `.ps1` wrapper has encoding and pipeline issues. When using Tier 2, the shell=true default in `execSync` resolves `gcloud` from PATH correctly, so the short form works.

### 3c. Cloud Build (Docker)

```powershell
& "C:\Python313\python.exe" -c "
import subprocess, os
gcloud = r'C:\Program Files (x86)\google-cloud-sdk\bin\gcloud.cmd'
cwd = r'<WINDOWS_PROJECT_ROOT>'
r = subprocess.run(
    [gcloud, 'builds', 'submit',
     '--tag', '<AR_REPO>',
     '--timeout=20m',
     '--async',
     '--project=<GCP_PROJECT_ID>'],
    capture_output=True, text=True, cwd=cwd,
    timeout=120, encoding='utf-8', errors='replace'
)
open(os.path.join(cwd, '_build_result.txt'), 'w', encoding='utf-8').write(
    f'RC:{r.returncode}\n{r.stdout}\n{r.stderr}'
)
"
```

Notes:
- Use `--async` to submit and poll separately (avoids very long waits)
- Without `--async`, builds block for the full duration (may need timeout=600+)
- `--timeout=20m` is the Cloud Build **server-side** timeout

Poll status via Tier 2:
```powershell
& "C:\Program Files\nodejs\node.exe" -e "const{execSync}=require('child_process');const r=execSync('gcloud builds list --limit=3 --format=csv(id,status,createTime,duration) --project=<GCP_PROJECT_ID>',{encoding:'utf8',timeout:30000});console.log(r)"
```

### 3d. Cloud Run Job

Execute:
```powershell
& "C:\Python313\python.exe" -c "
import subprocess, os
gcloud = r'C:\Program Files (x86)\google-cloud-sdk\bin\gcloud.cmd'
cwd = r'<WINDOWS_PROJECT_ROOT>'
r = subprocess.run(
    [gcloud, 'run', 'jobs', 'execute', '<CLOUD_RUN_JOB>',
     '--region=<CLOUD_RUN_REGION>', '--wait',
     '--project=<GCP_PROJECT_ID>'],
    capture_output=True, text=True, cwd=cwd,
    timeout=600, encoding='utf-8', errors='replace'
)
open(os.path.join(cwd, '_deploy_result.txt'), 'w', encoding='utf-8').write(
    f'RC:{r.returncode}\n{r.stdout}\n{r.stderr}'
)
"
```

Poll status via Tier 2:
```powershell
& "C:\Program Files\nodejs\node.exe" -e "const{execSync}=require('child_process');const r=execSync('gcloud run jobs executions list --job=<CLOUD_RUN_JOB> --region=<CLOUD_RUN_REGION> --limit=3 --format=csv(name,status.completionTime,status.succeededCount,status.failedCount) --project=<GCP_PROJECT_ID>',{encoding:'utf8',timeout:30000});console.log(r)"
```

### 3e. GCS Operations

Upload:
```powershell
# Tier 3 — use Python subprocess with gcloud.cmd
[gcloud, 'storage', 'cp', '<LOCAL_FILE>', 'gs://<GCS_BUCKET>/<REMOTE_PATH>']
```

Read content (inspect without downloading):
```powershell
# Tier 3 — use Python subprocess with gcloud.cmd
[gcloud, 'storage', 'cat', 'gs://<GCS_BUCKET>/<FILE>']
```

List files:
```powershell
# Tier 2 — short operation
& "C:\Program Files\nodejs\node.exe" -e "const{execSync}=require('child_process');console.log(execSync('gcloud storage ls gs://<GCS_BUCKET>/ --project=<GCP_PROJECT_ID>',{encoding:'utf8',timeout:30000}))"
```

Delete:
```powershell
# Tier 3
[gcloud, 'storage', 'rm', 'gs://<GCS_BUCKET>/<FILE>']
```

### 3f. Git Operations

**Read operations — Tier 1 (VM, preferred):**
```bash
git status --short
git log --oneline -5
git diff
git diff --cached
```

**Stage + Commit — Tier 1 (VM):**
```bash
# ALWAYS check for stale locks first:
find .git -name "*.lock" 2>/dev/null

# If no locks:
git add <files>
git commit -m "message"
```

**Push — Tier 2 (MCP Node.exe):**
```powershell
& "C:\Program Files\nodejs\node.exe" -e "const{execSync}=require('child_process');try{const r=execSync('git push <GIT_REMOTE_BRANCH>',{cwd:'<WINDOWS_PROJECT_ROOT_ESCAPED>',encoding:'utf-8',timeout:120000});console.log('OK:'+r)}catch(e){console.log('ERR:'+e.stderr+e.stdout)}"
```

**Verify push:**
```bash
git log --oneline -3    # from VM, should show latest commits
```
Or Tier 2:
```powershell
& "C:\Program Files\nodejs\node.exe" -e "const{execSync}=require('child_process');console.log(execSync('git status -sb',{cwd:'<WINDOWS_PROJECT_ROOT_ESCAPED>',encoding:'utf-8'}))"
```
> If output shows `## main...origin/main` without `[ahead N]`, push is complete.

### 3g. npm Operations

```bash
# All npm operations run from VM (Tier 1):
npm install              # install dependencies
npm test                 # run tests
npm run <script>         # run package.json scripts
npm ls --depth=0         # list installed packages
```

> Exception: If an npm script internally calls gcloud or other Windows-only tools, it must run via Tier 2 or Tier 3.

### 3h. Playwright (Windows Local Testing)

Install browsers (one-time):
```powershell
& "C:\Python313\python.exe" -c "
import subprocess, os
node = r'C:\Program Files\nodejs\node.exe'
cwd = r'<WINDOWS_PROJECT_ROOT>'
r = subprocess.run(
    [node, 'node_modules/playwright-core/cli.js', 'install', 'chromium'],
    capture_output=True, text=True, cwd=cwd,
    timeout=300, encoding='utf-8', errors='replace'
)
open(os.path.join(cwd, '_pw_install.txt'), 'w', encoding='utf-8').write(
    f'RC:{r.returncode}\n{r.stdout}\n{r.stderr}'
)
"
```

> Do NOT use `npx playwright install` — `npx.cmd` hangs in PowerShell. Use the direct `node node_modules/playwright-core/cli.js` path.

---

## 4. Standard Deploy Workflow (GCP Template)

Adapt this to your project. Steps are ordered by dependency.

| Step | Action | Tier | How to verify |
|---|---|---|---|
| 0 | Commit & push | Tier 1 + Tier 2 | `git status -sb` shows no `[ahead N]` |
| 1 | Run tests (optional) | Tier 1 | All tests pass |
| 2 | Cloud Build (Docker) | Tier 3 + Tier 2 poll | `gcloud builds list` shows SUCCESS |
| 3 | (Optional) Delete old cloud data | Tier 3 | Confirm deletion |
| 4 | Execute Cloud Run Job | Tier 3 + Tier 2 poll | `executions list` shows succeededCount=1 |
| 5 | Verify production | Tier 2 / WebFetch | Content correct, version correct |
| 6 | Sync local data from cloud | Tier 2 or Tier 3 | Local data matches cloud |
| 7 | Clean up temp files | Windows FileSystem | No `_*.txt` files in project root |

---

## 5. Known Pitfalls & Lessons Learned

All pitfalls below were discovered through actual failures on this machine. They are not theoretical.

### 5a. VM Has No sudo, No apt-get

The Cowork Linux VM cannot install system packages. No `sudo`, no `apt-get`, no `yum`. All heavy tooling (Playwright, gcloud, cloud CLIs) must be executed via the Windows side.

### 5b. PowerShell gcloud.ps1 Has Encoding Issues

`gcloud.ps1` (PowerShell wrapper) has encoding and pipeline bugs. Always use the `.cmd` batch wrapper:
```
r'C:\Program Files (x86)\google-cloud-sdk\bin\gcloud.cmd'
```

### 5c. npx.cmd Hangs in PowerShell

`npx.cmd` often hangs when called from MCP PowerShell. Use direct `node <path>` instead.
For Playwright CLI: `node node_modules/playwright-core/cli.js`.

### 5d. Git Lock File Cascading Failure (CRITICAL)

If `git add` or `git commit` fails on the VM (e.g. pre-existing lock), it creates `.git/index.lock`. The VM **cannot delete** this file. All subsequent git operations will fail with "Unable to create index.lock: File exists".

**Detection:**
```bash
find .git -name "*.lock" 2>/dev/null
```

**Recovery (from Windows):**
```
# Option A: MCP FileSystem tool (most reliable)
FileSystem delete → <WINDOWS_PROJECT_ROOT>\.git\index.lock
FileSystem delete → <WINDOWS_PROJECT_ROOT>\.git\HEAD.lock

# Option B: MCP PowerShell
Remove-Item "<WINDOWS_PROJECT_ROOT>\.git\index.lock" -Force -ErrorAction SilentlyContinue
```

**After deletion**, wait 5-10 seconds for FUSE sync, then verify:
```bash
sleep 10 && find .git -name "*.lock" 2>/dev/null
```

**Prevention**: Always run `find .git -name "*.lock"` before any `git add` / `git commit` from the VM.

> See §5j for the exception case where Windows-side deletion succeeds but VM kernel inode cache holds the stale entry beyond the typical 10-60s sync window.

### 5e. VM Cannot Delete Mounted Files

This is the single most important limitation to understand. The Linux VM can **create** and **write** files on the FUSE mount, but **cannot delete** them. `rm` returns "Operation not permitted" regardless of file ownership or permissions.

This affects: temp files, git lock files, build artifacts, any cleanup operation.

**Solution**: Always use Windows-side tools for deletion — MCP FileSystem tool (preferred) or PowerShell `Remove-Item`.

### 5f. Python.exe MCP Timeout

As of 2026-03-12, `& "C:\Python313\python.exe" -c "..."` from MCP PowerShell almost always exceeds the 60s timeout, even for trivial operations like `print('hello')`.

Node.exe (`& "C:\Program Files\nodejs\node.exe" -e "..."`) returns in <1 second for equivalent operations.

**Rule**: Use Node.exe (Tier 2) for all short commands. Reserve Python subprocess (Tier 3) **only** for operations that genuinely take >60s, and always write output to a file.

### 5g. FUSE Sync Delay Is 10-60 Seconds

Files written by Windows processes take 10-60 seconds to appear on the Linux VM mount. This delay is unpredictable and varies with system load.

**Mitigation**: Use the Windows FileSystem tool to read result files (bypasses FUSE entirely). If you must read from the VM, `sleep 15` is the minimum safe wait; `sleep 30` is conservative.

### 5h. Windows Console Encoding Noise

gcloud output often contains garbled characters in stderr — DOSKEY initialization, `where` command noise, or codepage artifacts. These are harmless. Ignore lines matching `DOSKEY` or `where` patterns.

Always use `encoding='utf-8', errors='replace'` in Python subprocess to prevent crash-on-decode.

### 5i. Temp File Convention

All temporary output files should be prefixed with `_` (underscore) for easy identification and `.gitignore` matching:
- `_output.txt`, `_build_result.txt`, `_deploy_result.txt`, `_gcloud_output.txt`, `_sync_result.txt`

Cleanup via Windows FileSystem tool (delete individually) or Node.exe:
```powershell
& "C:\Program Files\nodejs\node.exe" -e "const fs=require('fs'),p=require('path'),d='<WINDOWS_PROJECT_ROOT_ESCAPED>';fs.readdirSync(d).filter(f=>f.startsWith('_')&&f.endsWith('.txt')).forEach(f=>{fs.unlinkSync(p.join(d,f));console.log('deleted:',f)})"
```

Add to `.gitignore`:
```
_*.txt
```

### 5j. VM Inode Cache Can Outlive FUSE Sync (Exception to §5g)

Encountered 2026-05-02 (session Claude_20260502_1711). After Windows-side `Remove-Item .git\index.lock` succeeded (verified — file disappeared from Windows view), the Linux VM's kernel inode cache retained the metadata for **>5 minutes** — well past the 10-60s FUSE sync delay range documented in §5g. `sync`, `touch <parent>`, and time-wait did not invalidate the cache.

**Symptoms (all observed simultaneously):**
- `stat .git/index.lock` returns valid metadata (size, inode, timestamps)
- `ls -la .git/` does NOT list the file
- `find .git -name "index*"` matches only `index`, not `index.lock`
- `find .git -inum <stale-inode>` returns empty
- `rm` / `unlink` returns `Operation not permitted`
- `git commit` from VM fails with `Unable to create '.git/index.lock': File exists`

**Cause:** kernel-level dentry/inode cache holds stale entries even after the directory listing has refreshed. Cache TTL is implementation-dependent and may exceed 60s. No user-space workaround invalidates it; `sudo` is unavailable for `drop_caches`.

**Detection rule (3-test check):** if `stat <file>` succeeds **and** `find <dir> -name <basename>` returns empty **and** `rm <file>` returns `Operation not permitted` → the inode is stale; do not retry from VM.

**Workaround:** bypass the VM. Use Tier 2 MCP Node.exe to run the blocked operation (`git commit`, `git push`, etc.) from Windows side. The Windows process has its own filesystem view and is unaffected by Linux kernel cache.

**Verified working pattern (2026-05-02 — commit 79ab094 in this repo):**

```powershell
& "C:\Program Files\nodejs\node.exe" -e "const fs=require('fs'),path=require('path'),{execSync}=require('child_process');const cwd='<WINDOWS_PROJECT_ROOT_ESCAPED>';const lock=path.join(cwd,'.git','index.lock');if(fs.existsSync(lock)){try{fs.unlinkSync(lock)}catch(e){}}const msgFile=path.join(cwd,'_commit_msg.txt');fs.writeFileSync(msgFile,'commit message line 1\n\ndetails...','utf8');try{let r=execSync('git status -sb',{cwd,encoding:'utf-8',timeout:15000});console.log('STATUS:\n'+r);r=execSync('git commit -F _commit_msg.txt',{cwd,encoding:'utf-8',timeout:30000});console.log('COMMIT:\n'+r);r=execSync('git push origin main',{cwd,encoding:'utf-8',timeout:60000});console.log('PUSH:\n'+r)}catch(e){console.log('ERR:\n'+(e.stderr||'')+(e.stdout||''))}finally{try{fs.unlinkSync(msgFile)}catch(e){}}"
```

Cross-reference: §5d covers the typical lock recovery path (Windows delete + 5-10s wait + VM retry). §5j applies when §5d's wait does not clear VM cache after a reasonable window (>60s).

---

## 6. Multi-Step Chaining (Tier 3)

For sequential operations that each need Windows resources, combine them in a single Python script:

```powershell
& "C:\Python313\python.exe" -c "
import subprocess, os
gcloud = r'C:\Program Files (x86)\google-cloud-sdk\bin\gcloud.cmd'
cwd = r'<WINDOWS_PROJECT_ROOT>'
results = []

# Step 1
r1 = subprocess.run(
    [gcloud, '<command_1>', '<args>'],
    capture_output=True, text=True, cwd=cwd,
    timeout=60, encoding='utf-8', errors='replace'
)
results.append(f'STEP1 RC:{r1.returncode}\n{r1.stdout}\n{r1.stderr}')

# Step 2 (only if Step 1 succeeded)
if r1.returncode == 0:
    r2 = subprocess.run(
        [gcloud, '<command_2>', '<args>'],
        capture_output=True, text=True, cwd=cwd,
        timeout=600, encoding='utf-8', errors='replace'
    )
    results.append(f'STEP2 RC:{r2.returncode}\n{r2.stdout}\n{r2.stderr}')

open(os.path.join(cwd, '_chain_result.txt'), 'w', encoding='utf-8').write(
    '\n---\n'.join(results)
)
"
```

---

## 7. Quick Reference Cheat Sheet

| I want to... | Tier | Command pattern |
|---|---|---|
| Run node script | 1 | `node <script>.js` (VM Bash) |
| Run npm test | 1 | `npm test` (VM Bash) |
| Check git status | 1 | `git status --short` (VM Bash) |
| Stage + commit | 1 | `git add <files> && git commit` (VM Bash, check locks first) |
| Push to remote | 2 | `& "node.exe" -e "execSync('git push ...')"` (MCP) |
| Short gcloud query | 2 | `& "node.exe" -e "execSync('gcloud ...')"` (MCP) |
| Cloud Build | 3 | Python subprocess + `--async` + poll (MCP) |
| Cloud Run Job | 3 | Python subprocess + `--wait` + poll (MCP) |
| Delete a file | — | Windows FileSystem tool (VM cannot delete) |
| Read Tier 3 result | — | Windows FileSystem `read` (no FUSE delay) |
| Clear git locks | — | Windows FileSystem `delete` + wait 10s + verify from VM |
| Lock cleared on Windows but VM still blocks | 2 | §5j: bypass VM, run `git commit` + `git push` via Tier 2 Node.exe |

---

## 8. Session Start Checklist (Generic)

1. Discover VM mount path: `pwd` from Bash
2. Verify Node.js: `node -v`
3. Verify npm: `npm -v`
4. Verify git: `git status` (check for stale locks)
5. Run project tests: `npm test` (if applicable)
6. Sync data from cloud (if applicable)
7. Read project governance files (if applicable)

---

## Update Rule

Update this file whenever:
1. A new execution method or workaround is discovered and **verified working**
2. An existing method stops working (e.g. path change, tool update, version change)
3. A new tool is added to the Windows host or the VM
4. A new pitfall is encountered in production

Do not add patterns that are theoretical or untested. Every entry must have been run successfully (or failed instructively) on this specific machine.
