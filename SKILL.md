---
name: mes-workflow-skill
description: Use this skill when the user asks Codex or AI tools to analyze MES worktime records, calculate processing time, waiting time, Lead Time, machine utilization, KPI, abnormal records, and scheduling suggestions.
---

# MES Workflow Skill

## Purpose

This skill helps analyze MES worktime records and generate a simple manufacturing worktime report.

Default output language: Traditional Chinese.

## Workflow

1. Read MES worktime records
2. Normalize action status:
   - Start
   - Pause
   - Resume
   - End
3. Calculate processing time
4. Calculate waiting time
5. Detect abnormal records
6. Generate KPI summary
7. Provide scheduling suggestions

## Rules

- Start to Pause counts as processing time.
- Start to End counts as processing time.
- Resume to End counts as processing time.
- Pause to Resume counts as waiting time.
- Same machine should not generate station waiting time.
- Completed work orders must have an End record.
- Abnormal records should not be included in average worktime.

## Output Template

```markdown
# MES 工時分析報告

## 一、資料摘要
- 製令單總數：
- 已完成製令單：
- 進行中製令單：
- 異常資料數：

## 二、KPI 指標
| 指標 | 數值 | 說明 |
|---|---:|---|
| 總加工工時 |  |  |
| 總等待工時 |  |  |
| Lead Time |  |  |
| 機台利用率 |  |  |

## 三、製令單分析

## 四、異常資料說明

## 五、排程建議

## 六、結論
