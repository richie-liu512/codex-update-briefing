# Codex Update Briefing Skill

[简体中文](README.zh-CN.md)

Because the AI industry is moving quickly, Codex updates frequently, and each update can bring new features, plugins, or ways to work. Understanding those changes helps users adjust their workflows and work more efficiently. But Codex Desktop does not summarize those changes after each update, and reading through changelogs manually can be tedious.

`codex-update-briefing` records the version from your last briefing, compares it with the version installed now, and summarizes the whole interval rather than only the newest release. It also checks plugin and Skill status, uses global memory to recommend not-yet-installed tools that can help your work, and remembers past recommendations so the same items are not suggested again.

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
