# Codex 更新简报 Skill

[English](README.md)

因为 AI 行业快速发展，Codex 更新频繁，而每次更新都可能带来新的功能、插件或使用方式。了解这些变化，才能及时调整工作流，提高工作效率。但 Codex 更新后不会主动总结变化，自己翻看更新日志又很繁琐。

`codex-update-briefing` 会记录上次简报对应的版本，再和当前安装版本比较，汇总这段时间内的变化，而不是只追最新一个版本；同时检查插件和 Skill 的状态，结合全局记忆推荐尚未安装、但对工作有帮助的工具，并记录推荐历史，避免之后反复打扰。

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
