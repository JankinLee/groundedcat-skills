# groundedcat-skills

A collection of production-grade agent skills for Claude Code and other AI agent terminals.

<p align="center">
  <img src="https://img.shields.io/badge/Skills-1-blue" alt="1 Skill" />
  <img src="https://img.shields.io/badge/License-MIT-yellow" alt="MIT License" />
</p>

## Skills

| Skill | Description | Install |
|-------|-------------|---------|
| [**Novelist**](./skills/novelist/) | 中文长篇小说/网文创作全流程 Skill — 策划、大纲、人物、世界观、连载写作、EPUB 导出、字数检查、英文翻译 | `npx skills add JankinLee/groundedcat-skills --path skills/novelist` |

## Quick Start

Install any skill with:

```bash
npx skills add groundedcat/groundedcat-skills --path skills/<skill-name>
```

Then invoke in your agent terminal:

```bash
/novelist <书名>                  # Start planning a new novel
/novelist --mode 连载 <书名>      # Continue serializing chapters
/novelist --check-only novels/<书名>  # Quality check only
```

## License

MIT
