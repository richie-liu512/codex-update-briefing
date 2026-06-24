# Codex 更新简报 Skill

[English](README.md)

`codex-update-briefing` 是一个 Codex Skill，用来生成 Codex Desktop 更新简报。它会比较“上一次简报记录的版本”和“当前安装的 Codex 版本”，读取官方发布信息，整理跨版本累计变化，并检查插件或 Skill 的可安装、默认内置、已安装、已缓存和新增情况。

它适合经常更新 Codex Desktop、但不想逐条读更新日志的用户：你可以快速知道这几次更新累计改变了什么、对日常使用有什么影响，以及有哪些尚未安装但可能值得考虑的插件或 Skill。

## 功能

- 比较当前 Codex Desktop 版本和上次简报记录版本。
- 支持跨多个版本的累计更新简报。
- 检查 OpenAI Codex 官方 changelog 和 GitHub releases。
- 区分插件和 Skill 的状态：可安装、默认/内置、已安装/已缓存、当前 active、新增。
- 只推荐“尚未安装但值得安装”的插件或 Skill。
- 记录推荐历史，避免下次重复推荐同一个项目。
- 把本地状态保存在用户自己的 Codex 状态目录，不放进项目源码。

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

如果第一次运行时没有历史状态，它会建立基线。之后再运行时，就可以基于上次记录做跨版本比较。

## 本地状态

这个 Skill 会在用户本地 Codex 状态目录保存一个小型 JSON 状态文件，可能包含：

- 上次简报版本
- 上次简报时间
- 安装路径
- 插件和 Skill 清单快照
- 推荐历史

这个状态文件不属于仓库内容。

## 隐私说明

公开版已经移除了作者本机的绝对路径和个人工作流细节。它只要求 Codex 在运行时按当前会话提供的 memory 规则读取记忆；如果当前环境没有 memory，就跳过个性化推荐，不凭空猜测。

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

暂未加入许可证。对这个小型开源 Skill 来说，MIT 是比较合适的默认选择，但发布前应先确认。

