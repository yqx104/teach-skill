---
name: teach-fast
description: Plan, generate, and continue a detailed outcome-first fast-track course when the workspace COURSE-CONFIG.md records a confirmed fast mode. Use for deadline-driven, bounded learning outcomes that need the shortest reliable path to a real deliverable.
---

# Teach Fast Track

为已确认的速成模式规划和教授课程。速成意味着缩小范围并聚焦关键路径，不意味着少解释、跳步骤或默认用户已经掌握前置知识。

## 进入条件

每次调用先执行：

1. 读取工作区根目录的 `COURSE-CONFIG.md`。
2. 如果文件缺失或 `mode_status` 不是 `confirmed`，停止并加载 `teach` skill 完成访谈和模式确认。
3. 如果 `mode` 不是 `fast`，停止并加载 `teach` skill 重新路由；不要修改 mode，也不要生成速成内容。
4. 读取 `MISSION.md`、`LEARNER-PROFILE.md`、`MASTERY-LEDGER.md`、`NOTES.md`、`OUTLINE.md`、`RESOURCES.md`、已有 lesson、quiz、`reviews/` 和 `learning-records/`。不存在的可选文件跳过；如果账本缺失，加载 `teach` 完成初始化与迁移。
5. 比较账本中的 `下次复习` 与当前日期；已到日期且状态为 `未到期` 的项目改成 `到期`，保留优先级更高的 `疑似遗忘`，不要降低等级。

## 决定当前动作

- 用户要求复习、检查遗忘、考试复习、生成复习课件，正在回答未完成的复习考试，或报告完成了最近的复习课件：加载 `teach` skill 执行共享长期复习协议；不要在本 skill 另造一套复习状态。
- 没有 `OUTLINE.md` 或用户已确认需要重规划：执行“规划速成目录”。
- 用户要求下一节课或指定目录中的课程：执行“生成单课”。
- 用户说已经学完并准备接受测验：执行“生成或批改 Quiz”。
- 用户提出问题：先围绕当前课程答疑；发现新的能力证据时先更新账本，发现高层误解模式或偏好变化时再更新画像或学习记录。
- 用户目标、期限或范围发生实质变化：停止课程生成，加载 `teach` 重新访谈。

## 规划速成目录

1. 完整读取 [FAST-OUTLINE-FORMAT.md](references/FAST-OUTLINE-FORMAT.md) 和 [QUALITY-GATES.md](references/QUALITY-GATES.md)。
2. 加载 `grilling`，只确认速成路径仍缺失的决定，例如最终交付物形态、运行环境、截止时间和验收标准。一次只问一个问题，不重复询问已有可靠记录的内容。
3. 总结最短关键路径、明确跳过项和交付标准，并等待用户确认规划前提。如果现有状态已覆盖所有问题，也要展示摘要并取得确认，不要重新进行完整首次访谈。
4. 搜索并阅读支持目标任务所需的高可信来源。优先官方文档、一手资料、权威教材和维护良好的专业资料；对可能变化的信息使用最新来源。不要仅依赖参数化记忆。
5. 创建或更新 `RESOURCES.md`，为每个来源记录其覆盖内容、使用场景和对应课程；显式记录仍缺少可靠来源的部分。
6. 按模板创建 `OUTLINE.md`。只规划目录，不同时生成 lesson。
7. 将目录中的可独立评估成果、关键前置和最终任务映射为 `MASTERY-LEDGER.md` 中的稳定 KP ID；保留已有 ID，没有证据的新增点使用 `U 待确认`，不能假定为 L0。
8. 执行速成目录质量闸门。任何一项失败都先修订目录。
9. 将 `COURSE-CONFIG.md` 的 `course_status` 更新为 `active`。

## 生成单课

一次只生成一节 lesson：

