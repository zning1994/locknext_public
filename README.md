# locknext_public

Public CI control scaffold for LockNext. Application source remains private.

## Execution policy

- Manual dispatch only. No schedules, pull-request triggers, or push triggers.
- Default: standard Linux runner. Select standard macOS only after the owner explicitly approves that run.
- Setup validation has exercised standard Linux only. macOS has not been dispatched.
- A dedicated read-only deploy key can access only the private source repository. No write token, signing identity, provider API key, or production data belongs here.
- `LOCKNEXT_READONLY_DEPLOY_KEY` is an Actions secret. `LOCKNEXT_REVIEWED_COMMIT` is a separate secret containing the exact reviewed 40-character source commit.
- Source is fetched at that exact commit, detached, without submodules. The deploy key is removed before any project code runs.
- Private stdout/stderr remain in the ephemeral runner workspace. Only fixed generic status messages are intentionally published. No raw logs, source archives, test bundles, screenshots, caches, or build artifacts are uploaded.
- Ephemeral files are removed on completion. If GitHub terminates the runner before cleanup, disposal relies on the GitHub-hosted ephemeral runner lifecycle.
- The public workflow and run metadata are public. This design reduces disclosure risk; it is not an absolute confidentiality guarantee against malicious reviewed code, compromised tooling, or platform diagnostics. Only trusted source revisions may be selected. Debug logging must remain off.
- Linux setup encountered a preparation failure; pinning the verified GitHub SSH host key removed the runtime metadata dependency. The subsequent Linux source preparation, checks and cleanup passed. Earlier failures remain in Actions history.
- Failed checks remain failures. Reproduce privately for diagnostic detail; passing functional checks does not imply accessibility, signing, device, or distribution acceptance.

The repository is not a general-purpose runner service. It is limited to development and testing of the associated application. Standard public GitHub-hosted compute is free under GitHub's current billing documentation; larger runners are not free.

Do not publish application source or private diagnostic files to this repository.
