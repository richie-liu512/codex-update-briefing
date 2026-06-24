---
name: codex-update-briefing
description: Use when the user asks for a Codex Desktop update briefing, cumulative update summary since the last briefing, plugin/Skill changes or recommendations, or asks what a recent Codex Desktop update changed and whether it affects normal use.
---

# Codex Update Briefing

Use this skill when the user asks for a Codex Desktop update briefing after updating Codex or noticing a new Codex version.

## Core Rules

- Treat official OpenAI Codex release sources as the primary source. Use both the OpenAI Codex changelog and the `openai/codex` GitHub releases page before concluding what changed.
- Prefer official OpenAI / Codex release information. If the changelog and GitHub releases differ in detail or version granularity, explain the difference instead of guessing.
- Browse because Codex update information, plugin availability, and Skill availability are time-sensitive.
- Default to a cumulative briefing from the user's last recorded briefing version to the current installed version. Do not limit the briefing to only the latest version when the recorded version is older.
- Include plugin and Skill changes when official notes, local inventory, or the user's wording indicate that Codex's available tooling changed. Distinguish "officially announced", "locally observed", and "inferred from inventory diff".
- Recommend only not-yet-installed plugins and Skills from the user's current memory or workflow context at run time. Do not hardcode a user's memory topics, old task list, or personal workflow into this skill.
- Do not install plugins, enable plugins, repair plugins, modify Codex config, modify auth files, or run repair scripts unless the user explicitly asks after reading the briefing.
- Use the user's language for the final briefing. Keep exact product names, versions, commands, package names, URLs, and quoted error text in English when identification matters.
- Translate terse release-note language into practical user-facing meaning.

## Workflow

1. Read the current installed Codex Desktop version.

On Windows:

```powershell
Get-AppxPackage -Name OpenAI.Codex | Select-Object Name, Version, InstallLocation
```

If this command is unavailable, use the current platform's reliable package/app inventory and clearly state the evidence source.

2. Resolve the prior local briefing state.

Use a user-local Codex state file. Prefer:

```text
$CODEX_HOME/state/codex-update-briefing-state.json
```

If `CODEX_HOME` is not set, use:

```text
~/.codex/state/codex-update-briefing-state.json
```

State rules:

- If the state exists and is valid JSON, use it.
- If no state exists, treat the current version as the baseline and say that this run establishes the baseline.
- If the state is invalid JSON, stop and ask the user whether to repair, replace, or ignore it. Do not overwrite it silently.
- After a successful briefing, update only this state file unless the user asks for another storage location.

3. Compare current version with the recorded version.

- If the version is unchanged, say no new installed Codex Desktop version was detected, then still provide a short current-version briefing if the user asked for one.
- If there is no prior state, treat the current version as the baseline and still produce a short current-version briefing.
- If the version changed, produce a cumulative update briefing from the recorded version to the current installed version.

4. Look for official release information.

Check both official sources:

- OpenAI Codex changelog: `https://developers.openai.com/codex/changelog`
- GitHub releases: `https://github.com/openai/codex/releases`

Build a version chain covering the recorded version, every official version entry found between that version and the current installed version, and the current installed version. If an exact app patch version is not listed in one source, use the nearest official entry that matches the major release line and say which source had the exact match.

For each version after the recorded version, summarize what changed compared with the previous version when official notes make that possible. If official notes skip a version, say the gap is not documented instead of guessing.

5. Check plugin and Skill changes.

Use read-only evidence only. Keep this section short unless the user asks for a full plugin audit.

Evidence sources, in priority order:

- Official Codex release notes and GitHub release text for newly announced plugins, Skills, bundled tools, marketplace entries, or connector changes.
- The current session's visible tool, plugin, app, and Skill metadata.
- Local plugin and Skill inventory under the user's Codex home when available:
  - `$CODEX_HOME/plugins/cache/openai-bundled`
  - `$CODEX_HOME/plugins/cache/openai-curated-remote`
  - `$CODEX_HOME/skills`
  - fallback `~/.codex/plugins/cache/...` and `~/.codex/skills`
- Any current tool/plugin discovery surface that is explicitly allowed by its own instructions. Do not use a discovery or install tool in a way that conflicts with that tool's restrictions.
- The prior `plugin_skill_inventory` snapshot in the state file, if present.

