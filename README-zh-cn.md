# AI TRPG World Engine

版本：v1.1

一个用于长期运行 AI TRPG 世界模拟与状态管理的系统仓库。

这个仓库的目标不是保存聊天记录，而是保存持续存在、逻辑自洽、状态可追踪的 TRPG 世界。引擎文件定义可复用的运行规则，`saves/` 下的每个存档保存一个故事或战役的事实来源。聊天记录只能作为辅助上下文。

## 目录结构

- `rules/`：可复用的世界引擎规则与运行原则。
- `saves/`：故事或战役存档。
- `saves/active_save.example.md`：当前活跃存档指针示例。
- `saves/active_save.md`：本地当前活跃存档指针，默认不进入 Git。
- `saves/_template/`：新故事使用的空存档模板。
- `saves/<save-name>/`：本地故事存档，默认不进入 Git。
- `saves/<save-name>/save.md`：某个存档的元数据，包括状态。
- `saves/<save-name>/state/`：某个存档的世界、玩家、时间线与线索状态。
- `saves/<save-name>/npcs/`：某个存档中的 NPC 文件，每个 NPC 单独保存。
- `saves/<save-name>/logs/`：某个存档的会话日志。
- `saves/<save-name>/docs/story_summary_zh-cn.md`：给玩家阅读的中文剧情摘要。
- `templates/`：新建 NPC 或其他实体时使用的模板。
- `.agents/skills/ai-trpg-world-engine/`：用于 Codex 的 AI TRPG 世界引擎 Skill。

## 每次会话开始的读取顺序

先从 `saves/active_save.md` 确认当前活跃存档，然后按以下顺序读取：

1. `rules/engine_rules.md`
2. `saves/<save-name>/save.md`
3. `saves/<save-name>/state/world_state.md`
4. `saves/<save-name>/state/timeline.md`
5. `saves/<save-name>/state/player.md`
6. `saves/<save-name>/npcs/` 中相关 NPC 文件
7. `saves/<save-name>/state/clues.md`
8. `saves/<save-name>/logs/session_log.md` 中最近的记录

## 创建新存档

复制 `saves/_template/` 为 `saves/<new-save-name>/`，复制 `saves/active_save.example.md` 为 `saves/active_save.md`，填写 `saves/<new-save-name>/save.md`，并更新 `saves/active_save.md`。真实存档默认被 Git 忽略，这样公开仓库时不会泄露故事状态。

推荐分支流程：

```powershell
git checkout main
git pull
git checkout -b story/<new-save-name>
```

保持 `main` 作为可复用的引擎底座。每个故事或实验使用自己的 `story/<save-name>` 分支。由于真实存档默认被 Git 忽略，除非你明确强制加入，否则它们只保留在本地。

如果你确实想版本化某个存档：

```powershell
git add -f saves/active_save.md saves/<save-name>/
git commit -m "Add <save-name> story save"
```

只建议在私有仓库、私有远端或你愿意公开内容的分支上这样做。

## 维护规则

- 当前存档的 `state/timeline.md` 只能追加，不要重写历史。
- 世界当前状态变化时，更新当前存档的 `state/world_state.md`。
- 玩家状态变化时，更新当前存档的 `state/player.md`。
- NPC 的行为只能依据其文件中记录的目标、动机和已知信息。
- 线索必须区分事实、推论、猜测和传闻。
- 当前存档的 `logs/session_log.md` 只记录发生了什么，不记录隐藏真相或 GM 信息。
- 面向玩家阅读的剧情摘要使用中文。
- 面向 AI 读取的状态、NPC、线索、时间线、日志文件使用英文。

## 运行模式

ATWE v1.1 支持两种运行模式。

**FULL 模式**

用于模型或工具第一次接手存档、审计连续性、修复状态漂移时。应较完整读取当前活跃存档，包括元数据、世界状态、玩家状态、时间线、线索、相关 NPC 文件和最近会话日志。

**LITE 模式**

用于日常游玩，减少 token 消耗。只读取当前场景、在场 NPC、相关线索和最新 `context_manifest`。普通对话保留在工作上下文中，不每轮写入 Markdown。

**Lite 日循环**

一个游戏日内使用 LITE 模式。每个游戏日结束时，全量更新当前活跃存档和 `saves/context_manifest.md`。新游戏日开始时重新读取当前存档核心文件，然后再次切回 LITE 模式。

## 案例研究

本项目起源于一次真实的长期 AI TRPG 跑团：随着聊天上下文变长，一个关键 NPC 逐渐偏离了最初的身份与动机。

请阅读 [Ghost Island C-12 Investigation](docs/case-studies/ghost-island-c12.md)，了解第一个参考案例以及这个引擎诞生的设计原因。

## 许可

本项目源代码与文本内容公开供学习、研究、个人娱乐和非商业创作使用。

禁止未经授权的商业使用，包括但不限于销售、商业 SaaS、付费产品集成、商业出版、商业素材包、营利性培训或商业化再分发。

详情见 `LICENSE`。

## 引用

如果你在研究、文章、衍生工具或公开的非商业作品中使用本项目，请根据 `CITATION.cff` 进行引用。
