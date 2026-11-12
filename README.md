# UCD Sonic HPC Skill

Use Codex or Claude Code to prepare research tasks for UCD Sonic HPC.

The skill packages your code and data, creates Slurm scripts, and provides commands to upload files, test the setup, submit jobs, and download results.

You need a Sonic account, working SSH access, and a suitable software environment on Sonic. You run the transfer and submission commands.

## Install

Choose **Code > Download ZIP** on GitHub and extract it. Copy the entire `skills/ucd-sonic-hpc` folder, including `references`, into your tool's skills directory.

| Tool | Install location |
| --- | --- |
| Codex | `~/.agents/skills/ucd-sonic-hpc/` |
| Claude Code | `~/.claude/skills/ucd-sonic-hpc/` |

On Windows, `~` is your Windows user folder. For both tools, install in both locations. Check existing copies before replacing them. If the skill is missing, open a new agent session.

## Use

Open your project and send the matching prompt.

| Tool | Prompt |
| --- | --- |
| Codex | `$ucd-sonic-hpc Prepare this experiment for Sonic.` |
| Claude Code | `/ucd-sonic-hpc Prepare this experiment for Sonic.` |

The agent finds the training command from your project. On first use, it may ask for your SSH alias, notification email, and Sonic working directory.

Upload the prepared archive using the supplied `scp` command, then run the smoke test, a small trial that checks inputs, resources, and output writes. Share the outcome with the agent before starting the full run. Results return with directory structure and checksums.

Full runs request end and failure emails. Smoke tests disable email notifications.

## Privacy and help

Keep account settings outside this repository and credentials in your SSH setup. Check generated packages and logs for personal information or research data before sharing.

This is a community workflow. For cluster access and policy, consult the [UCD Sonic guide](https://ucdprod.service-now.com/itucd/?id=kb_article_view&sysparm_article=KB0011715) and [software guide](https://ucdprod.service-now.com/itucd/?id=kb_article_view&sysparm_article=KB0011721). Report skill problems through [GitHub Issues](https://github.com/sunbohaogc-code/ucd-sonic-hpc-skill/issues).

## License

[MIT](LICENSE). Copyright (c) 2026 sunbohaogc-code.
