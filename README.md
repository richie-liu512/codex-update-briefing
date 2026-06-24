# Codex Update Briefing Skill

[简体中文](README.zh-CN.md)

Codex Desktop updates often arrive quietly. The app version changes, but users still need to know what matters: what changed, whether it affects daily work, and whether any new plugins or Skills are worth installing.

`codex-update-briefing` turns Codex updates into a practical briefing. It remembers the last version you checked, summarizes the full update range since then, checks plugin and Skill changes, and uses your global memory or available workflow context to recommend not-yet-installed tools that can help your daily Codex work.

Codex is a daily productivity tool, and it changes quickly. New releases can affect how you prompt, which tools are available, what plugins or Skills are worth using, and how much leverage you get from the app.

Most users do not have time to track every update manually. This Skill keeps a small local state file with the last reported Codex version. On the next run, it compares that version with the currently installed Codex version and produces one readable briefing for the whole interval. If you skipped several versions, you still get the full story since your last briefing.

It also treats plugin and Skill recommendations as a noise-control problem. It checks what is bundled, installed, cached, active, newly observed, or still installable. When memory or workflow context is available, it uses that context to recommend only not-yet-installed items that fit your work, then remembers past suggestions so it does not keep repeating the same recommendation.

## Highlights

- **Cumulative update briefings**: summarizes everything that changed since your last briefing, even if you skipped several Codex versions.
- **Context-aware tool recommendations**: checks plugin and Skill status, recommends only not-yet-installed items that fit your workflow, and avoids repeating the same suggestion in later briefings.

## Install

Copy the `codex-update-briefing` folder into your Codex skills directory.

Typical locations:

```text
%USERPROFILE%\.codex\skills\codex-update-briefing
~/.codex/skills/codex-update-briefing
```

If your setup uses `CODEX_HOME`, place it under:

```text
$CODEX_HOME/skills/codex-update-briefing
```

## Usage

Ask Codex:

```text
Use $codex-update-briefing to summarize what changed since my last Codex update briefing.
```

The first run establishes a baseline if no previous state exists. Later runs compare against the saved state and report cumulative changes.

## Local State

The Skill keeps a small JSON state file in a user-local Codex state directory. The state may include:

- last reported Codex version
- last reported time
- install location
- plugin and Skill inventory snapshot
- recommendation history

The state file is intentionally not part of this repository.

## Verification

Validate the Skill folder with the Codex skill creator validator:

```shell
python path/to/quick_validate.py codex-update-briefing
```

On Windows, use UTF-8 mode if your environment has non-ASCII text:

```powershell
$env:PYTHONUTF8='1'
python path\to\quick_validate.py .\codex-update-briefing
```

## Feedback

Suggestions and bug reports are welcome through GitHub Issues.

## License

MIT License. See [LICENSE](LICENSE).
