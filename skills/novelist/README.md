# novelist

面向中文长篇小说和网文创作的 Markdown skill——不是"随便写个故事"的提示词集合，而是一套可持续执行的长篇创作工作流。

## 为什么用它

- 把模糊脑洞快速落成可执行的大纲
- 让长篇连载不容易写散、写崩、写成模板文
- 强化首章钩子、对白张力、场景拆分和结局收束
- 降低常见 AI 痕迹（空泛情绪句、解释腔、四字词堆砌）

## 适合谁

- 从零开始写中文长篇或网文
- 已有设定，缺总纲、人物档案或分章规划
- 已写几章，想续写并保持前后连贯
- 想重写某章，增强钩子、对白或人物张力

## 快速开始

```text
使用 novelist，帮我策划一部 20 章的悬疑小说。
```

```text
使用 novelist，继续写 novels/夜雨旧案/ 里的下一章。
```

```text
使用 novelist --mode 完稿 --chapter 15，从第 15 章开始连续完稿。
```

```text
使用 novelist --check-only novels/夜雨旧案/，只做质量检查不写新内容。
```

如果你的工具支持按 skill 名调用，优先显式写出 `novelist`。

## 参数

| 参数 | 说明 |
|------|------|
| `[书名]` | 指定小说项目名称 |
| `--mode 策划\|试写\|连载\|完稿` | 直接进入指定模式 |
| `--chapter N` | 从第 N 章开始续写 |
| `--check-only` | 只做质量检查，不写新内容 |
| `--quick` | 跳过确认环节，使用默认值 |

## 四种工作模式

| 模式 | 何时使用 |
|------|----------|
| `策划模式` | 新项目，先做题材定位、大纲、人物、世界观、伏笔台账 |
| `试写模式` | 策划完成后，先写首章或样章验证文风 |
| `连载模式` | 按章推进，每次交付 1 章或少量连续章节 |
| `完稿模式` | 用户明确要求整本初稿时，连续写完整部 |

推荐顺序：策划 → 试写首章 → 逐章连载。不建议一开始就从第 1 章写到第 30 章。

## 安装

1. 下载或克隆本仓库
2. 把整个目录放到对应工具的 skill 目录中
3. 让工具重新加载 skill

支持 `Codex`、`Claude Code`、`OpenCode`、`OpenClaw` 等工具，具体路径和加载方式请以对应工具文档为准。

## 产出物

```text
novels/
└── 书名/
    ├── 00-大纲.md
    ├── 01-人物档案.md
    ├── 02-项目管理.md
    ├── 03-世界观与时间线.md
    ├── 04-章节规划.md
    ├── 第01章-章节标题.md
    ├── 第02章-章节标题.md
    └── ...
```

## 内置能力

- **开篇与章节推进**：[chapter-guide.md](references/chapter-guide.md)、[opening-design.md](references/opening-design.md)、[scene-design.md](references/scene-design.md)、[hook-techniques.md](references/hook-techniques.md)
- **人物、对白与文风**：[dialogue-writing.md](references/dialogue-writing.md)、[style-polishing.md](references/style-polishing.md)、[character-template.md](references/character-template.md)
- **长篇连贯与结构**：[plot-structures.md](references/plot-structures.md)、[consistency.md](references/consistency.md)、[story-bible-template.md](references/story-bible-template.md)、[outline-template.md](references/outline-template.md)
- **扩写与收尾**：[content-expansion.md](references/content-expansion.md)、[ending-design.md](references/ending-design.md)、[quality-checklist.md](references/quality-checklist.md)
- **书名生成**：[naming-guide.md](references/naming-guide.md)
- **翻译**：[translation-guide.md](references/translation-guide.md)

完整 references 索引见 [SKILL.md Resources 章节](SKILL.md)。

## 字数检查

```bash
python3 scripts/check_chapter_wordcount.py novels/书名/第01章-标题.md
python3 scripts/check_chapter_wordcount.py --all novels/书名
python3 scripts/check_chapter_wordcount.py novels/书名/第01章-标题.md 2500
```

## 导出 EPUB

```bash
python3 scripts/generate_epub.py novels/书名
python3 scripts/generate_epub.py novels/书名 --author "肥猫" -o output.epub
python3 scripts/generate_epub.py novels/书名 --lang en
```

前提：`00-大纲.md` 存在、章节文件以 `第` 开头。EPUB 只导出 `## 正文` 部分。

## 翻译成英文

```text
使用 novelist，帮我把这本小说翻译成英文。
```

翻译流程（术语提取 → 并行翻译 → 最终校对）详见 [translation-guide.md](references/translation-guide.md)。英文版保存在 `en/` 目录，同样支持导出 EPUB。

## 兼容性与版本

- 当前版本：`0.9.0`
- 版本记录：见 [CHANGELOG.md](CHANGELOG.md)
- SKILL.md frontmatter 保持最小化，优先兼容只识别 `name` 与 `description` 的 skill loader

## 常见问题

### 为什么不建议直接一次写完整本书？

因为中文长篇最容易在中段失控。先规划、再试写、再连载，通常质量更稳。

### 适合哪些题材？

悬疑、言情、奇幻、仙侠、科幻、都市现实、群像长篇都可以。它偏长篇叙事流程，而不是某个单一题材。

### 只适合某一个工具吗？

不是。它尽量保持对主流 skill 工具的兼容性，具体加载方式取决于工具本身。

## 许可证

MIT
