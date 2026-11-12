# UCD Sonic HPC Skill

Prepare a research computation for University College Dublin's Sonic cluster with Codex or Claude Code. Describe the task in ordinary language. The agent finds the launch command and dependencies, prepares an upload package and Slurm scripts, and gives you commands to transfer files, test the setup, submit the job, and bring results back.

You need an existing Sonic account, a working SSH connection, and a suitable software environment on Sonic. An agent with local file access prepares the files. You run the transfer and submission commands. This is a community-maintained workflow. Consult UCD Research IT for account access and cluster policy.

## Install

On this repository's GitHub page, choose **Code > Download ZIP** and extract it. Copy the entire `skills/ucd-sonic-hpc` folder, including `references`, into the appropriate user-level skills directory.

| Tool | Installed folder |
| --- | --- |
| Codex | `~/.agents/skills/ucd-sonic-hpc/` |
| Claude Code | `~/.claude/skills/ucd-sonic-hpc/` |

On Windows, `~` means your Windows user folder. For both tools, copy the same source folder into both locations. Check any existing same-named skill before replacing it. Update both installed copies when adopting a newer release. Open a new agent session after installation if the skill is missing from the available skills.

These locations follow the tools' documented local skill conventions. [Codex skills](https://learn.chatgpt.com/docs/build-skills) and [Claude Code skills](https://code.claude.com/docs/en/skills).

## Use

In your project's Codex chat, send:

```text
$ucd-sonic-hpc Prepare this experiment for Sonic.
```

In Claude Code, send:

```text
/ucd-sonic-hpc Prepare this experiment for Sonic.
```

Use the same chat that prepared your experiment, or identify the experiment folder. The agent can find the training command from project files and run records. It asks for task details when the available evidence leaves an important choice unresolved.

On first use, it may need your SSH host alias, notification email, remote working directory, or the resources your account can access. Provide your own account settings. Keep passwords and private keys in your normal SSH authentication setup. You can activate your Sonic environment manually before submission.

You receive one upload archive in your local project, its manifest and runbook, and commands labeled for your local terminal or the Sonic terminal. Run the short smoke test first. Share its outcome with the agent to get the full-run submission step. Full runs request end and failure emails. Smoke tests disable email notifications. Results return with the project's directory layout and checksums. Checkpoints and temporary files are excluded from the default result download.

A smoke test is a small trial job that checks whether the code can load its inputs, access the required resources, and write outputs on Sonic before starting the full computation.

The agent adapts commands to Windows PowerShell or your local shell. An SSH alias configured for VS Code can also be used with `scp` when both use the same SSH configuration.

## Privacy and scope

The distributed skill contains generic instructions and official documentation links. At use time, the agent resolves account settings locally. Keep personal settings outside this public repository. Generated task packages and manifests can contain account names, local paths, research code, and data. Review them separately before sharing.

The skill supports training, CPU preprocessing, and other project-defined computations through Slurm. Resource requests depend on the task and account. A local packaging check is followed by a compute-node smoke test. Record their outcomes independently.

## Official references

- [UCD Sonic user guide](https://ucdprod.service-now.com/itucd/?id=kb_article_view&sysparm_article=KB0011715)
- [UCD software on Sonic](https://ucdprod.service-now.com/itucd/?id=kb_article_view&sysparm_article=KB0011721)
- [Slurm submission reference](https://slurm.schedmd.com/sbatch.html)

## License

Released under the [MIT License](LICENSE). Copyright (c) 2026 sunbohaogc-code.

## Feedback

Report problems or suggest improvements through [GitHub Issues](https://github.com/sunbohaogc-code/ucd-sonic-hpc-skill/issues). Include your operating system, agent, and the failing step. Remove account details, private paths, credentials, and research data from shared logs.
