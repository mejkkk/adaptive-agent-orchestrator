# คู่มือติดตั้ง Adaptive Agent Orchestrator v1.0

Skill: `adaptive-agent-orchestrator`  
Package: `skill.zip` (มีโฟลเดอร์ `adaptive-agent-orchestrator/` อยู่ใน ZIP)

## 1) สิ่งที่อยู่ใน Skill

```text
adaptive-agent-orchestrator/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── strategy-and-approval.md
    ├── execution-contracts.md
    └── verification-and-escalation.md
```

Skill เก็บเฉพาะนโยบาย Orchestration ไม่เก็บ Requirement เฉพาะโครงการหรือ Agent Role ที่ตายตัว หลังผู้ใช้เตรียม Requirement และ Implementation Plan แล้ว Skill จะเสนอการใช้ SOLO หรือ Subagents ให้ผู้ใช้อนุมัติก่อนลงมือทำ

## 2) ตำแหน่งติดตั้งที่รองรับ

| แพลตฟอร์ม | ติดตั้งใน Project (แนะนำให้เริ่มแบบนี้) | ติดตั้งใช้ทุก Project (Global) | วิธีเรียก |
|---|---|---|---|
| Codex CLI / IDE | `<project>/.agents/skills/adaptive-agent-orchestrator/` | `~/.agents/skills/adaptive-agent-orchestrator/` | `$adaptive-agent-orchestrator` |
| Claude Code | `<project>/.claude/skills/adaptive-agent-orchestrator/` | `~/.claude/skills/adaptive-agent-orchestrator/` | `/adaptive-agent-orchestrator` |
| Antigravity App / IDE | `<project>/.agents/skills/adaptive-agent-orchestrator/` | `~/.gemini/config/skills/adaptive-agent-orchestrator/` | `/adaptive-agent-orchestrator` |
| Antigravity CLI | `<project>/.agents/skills/adaptive-agent-orchestrator/` | `~/.gemini/antigravity-cli/skills/adaptive-agent-orchestrator/` | `/adaptive-agent-orchestrator` |

ตำแหน่ง Project `.agents/skills` สามารถใช้ร่วมกันระหว่าง Codex และ Antigravity ได้ ส่วน Claude Code ใช้ `.claude/skills` แยกต่างหาก

## 3) ติดตั้งบน Windows (PowerShell)

ให้เปิด PowerShell ในโฟลเดอร์ Project และวาง `skill.zip` ไว้ในโฟลเดอร์นั้นก่อน

```powershell
# แตก ZIP ซึ่งมีโฟลเดอร์ adaptive-agent-orchestrator อยู่แล้ว
Expand-Archive -LiteralPath .\skill.zip -DestinationPath .\_skill-unpacked -Force
$src = Join-Path (Get-Location) '_skill-unpacked\adaptive-agent-orchestrator'

# Codex + Antigravity : Project scope
$dest = Join-Path (Get-Location) '.agents\skills\adaptive-agent-orchestrator'
New-Item -ItemType Directory -Force -Path $dest | Out-Null
Copy-Item -Path (Join-Path $src '*') -Destination $dest -Recurse -Force

# Claude Code : Project scope (optional)
$claudeDest = Join-Path (Get-Location) '.claude\skills\adaptive-agent-orchestrator'
New-Item -ItemType Directory -Force -Path $claudeDest | Out-Null
Copy-Item -Path (Join-Path $src '*') -Destination $claudeDest -Recurse -Force
```

หากต้องการติดตั้งแบบ Global ให้เปลี่ยน `$dest` เป็น `$HOME\.agents\skills\adaptive-agent-orchestrator` (Codex), `$HOME\.gemini\config\skills\adaptive-agent-orchestrator` (Antigravity IDE/App), หรือ `$HOME\.claude\skills\adaptive-agent-orchestrator` (Claude Code) แล้วรันคำสั่ง `New-Item` และ `Copy-Item` เหมือนด้านบน สำหรับ Antigravity CLI ใช้ `$HOME\.gemini\antigravity-cli\skills\adaptive-agent-orchestrator`

## 4) ติดตั้งบน macOS / Linux (Bash)

เปิด Terminal ในโฟลเดอร์ Project ซึ่งมีไฟล์ `skill.zip`

```bash
unzip -o skill.zip -d ./_skill-unpacked

# Codex + Antigravity : Project scope
mkdir -p .agents/skills
cp -R ./_skill-unpacked/adaptive-agent-orchestrator .agents/skills/

# Claude Code : Project scope (optional)
mkdir -p .claude/skills
cp -R ./_skill-unpacked/adaptive-agent-orchestrator .claude/skills/
```

สำหรับ Global ให้นำโฟลเดอร์ `adaptive-agent-orchestrator` ไปไว้ในตำแหน่ง Global ตามตารางข้อ 2

