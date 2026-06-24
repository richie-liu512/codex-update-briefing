# Codex Update Briefing Skill

[简体中文](README.zh-CN.md)

`codex-update-briefing` is a Codex Skill for producing a practical Codex Desktop update briefing. It compares the user's last recorded briefing version with the currently installed Codex version, checks official release information, summarizes cumulative changes, and calls out plugin or Skill availability changes.

It is useful for Codex Desktop users who update frequently and want a concise explanation of what changed, what matters in normal use, and which not-yet-installed plugins or Skills may be worth considering.

This is an unofficial community Skill for Codex users.

## Features

- Compares the current Codex Desktop version with the last recorded briefing version.
- Produces a cumulative update summary instead of only summarizing the latest version.
- Checks official OpenAI Codex changelog and GitHub release sources.
- Distinguishes plugin and Skill status such as installable, bundled/default, installed/cached, active, and newly observed.
- Recommends only not-yet-installed plugins or Skills, and records recommendation history to avoid repeating the same suggestions.
- Keeps local state in a user-local Codex directory instead of project source files.

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

The first run establishes a baseline if no previous state exists. Later runs can compare against the saved state and report cumulative changes.

## Local State

The Skill is designed to keep a small JSON state file in a user-local Codex state directory. The state may include:

- last reported Codex version
- last reported time
- install location
- plugin and Skill inventory snapshot
- recommendation history

The state file is intentionally not part of this repository.

## Privacy Notes

This public version avoids user-specific absolute paths and personal workflow details. It instructs Codex to read memory only at run time when the current session provides memory guidance. If memory is unavailable, personalized recommendations should be skipped instead of guessed.

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

## Roadmap

- Add sample output fixtures.
- Add a small helper script for portable state-file resolution.
- Add tests for recommendation-history behavior.

## Feedback

Suggestions and bug reports are welcome through GitHub Issues.

## License

MIT License. See [LICENSE](LICENSE).
