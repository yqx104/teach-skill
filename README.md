# Teach Skill

`teach` 是一个 Codex skill，用于把当前工作区变成一个有状态的学习环境。

它不是为一次性问答设计的，而是帮助用户在多个会话中持续学习一个主题。它会记录学习使命、学习路线、可信资源、课程、小测验和学习记录，让后续教学能接着之前的上下文继续推进。

## 它做什么

这个 skill 会引导 Codex 通过一组持久化文件进行教学：

- `MISSION.md` 记录用户为什么想学习这个主题。
- `OUTLINE.md` 定义学习路线图和课程顺序。
- `RESOURCES.md` 收集后续课程应依赖的可信来源。
- `lessons/*.html` 保存聚焦、独立、可复习的课程。
- `quiz/*.md` 保存用户完成并讨论课程后生成的小测验。
- `learning-records/*.md` 记录已经确认的理解、被纠正的误解，以及重要学习节点。
- `NOTES.md` 记录用户关于教学方式的偏好。

目标是让学习能够累积。每节课都应该基于用户的真实使命、已有进度和当前最近发展区来设计。

## 设计原则

- 从用户的真实世界使命出发，而不是从抽象主题出发。
- 优先使用高质量外部资源，而不是依赖模型记忆。
- 每节课保持足够小，让用户能快速完成。
- 在合适的地方使用提取练习、间隔学习和交错练习。
- 记录真正影响后续教学的学习进展，而不是写活动流水账。
- 只有在用户学习并讨论完课程后，才生成 quiz。

## 仓库文件

- `SKILL.md` 包含主要 skill 指令。
- `MISSION-FORMAT.md` 定义 `MISSION.md` 的格式。
- `OUTLINE-FORMAT.md` 定义 `OUTLINE.md` 的格式。
- `RESOURCES-FORMAT.md` 定义 `RESOURCES.md` 的格式。
- `LEARNING-RECORD-FORMAT.md` 定义学习记录的格式。
- `QUIZ-FORMAT.md` 定义 quiz 的格式。

## 安装

将这个仓库 clone 或复制到你的 Codex skills 目录：

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/yqx104/teach-skill.git ~/.agents/skills/teach
```

如果你本地已经有 `teach` skill，请先备份或移除旧目录，再执行 clone。

## 使用方式

在你想学习的工作区里打开 Codex 会话，然后带着学习目标调用这个 skill，例如：

```text
使用 teach skill 教我学习 RAG，我想做出一个可运行的原型。
```

这个 skill 会先澄清你的学习使命、当前基础和约束条件。之后，它会创建或更新学习工作区文件，并一次只生成一节课程。

## 推荐工作流

1. 在 `MISSION.md` 中定义学习使命。
2. 在 `OUTLINE.md` 中建立紧凑的学习路线图。
3. 在 `RESOURCES.md` 中收集高质量来源。
4. 每次只在 `lessons/` 中生成一节聚焦课程。
5. 和 Codex 讨论这节课。
6. 准备好后再请求 quiz。
7. 在 `learning-records/` 中记录有意义的学习进展。

## 说明

这个 skill 有意保持轻量。它不试图成为完整的学习管理系统，而是让 Codex 在持续教学时始终围绕用户的目标、证据和进展来生成有用的课程。
