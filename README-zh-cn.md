# AI TRPG World Engine

一个用于长期运行 AI TRPG 世界模拟与状态管理的系统仓库。

这个仓库的目标不是保存聊天记录，而是保存持续存在、逻辑自洽、状态可追踪的 TRPG 世界。引擎文件定义可复用的运行规则，`saves/` 下的每个存档保存一个故事或战役的事实来源。聊天记录只能作为辅助上下文。

## 目录结构

- `rules/`：可复用的世界引擎规则与运行原则。
- `saves/`：故事或战役存档。
- `saves/active_save.md`：当前活跃存档指针。
- `saves/_template/`：新故事使用的空存档模板。
- `saves/ghost-island/`：从原始项目结构迁移来的第一个故事存档。
- `saves/<save-name>/save.md`：某个存档的元数据，包括状态。
- `saves/<save-name>/state/`：某个存档的世界、玩家、时间线与线索状态。
- `saves/<save-name>/npcs/`：某个存档中的 NPC 文件，每个 NPC 单独保存。
- `saves/<save-name>/logs/`：某个存档的会话日志。
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

复制 `saves/_template/` 为 `saves/<new-save-name>/`，填写 `saves/<new-save-name>/save.md`，并更新 `saves/active_save.md`。旧故事完结后保留其存档，不要继续修改，除非你明确要续写或修订该故事。

## 维护规则

- 当前存档的 `state/timeline.md` 只能追加，不要重写历史。
- 世界当前状态变化时，更新当前存档的 `state/world_state.md`。
- 玩家状态变化时，更新当前存档的 `state/player.md`。
- NPC 的行为只能依据其文件中记录的目标、动机和已知信息。
- 线索必须区分事实、推论、猜测和传闻。
- 当前存档的 `logs/session_log.md` 只记录发生了什么，不记录隐藏真相或 GM 信息。

## 许可

本项目源代码与文本内容公开供学习、研究、个人娱乐和非商业创作使用。

禁止未经授权的商业使用，包括但不限于销售、商业 SaaS、付费产品集成、商业出版、商业素材包、营利性培训或商业化再分发。

详情见 `LICENSE`。

## 引用

如果你在研究、文章、衍生工具或公开的非商业作品中使用本项目，请根据 `CITATION.cff` 进行引用。
