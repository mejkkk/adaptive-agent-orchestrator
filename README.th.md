# Adaptive Agent Orchestrator

**Version 1.1 — ใช้งานจริง** · [English](README.md)

Skill สำหรับกำหนด Orchestration Policy ให้ Codex, Claude Code และ Antigravity โดยใช้ Requirements และ Implementation Plan ที่เตรียมไว้ก่อนหน้า วิเคราะห์ว่าจะใช้ **SOLO (0 Workers; Lead ทำเอง)** หรือ **DELEGATED (1+ Workers; Workers ทำ Implementation)** โดย Multi-Agent/Parallel เป็น Execution Style ใน DELEGATED แล้วแสดง Execution Strategy เพื่อให้ผู้ใช้อนุมัติก่อนเริ่มงาน

## Workflow 5 Phases

1. **Intake & Review:** อ่าน Requirement, Plan และคำสั่งเพิ่มเติม ถามเฉพาะข้อมูลสำคัญที่ยังขาด
2. **Strategy & Approval:** แบ่ง Task และ Dependency เสนอ Initial/Maximum Workers, Initial Roles, Model, Effort และ Execution Approach ที่กระชับ ก่อนรออนุมัติ
3. **Execution:** SOLO → DELEGATED ได้ภายใน Maximum ที่อนุมัติ เมื่อ Delegate แล้ว Lead ห้ามกลับมา Implement เอง และต้องแจ้งผู้ใช้เมื่อเพิ่ม Worker
4. **Verification & Escalation:** Lead อ่าน Report ตรวจ Acceptance Criteria และตรวจของจริงอย่างน้อย 1 Critical Check ถ้าไม่ผ่านให้ผู้ทำเดิมแก้หนึ่งรอบ และพิจารณา Worker ใหม่ได้อีกหนึ่งรอบภายใต้สิทธิ์ที่อนุมัติ
5. **Final Report:** สรุปผลจริงพร้อม Evidence, Worker Usage แบบสะสม, Scaling, Retry, Blockers และ Risks

Skill เก็บเฉพาะกฎ Orchestration โดยไม่มี Requirement เฉพาะ Project

## เอกสาร

| เอกสาร | รายละเอียด |
|---|---|
| [Change History](CHANGELOG.md) | ประวัติการเปลี่ยนแปลงแต่ละเวอร์ชัน |
| [Adaptive Agent Orchestrator Workflow (English)](docs/ADAPTIVE_AGENT_ORCHESTRATOR_WORKFLOW_EN.md) | Workflow ภาษาอังกฤษครบ 5 Phases พร้อม Mermaid |
| [Adaptive Agent Orchestrator Workflow (ภาษาไทย)](docs/ADAPTIVE_AGENT_ORCHESTRATOR_WORKFLOW.md) | Workflow ภาษาไทยครบ 5 Phases พร้อม Mermaid |
| [Installation Guide (English)](INSTALLATION.md) | วิธี Clone, Pull และติดตั้ง |
| [คู่มือติดตั้งภาษาไทย](INSTALLATION.th.md) | ขั้นตอนภาษาไทย |
| [SKILL.md](skill/adaptive-agent-orchestrator/SKILL.md) | Orchestration Policy ภาษาอังกฤษ |
| [Agent Configuration](skill/adaptive-agent-orchestrator/agents/openai.yaml) | Metadata |
| [Execution Contracts](skill/adaptive-agent-orchestrator/references/execution-contracts.md) | ขอบเขตการมอบหมายงาน |
| [Strategy & Approval](skill/adaptive-agent-orchestrator/references/strategy-and-approval.md) | วิธีเลือก SOLO/Subagent และขออนุมัติ |
| [Verification & Escalation](skill/adaptive-agent-orchestrator/references/verification-and-escalation.md) | วิธีตรวจจริงและ Retry |

## เริ่มใช้งาน

```bash
git clone https://github.com/mejkkk/adaptive-agent-orchestrator.git
mkdir -p /path/to/project/.agents/skills
cp -R adaptive-agent-orchestrator/skill/adaptive-agent-orchestrator /path/to/project/.agents/skills/
```

## ตัวอย่าง Prompt

### Standard Prompt Template

```text
/adaptive-agent-orchestrator

Execute based on: <requirements.md or implementation-plan.md>

<Optional Overrides>
Model Preference: <optional model and effort preference>
Additional Instructions: <optional task-specific instructions>
```

ส่วน **Optional Overrides** ไม่จำเป็นต้องระบุ หากไม่มีคำสั่งเพิ่มเติม สามารถตัดออกทั้งหมดได้ โดย Requirement และ Plan ของแต่ละงานยังคงอยู่ภายนอก Skill

### Example 1 — Standard Execution (No Override)

```text
/adaptive-agent-orchestrator

Execute based on: implementation-plan.md
```

Lead จะตรวจ Requirement/Plan, วิเคราะห์ Task Breakdown และ Dependencies, เลือก SOLO หรือ Subagents ตามความเหมาะสม แล้วเสนอ Execution Strategy เพื่อรอการอนุมัติ

### Example 2 — Execution with Overrides

```text
/adaptive-agent-orchestrator

Execute based on:
- requirements.md
- implementation-plan.md

Model Preference: Prefer Luna with Max Effort.

Additional Instructions:
- Prioritize security verification.
- Do not deploy to production.
```

`Prefer Luna with Max Effort` เป็น **Preference** ไม่ใช่ข้อบังคับให้ใช้ Model นี้เท่านั้น Lead จึงเสนอทางเลือกที่เหมาะสมกว่าได้พร้อมเหตุผลและต้องตรวจความพร้อมใช้งานของ Runtime ส่วน `Do not deploy to production` เป็น **ข้อห้ามที่ต้องปฏิบัติตาม** และให้ความสำคัญกับ Security Verification ตามคำสั่ง

**การเรียกใช้บนแพลตฟอร์ม:** ตัวอย่างใช้ `/adaptive-agent-orchestrator` สำหรับ Claude Code และ Antigravity ที่รองรับ ส่วน **Codex ใช้ `$adaptive-agent-orchestrator`** แทน

**Mandatory Approval:** คำว่า `Execute based on` เริ่มกระบวนการวิเคราะห์ Strategy ไม่ใช่คำสั่งข้ามขั้นตอนอนุมัติ Lead ต้องแสดง Execution Strategy แล้วรอผู้ใช้ยืนยันก่อนเริ่ม Implementation หรือ Spawn Execution Workers

**หมายเหตุ:** การเลือก Model, Effort, Permission และ Subagents จริงยังขึ้นกับ Runtime ของแต่ละแพลตฟอร์ม
