# Codex Update Briefing Skill

[简体中文](README.zh-CN.md)

Codex Desktop moves quickly, but most update notes answer only one question: what changed in the latest release? Returning users often need a different answer: what changed since the last time I checked?

`codex-update-briefing` is an unofficial community Skill for Codex users. It turns Codex updates into a practical briefing by remembering the last version you reviewed, summarizing the full update range since then, and checking plugin or Skill changes that may affect your workflow.

## Why It Exists

A normal changelog is organized around releases. A useful personal briefing is organized around continuity.

This Skill keeps a small local state file with the last reported Codex version. On the next run, it compares that version with the currently installed Codex version, looks up official release information, and produces a cumulative summary for the whole interval. If you skipped several updates, you get one readable briefing instead of reconstructing the story from multiple release notes.

It also treats plugin and Skill recommendations as a noise-control problem. It can use the current session's memory or workflow context, but it recommends only not-yet-installed items that appear relevant. Bundled, installed, cached, active, and previously recommended items are filtered out.

## Highlights

- **Cumulative update briefings**: summarizes the range since the last recorded briefing, not only the newest release.
- **Official-source first**: uses the OpenAI Codex changelog and `openai/codex` GitHub releases as primary evidence.
- **Plugin and Skill change detection**: classifies items as installable, bundled/default, installed/cached, active, or newly observed.
- **Context-aware recommendations**: uses available memory or workflow context to suggest only not-yet-installed plugins or Skills that fit the user's actual work.
- **Recommendation history**: avoids repeating the same suggestion in future briefings.
- **Portable local state**: stores state in the user's Codex directory, not in the project repository.

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

## Privacy Notes

This public version avoids user-specific absolute paths and personal workflow details. It reads memory only at run time when the current agent environment provides memory guidance. If memory or workflow context is unavailable, personalized recommendations should be skipped instead of guessed.

The Skill should not copy personal memory content into the repository, and recommendation history should store only concise item names and short reason summaries.

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

