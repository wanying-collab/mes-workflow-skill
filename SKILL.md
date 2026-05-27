---
name: mes-workflow-skill
description: Use this skill when the user asks Codex or AI tools to analyze MES worktime records, calculate processing time, waiting time, Lead Time, machine utilization, abnormal records, KPI dashboards, and scheduling suggestions.
---

# MES Workflow Skill

## Purpose

This skill helps Codex produce a reliable MES worktime analysis workflow.

Use this skill when the task involves:

- MES worktime analysis
- Processing time calculation
- Waiting time analysis
- Machine utilization analysis
- Lead Time calculation
- Abnormal record detection
- KPI dashboard generation
- Scheduling suggestions

Default output language: Traditional Chinese.

Default audience: manufacturing managers, students, administrators, engineers, or users who need a clear MES worktime analysis report.

---

## Core Principles

1. Normalize Start / Pause / Resume / End status.
2. Separate processing time and waiting time correctly.
3. Same machine should not generate station waiting time.
4. Completed work orders must contain an End record.
5. Abnormal records should not be included in average worktime calculations.
6. Keep calculations clear and repeatable.

---

## Standard Workflow

### 1. Read MES Records

Read uploaded MES Excel records.

Supported fields:

- Work Order Number
- Machine ID
- Machine Name
- Operator
- Action Status
- Timestamp
- Processing Hours

---

### 2. Normalize Action Status

Normalize status values:

- Start
- Pause
- Resume
- End

---

### 3. Calculate Processing Time

Rules:

- Start → Pause
- Start → End
- Resume → End

All count as processing time.

---

### 4. Calculate Waiting Time

Rules:

- Pause → Resume = waiting time
- Different machines may generate station waiting time
- Same machine should not generate waiting time

---

### 5. Detect Abnormal Records

Exclude records if:

- Missing work order number
- Invalid timestamp
- Invalid action order
- Negative worktime
- Duplicate Start status

Flag suspicious records if:

- CNC processing time > 72 hours
- Waiting time > 24 hours

---

### 6. Generate KPI

Generate:

- Total processing hours
- Total waiting hours
- Machine utilization
- Lead Time
- Completed work orders
- Abnormal records

---

### 7. Generate Scheduling Suggestions

Rules:

- Completed orders should not be scheduled
- In-progress orders keep current machine
- Prefer machines with best historical performance

---

## Report Template

```markdown
# MES 工時分析報告

## 一、資料摘要

- 製令單總數：
- 已完成製令單：
- 進行中製令單：
- 異常資料數：

---

## 二、KPI 指標

| 指標 | 數值 | 說明 |
|---|---:|---|
| 總加工工時 |  |  |
| 總等待工時 |  |  |
| Lead Time |  |  |
| 機台利用率 |  |  |

---

## 三、製令單分析

---

## 四、異常資料說明

---

## 五、排程建議

---

## 六、結論
```

---

## Writing Style

- Use clear Traditional Chinese
- Keep paragraphs short
- Avoid unnecessary technical jargon
- Prefer exact numbers and timestamps
- Keep workflow descriptions structured and repeatable

---

## Quality Checklist

Before finalizing, verify:

- [ ] Processing time is calculated correctly
- [ ] Waiting time excludes same-machine operations
- [ ] Completed work orders contain End records
- [ ] Abnormal records are excluded
- [ ] KPI values are generated correctly
- [ ] Lead Time is calculated correctly

---

## Optional Outputs

If the user asks for specific file formats:

- Markdown report
- HTML dashboard
- Excel summary
- PDF report

---

## Example Prompt for Codex Users

```text
請使用 mes-workflow-skill，分析 MES 工時資料，計算加工工時、等待工時、Lead Time、機台利用率與異常資料，並輸出 Markdown 工時分析報告。
```
