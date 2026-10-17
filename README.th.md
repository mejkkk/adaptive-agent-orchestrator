# Adaptive Agent Orchestrator

**Version 1.0 — ใช้งานจริง** · [English](README.md)

Skill สำหรับกำหนด Orchestration Policy ให้ Codex, Claude Code และ Antigravity โดยใช้ Requirements และ Implementation Plan ที่เตรียมไว้ก่อนหน้า วิเคราะห์ว่าจะใช้ **SOLO (Lead ทำเอง)**, **DELEGATED (1 Worker)** หรือ **MULTI-AGENT (2+ Workers)** แล้วแสดง Execution Strategy เพื่อให้ผู้ใช้อนุมัติก่อนเริ่มงาน

## Workflow 5 Phases

1. **Intake & Review:** อ่าน Requirement, Plan และคำสั่งเพิ่มเติม ถามเฉพาะข้อมูลสำคัญที่ยังขาด
2. **Strategy & Approval:** แบ่ง Task และ Dependency เลือก Mode, Worker, Role, Model, Effort, Permission และแผนตรวจสอบ จากนั้นรอการอนุมัติ
3. **Execution:** SOLO ให้ Lead ลงมือเอง; โหมด Delegated ให้ Worker ลงมือและ Lead ประสานงาน/Review พร้อม Parallel เฉพาะงานอิสระ
4. **Verification & Escalation:** Lead อ่าน Report ตรวจ Acceptance Criteria และตรวจของจริงอย่างน้อย 1 Critical Check ถ้าไม่ผ่านให้ผู้ทำเดิมแก้หนึ่งรอบ และพิจารณา Worker ใหม่ได้อีกหนึ่งรอบภายใต้สิทธิ์ที่อนุมัติ
5. **Final Report:** สรุปผลจริงพร้อม Evidence, Retry, Blockers และ Remaining Risks

Skill เก็บเฉพาะกฎ Orchestration โดยไม่มี Requirement เฉพาะ Project

## เอกสาร

| เอกสาร | รายละเอียด |
|---|---|
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

ตัวอย่าง Codex:

```text
$adaptive-agent-orchestrator

Requirements: requirements.md
Implementation Plan: implementation-plan.md
Model preference: Luna, Max Effort
```

Claude Code และ Antigravity (เมื่อรองรับการเรียกแบบนี้) ใช้ `/adaptive-agent-orchestrator`

**หมายเหตุ:** ต้องยืนยัน Execution Strategy ก่อนเริ่ม Implementation ทุกครั้ง และการเลือก Model, Effort, Permission และ Subagent จริงยังขึ้นกับ Runtime ของแต่ละแพลตฟอร์ม
