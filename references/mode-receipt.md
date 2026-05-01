# 模具：小票（receipt）

## 步骤 1：读取模板

Read `assets/receipt_template.html`

## 步骤 2：解析内容

用户输入为一组任务，每条任务包含：

- **任务名**（必填）：简短描述
- **耗时**（必填）：如 2h, 30min, 1.5h
- **DDL**（必填）：截止日期，如 今天, 今晚, 05/03, 下周五
- **人生课题**（可选）：分类，如 工作/学习/健康/沟通

如果用户没有提供完整结构，从文本中合理推断。

获取当天日期作为小票日期。

## 步骤 3：格式化为 HTML

**头部：**
```html
<div class="receipt-header">
  <h1>{{TITLE}}</h1>
  <div class="date">{{DATE}}</div>
</div>
<hr class="dashed-line">
```
- `{{TITLE}}`：默认 "TODAY"，用户可自定义
- `{{DATE}}`：当天日期，格式 `YYYY/MM/DD  DDD`（英文星期三字母缩写）

**每个任务：**
```html
<li class="task-item">
  <div class="task-checkbox"></div>
  <div class="task-body">
    <div class="task-name-row">
      <span class="task-name">任务名</span>
      <span class="task-time">2h</span>
    </div>
    <div class="task-meta">DDL: 今晚</div>
    <span class="task-tag">工作</span>
  </div>
</li>
```
- 耗时显示在任务名右侧（`.task-time`）
- DDL 显示在任务名下方（`.task-meta`）
- 有人生课题时才加 `.task-tag`

**汇总：**
```html
<hr class="dashed-line">
<div class="summary-row">
  <span>TOTAL TASKS</span>
  <span>{{总数}}</span>
</div>
<div class="summary-row">
  <span>TOTAL TIME</span>
  <span>{{总耗时}}</span>
</div>
<div class="summary-row total">
  <span>REMAINING</span>
  <span>{{总数}}</span>
</div>
```
- 总耗时 = 所有任务的耗时求和

**底部：**
```html
<div class="receipt-footer">
  <div class="motto">{{格言}}</div>
  <div class="barcode-text">||||| |||| ||| |||||</div>
</div>
```
- `{{格言}}`：根据任务内容生成一句简短激励语，或用户指定

## 步骤 4：渲染模板

替换模板中的 `{{RECEIPT_CONTENT}}` 为步骤 3 生成的完整 HTML。

写入：`/tmp/001_receipt_{name}.html`

## 步骤 5：截图

必须使用 `.receipt` 选择器精确截图，只截小票元素，不截外部背景和 padding：

```bash
node assets/capture.js /tmp/001_receipt_{name}.html ~/Downloads/{name}.png 720 800 fullpage .receipt
```

## 步骤 6：交付

报告文件路径：`~/Downloads/{name}.png`