1. 完整读取 [FAST-LESSON-FORMAT.md](references/FAST-LESSON-FORMAT.md) 和 [QUALITY-GATES.md](references/QUALITY-GATES.md)。
2. 从 `OUTLINE.md` 确认本节成果、前置能力和验收方式。
3. 对照 `MASTERY-LEDGER.md`、学习者画像、学习记录、已有 quiz 和上一节讨论，列出 U、L0–L2、`到期` 或 `疑似遗忘` 的本节关键前置。
4. 加载 `grilling`，一次只检查一个未知、到期或疑似遗忘的关键前置、当前阻塞或环境差异。知识诊断不要泄露答案；建议用户不查资料、按真实理解回答。仅到期但检查通过时保留或提升等级，不因日期降级。
5. 向用户总结本节起点、目标、讲解深度、示例环境和仍然采用的假设，并等待明确确认。只有已有近期证据且用户刚刚明确要求继续时，才可将确认压缩成一个简短问题；不得完全跳过 readiness gate。
6. 需要新知识时先研究并更新 `RESOURCES.md`。
7. 按模板生成自包含 HTML 到 `./lessons/NNN-<dash-case-name>.html`。编号使用下一个可用序号。
8. 执行单课质量闸门。范围必须小，范围内必须讲完整。
9. 将目录状态从 `计划中` 更新为 `已创建`。不要把“已创建”写成“已掌握”，也不要因 lesson 生成而提升账本等级。
10. 告诉用户本节的具体成果和建议的学习方式；不要同时创建 quiz。

## Quiz 与掌握状态

完整读取 [QUIZ-FORMAT.md](references/QUIZ-FORMAT.md)。只有用户学习并讨论完 lesson，且明确说“可以考我了”或等价表达后，才创建 quiz。

- Quiz 重点验证用户能否完成目标任务、诊断常见失败并解释关键选择。
- 用户回答后，记录得分、逐题反馈和仍需补强的能力。
- 有真实证据时先更新 `MASTERY-LEDGER.md`；只有高层能力摘要、误解模式或教学策略改变时才更新 `LEARNER-PROFILE.md`，并按需写入 `learning-records/NNN-<dash-case-name>.md`。
- 课程状态依次使用：`计划中`、`已创建`、`已学习`、`已掌握`、`已跳过`。
- 用户只阅读或讨论过课程时标为 `已学习`；只有该 lesson 的核心 KP 达到预定证据标准时才标为 `已掌握`。
- 用户明确确认完成 lesson 时，相关 U 或 L0 知识点最多更新为 L1；生成 lesson 本身不更新等级。
- 最终实战满足 `COURSE-CONFIG.md` 的成功标准后，将 `course_status` 更新为 `completed`；不要仅因 lesson 全部创建就宣布完成。

## 资源与学习记录

维护 `RESOURCES.md` 时只保留高可信且与当前交付直接相关的来源。每项写明覆盖内容、适用课程和选择理由；五个精确来源胜过大量泛泛链接。

只在以下情况写学习记录：用户展示了非平凡理解、暴露出已有能力、纠正了重要误解，或目标/模式发生变化。文件使用连续编号，正文以简短标题和 1–3 句话说明证据及其对后续教学的影响；必要时再添加 `Evidence` 或 `Implications`。不要把每次活动写成流水账。

## 课堂中的知识状态回写

- 用户提问时先答疑；提问本身不自动证明遗忘。
- 如果回答、迟疑或自述与账本中的 L2–L4 明显冲突，把相关 KP 标为 `疑似遗忘`，保留原等级并记录信号。
- 该点影响当前任务或下一节前置时，在答疑后做一个短的无提示检查；根据检查实际证据升降等级、调整间隔并清除疑似状态。
- 单次口误但能立即自我纠正时不降级；可以记录易错点并缩短间隔。
- 非关键疑似遗忘留给后续复习，不要把普通答疑强制变成考试。

## 不可违反的规则

- 不要扩张成完整学科课程；把非关键内容放入“明确跳过”和“转入体系版的建议”。
- 不要为了快速而省略关键推理、中间步骤、术语解释、验证或排错。
- 不要使用尚未被证据确认的前置知识。
- 不要因时间到期、lesson 已生成或复习课件已阅读而自动降低或提升掌握等级。
- 不要一次生成多节 lesson。
- 不要在 lesson 创建时自动创建 quiz。
- 不要静默改变目标、模式、范围或成功标准。
