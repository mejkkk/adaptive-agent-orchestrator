# ติดตั้ง Adaptive Agent Orchestrator จาก GitHub

Repository: https://github.com/mejkkk/adaptive-agent-orchestrator

โฟลเดอร์ Skill ที่ต้องใช้: `skill/adaptive-agent-orchestrator/` ซึ่งมี `SKILL.md`, `agents/openai.yaml` และ `references/`

## ใช้ Git clone

```bash
git clone https://github.com/mejkkk/adaptive-agent-orchestrator.git
cd adaptive-agent-orchestrator
```

### Codex (ระดับ Project)

```bash
mkdir -p .agents/skills
cp -R skill/adaptive-agent-orchestrator .agents/skills/
```

### Claude Code (ระดับ Project)

```bash
mkdir -p .claude/skills
cp -R skill/adaptive-agent-orchestrator .claude/skills/
```

### Antigravity (ระดับ Project)

```bash
mkdir -p .agents/skills
cp -R skill/adaptive-agent-orchestrator .agents/skills/
```

สำหรับ Windows PowerShell:

```powershell
git clone https://github.com/mejkkk/adaptive-agent-orchestrator.git
cd adaptive-agent-orchestrator
New-Item -ItemType Directory -Force .agents\skills
Copy-Item .\skill\adaptive-agent-orchestrator .agents\skills\ -Recurse -Force
New-Item -ItemType Directory -Force .claude\skills
Copy-Item .\skill\adaptive-agent-orchestrator .claude\skills\ -Recurse -Force
```

ติดตั้ง Skill ใน Project ที่ต้องการใช้งาน หาก clone อยู่ใน Project repository ของ Skill เอง ตัวอย่างข้างต้นจะติดตั้งลงใน Project ปัจจุบัน ให้ปรับเส้นทางต้นทางและปลายทางก่อนใช้กับ Project อื่น

## เรียกใช้

Codex: `$adaptive-agent-orchestrator`

Claude Code / Antigravity: `/adaptive-agent-orchestrator` (ตาม Runtime ที่รองรับ)

```text
Requirements: requirements.md
Implementation Plan: implementation-plan.md
Model Preference: Luna, Max Effort
```

ตรวจข้อจำกัด Model/Effort และ Subagent Tools ของแพลตฟอร์มก่อนใช้งานจริง อ่านคำอธิบายเพิ่มเติมที่ [INSTALLATION.md](../INSTALLATION.md)