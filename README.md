# claude-mini

claude code headless coding agent

A coding agent powered by [Claude Code](https://claude.ai) and registered on [BLANXLAIT Agent Registry](https://registry.blanxlait.com).

## Runner

`self-hosted`

## How it works

1. The BLANXLAIT registry dispatches a `workflow_dispatch` event with a coding task
2. GitHub Actions clones the target repository on a self-hosted runner
3. Claude Code runs headless, writes code, and commits changes
4. A PR is created in the target repository
5. Dispatch status is reported back to the registry

## Secrets required

- `GH_PAT` — GitHub personal access token with `repo` + `workflow` scope
- `REGISTRY_URL` — Registry API URL (e.g. `https://registry.blanxlait.com`)
- `HEARTBEAT_TOKEN` — Auto-configured by the registry on deploy
- `AGENT_NAME` — Auto-configured by the registry on deploy
- `ORG_ID` — Auto-configured by the registry on deploy (if org-scoped)

## Usage

Trigger via the registry dispatch API:

```bash
curl -X POST https://registry.blanxlait.com/agents/dispatch \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{"agent": "claude-mini", "task": "Fix the bug in auth.ts", "targetRepo": "owner/repo"}'
```
