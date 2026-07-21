# Teach Skills

这套 skills 把当前工作区变成一个有状态的学习环境，并根据用户目标选择两种独立课程模式：

- **速成版**：围绕近期交付物建立最短可靠路径。
- **体系版**：围绕长期掌握建立完整能力地图和前置依赖。

“速成”只缩小范围，不降低讲解完整性；“体系”追求目标范围内完整，不做无边界扩张。

## 三个 skills

- `teach`：入口路由器。使用 `grilling` 逐题确认目标、当前基础、约束和成功标准，推荐并记录课程模式。
- `teach-fast`：只负责速成版目录、lesson、quiz 和学习进度。
- `teach-systematic`：只负责体系版能力地图、目录、lesson、quiz 和学习进度。

首次确认后，工作区中的 `COURSE-CONFIG.md` 成为模式的唯一事实来源。后续教学自动进入对应执行 skill，不再反复询问用户选择速成版还是体系版。

## 工作区文件

- `COURSE-CONFIG.md`：模式、状态、节奏和路由依据。
- `MISSION.md`：为什么学习、成功的样子和范围边界。
- `LEARNER-PROFILE.md`：已掌握、部分掌握、未知、误解、环境和教学偏好，并记录证据。
- `OUTLINE.md`：当前模式的课程目录。
- `RESOURCES.md`：课程依赖的高可信来源及覆盖范围。
- `lessons/*.html`：自包含课程。
- `quiz/*.md`：用户学完并明确表示准备好后生成的测验。
- `learning-records/*.md`：会影响后续教学的重要能力证据和认知变化。
- `NOTES.md`：其他教学偏好。

## 安装

将三个 skill 目录都复制到 skills 目录：

如果已经安装旧版 `teach`，先把旧目录移到工作区外备份，确保下面三个目标目录不存在。这样不会残留旧版格式文件。

```bash
git clone https://github.com/yqx104/teach-skill.git
mkdir -p ~/.agents/skills
cp -R teach-skill/teach ~/.agents/skills/teach
cp -R teach-skill/teach-fast ~/.agents/skills/teach-fast
cp -R teach-skill/teach-systematic ~/.agents/skills/teach-systematic
```

这套 skills 还需要本地安装名为 `grilling` 的 skill。入口和两个执行 skill 都使用它进行一次一题的目标访谈或课前 readiness check。

## 使用方式

从 `teach` 开始，不要直接从两个执行 skill 创建新课程：

```text
使用 teach skill 教我 RAG。我想做一个能演示的项目，但还不确定该走速成还是体系路线。
```

首次流程：

1. 检查工作区已有事实和学习记录。
2. 一次只询问一个目标或能力问题。
3. 推荐速成版或体系版，并解释理由。
4. 用户确认后写入课程配置、使命和学习者画像。
5. 路由到对应执行 skill 规划课程目录。
6. 后续一次只生成一节 lesson。
7. 用户学习并讨论后，明确说“可以考我了”才生成 quiz。

## 模式切换

模式不会静默切换。用户改变目标时，`teach` 会重新访谈、说明影响、等待确认、归档旧目录，并保留已有 lesson、quiz 和学习记录。

## 仓库结构

```text
teach/               入口、访谈协议和状态文件格式
teach-fast/          速成版课程规则和模板
teach-systematic/    体系版课程规则和模板
```
