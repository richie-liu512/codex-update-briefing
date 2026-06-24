# Codex 更新简报 Skill

[English](README.md)

Codex Desktop 更新很频繁，但版本更新之后，软件本身通常不会主动告诉你这次到底变了什么。大多数人也没有时间每次都去翻更新日志。

`codex-update-briefing` 的作用是把这些更新整理成一份可读的简报：它会记住你上次查看到哪个版本，汇总这段时间内的变化，检查插件和 Skill 的状态变化，并结合你的全局记忆或当前工作上下文，推荐版本更新后可能有助于你工作的插件或 Skill。

## 为什么做这个项目

Codex 是日常生产力工具，而且更新节奏很快。新版本可能会影响提示词写法、可用工具、插件和 Skill 的选择，以及你能从 Codex 里获得多少效率提升。

大多数用户没有时间手动追每一次更新。这个 Skill 会用一个很小的本地状态文件记录“上次简报到哪个版本”。再次运行时，它会把这个版本和当前安装版本做比较，生成一份覆盖整个时间区间的简报。即使中间跳过了几个版本，也能直接看到从上次简报到现在的完整变化。

插件和 Skill 推荐也做了降噪设计。它会检查哪些项目是默认内置、已经安装、已经缓存、当前可用、新发现或仍可安装；在当前环境提供全局记忆或工作流上下文时，只推荐尚未安装、且适合你实际工作的项目，并记录推荐历史，避免之后反复推荐同一个东西。

## 亮点

- **按时间区间总结更新**：不是只总结最新版本，而是整理“上次简报之后到现在”的完整变化。
- **结合上下文推荐工具**：识别插件和 Skill 的状态，只推荐尚未安装、但适合你工作流的项目，并避免之后重复推荐同一个东西。

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

## 反馈

欢迎通过 GitHub Issues 提建议或反馈问题。

## License

MIT License。见 [LICENSE](LICENSE)。
