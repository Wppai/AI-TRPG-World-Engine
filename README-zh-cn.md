# The Ghost Iland

一个用于长期运行 AI TRPG 世界模拟的状态仓库。

这个仓库的目标不是保存聊天记录，而是保存一个持续存在、逻辑自洽、状态可追踪的 TRPG 世界。世界状态文件是模拟的事实来源，聊天记录只能作为辅助上下文。

## 目录结构

- `rules/`：世界引擎规则与运行原则。
- `state/`：当前世界状态、玩家状态、时间线与线索。
- `npcs/`：NPC 文件，每个 NPC 单独保存。
- `logs/`：会话日志，只记录实际发生的事情。
- `templates/`：新建 NPC 或其他实体时使用的模板。
- `.agents/skills/ai-trpg-world-engine/`：用于 Codex 的 AI TRPG 世界引擎 Skill。

## 每次会话开始的读取顺序

继续游玩或维护世界前，按以下顺序读取：

1. `rules/engine_rules.md`
2. `state/world_state.md`
3. `state/timeline.md`
4. `state/player.md`
5. `npcs/` 中相关 NPC 文件
6. `state/clues.md`
7. `logs/session_log.md` 中最近的记录

## 维护规则

- `state/timeline.md` 只能追加，不要重写历史。
- 世界当前状态变化时，更新 `state/world_state.md`。
- 玩家状态变化时，更新 `state/player.md`。
- NPC 的行为只能依据其文件中记录的目标、动机和已知信息。
- 线索必须区分事实、推论、猜测和传闻。
- `logs/session_log.md` 只记录发生了什么，不记录隐藏真相或 GM 信息。

## 许可

本项目源代码与文本内容公开供学习、研究、个人娱乐和非商业创作使用。

禁止未经授权的商业使用，包括但不限于销售、商业 SaaS、付费产品集成、商业出版、商业素材包、营利性培训或商业化再分发。

详情见 `LICENSE`。
