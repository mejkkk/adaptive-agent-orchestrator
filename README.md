# Adaptive Agent Orchestrator

Skill สำหรับควบคุมการทำงานแบบ Adaptive Execution รองรับ **SOLO**, **DELEGATED** (1 Worker) และ **MULTI-AGENT** (2+ Workers) พร้อม Mandatory User Approval, Direct Lead Verification และ Bounded Retry/Escalation ตาม Workflow ที่อนุมัติแล้ว

## เอกสารใน Repository

| เอกสาร | รายละเอียด |
|---|---|
| [Full Workflow — Final Design Review](docs/FULL_WORKFLOW_FINAL_DESIGN_REVIEW.md) | ฉบับอ่านผ่าน GitHub พร้อมแผนภาพ Mermaid และเนื้อหาตาม Final Review เดิม |
| [Full Workflow — Original](docs/FULL_WORKFLOW_FINAL_DESIGN_REVIEW_ORIGINAL.txt) | เก็บต้นฉบับตามที่แสดงในการสนทนา โดยไม่เปลี่ยนถ้อยคำ ชื่อ Skill เก่า และตัวอย่างเดิม |
| [Installation Guide](INSTALLATION.md) | คู่มือติดตั้งฉบับเดิมบน Codex, Claude Code และ Antigravity |
| [Install from this Repository](docs/INSTALL_FROM_GITHUB.md) | คำสั่งติดตั้งจาก GitHub Repo โดยตรง |
| [Publish to GitHub](docs/PUBLISH_TO_GITHUB.md) | วิธีสร้าง Repo เปล่าและ Push ไฟล์ชุดนี้ |
| [Skill entrypoint](skill/adaptive-agent-orchestrator/SKILL.md) | Orchestration Policy 5 Phases |
| [Agent metadata](skill/adaptive-agent-orchestrator/agents/openai.yaml) | ชื่อและค่าการเรียกใช้ Skill |
| [Worker contract](skill/adaptive-agent-orchestrator/references/execution-contracts.md) | Task Contract, Permission, Output และ Evidence |
| [Strategy & Approval](skill/adaptive-agent-orchestrator/references/strategy-and-approval.md) | ตัดสินใจ SOLO/Subagents, Model/Effort และ Approval |
| [Verification & Escalation](skill/adaptive-agent-orchestrator/references/verification-and-escalation.md) | Direct Check, Retry 1 ครั้ง และ Escalation 1 ครั้ง |

> **หมายเหตุเรื่องชื่อ:** เอกสาร Full Workflow ฉบับต้นฉบับยังใช้ชื่อ `multi-agent-orchestrator` ตามวันที่ Review เพื่อรักษาข้อความเดิมตามคำขอ ส่วน Skill ที่ใช้งานจริงชื่อ `adaptive-agent-orchestrator` ทั้งใน `SKILL.md` และไฟล์ Agent

## เริ่มใช้งาน

1. เตรียม `requirements.md` และ `implementation-plan.md` ผ่านการสนทนา / Grill Me / Plan Mode ก่อน
2. ติดตั้ง Skill ด้วย [คู่มือติดตั้ง](INSTALLATION.md) หรือ [คำสั่งจาก GitHub](docs/INSTALL_FROM_GITHUB.md)
3. เรียก `$adaptive-agent-orchestrator` บน Codex หรือ `/adaptive-agent-orchestrator` บน Claude Code / Antigravity ที่รองรับ
4. ระบุไฟล์ Requirements, Plan และ Model Preference (ถ้ามี)
5. **ตรวจและอนุมัติ Execution Strategy ก่อนให้เริ่ม Implementation**

ตัวอย่าง Codex:

```text
$adaptive-agent-orchestrator

Requirements: requirements.md
Implementation Plan: implementation-plan.md
Model Preference: Luna, Max Effort
```

Skill จะเสนอวิธีทำงานและรอการอนุมัติ หลังจากนั้นจึงทำตามแผนที่อนุมัติภายใต้สิทธิ์ที่ Runtime รองรับ

## ข้อจำกัด

การแยก Permission ของ Lead/Worker, จำนวน Subagent, Model และ Effort ขึ้นกับ Runtime ของ Codex, Claude Code หรือ Antigravity ตัว Skill เป็นชุดนโยบายและไม่บังคับสิทธิ์ระดับ OS/Runtime โดยอัตโนมัติ

ไฟล์ Skill และคู่มือติดตั้งนำมาจากชุดที่จัดทำก่อนหน้าโดยไม่แก้ไขเนื้อหา ส่วนเอกสาร Workflow มีไฟล์ต้นฉบับเก็บแยกไว้เพื่อเทียบแบบถ้อยคำต่อถ้อยคำ