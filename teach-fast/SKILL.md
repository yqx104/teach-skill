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
4. 读取 `MISSION.md`、`LEARNER-PROFILE.md`、`NOTES.md`、`OUTLINE.md`、`RESOURCES.md`、已有 lesson、quiz 和 `learning-records/`。不存在的可选文件跳过。

## 决定当前动作

- 没有 `OUTLINE.md` 或用户已确认需要重规划：执行“规划速成目录”。
- 用户要求下一节课或指定目录中的课程：执行“生成单课”。
- 用户说已经学完并准备接受测验：执行“生成或批改 Quiz”。
- 用户提出问题：先围绕当前课程答疑；发现新的能力证据、误解或偏好时更新画像或学习记录。
- 用户目标、期限或范围发生实质变化：停止课程生成，加载 `teach` 重新访谈。

## 规划速成目录

1. 完整读取 [FAST-OUTLINE-FORMAT.md](references/FAST-OUTLINE-FORMAT.md) 和 [QUALITY-GATES.md](references/QUALITY-GATES.md)。
2. 加载 `grilling`，只确认速成路径仍缺失的决定，例如最终交付物形态、运行环境、截止时间和验收标准。一次只问一个问题，不重复询问已有可靠记录的内容。
3. 总结最短关键路径、明确跳过项和交付标准，并等待用户确认规划前提。如果现有状态已覆盖所有问题，也要展示摘要并取得确认，不要重新进行完整首次访谈。
4. 搜索并阅读支持目标任务所需的高可信来源。优先官方文档、一手资料、权威教材和维护良好的专业资料；对可能变化的信息使用最新来源。不要仅依赖参数化记忆。
5. 创建或更新 `RESOURCES.md`，为每个来源记录其覆盖内容、使用场景和对应课程；显式记录仍缺少可靠来源的部分。
6. 按模板创建 `OUTLINE.md`。只规划目录，不同时生成 lesson。
7. 执行速成目录质量闸门。任何一项失败都先修订目录。
8. 将 `COURSE-CONFIG.md` 的 `course_status` 更新为 `active`。

## 生成单课

一次只生成一节 lesson：

1. 完整读取 [FAST-LESSON-FORMAT.md](references/FAST-LESSON-FORMAT.md) 和 [QUALITY-GATES.md](references/QUALITY-GATES.md)。
2. 从 `OUTLINE.md` 确认本节成果、前置能力和验收方式。
3. 对照 `LEARNER-PROFILE.md`、学习记录、已有 quiz 和上一节讨论，列出仍未确认的本节前置知识。
4. 加载 `grilling`，一次只检查一个未知前置、当前阻塞或环境差异。知识诊断不要泄露答案；建议用户不查资料、按真实理解回答。
5. 向用户总结本节起点、目标、讲解深度、示例环境和仍然采用的假设，并等待明确确认。只有已有近期证据且用户刚刚明确要求继续时，才可将确认压缩成一个简短问题；不得完全跳过 readiness gate。
6. 需要新知识时先研究并更新 `RESOURCES.md`。
7. 按模板生成自包含 HTML 到 `./lessons/NNN-<dash-case-name>.html`。编号使用下一个可用序号。
8. 执行单课质量闸门。范围必须小，范围内必须讲完整。
9. 将目录状态从 `计划中` 更新为 `已创建`。不要把“已创建”写成“已掌握”。
10. 告诉用户本节的具体成果和建议的学习方式；不要同时创建 quiz。

## Quiz 与掌握状态

完整读取 [QUIZ-FORMAT.md](references/QUIZ-FORMAT.md)。只有用户学习并讨论完 lesson，且明确说“可以考我了”或等价表达后，才创建 quiz。

- Quiz 重点验证用户能否完成目标任务、诊断常见失败并解释关键选择。
- 用户回答后，记录得分、逐题反馈和仍需补强的能力。
- 有真实证据时更新 `LEARNER-PROFILE.md`，并按需写入 `learning-records/NNN-<dash-case-name>.md`。
- 课程状态依次使用：`计划中`、`已创建`、`已学习`、`已掌握`、`已跳过`。
- 用户只阅读或讨论过课程时标为 `已学习`；只有练习、项目或 quiz 提供足够证据时才标为 `已掌握`。
- 最终实战满足 `COURSE-CONFIG.md` 的成功标准后，将 `course_status` 更新为 `completed`；不要仅因 lesson 全部创建就宣布完成。

## 资源与学习记录

维护 `RESOURCES.md` 时只保留高可信且与当前交付直接相关的来源。每项写明覆盖内容、适用课程和选择理由；五个精确来源胜过大量泛泛链接。

只在以下情况写学习记录：用户展示了非平凡理解、暴露出已有能力、纠正了重要误解，或目标/模式发生变化。文件使用连续编号，正文以简短标题和 1–3 句话说明证据及其对后续教学的影响；必要时再添加 `Evidence` 或 `Implications`。不要把每次活动写成流水账。

## 不可违反的规则

- 不要扩张成完整学科课程；把非关键内容放入“明确跳过”和“转入体系版的建议”。
- 不要为了快速而省略关键推理、中间步骤、术语解释、验证或排错。
- 不要使用尚未被证据确认的前置知识。
- 不要一次生成多节 lesson。
- 不要在 lesson 创建时自动创建 quiz。
- 不要静默改变目标、模式、范围或成功标准。
