# Supervertaler SuperMemory — Claude Context

## What this project is
SuperMemory is a self-organizing, AI-maintained translation knowledge base for the Supervertaler ecosystem. Inspired by Andrej Karpathy's "LLM Knowledge Base" pattern (April 2026), it replaces traditional translation memories (TM) and term bases with a structured Markdown wiki that the AI processes, maintains, and consults.

The vault is an Obsidian vault. All knowledge is stored as interlinked Markdown files.

## Architecture

### Folder structure
```
00_INBOX/        — Raw material drop zone (articles, glossaries, feedback, style guides)
01_CLIENTS/      — Client profiles (preferences, style rules, terminology decisions)
02_TERMINOLOGY/  — Term articles with approved translations, rejected alternatives, and reasoning
03_DOMAINS/      — Domain knowledge (legal, medical, tech, marketing — conventions and pitfalls)
04_STYLE/        — Style guides and formatting conventions
05_INDICES/      — Auto-generated indexes and maps of content
06_TEMPLATES/    — AI agent prompt templates (Process Inbox, Health Check, query, translate)
```

### Three-phase workflow
1. **Ingest:** User drops raw material into `00_INBOX/`
2. **Process Inbox:** AI reads raw material, produces structured articles in 01–04, creates `[[backlinks]]`
3. **Health Check:** AI periodically scans the vault for inconsistencies, broken links, stale content, and missing cross-references

### Agent templates (in `06_TEMPLATES/`)
- `compile.md` — **Process Inbox**: raw material → structured articles
- `lint.md` — **Health Check**: scans KB for problems, auto-fixes what it can
- `translate_with_kb.md` — Translation agent: consults KB before translating
- `query.md` — Query agent: answers questions from KB content

## Terminology alignment
The following terms are used consistently across the plugin UI, help docs, and vault templates:

| User-facing term | Internal / file name | Description |
|---|---|---|
| **Process Inbox** | `compile.md` | Reads raw inbox files, writes structured articles |
| **Health Check** | `lint.md` | Scans vault for problems, fixes and reports |
| **Quick Add** (Ctrl+Alt+M) | `SuperMemoryQuickAddAction` | Captures terms from Trados editor |
| **Active prompt** | `ActivePromptPath` | Per-project prompt for Quick Add and Batch Translate |

Avoid using "compile", "compilation agent", "lint", or "linting agent" in user-facing text. These are internal terms only.

## Integration target
Primary integration: **Supervertaler for Trados** (C#/.NET plugin, `C:\Dev\Sv\Supervertaler-for-Trados\`)
Future: Supervertaler Workbench (Python), Supervertaler Workbench v2 (Tauri/Rust)

## Deployment
- **GitHub repo:** Ships the skeleton (folders, `_EXAMPLE_*` files, templates)
- **User data folder:** `C:\Users\{user}\Supervertaler\supermemory\`
- **Developer data:** Real translation data lives in the deployed vault, excluded from Git by `.gitignore`
- Pattern matches existing deployment: prompt library at `C:\Users\{user}\Supervertaler\prompt_library\`

## Git conventions
- `_EXAMPLE_*` files are tracked and shipped — they show users the format
- `06_TEMPLATES/` is fully tracked — agent prompts are shipped
- All other `.md` files in 00–05 folders are gitignored (user data)
- The `.obsidian/` folder is partially tracked (core config shipped, workspace/cache ignored)

## Key design decisions
- **No vector DB, no RAG.** Structured Markdown + LLM reasoning is sufficient at translation project scale.
- **`[[Backlinks]]` are mandatory.** They make the vault navigable in Obsidian's graph view and allow the LLM to follow connections.
- **Term articles record WHY.** Rejected alternatives and reasoning prevent re-litigation of terminology decisions.
- **Client overrides trump general rules.** The terminology hierarchy: client profile > term article > domain conventions > general style guide.
