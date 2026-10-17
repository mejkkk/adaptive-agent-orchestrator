# Install from GitHub

**Adaptive Agent Orchestrator v1.0 — Released** · [English installation](../INSTALLATION.md) · [ภาษาไทย](../INSTALLATION.th.md)

Clone the source once:

```bash
git clone https://github.com/mejkkk/adaptive-agent-orchestrator.git
```

On subsequent updates:

```bash
cd adaptive-agent-orchestrator
git pull --ff-only origin main
```

Install the source directory `skill/adaptive-agent-orchestrator/` in your target project. Codex and Antigravity normally use `.agents/skills/`; Claude Code uses `.claude/skills/`:

```bash
PROJECT="/path/to/your-project"
mkdir -p "$PROJECT/.agents/skills" "$PROJECT/.claude/skills"
cp -R skill/adaptive-agent-orchestrator "$PROJECT/.agents/skills/"
cp -R skill/adaptive-agent-orchestrator "$PROJECT/.claude/skills/"
```

If you have copied the Skill to a project, **repeat the copy after every `git pull`** to deploy the updated source.

For tested-by-user Windows PowerShell commands, global paths, compatibility notes and invocation examples, consult the full [Installation Guide](../INSTALLATION.md) or [คู่มือติดตั้ง](../INSTALLATION.th.md).