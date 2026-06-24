# Codex 更新简报 Skill

[English](README.md)

Codex Desktop 更新很快，但普通更新日志通常只回答一个问题：最新版本改了什么。实际使用时，很多人更关心的是：我上次看更新之后，到现在到底变了什么？

`codex-update-briefing` 是一个面向 Codex 用户的非官方社区 Skill。它会记录你上次简报对应的 Codex 版本，下次运行时整理这段时间里的累计变化，并检查插件和 Skill 的新增、默认内置、已安装、可安装等状态。

## 为什么做这个项目

普通 changelog 是按版本组织的；真正有用的个人简报，应该按使用者的连续体验组织。

这个 Skill 会用一个很小的本地状态文件记录“上次简报到哪个版本”。再次运行时，它会把这个版本和当前安装版本做比较，再结合官方更新说明，生成一份覆盖整个时间区间的简报。即使中间跳过了几个版本，也不需要自己一条条拼更新记录。

插件和 Skill 推荐也做了降噪设计。它可以结合当前环境提供的记忆或工作流上下文，但只推荐尚未安装、且看起来适合当前工作的项目。已经内置、已经安装、已经缓存、当前已可用、以前推荐过的项目都会被过滤掉。

## 亮点

- **按时间区间总结更新**：不是只总结最新版本，而是整理“上次简报之后到现在”的完整变化。
- **优先使用官方来源**：以 OpenAI Codex changelog 和 `openai/codex` GitHub releases 作为主要依据。
- **识别插件和 Skill 状态**：区分可安装、默认内置、已安装/已缓存、当前已可用、新发现等状态。
- **结合上下文做推荐**：在当前环境提供记忆或工作流上下文时，只推荐尚未安装、但可能适合实际工作的插件或 Skill。
- **避免重复打扰**：记录推荐历史，下次不再反复推荐同一个项目。
- **状态留在本地**：版本记录、清单快照和推荐历史都保存在用户自己的 Codex 目录，不进入仓库。

## 安装

把 `codex-update-briefing` 文件夹复制到你的 Codex skills 目录。

常见位置：

```text
%USERPROFILE%\.codex\skills\codex-update-briefing
~/.codex/skills/codex-update-briefing
```

如果你的环境使用 `CODEX_HOME`，放到：

```text
$CODEX_HOME/skills/codex-update-briefing
```

## 使用

对 Codex 说：

```text
使用 $codex-update-briefing 总结我上次 Codex 更新简报之后又变化了什么。
```

如果第一次运行时没有历史状态，它会先建立基线。之后再运行时，就可以基于上次记录做跨版本比较。

## 本地状态

这个 Skill 会在用户本地 Codex 状态目录保存一个小型 JSON 状态文件，可能包含：

- 上次简报版本
- 上次简报时间
- 安装路径
- 插件和 Skill 清单快照
- 推荐历史

这个状态文件不属于仓库内容。

## 隐私说明

公开版不包含作者本机路径和个人工作流细节。它只在运行时读取当前环境提供的记忆或工作流上下文；如果当前环境没有这些信息，就跳过个性化推荐，不硬猜。

这个 Skill 不应该把个人记忆内容写进仓库。推荐历史也只应该保存项目名称和简短理由，不保存大段私人上下文。

## 验证

可以使用 Codex skill creator 的校验脚本验证：

```shell
python path/to/quick_validate.py codex-update-briefing
```

Windows 环境如果包含中文，建议打开 UTF-8：

```powershell
$env:PYTHONUTF8='1'
python path\to\quick_validate.py .\codex-update-briefing
```

## 后续计划

- 增加示例输出。
- 增加一个小型脚本，用来跨平台解析状态文件路径。
- 增加推荐历史去重行为的测试样例。

## 反馈

欢迎通过 GitHub Issues 提建议或反馈问题。

## License

MIT License。见 [LICENSE](LICENSE)。

