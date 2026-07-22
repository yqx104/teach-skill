---
name: teach
description: Route and manage a stateful long-term learning program by interviewing the learner, confirming a fast-track or systematic course mode, maintaining evidence-based knowledge mastery and review schedules, running personalized review exams or review courseware, and dispatching curriculum and lesson work to the matching teaching skill. Use when starting, resuming, reviewing, re-planning, or switching a persistent course in a workspace.
---

# Teach Course Router

把当前目录视为有状态的长期教学工作区。负责访谈、模式确认、知识状态维护、复习和路由；常规课程目录与 lesson 交给执行 skill。

## 每次调用都先决定动作

1. 检查工作区中的 `COURSE-CONFIG.md`。
2. 如果文件不存在、`mode_status` 不是 `confirmed`，或用户的目标已经改变，执行“首次访谈与模式确认”。
3. 配置已确认后，确保 `MASTERY-LEDGER.md` 存在；缺失时执行“掌握度账本初始化与迁移”。
4. 比较账本中的 `下次复习` 与当前日期；已到日期且状态为 `未到期` 的项目改成 `到期`，保留优先级更高的 `疑似遗忘`，不要降低等级。
5. 如果用户要求复习、检查遗忘、考试复习、生成复习课件，正在回答 `reviews/` 中未完成的复习考试，或报告完成了最近的复习课件，完整读取 [REVIEW-PROTOCOL.md](references/REVIEW-PROTOCOL.md) 并执行；此时不要路由到常规课程生成。
6. 如果 `mode: fast`，加载并遵循已安装的 `teach-fast` skill。
7. 如果 `mode: systematic`，加载并遵循已安装的 `teach-systematic` skill。
8. 如果记录了其他 mode，停止并修正配置；不要猜测路由。
9. 如果对应的执行 skill 未安装，说明缺失的确切 skill 名称并停止；不要在 `teach` 中退化生成常规课程。

`COURSE-CONFIG.md` 是模式的唯一事实来源。不要从 `OUTLINE.md` 文件名、课程数量或用户的一句临时表达推断模式。

## 首次访谈与模式确认

完整读取 [INTAKE-PROTOCOL.md](references/INTAKE-PROTOCOL.md)，然后执行以下硬闸门：

1. 先检查本地文件、项目、旧课程、学习记录和已有测验；能够从环境确认的事实不要再问用户。
2. 加载并遵循已安装的 `grilling` skill。一次只问一个问题，并等待用户回答后再继续。
3. 依次确认真实目标、可观察成果、截止时间、投入时间、当前能力证据、关键前置知识、实践环境、期望深度、教学偏好和范围边界。
4. 对学习目标、课程范围和模式等决策给出推荐答案；对知识诊断题不要泄露正确答案，只建议用户不查资料、按真实理解回答。
5. 在信息充分后，总结：学习使命、当前基础、未知项、成功标准、约束、推荐模式、推荐理由、范围内和范围外内容。
6. 明确询问用户是否确认双方已经达成共同理解。
7. 在用户明确确认前，不得创建或修改 `COURSE-CONFIG.md`、`MISSION.md`、`LEARNER-PROFILE.md`、`MASTERY-LEDGER.md`、`OUTLINE.md` 或 lesson。
8. 用户确认后，按照以下格式写入状态文件：
   - [COURSE-CONFIG-FORMAT.md](references/COURSE-CONFIG-FORMAT.md)
   - [MISSION-FORMAT.md](references/MISSION-FORMAT.md)
   - [LEARNER-PROFILE-FORMAT.md](references/LEARNER-PROFILE-FORMAT.md)
   - [MASTERY-LEDGER-FORMAT.md](references/MASTERY-LEDGER-FORMAT.md)
9. 写入后立刻按已确认的 mode 路由到对应执行 skill。

如果 `grilling` 不可用，严格复现其交互约束：一次只问一个问题、先查事实再问决定、给决策提供推荐、在共同理解得到明确确认前不行动。

## 掌握度账本初始化与迁移

