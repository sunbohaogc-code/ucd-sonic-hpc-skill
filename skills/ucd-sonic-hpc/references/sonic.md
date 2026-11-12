# Sonic operations

## Account and environment discovery

Use the user's SSH configuration and any VS Code remote.SSH.configFile setting to identify the Sonic host alias, username, port, identity-file reference, and jump-host setup. Keep credentials in SSH authentication. Read only the connection settings needed for this task. Request a missing alias or notification address once and reuse it in the current handoff. Keep persistent personal settings in a user-selected location outside the public skill repository.

UCD documents login.ucd.ie and home directories under /home/people/USERNAME. Discover the user's effective HOME and scratch path through existing records or user-provided remote command output. Scratch is temporary and unbacked. Use a fresh task directory in the selected working area. Prefer a resolved remote absolute path or ~/scratch in local transfer commands. Establish partition eligibility, GPU type and VRAM, memory, and time limits for this task rather than relying on another account's observations. sinfo -o '%P %a %l %G' can describe partitions and resources. The UCD guide documents gpu, csgpu, and dev. Confirm current access and limits when choosing resources.

The user may activate an existing environment manually. Slurm defaults to exporting the submission environment. For that setup, use #!/bin/bash unless a login shell is needed, because login startup files can alter PATH. Invoke the selected interpreter and log its path and framework-visible resources on the compute node. GPU-required jobs should fail early if the selected framework cannot use a GPU. CPU jobs should exercise their CPU path. If batch activation is requested, UCD documents loading an Anaconda module and activating the chosen environment. Use the user's actual Sonic names.

## Slurm and notification settings

For one Python process, request one task and select CPUs per task, host RAM, GPUs if needed, and walltime for the workload. --mem requests host RAM. GPU VRAM must meet the task's requirement independently. Create log parent directories before sbatch and use %j in log filenames. Slurm parses #SBATCH directives before executing the shell. Use literal directive values or expand shell variables in submission arguments.

Full runs use --mail-type=END,FAIL with --mail-user set to the user's confirmed notification email. Obtain the address from the user or their established task configuration. Smoke tests use --mail-type=NONE. A shared smoke/full launcher can retain full-run mail directives while the smoke submission overrides the type with --mail-type=NONE. Verify both generated commands. Check effective submitted settings and then delivery when expected mail is missing.

Use squeue to inspect queue state, sacct to inspect exit state, and the current job's logs and expected artifacts to assess completion. Fill actual job identifiers or capture them into a shell variable for copyable monitoring commands.

## Packaging and transfer

Keep local archives, result downloads, generated code, and bulk temporaries under the corresponding local project or experiment. Use its existing storage convention or an hpc directory on a drive with enough space. Read large unchanged inputs directly into the archive when practical. Preserve workspace subtrees needed by code and data readers under one task-specific top-level directory. Check producer and consumer paths explicitly. Extract into a fresh destination with protection against replacing existing files.

Build from relative archive names. Reject absolute members, parent traversal, duplicate destinations, case collisions, and dependencies on local-only link targets. Resolve required linked inputs to payload contents at their intended paths. The manifest records each payload file's local source, archive path, Sonic destination, purpose, size, and SHA-256. Exclude the manifest from its own checksum list. Verify archive contents and hashes and resolve every required input to a payload, an earlier stage's output, or a declared cluster dependency. Run bash -n when Bash is available and use existing bounded code checks. Report any pending compute-node check.

Generate filled scp commands for the user's local shell, labeling local and remote blocks. Reuse SSH configuration and pass scp -F if a non-default file is used. Quote local paths and the whole remote operand. In PowerShell, brace a host variable before a colon and avoid expanding remote home references as the Windows home. For macOS or Linux, use the corresponding shell quoting. Include required parent-directory creation on the appropriate machine and check destination collisions. For direct-download directories use scp -r and specify the resulting local layout. Keep explanatory placeholders outside executable blocks.

The runbook includes exact upload, extraction, working and log directories, smoke and full submission commands, monitoring, package requirements, results to retrieve, and pending checks. Keep the chat focused on the user's current step.

## Provenance and output collisions

Inspect actual result and run-record writes. A recorder may replace a script-named manifest on each invocation. Use distinct run and smoke destinations according to the project's rules. Copy needed shared artifacts into the required locations and record their provenance and hashes. Preserve established splits and scientific parameters.

For an uploaded copy without a Git repository, record the local source commit, local changes, and hashes of the actual deployed code. Print source provenance in the job log or a supported purpose field. The commit identifies the baseline and the hashes identify deployed files. If a recorder calls the git executable, declare that runtime dependency even for a repository-free upload.

## Structured result retrieval

Derive the return collection from outputs needed for local analysis. Include the run's tables, figures, data products, application logs, run records, and current job's Slurm stdout and stderr. Exclude checkpoints, temporary files, and unrelated job outputs from the default return. Retain remote checkpoints according to the task's resume and retention needs.

Use one explicit payload list for both checksums and collection. Record each file's workspace-relative destination path, size, and SHA-256. Exclude the result manifest from its own checksum list. Preserve directory structure in either an archive or a download folder. Record run identity, code provenance, and observed complete, failed, or partial status. Verify returned contents before restoring them locally.

Finalize collection after the job ends so Slurm logs have finished writing. Optional on-exit collection may package finalized application outputs while preserving the training exit status and reporting collection errors separately. Final logs and late writes still need collection and hashing after exit. Include only this job's logs. For failed or interrupted jobs, identify available diagnostics and missing outputs.

Choose an archive for many or large files or one clearly named folder for a few small files. The runbook gives exact remote sources, download destinations inside the local project, checksum commands, and the workspace root for restoring relative paths. Stage validation in the local project when needed. Skip identical local files and identify differing existing files for a decision before replacement.

## Sources

- [UCD Sonic user guide](https://ucdprod.service-now.com/itucd/?id=kb_article_view&sysparm_article=KB0011715)
- [UCD software on Sonic](https://ucdprod.service-now.com/itucd/?id=kb_article_view&sysparm_article=KB0011721)
- [Slurm sbatch](https://slurm.schedmd.com/sbatch.html) and [sinfo](https://slurm.schedmd.com/sinfo.html)
- [OpenSSH scp](https://man.openbsd.org/scp) and [VS Code SSH configuration](https://code.visualstudio.com/docs/remote/ssh#_remember-hosts-and-advanced-settings)
