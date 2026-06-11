# TOOLS.md - Local Notes

Skills define _how_ tools work. This file is for _your_ specifics — the stuff that's unique to your setup.

## What Goes Here

Things like:

- Camera names and locations
- SSH hosts and aliases
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- Anything environment-specific

## Examples

```markdown
### Cameras

- living-room → Main area, 180° wide angle
- front-door → Entrance, motion-triggered

### SSH

- home-server → 192.168.1.100, user: admin

### TTS

- Preferred voice: "Nova" (warm, slightly British)
- Default speaker: Kitchen HomePod
```

## Why Separate?

Skills are shared. Your setup is yours. Keeping them apart means you can update skills without losing your notes, and share skills without leaking your infrastructure.

---

Add whatever helps you do your job. This is your cheat sheet.

## Current Setup

### Models

| Model | Command/Usage | Notes |
|-------|--------------|-------|
| `kimi-coding/k2p6` | Default | 200K context, reasoning |
| `volcengine/doubao-seed-2.0-4k` | `/model volcengine/doubao-seed-2.0-4k` | Lightweight, 4K context |
| `volcengine/minimax-m2.5` | `/model volcengine/minimax-m2.5` | Deep reasoning, 200K context |

### Agent Swarm

```javascript
// Parallel spawn
sessions_spawn({ label: "coder", runtime: "subagent", task: "[coder] ..." })
sessions_spawn({ label: "researcher", runtime: "subagent", task: "[researcher] ..." })
sessions_yield()
```

Installed skills: `openclaw-agent-swarm`, `claw-swarm`, `swarm-kanban`, `swarm-janitor`, `agent-swarm-orchestrator`

### Browser / WebBridge

- **Kimi WebBridge**: `http://127.0.0.1:10086`
- **Status**: `curl -s http://127.0.0.1:10086/status`
- **Extension**: Edge, connected (`v1.9.13`)
- **OpenClaw tool**: `browser` (navigate, snapshot, click, fill, screenshot)

### Kimi Code CLI

- **Path**: `~/.kimi-code/bin/kimi` (symlinked to `~/.local/bin/kimi`)
- **Version**: `0.6.0`
- **Config**: `~/.kimi-code/config.toml`
- **MCP**: `~/.kimi-code/mcp.json` (filesystem + puppeteer)
- **Usage**: `kimi -p "prompt"` (one-shot) or `kimi` (interactive)

### MCP Servers

| Server | Config | Status |
|--------|--------|--------|
| `filesystem` | `npx -y @modelcontextprotocol/server-filesystem /Users/hufujun` | Enabled |
| `puppeteer` | `npx -y @modelcontextprotocol/server-puppeteer` | Enabled |
| `blender` | `python3 -m blender_mcp.server` | Disabled (needs Blender running) |

### Feishu

- **App ID**: `cli_aa8c0528d1395bdf`
- **Domain**: `feishu` (websocket mode)
- **Skills**: 47 `lark-*` skills installed
- **Wiki**: 2 spaces (胡富钧知识库 + 藏山海运营内容)

### Blender

- **Command**: `blender --background --python script.py -- args`
- **Skills**: `blender` (general), `blender-interior` (interior design)
- **No `blender-cli`**: Deleted, use direct command
- **Guard**: Always `2>&1 | tail -N` to avoid log spam

### Memory

- **Daily**: `memory/YYYY-MM-DD.md`
- **Long-term**: `MEMORY.md` (main session only)
- **Vector**: `memory_search` via `doubao-embedding-vision`
- **API**: `https://ark.cn-beijing.volces.com/api/plan/v3`

### Backup

- **Git repo**: `~/.kimi_openclaw/backups/20260612-030910/`
- **Commit**: `11a8f4d`
- **Update**: `cd ~/.kimi_openclaw/backups/20260612-030910 && git add . && git commit`

---

## Quick Reference

| Task | Tool | Command |
|------|------|---------|
| Spawn subagent | `sessions_spawn` | `{ label, runtime: "subagent", task }` |
| Browser control | `browser` | `action: navigate/snapshot/click/fill` |
| File read/write | `read` / `write` | `file_path` |
| Shell command | `exec` | `command` (pty: true for TUI) |
| Kimi Code CLI | `kimi` | `kimi -p "prompt"` |
| WebBridge API | `curl` | `curl -X POST http://127.0.0.1:10086/command` |
| Search | `kimi_search` | `query` |
| Vector memory | `memory_search` | `query` |
| Feishu doc | `lark-doc` | `feishu_fetch_doc` / `feishu_create_doc` |
| Feishu slide | `lark-slides` | `feishu_slides` tools |
| Blender render | `exec` | `blender --background --python ...` |
