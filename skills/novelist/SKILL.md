---
name: novelist
description: "中文长篇小说/网文创作全流程 Skill。策划模式/试写模式/连载模式/完稿模式/翻译。使用场景：写小说、续写、改稿、大纲、人物档案、世界观、伏笔管理、章节规划、EPUB 导出、字数检查、英文翻译。触发词：小说、网文、连载、大纲、人物、世界观、伏笔、章节、EPUB、字数、翻译、改稿。Triggers on: novel, story, writing, outline, character, worldview, foreshadowing, serialize, chapter, EPUB, wordcount, translate."
---

# Novelist

## Version

- **Version**: `0.9.0`
- **Version Date**: `2026-04-15`
- **Compatibility**: standard Markdown skill loaders that support `name` and `description` frontmatter
- **Previous Versions**: see [CHANGELOG.md](CHANGELOG.md)

## Overview

为中文长篇小说和网文创作提供一套可持续执行的工作流：先稳住设定与大纲，再按章节推进，持续维护人物状态、悬念台账和文风质量，避免写到后面失控、注水或前后打架。

## When to Use

- 用户要从零开始写中文小说、网文、长篇故事、连载故事
- 用户已有设定，想补大纲、人物档案、世界观、章节规划
- 用户要续写已有章节，要求前后连贯
- 用户要重写某章，增强钩子、节奏、对白、人物张力或减少 AI 味
- 用户要将小说导出为 EPUB 电子书
- 用户要检查章节字数
- 用户要翻译成英文

## Parameters

使用 `$ARGUMENTS` 解析用户参数：

| Option | Description |
|--------|-------------|
| `[书名]` | 指定小说项目名称 |
| `--mode 策划\|试写\|连载\|完稿` | 直接进入指定模式 |
| `--chapter N` | 从第 N 章开始续写 |
| `--check-only` | 只做质量检查，不写新内容 |
| `--quick` | 跳过确认环节，使用默认值 |

## Default Working Mode

先判断用户要的交付深度，再选最轻的有效模式：

1. `策划模式`：只做题材定位、故事引擎、大纲、人物、世界观、伏笔台账
2. `试写模式`：策划完成后，只写首章或样章
3. `连载模式`：按章推进，每次交付 1 章或少量连续章节
4. `完稿模式`：只有在用户明确要求整本初稿时，才连续写完整部长篇

如果用户没有说清楚：

- 新项目默认 `策划模式`
- 已有章节的项目默认 `连载模式`
- 模式执行规则请参考 `references/mode-design.md`。

## Intake

只补问真正缺失的关键信息，优先补齐以下 6 项：

- 题材 / 子类型
- 一句话 premise 或核心冲突
- 主角身份、最大欲望、致命缺陷
- 目标读者、文风关键词、禁忌
- 叙事视角（第一人称 / 第三人称 / 群像）
- 篇幅目标与交付模式

如果用户只给了模糊想法，不要空泛追问；应给出具体备选并推荐更稳的方案。

## 书名生成

策划模式开始时，**必须**为小说生成 3-5 个候选书名供用户选择。

→ 加载 [naming-guide.md](references/naming-guide.md) 获取命名原则、标题结构参考和生成流程。

## Required Files

在 `novels/<书名>/` 内创建或更新：

- `00-大纲.md` → 使用 [outline-template.md](references/outline-template.md)
- `01-人物档案.md` → 使用 [character-template.md](references/character-template.md)
- `02-项目管理.md` → 使用 [story-bible-template.md](references/story-bible-template.md)
- `03-世界观与时间线.md` → 使用 [worldview-template.md](references/worldview-template.md)
- `04-章节规划.md` → 使用 [chapter-planning.md](references/chapter-planning.md)
- `第XX章-标题.md` → 使用 [chapter-template.md](references/chapter-template.md)

## Planning Rules

开始批量写章节前，至少锁定以下内容：

- `logline`
- 主线冲突、对抗力量、利害关系
- 主角外部目标与内在成长弧线
- 结局类型与兑现方式
- 采用的结构模板（参见 [plot-structures.md](references/plot-structures.md)）
- 逐章功能分配
- 未回收悬念、伏笔、时间线、关系状态

除非用户明确要求跳过规划，否则不要直接写完全书。即使用户要求"直接开写"，也先产出一页精简总纲再动笔。

## Chapter Loop

每写一章都按这个循环执行：

- [ ] **Step 1: 读取上下文** — 读取 `00-大纲.md`、`02-项目管理.md` 中最近章节摘要、`04-章节规划.md` 中对应章节规划
- [ ] **Step 2: 明确本章目标** — `本章目标 / 阻碍 / 转折 / 结尾钩子`
- [ ] **Step 3: 伏笔回收检查** — 参考 [foreshadowing-guide.md](references/foreshadowing-guide.md)
- [ ] **Step 4: 拆场景** — 先拆 3-6 个场景，再落正文；剧情设计启示参考 `03-世界观与时间线.md` 中维护的所有创作启示
- [ ] **Step 5: 创作关键原则** ⚠️ — 参考 [chapter-guide.md](references/chapter-guide.md)；首章额外参考 [opening-design.md](references/opening-design.md)
- [ ] **Step 6: 细节打磨** — 对话/扩写/连贯性/钩子/场景/文风分别参考：
  - [dialogue-writing.md](references/dialogue-writing.md)
  - [content-expansion.md](references/content-expansion.md)
  - [consistency.md](references/consistency.md)
  - [hook-techniques.md](references/hook-techniques.md)
  - [scene-design.md](references/scene-design.md)
  - [style-polishing.md](references/style-polishing.md)