## 5) ตรวจว่าติดตั้งถูกต้อง

โครงสร้างสำคัญต้องเป็น `.../skills/adaptive-agent-orchestrator/SKILL.md` ไม่ควรซ้อนเป็น `.../adaptive-agent-orchestrator/adaptive-agent-orchestrator/SKILL.md`

- **Codex:** เปิด Codex ที่ Project นั้น แล้วใช้ `/skills` ตรวจรายการ หรือพิมพ์ `$adaptive-agent-orchestrator` ในช่อง Prompt
- **Claude Code:** เปิด session ใน Project แล้วใช้ `/skills` ตรวจรายการ หรือพิมพ์ `/adaptive-agent-orchestrator`
- **Antigravity:** ตรวจ Customizations/Skills ใน IDE หรือพิมพ์ `/adaptive-agent-orchestrator`; สำหรับ CLI ตรวจ slash command
- หากไม่พบ Skill ให้เปิด session ใหม่ หรือรีสตาร์ตแอป/CLI และตรวจตำแหน่งติดตั้งอีกครั้ง

**การบังคับเรียกด้วยตนเองเท่านั้น:** ไฟล์ `agents/openai.yaml` ปิด implicit invocation สำหรับ Codex ที่รองรับค่านี้ ใน Claude Code สามารถเพิ่มบรรทัด `disable-model-invocation: true` ใน YAML frontmatter ของสำเนา `SKILL.md` ที่ติดตั้งไว้ (เฉพาะ Claude Code) เพื่อปิดการเรียกโดยโมเดลอัตโนมัติ Antigravity รองรับ automatic skill discovery; Skill ระบุขอบเขตว่าควรทำงานเมื่อผู้ใช้เรียกโดยตรง แต่ Prompt เพียงอย่างเดียวไม่สามารถรับประกันว่าจะปิด discovery ของแพลตฟอร์มได้

## 6) ตัวอย่างใช้งาน

เตรียม `requirements.md` และ `implementation-plan.md` ไว้ใน Project จากนั้นเรียก Skill:

**Codex**

```text
$adaptive-agent-orchestrator

Requirements: requirements.md
Implementation Plan: implementation-plan.md
Model preference: Luna, Max Effort

Review the provided requirements and plan, then propose an execution strategy for my approval.
```

**Claude Code / Antigravity**

```text
/adaptive-agent-orchestrator

Requirements: requirements.md
Implementation Plan: implementation-plan.md
Model preference: Luna, Max Effort

Review the provided requirements and plan, then propose an execution strategy for my approval.
```

Luna Max เป็นตัวอย่าง **Preference** ผู้ใช้เปลี่ยน Model หรือ Effort ได้ และ Skill ต้องตรวจสอบความพร้อมใช้งานจริงของแต่ละแพลตฟอร์ม ถ้าต้องใช้ Model ใดเท่านั้น ให้ระบุว่า `Hard constraint: use only ...`

ผลรอบแรกจะเป็น **Execution Strategy Proposal** ระบุ SOLO/DELEGATED/MULTI_AGENT, เหตุผล, Role, Model/Effort, Dependency, Cost/Risk/Permissions, การตรวจสอบของ Lead และแผน Retry จากนั้นต้องหยุด **รอคำยืนยันของผู้ใช้** ก่อน Implementation และการ Spawn Execution Workers

## 7) ข้อจำกัดที่ต้องทราบ

- ตัว ZIP เป็น Policy Skill ที่ใช้ข้ามแพลตฟอร์มได้ ไม่ได้รวม Native Subagent Runtime, Agent Configuration ของแต่ละแพลตฟอร์ม, Sandbox, หรือ Model Access ไว้ให้
- การแยก Tool Permission ระหว่าง Lead และ Worker ต้องอาศัยฟีเจอร์ของ Runtime จึงไม่สามารถบังคับได้ด้วย Prompt อย่างเด็ดขาด
- หาก Runtime ไม่รองรับ Model/Effort หรือ Subagent ที่ต้องการ Skill จะต้องแสดงข้อจำกัดและขออนุมัติทางเลือกก่อนดำเนินงาน
- ผลผ่าน Validation หมายถึงไฟล์ Skill มีโครงสร้างและรูปแบบถูกต้อง ไม่ได้หมายความว่าทดสอบ End-to-end กับ Codex/Claude Code/Antigravity ในเครื่องของคุณแล้ว

## 8) เอกสารอ้างอิงสำหรับการติดตั้ง

- Codex / ChatGPT Skills: https://learn.chatgpt.com/docs/build-skills
- Claude Code Skills: https://code.claude.com/docs/en/skills
- Antigravity Skills: https://www.antigravity.google/docs/skills