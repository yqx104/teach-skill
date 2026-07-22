---
name: teach-systematic
description: Plan, generate, and continue a comprehensive dependency-aware course when the workspace COURSE-CONFIG.md records a confirmed systematic mode. Use for durable mastery, professional competence, research, examination, teaching, and transferable problem-solving ability.
---

# Teach Systematic

为已确认的体系模式建立目标范围内完整的能力地图、前置依赖和长期学习路线。完整是指对用户目标所需能力覆盖完整，不是把整个学科无边界地塞入目录。

## 进入条件

每次调用先执行：

1. 读取工作区根目录的 `COURSE-CONFIG.md`。
2. 如果文件缺失或 `mode_status` 不是 `confirmed`，停止并加载 `teach` skill 完成访谈和模式确认。
3. 如果 `mode` 不是 `systematic`，停止并加载 `teach` skill 重新路由；不要修改 mode，也不要生成体系内容。
4. 读取 `MISSION.md`、`LEARNER-PROFILE.md`、`MASTERY-LEDGER.md`、`NOTES.md`、`OUTLINE.md`、`RESOURCES.md`、已有 lesson、quiz、`reviews/` 和 `learning-records/`。不存在的可选文件跳过；如果账本缺失，加载 `teach` 完成初始化与迁移。
5. 比较账本中的 `下次复习` 与当前日期；已到日期且状态为 `未到期` 的项目改成 `到期`，保留优先级更高的 `疑似遗忘`，不要降低等级。

## 决定当前动作

- 用户要求复习、检查遗忘、考试复习、生成复习课件，正在回答未完成的复习考试，或报告完成了最近的复习课件：加载 `teach` skill 执行共享长期复习协议；不要在本 skill 另造一套复习状态。
- 没有 `OUTLINE.md` 或用户已确认需要重规划：执行“规划体系目录”。
- 用户要求下一节课或指定目录中的课程：执行“生成单课”。
- 用户说已经学完并准备接受测验：执行“生成或批改 Quiz”。
- 用户提出问题：围绕当前课程答疑；发现新的能力证据时先更新账本，发现高层误解模式或偏好变化时再更新画像或学习记录。
- 用户目标、可投入时间、深度或范围发生实质变化：停止课程生成，加载 `teach` 重新访谈。

## 规划体系目录

1. 完整读取 [SYSTEMATIC-OUTLINE-FORMAT.md](references/SYSTEMATIC-OUTLINE-FORMAT.md) 和 [QUALITY-GATES.md](references/QUALITY-GATES.md)。
2. 加载 `grilling`，只确认体系规划仍缺失的决定，例如专业深度、数学或理论要求、实践领域、最终综合能力和明确范围边界。一次只问一个问题，不重复询问已有可靠记录的内容。
3. 总结目标能力、课程深度、范围和规划假设，并等待用户确认。如果现有状态已经充分，也要展示摘要并取得确认，不要重新进行完整首次访谈。
4. 搜索并阅读权威教材、官方文档、课程标准、同行评审综述或成熟课程。对可能变化的信息使用最新来源；不要仅依赖参数化记忆。
5. 在可获得的情况下，比较至少两个彼此独立的权威课程或知识结构，识别共同核心、顺序差异和目标相关分支。
6. 创建或更新 `RESOURCES.md`，记录每个来源的可信度、覆盖能力、对应单元和已知缺口。
7. 先建立完整能力地图和前置依赖，再将其裁剪为个性化执行路线。不要直接从一串常见章节标题开始。
8. 按模板创建或更新 `OUTLINE.md`。只规划目录，不同时生成 lesson。
9. 将能力地图中的可独立评估能力、关键前置和迁移目标映射为 `MASTERY-LEDGER.md` 中的稳定 KP ID；保留已有 ID，没有证据的新增点使用 `U 待确认`，不能假定为 L0。
10. 执行体系目录质量闸门。任何一项失败都先补充研究、访谈或修订。
11. 将 `COURSE-CONFIG.md` 的 `course_status` 更新为 `active`。

## 生成单课

一次只生成一节 lesson：