完整读取 [MASTERY-LEDGER-FORMAT.md](references/MASTERY-LEDGER-FORMAT.md)。

- 新课程只登记访谈中出现且与目标相关的知识点；执行 skill 创建 `OUTLINE.md` 后再补齐课程能力节点。
- 现有工作区缺少账本时，从 `LEARNER-PROFILE.md`、`OUTLINE.md`、quiz、项目和 `learning-records/` 提取知识点与证据。
- 没有证据时使用 `U 待确认`；只有证据显示目前不会时才使用 `L0 陌生`。不要根据 lesson 已创建、已阅读或旧目录状态推断掌握。
- 保留历史证据的原日期并按默认间隔计算下次复习；证据没有可靠日期时标为 `到期`，不要假装它仍然新鲜。
- 为知识点分配稳定 ID；后续重命名保留 ID，移出范围时归档而不复用 ID。
- 初始化是状态迁移，不改变使命、模式和范围；完成后继续当前动作。

## 模式选择

### 推荐 `fast`

在以下信号占主导时推荐速成版：

- 有明确、近期的交付物或截止时间。
- 目标是完成一个范围有限的任务。
- 用户接受暂时跳过不影响交付的理论分支。
- 成功标准主要是“能够做出或完成某件事”。

### 推荐 `systematic`

在以下信号占主导时推荐体系版：

- 目标是长期、可迁移的专业能力。
- 未来需要独立处理未见过的问题。
- 学习用于职业、研究、考试或教学。
- 用户愿意补齐前置知识和底层原理。
- 成功标准主要是“能够解释、应用、诊断并迁移”。

如果用户既有近期交付又想长期掌握，只确认当前模式。通常建议先完成速成版，再显式切换到体系版；不要发明第三种混合模式。

## 现有工作区迁移

如果已有 `OUTLINE.md` 或 lesson，但没有 `COURSE-CONFIG.md`：

1. 保留全部已有文件，不覆盖、不删除。
2. 阅读旧目录、课程、`MISSION.md`、`RESOURCES.md`、quiz 和学习记录。
3. 使用首次访谈流程确认旧目标是否仍然有效，并推荐 `fast` 或 `systematic`。
4. 用户确认后创建四份状态文件，再交给对应执行 skill 审计和调整旧目录。

## 模式切换

只有用户明确要求或目标实质变化时才切换模式：

1. 加载 `grilling`，确认切换原因、新成功标准、时间和范围。
2. 说明切换对现有路线和进度的影响。
3. 等待用户明确确认。
4. 保留旧 `OUTLINE.md`；将其移动到 `archive/OUTLINE-{old-mode}-v{n}.md`，不要删除。
5. 更新 `COURSE-CONFIG.md`、`MISSION.md`、`LEARNER-PROFILE.md` 和账本中的范围映射；保留知识点 ID 与历史证据。
6. 在 `learning-records/` 中记录模式变化及其对后续教学的影响。
7. 路由到新的执行 skill，由它重新规划目录。

## 状态维护规则

- `MISSION.md` 只记录为什么学、成功的样子和边界。
- `LEARNER-PROFILE.md` 记录高层能力摘要、误解、环境和教学偏好，不充当逐知识点数据库。
- `MASTERY-LEDGER.md` 是每个可评估知识点的当前等级、复习状态、证据和下次复习日期的唯一事实来源。
- `COURSE-CONFIG.md` 记录模式、状态、节奏和路由依据。
- 不要把“用户听过”记录成“用户已掌握”。阅读或听课最多支持 `L1 已接触`；提升到更高等级必须有回答、练习、项目或测验证据。
- 日期到期只把复习状态改为 `到期`，不能自动降低掌握等级。
- 用户的提问、迟疑或自述遗忘与账本冲突时，先标记 `疑似遗忘`；只有定向检查提供证据后才升降等级。
- 用户改变使命前必须确认；确认后同步更新状态文件并写学习记录。
- 除 [REVIEW-PROTOCOL.md](references/REVIEW-PROTOCOL.md) 定义的复习考试和复习课件外，不要在此 skill 中创建 quiz、lesson 或课程目录。
