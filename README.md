# Codex Update Briefing Skill

[简体中文](README.zh-CN.md)

Driven by the rapid pace of the AI industry, Codex updates frequently, introducing new features, plugins, or workflows with each release. If you use Codex frequently, staying on top of these changes helps you promptly adjust your workflow and boost productivity. However, Codex does not proactively summarize these updates, and manually combing through changelogs is both time-consuming and tedious.

`codex-update-briefing` was built specifically to address this pain point. It tracks the version from your last briefing and compares it with your current version to recap the cumulative changes over that period, rather than just focusing on the single latest release. Additionally, it scans the status of your plugins and Skills, leveraging global memory to recommend helpful, uninstalled tools while maintaining a recommendation history to prevent repetitive notifications.

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
