# คู่มือติดตั้ง Adaptive Agent Orchestrator

**Version 1.0 — ใช้งานจริง** · [English](INSTALLATION.md)

ใช้ Source ของ Skill จาก [GitHub Repository](https://github.com/mejkkk/adaptive-agent-orchestrator) โดยตรง ไม่ต้องดาวน์โหลดแพ็กเกจ ZIP

## 1. เตรียมพร้อม

ติดตั้ง Git และ Codex, Claude Code หรือ Antigravity ที่รองรับ Skills พร้อมสิทธิ์สร้างโฟลเดอร์ใน Project หากต้องการใช้ Multi-Agent ต้องเปิดความสามารถ Native Subagent ของแพลตฟอร์มนั้นด้วย

ไฟล์ที่ต้องติดตั้งคือ `skill/adaptive-agent-orchestrator/` ซึ่งประกอบด้วย `SKILL.md`, `agents/openai.yaml` และโฟลเดอร์ `references/`

## 2. ตำแหน่งติดตั้ง

| เครื่องมือ | ตำแหน่งใน Project | Global (เมื่อรองรับ) | เรียกใช้ |
|---|---|---|---|
| Codex | `<project>/.agents/skills/adaptive-agent-orchestrator/` | `~/.agents/skills/adaptive-agent-orchestrator/` | `$adaptive-agent-orchestrator` |
| Claude Code | `<project>/.claude/skills/adaptive-agent-orchestrator/` | `~/.claude/skills/adaptive-agent-orchestrator/` | `/adaptive-agent-orchestrator` |
| Antigravity | `<project>/.agents/skills/adaptive-agent-orchestrator/` | ตรวจตามรุ่นและ Runtime | `/adaptive-agent-orchestrator` เมื่อรองรับ |

## 3. Clone Repository

**macOS / Linux (Bash)**

```bash
mkdir -p ~/agent-skill-sources
cd ~/agent-skill-sources
git clone https://github.com/mejkkk/adaptive-agent-orchestrator.git
```

**Windows (PowerShell)**

```powershell
New-Item -ItemType Directory -Force "$HOME\agent-skill-sources" | Out-Null
Set-Location "$HOME\agent-skill-sources"
git clone https://github.com/mejkkk/adaptive-agent-orchestrator.git
```

หาก Clone มาแล้ว ให้ใช้ `git pull` ตามหัวข้อ 5 แทน

## 4. คัดลอก Skill เข้า Project

แก้ค่า `PROJECT` หรือ `$Project` ให้เป็นเส้นทาง Project ที่ต้องการ

**macOS / Linux (Bash)**

```bash
SOURCE="$HOME/agent-skill-sources/adaptive-agent-orchestrator/skill/adaptive-agent-orchestrator"
PROJECT="/path/to/your-project"

# Codex / Antigravity
mkdir -p "$PROJECT/.agents/skills"
cp -R "$SOURCE" "$PROJECT/.agents/skills/"

# Claude Code
mkdir -p "$PROJECT/.claude/skills"
cp -R "$SOURCE" "$PROJECT/.claude/skills/"
```

**Windows (PowerShell)**

```powershell
$Source = Join-Path $HOME "agent-skill-sources\adaptive-agent-orchestrator\skill\adaptive-agent-orchestrator"
$Project = "C:\path\to\your-project"

# Codex / Antigravity
$Dest = Join-Path $Project ".agents\skills\adaptive-agent-orchestrator"
New-Item -ItemType Directory -Force $Dest | Out-Null
Copy-Item -Path (Join-Path $Source '*') -Destination $Dest -Recurse -Force

# Claude Code
$ClaudeDest = Join-Path $Project ".claude\skills\adaptive-agent-orchestrator"
New-Item -ItemType Directory -Force $ClaudeDest | Out-Null
Copy-Item -Path (Join-Path $Source '*') -Destination $ClaudeDest -Recurse -Force
```

คัดลอกเฉพาะปลายทางของแพลตฟอร์มที่ใช้งานก็เพียงพอ

## 5. อัปเดต Skill ผ่าน Git Pull

**สำคัญ:** `git pull` อัปเดตโฟลเดอร์ Source ที่ Clone มาเท่านั้น หากติดตั้งด้วยการ Copy ต้อง Copy Skill ใหม่เข้า Project อีกครั้ง

**macOS / Linux (Bash)**

```bash
cd ~/agent-skill-sources/adaptive-agent-orchestrator
git pull --ff-only origin main

SOURCE="$HOME/agent-skill-sources/adaptive-agent-orchestrator/skill/adaptive-agent-orchestrator"
PROJECT="/path/to/your-project"
mkdir -p "$PROJECT/.agents/skills" "$PROJECT/.claude/skills"
cp -R "$SOURCE" "$PROJECT/.agents/skills/"
cp -R "$SOURCE" "$PROJECT/.claude/skills/"
```

**Windows (PowerShell)**

```powershell
Set-Location "$HOME\agent-skill-sources\adaptive-agent-orchestrator"
git pull --ff-only origin main

$Source = Join-Path $HOME "agent-skill-sources\adaptive-agent-orchestrator\skill\adaptive-agent-orchestrator"
$Project = "C:\path\to\your-project"

$Dest = Join-Path $Project ".agents\skills\adaptive-agent-orchestrator"
New-Item -ItemType Directory -Force $Dest | Out-Null
Copy-Item -Path (Join-Path $Source '*') -Destination $Dest -Recurse -Force

$ClaudeDest = Join-Path $Project ".claude\skills\adaptive-agent-orchestrator"
New-Item -ItemType Directory -Force $ClaudeDest | Out-Null
Copy-Item -Path (Join-Path $Source '*') -Destination $ClaudeDest -Recurse -Force
```

ก่อนคัดลอกทับ ควรสำรองไฟล์ที่ปรับแต่งเองไว้ การ Copy ทับจะไม่ลบไฟล์เก่าที่ถูกถอดออกจาก Source โดยอัตโนมัติ

## 6. ตรวจสอบและเรียกใช้

ตรวจสอบว่ามีไฟล์ `.../skills/adaptive-agent-orchestrator/SKILL.md` และไฟล์ใน `references/` ครบ ถ้าไม่พบ Skill ให้เริ่ม Session ใหม่หรือ Reload Skills

ตัวอย่าง Codex:

```text
$adaptive-agent-orchestrator

Requirements: requirements.md
Implementation Plan: implementation-plan.md
Model preference: Luna, Max Effort
```

Claude Code และ Antigravity (ถ้ารองรับ) ให้ใช้ `/adaptive-agent-orchestrator` แทน

Skill ต้องเสนอ Execution Strategy และ **รอผู้ใช้ยืนยันก่อน Implementation** ทั้งกรณี SOLO และ Multi-Agent

## 7. ข้อจำกัด

Skill กำหนด Orchestration Policy เท่านั้น การ Spawn Worker, ตั้งค่า Model/Effort, แยก Permission และเข้าถึงระบบจริงขึ้นกับ Runtime ของแต่ละแพลตฟอร์ม การตรวจสอบโครงสร้างไฟล์ไม่ได้ยืนยันว่าทดสอบ End-to-end บนเครื่องผู้ใช้แล้ว

เอกสารอ้างอิง: [Codex](https://developers.openai.com/codex/skills) · [Claude Code](https://code.claude.com/docs/en/skills) · [Antigravity](https://www.antigravity.google/docs/skills)
