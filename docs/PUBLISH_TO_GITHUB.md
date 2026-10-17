# เผยแพร่ Repository ไปยัง GitHub

Repository นี้ได้รับการสร้างแล้วที่ https://github.com/mejkkk/adaptive-agent-orchestrator

## Update ผ่าน Git CLI

```bash
git clone https://github.com/mejkkk/adaptive-agent-orchestrator.git
cd adaptive-agent-orchestrator
# แก้ไฟล์ตามที่ต้องการแล้ว:
git add .
git commit -m "Update orchestrator skill"
git push origin main
```

ตรวจสอบว่ามี `README.md`, `INSTALLATION.md`, `AGENTS.md`, `docs/`, `skill/adaptive-agent-orchestrator/SKILL.md`, `skill/adaptive-agent-orchestrator/agents/openai.yaml` และไฟล์อ้างอิง 3 ไฟล์

Full Workflow ต้นฉบับที่ `docs/FULL_WORKFLOW_FINAL_DESIGN_REVIEW_ORIGINAL.txt` เป็นบันทึกที่ห้ามแก้ไขตามข้อกำหนดของเจ้าของ Repository

หากต้องการเผยแพร่ไฟล์ `skill.zip` แบบไบนารี ให้อัปโหลดด้วย Git CLI หรือ GitHub Releases; GitHub Connector บางชุดรองรับเฉพาะไฟล์ UTF-8 ขณะส่งเนื้อหาไปยัง Contents API.