1. 完整读取 [SYSTEMATIC-LESSON-FORMAT.md](references/SYSTEMATIC-LESSON-FORMAT.md) 和 [QUALITY-GATES.md](references/QUALITY-GATES.md)。
2. 从能力地图和课程路线中确认本节位置、前后依赖、可观察成果和掌握证据。
3. 对照 `MASTERY-LEDGER.md`、学习者画像、学习记录、已有 quiz 和上一节讨论，列出 U、L0–L2、`到期` 或 `疑似遗忘` 的本节关键前置和潜在误解。
4. 加载 `grilling`，一次只检查一个未知、到期或疑似遗忘的关键前置或误解。知识诊断不要泄露答案；建议用户不查资料、按真实理解回答。仅到期但检查通过时保留或提升等级，不因日期降级。
5. 向用户总结本节起点、目标、深度、示例语境和假设，并等待明确确认。只有已有近期证据且用户刚刚明确要求继续时，才可将确认压缩成一个简短问题；不得完全跳过 readiness gate。
6. 搜索并阅读本节需要的高可信来源，更新 `RESOURCES.md`。
7. 按模板生成自包含 HTML 到 `./lessons/NNN-<dash-case-name>.html`。编号使用下一个可用序号。
8. 执行单课质量闸门。范围必须小，范围内必须讲完整。
9. 将目录状态从 `计划中` 更新为 `已创建`。不要把“已创建”写成“已掌握”，也不要因 lesson 生成而提升账本等级。
10. 告诉用户本节在能力地图中的位置、建议学习方式和后续连接；不要同时创建 quiz。

## Quiz 与掌握状态

完整读取 [QUIZ-FORMAT.md](references/QUIZ-FORMAT.md)。只有用户学习并讨论完 lesson，且明确说“可以考我了”或等价表达后，才创建 quiz。

- Quiz 同时检查解释、比较、应用、诊断、反例和迁移，不只检查回忆。
- 后续 quiz 应适量混入早期关键能力，形成间隔提取和交错练习。
- 用户回答后记录得分、逐题反馈、误解模式和下一步建议。
- 有真实证据时先更新 `MASTERY-LEDGER.md`；只有高层能力摘要、误解模式或教学策略改变时才更新 `LEARNER-PROFILE.md`，并按需写入 `learning-records/NNN-<dash-case-name>.md`。
- 课程状态依次使用：`计划中`、`已创建`、`已学习`、`已掌握`、`已跳过`。
- 用户只阅读或讨论过课程时标为 `已学习`；只有该 lesson 的核心 KP 达到预定证据标准时才标为 `已掌握`。
- 用户明确确认完成 lesson 时，相关 U 或 L0 知识点最多更新为 L1；生成 lesson 本身不更新等级。
- 综合项目达到 `COURSE-CONFIG.md` 的最终能力和成功标准后，将 `course_status` 更新为 `completed`；不要仅因 lesson 全部创建就宣布完成。

## 资源与学习记录

维护 `RESOURCES.md` 时优先一手资料、权威教材、官方文档、同行评审研究和高质量专业课程。每项写明其覆盖能力、对应单元、选择理由和局限；显式记录知识覆盖缺口。

只在以下情况写学习记录：用户展示了非平凡理解、暴露出已有能力、纠正了重要误解，或目标/模式发生变化。文件使用连续编号，正文以简短标题和 1–3 句话说明证据及其对后续教学的影响；必要时再添加 `Evidence` 或 `Implications`。不要把每次活动写成流水账。

## 课堂中的知识状态回写

- 用户提问时先答疑；提问本身不自动证明遗忘。
- 如果回答、迟疑或自述与账本中的 L2–L4 明显冲突，把相关 KP 标为 `疑似遗忘`，保留原等级并记录信号。
- 该点影响当前课程或后续依赖时，在答疑后做一个短的无提示检查；根据检查实际证据升降等级、调整间隔并清除疑似状态。
- 单次口误但能立即自我纠正时不降级；可以记录易错点并缩短间隔。
- 非关键疑似遗忘留给后续复习，不要把普通答疑强制变成考试。

## 不可违反的规则

- 不要把完整性等同于无边界扩张；所有内容都必须能追溯到目标能力或明确的前置依赖。
- 不要在依赖未满足时推进后续课程。
- 不要使用尚未被证据确认的前置知识。
- 不要因时间到期、lesson 已生成或复习课件已阅读而自动降低或提升掌握等级。
- 不要使用未定义术语或省略关键机制、推导和中间步骤。
- 不要一次生成多节 lesson。
- 不要在 lesson 创建时自动创建 quiz。
- 不要静默改变目标、模式、范围或成功标准。