- [ ] **Step 7: 字数检查** — 长章节交付前运行 `python3 scripts/check_chapter_wordcount.py <章节文件路径>`
- [ ] **Step 8: 质量自查** ⚠️ — 使用 [quality-checklist.md](references/quality-checklist.md) 自查
- [ ] **Step 9: 世界观契合度检查** — 使用 [worldview-consistency-checklist.md](references/worldview-consistency-checklist.md)，特别关注新能力/技术/地点/角色行为是否与设定一致
- [ ] **Step 10: 伏笔自动提取** — 参考 [foreshadowing-guide.md](references/foreshadowing-guide.md)
- [ ] **Step 11: 定期评估与信息回填** ⚠️
  - **每章**：章节信息回填，使用 [plot-health-checklist.md](references/plot-health-checklist.md) 中"章节信息回填检查"部分
  - **每 3 章**：全面剧情健康度评估（节奏、悬念、人物弧线、结构完整性）
  - **每 10 章**：结构完整性深度检查
  - **关键节点**：第一幕结束、中点、高潮前自动触发
  - 评估结果与变更决策记录在 `02-项目管理.md` 的"自检流程配置"部分

### 检查结果处理

1. **发现问题**：记录在对应检查清单中
2. **评估影响**：判断是否必须立即修复
3. **提出方案**：提供调整建议供用户选择
4. **执行修复**：根据用户选择更新相关文档
5. **验证修复**：重新检查确保问题解决

## Export

当用户要求导出 EPUB 时：

1. 确认小说目录路径（用户已提供或在 novels/ 下查找）
2. 运行导出脚本：
   ```bash
   python3 scripts/generate_epub.py <小说目录路径>
   ```
3. 可选参数：
   - `--author <作者名>` 覆盖大纲中的作者
   - `-o <输出路径>` 指定输出文件位置
   - `--lang en` 导出英文版（需要先通过翻译功能生成 `en/` 目录）
4. 告诉用户生成的 EPUB 文件路径

## Quality Bar

每章至少满足：

- 本章发生了不能删除的变化
- 回应、升级或偏转至少一条已有悬念
- 结尾钩子强度与全书位置匹配
- 人物通过动作、选择、对白被展示，而不是只被描述
- 避免空泛形容词堆砌、抽象情绪总结、整段均匀句式和过度书面腔
- 每个章节至少包含若干有任务的场景，而不是流水账拼接

## Completion

在 `完稿模式` 收尾时，必须额外检查：

- 主线悬念是否回收
- 主角弧线是否完成
- 设定规则是否前后一致
- 是否存在遗失角色、断裂线索、无兑现伏笔
- 是否需要留下续作钩子；只有用户要时才保留
- 终稿收尾方式参考 [ending-design.md](references/ending-design.md)

## Translation

当用户要求翻译成英文时：

→ 加载 [translation-guide.md](references/translation-guide.md) 获取完整翻译流程、术语表格式和 subagent 提示词模板。

## Resources

### references/

| File | Purpose | When to Load |
|------|---------|-------------|
| `mode-design.md` | 模式执行规则 | 判断模式时 |
| `naming-guide.md` | 书名生成指南 | 策划模式首次使用 |
| `outline-template.md` | 大纲模板 | 策划阶段 |
| `character-template.md` | 人物档案模板 | 策划阶段 |
| `story-bible-template.md` | 项目管理模板 | 策划阶段 |
| `worldview-template.md` | 世界观模板 | 策划阶段 |
| `chapter-planning.md` | 章节规划模板 | 策划阶段 |
| `chapter-template.md` | 章节模板 | 写作阶段 |
| `plot-structures.md` | 结构模板 | 策划阶段 |
| `chapter-guide.md` | 创作关键原则 | Chapter Loop Step 5 |
| `opening-design.md` | 首章设计 | 写首章时 |
| `foreshadowing-guide.md` | 伏笔管理 | Chapter Loop Step 3, 10 |
| `dialogue-writing.md` | 对话写作 | Chapter Loop Step 6 |
| `content-expansion.md` | 内容扩写 | Chapter Loop Step 6 |
| `consistency.md` | 连贯性维护 | Chapter Loop Step 6 |
| `hook-techniques.md` | 钩子技巧 | Chapter Loop Step 6 |
| `scene-design.md` | 场景设计 | Chapter Loop Step 6 |
| `style-polishing.md` | 文风打磨 | Chapter Loop Step 6 |
| `quality-checklist.md` | 质量检查清单 | Chapter Loop Step 8 |
| `worldview-consistency-checklist.md` | 世界观契合度检查 | Chapter Loop Step 9 |
| `plot-health-checklist.md` | 剧情健康度评估 | Chapter Loop Step 11 |
| `ending-design.md` | 终稿收尾 | 完稿模式 |
| `translation-guide.md` | 翻译流程指南 | 翻译模式 |

### scripts/

| Script | Purpose |
|--------|---------|
| `check_chapter_wordcount.py` | 章节字数统计 |
| `generate_epub.py` | EPUB 导出 |
| `translate_to_english.py` | 英文翻译辅助 |