---
name: task-receipt
description: "Use when user wants to generate a receipt-style daily task card. Triggers: '小票', '任务卡', '今日任务', 'todo card', 'receipt card', 'daily tasks'. Output PNG to ~/Downloads/."
user_invocable: true
version: "1.0.0"
---

# task-receipt

超市小票风格的每日任务卡片。任务进去，小票出来。

## 输入

用户给出一组任务（文本列表），每条可包含：
- 任务名（必填）
- 耗时（必选，比如2h,30min）
- DDL（必选，截止日期）
- 人生课题（可选，如 工作/学习/健康）

## 执行

Read `references/mode-receipt.md`，按其步骤执行。

模板：`assets/receipt_template.html`

## 文件命名

从内容提取主题作为 `{name}`（中文直接用，去标点，≤ 20 字符）。默认用当天日期如 `今日任务0501`。

## 截图工具

```bash
node assets/capture.js <html> <png> <width> <height> [fullpage]
```

从 skill 根目录运行。依赖 `node_modules/` 中的 playwright。如报错：

```bash
npm install playwright && npx playwright install chromium
```

## 交付

1. 报告文件路径
