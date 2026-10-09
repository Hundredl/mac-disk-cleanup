# Mac Disk Cleanup Assistant

[简体中文](README.md) | English

A skill for Codex and other AI assistants with access to your Mac: inspect disk usage and application leftovers, let you review the candidates, clean approved items, and save traceable maintenance records.

Use it to investigate a slow Mac or low disk space, review old applications and files, or trace changes when something stops working after cleanup. It supports inspection only and execution of previously approved items.

## Copy this prompt

Without installing the skill, you can give this prompt to an AI assistant that can access your computer:

```text
Help me inspect disk usage and old application leftovers on this Mac. Start with read-only checks and list candidates with exact paths, sizes, purposes, recovery conditions, and recommended actions for me to review. Track what I want to keep. Clean only the specific items I approve, without asking again for approval already given. Do not expand the scope just to meet a space target. Distinguish caches from account and chat databases, documents, saves, and runtime dependencies; follow my backup preferences. Recheck paths and active use before acting. Save the plan first and log each result, including failures. Verify the outcome and measure the actual change in available disk space. Save the removals, retained items, errors, current backup status, and potentially affected features in the maintenance location I specify, so I can refer to them later or investigate problems. If you lack local tools or permissions, explain the limitation.
```

A model in a normal chat webpage may not have access to your Mac. Copying the prompt does not grant terminal, filesystem, or administrator access.

## Install as a Codex skill

Run this in your local terminal. Git is required, and the destination directory must not already exist:

```sh
git clone https://github.com/Hundredl/mac-disk-cleanup.git "${CODEX_HOME:-$HOME/.codex}/skills/mac-disk-cleanup"
```

In a new Codex conversation, use:

```text
Use $mac-disk-cleanup to inspect disk usage and old applications. Do not delete anything yet; list candidates for me to review.
```

You can also ask an assistant to read [SKILL.en.md](SKILL.en.md) directly. Other assistants that support SKILL.md can use their own installation method.

[SKILL.md](SKILL.md) remains the single discoverable entry point and routes English requests to the English guide. You do not need two installations, and the same authorization and retention rules apply in both languages.

## Files

- [SKILL.md](SKILL.md): the discoverable entry point and Chinese workflow.
- [SKILL.en.md](SKILL.en.md): the complete English workflow.
- [Inspection notes](references/inspection.en.md): space measurements, candidate evidence, and permission boundaries.
- [Execution and records](references/execution-record.en.md): operation logs, verification, backup status, and investigating later problems.
- `agents/openai.yaml`: Codex display metadata and an example invocation.

This repository contains general guidance. It does not include personal maintenance reports, automatic deletion scripts, or a one-click cleaner. Measure disk space and performance improvements separately. Some removals require downloading, rebuilding, or reinstalling; recovery depends on the actual backups and original sources.

License: [MIT](LICENSE).