Classify each relevant item with conservative labels:

- `installable`: official notes or an allowed discovery surface show the item can be installed or used, but it is not confirmed active locally.
- `default`: it is bundled with Codex, appears under an `openai-bundled` source, or is active in the current session without a user install step.
- `installed_or_cached`: it is present under the local plugin cache or active Skill list, but the evidence does not prove it was default-installed.
- `active`: it is visible as active in the current session.
- `newly_observed`: it appears in the current official/local inventory but not in the prior state snapshot. If there is no prior snapshot, say this run establishes the baseline and do not overclaim exact newness.

Do not treat every cached folder as a recommendation.

6. Recommend useful not-yet-installed plugins and Skills.

Run a bounded memory or workflow-context pass at briefing time when the current session provides memory instructions or project history. Prefer summaries and targeted index hits over broad scans. If memory is unavailable, stale, or too thin for a confident recommendation, skip personalized recommendations instead of guessing.

Recommendation rules:

- Recommend only plugins or Skills that are worth installing and are not already confirmed available to the user.
- Exclude any item classified as `default`, `installed_or_cached`, or `active`.
- Exclude any item that appears in local plugin or Skill inventory, unless the evidence clearly says the local copy is only metadata for an installable item and not an installed or cached usable item.
- Exclude any item already present in the state's `recommendation_history`, even if it still looks useful. Do not repeat prior recommendations unless the user explicitly asks to revisit them.
- Prefer items classified as `installable`. If installation status is unclear, either skip the item or say it could not be confidently recommended because it may already be present.
- For each recommendation, label it as `not installed / worth considering` and give one concise reason tied to the user's current remembered work patterns.
- Do not recommend installing anything as an action unless the user asks for installation help.

7. Reorganize the briefing for readability.

- Start with the version path, for example `26.609.9530.0 -> ... -> 26.xxx.xxxx.0`, so the user can see what interval the briefing covers.
- Include a concise per-version section when there are multiple documented versions.
- Add a merged cumulative impact section that explains the combined practical impact across all versions.
- Add a plugin and Skill section only when there is meaningful evidence to report.
- Keep low-impact implementation details out of the main flow unless they affect user decisions.
- If prior local memory or workflow context is directly relevant, mention it inside the explanation for the specific recommendation or update item. Do not add a separate memory dump.

8. Write or update the local state after the briefing.

Example state shape:

```json
{
  "last_reported_version": "26.xxx.xxxx.0",
  "last_reported_at": "ISO timestamp",
  "install_location": "platform-specific location or null",
  "plugin_skill_inventory": {
    "collected_at": "ISO timestamp",
    "codex_version": "26.xxx.xxxx.0",
    "installable_items": [
      {
        "name": "item-name",
        "kind": "plugin|skill|app|connector|unknown",
        "source": "official|discovery|local|session",
        "status": "installable|default|installed_or_cached|active|unknown"
      }
    ]
  },
  "recommendation_history": [
    {
      "name": "item-name",
      "kind": "plugin|skill|app|connector|unknown",
      "first_recommended_at": "ISO timestamp",
      "reason_summary": "short reason"
    }
  ]
}
```

Create the state directory if needed. Preserve older state fields when adding `plugin_skill_inventory` and `recommendation_history`. Append newly recommended items to `recommendation_history` after the briefing.

## Output Shape

Use this shape flexibly:

```text
Codex update briefing

Current version: ...
Last briefing version: ...
Covered range: ...
Official entries: ...

Summary:
...

Version changes:
1. ... -> ...
   - Change: ...
   - Practical meaning: ...

Cumulative impact:
...

Plugins and Skills:
- New or changed: ...
- Default or already installed: ...
- Not installed but worth considering: ...

Sources:
...
```

Conditional sections:

- Include "Possible impact" only when there is a real likely impact on normal use.
- Include "What you need to do" only when the user actually needs to act.
- Do not mechanically say there is no plugin impact. Mention that only if the user asked, symptoms exist, or official notes make it relevant.

If no official release notes are found:

```text
No detailed official change notes were found; the following is based only on the local version change and visible official information.
```

