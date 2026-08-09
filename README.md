> ## ⚠️ Archived &mdash; this describes a format that is no longer used
>
> SuperMemory was redesigned in **Supervertaler for Trados v18.20.169**
> (August 2026). A memory bank is no longer a folder of interlinked articles
> with YAML frontmatter and `[[backlinks]]`; it is **three Markdown files** you
> edit by hand &mdash; `brief.md`, `terminology.md` and `style.md` &mdash; plus
> a `reference/` folder for source material, and a `_shared` bank of house
> defaults that any client bank can override.
>
> **Why it changed.** A real bank reached 136 terminology files &mdash; for what
> is a 136-row table &mdash; behind a 97-file backlog nobody had processed, with
> around 15% of articles carrying malformed frontmatter that silently excluded
> them from the very filtering the structure existed to enable. Nothing said so,
> and by that size nobody could read the bank and tell. Knowledge you cannot
> audit is not knowledge you can rely on.
>
> The format is now simple enough that it does not need a specification
> repository: it is documented in full at
> **[docs.supervertaler.com/trados/ai-assistant/super-memory/](https://docs.supervertaler.com/trados/ai-assistant/super-memory/)**.
>
> The plugin **detects and converts** banks in the old format described below;
> nothing is deleted in the process. Everything past this notice is kept for
> reference only.

---

# SuperMemory — the Supervertaler memory-bank format

**SuperMemory** is the knowledge-base system built into [Supervertaler for Trados](https://github.com/Supervertaler/Supervertaler-for-Trados). Where a translation memory stores previous wordings and a termbase stores approved term pairs, SuperMemory stores the *reasoning*: why a term was chosen, what a client insists on, what was rejected last time, and which domain conventions apply.

That knowledge lives in a **memory bank** — a plain folder of Obsidian-compatible Markdown articles with YAML frontmatter and `[[backlinks]]`. No database, no embeddings, no vendor lock-in. If every tool in this ecosystem disappeared tomorrow, your knowledge would still open in any text editor.

This repository is the **format definition**: the specification, and a starting skeleton.

## What's here

| Path | What it is |
|---|---|
| [`SPEC.md`](SPEC.md) | The format specification (v1.1) — folder layout, frontmatter schema, `### FILE:` output markers, scoring rules, code-fence tolerance |
| [`skeleton/`](skeleton/) | A ready-to-copy empty bank: the seven folders, `.obsidian/` defaults, one `_EXAMPLE_` article per folder, and the agent prompt templates |

> **This repository is not itself a memory bank.** The skeleton is deliberately nested under `skeleton/` so that no one is tempted to point a live bank at a clone of this repo. Keep your real banks well away from version control you might publish — or if you do want history, use a repository with no remote.

## Where banks actually live

Supervertaler for Trados keeps banks under your user-data folder:

```
<user data>\memory-banks\
├── default\
├── acme-legal\
└── pharma\
```

Each is a self-contained bank with the seven-folder skeleton. You switch between them from the Memory Bank dropdown in the Supervertaler Assistant panel. The plugin ships its own copies of the templates and writes the skeleton for you whenever you create a bank, so you never need to clone this repo to get started — it is here as the reference, not as a dependency.

## Reading a bank from outside Trados

Since **v18.20.146** the plugin exposes memory banks over the [Supervertaler MCP server](https://docs.supervertaler.com/trados/mcp-server/), so any MCP client (Claude Desktop, Claude Code, and others) can consult your bank while you work — whatever CAT tool you happen to have open:

- `get_supermemory_context` — the bank for the current project, with the article paths it drew from
- `search_supermemory` — free-text search across the active bank
- `list_supermemory_banks` — which banks exist and which is active

Because a bank is just Markdown on disk, you can also open it in [Obsidian](https://obsidian.md/), search it with ordinary tools, or point a filesystem MCP server at the folder.

## The seven folders

| Folder | Contents |
|---|---|
| `00_INBOX` | Raw material awaiting processing — briefs, feedback notes, reference articles |
| `01_CLIENTS` | Client profiles: preferences, style rules, terminology decisions |
| `02_TERMINOLOGY` | Term articles with approved translations, rejected alternatives, and the reasoning |
| `03_DOMAINS` | Domain conventions and common pitfalls |
| `04_STYLE` | Style guides, register notes, formatting rules |
| `05_INDICES` | Auto-generated indexes |
| `06_TEMPLATES` | The agent prompts that drive Process Inbox, Health Check and Distill |

Full details, including the frontmatter schema and the rules a conformant host must follow, are in [`SPEC.md`](SPEC.md).

## Design notes

The approach is inspired by Andrej Karpathy's [LLM knowledge base](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) pattern: structured Markdown that a model reasons over directly, rather than embeddings and retrieval. At translation-project scale — hundreds of articles, not millions — that stays auditable in a way a vector store does not. Every answer traces to a file you can open, read and correct by hand.

## History

An earlier plan for a standalone cross-platform "Supervertaler Assistant" app that would read these banks outside Trados was not pursued; the MCP server covers that ground without a second application to maintain. Its code remains in [supervertaler-assistant](https://github.com/Supervertaler/supervertaler-assistant) for reference.

## Licence

MIT — see [LICENSE](LICENSE).
