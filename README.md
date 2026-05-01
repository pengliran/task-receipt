# task-receipt

A receipt-style daily task card generator for Claude Code. Turns your task list into a PNG that looks like a supermarket receipt.

## What it looks like

Your tasks get rendered as a thermal-paper receipt with:

- Task name + estimated time (right-aligned)
- DDL (deadline) under each task
- Life topic tags (e.g. Work, Study, Health)
- Summary block: total tasks, total time, remaining count
- Bottom motto + barcode decoration

## Install

Copy the `task-receipt` folder into your Claude Code skills directory:

```bash
cp -r task-receipt ~/.claude/skills/
```

Install dependencies:

```bash
cd ~/.claude/skills/task-receipt
npm install && npx playwright install chromium
```

## Usage

In Claude Code, just give your task list:

```
📅 2026-04-29 每日任务清单
🔴 AI产品经理手册 ddl:5.1, 2h, 人生课题：AIPM
🟡 实习投递 ddl:5.2, 30min
🟡 单词 ddl:5.1, 2h
🟡 英语播客 30min, ddl:6.1
```

Claude will generate a receipt PNG and save it to `~/Downloads/`.

### Task format

Each task supports:

| Field | Required | Example |
|-------|----------|---------|
| Task name | Yes | `AI产品经理手册` |
| Time | Yes | `2h`, `30min`, `1.5h` |
| DDL | Yes | `5.1`, `今天`, `今晚`, `下周五` |
| Life topic | No | `工作`, `学习`, `健康` |

## File structure

```
task-receipt/
├── SKILL.md                    # Skill entry point
├── README.md
├── assets/
│   ├── receipt_template.html   # HTML/CSS template
│   ├── capture.js              # Playwright screenshot tool
│   └── logo.png
├── references/
│   └── mode-receipt.md         # Step-by-step generation guide
├── package.json
└── node_modules/
```

## How it works

1. Parse task list from user input
2. Fill data into HTML template (Courier New monospace font, dotted borders, dashed lines)
3. Use Playwright (headless Chromium) to open the HTML and screenshot the `.receipt` element
4. Output PNG to `~/Downloads/`

## Customize

Edit `assets/receipt_template.html` to change:

- Colors (`--bg`, `--paper`, `--text`, etc.)
- Width (default 720px)
- Font family
- Layout and spacing

## License

MIT
