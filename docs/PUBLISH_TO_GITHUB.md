# Maintaining the repository

**Adaptive Agent Orchestrator v1.0 — Released**

The public repository is https://github.com/mejkkk/adaptive-agent-orchestrator.

To update your local checkout and publish documentation changes:

```bash
git clone https://github.com/mejkkk/adaptive-agent-orchestrator.git
cd adaptive-agent-orchestrator
git pull --ff-only origin main
# Edit files, review diffs, and then:
git add .
git commit -m "Update documentation"
git push origin main
```

Documentation is published in English primarily (`README.md`, `INSTALLATION.md`) and Thai companion files (`README.th.md`, `INSTALLATION.th.md`).

The operational workflow is available as `docs/ADAPTIVE_AGENT_ORCHESTRATOR_WORKFLOW.md` and `docs/ADAPTIVE_AGENT_ORCHESTRATOR_WORKFLOW_ORIGINAL.txt`. Keep the two versions synchronized if the workflow changes; retain the semantics of all five phases.

The authoritative English-language Skill policy remains in `skill/adaptive-agent-orchestrator/`. No prebuilt package is required for installation; use Git clone/pull and copy the directory to a supported Skills location.