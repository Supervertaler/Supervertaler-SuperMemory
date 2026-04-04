# Supervertaler SuperMemory

A self-organizing, AI-maintained translation knowledge base for the [Supervertaler](https://supervertaler.com) ecosystem.

Inspired by Andrej Karpathy's [LLM Knowledge Base](https://venturebeat.com/data/karpathy-shares-llm-knowledge-base-architecture-that-bypasses-rag-with-an) architecture. No vector database, no RAG — just structured Markdown, `[[backlinks]]`, and an LLM acting as your research librarian.

## What is SuperMemory?

SuperMemory replaces traditional translation memories and term bases with a **living knowledge base** that organizes itself. You drop raw material in, and the AI processes it into structured, interlinked articles about your clients, terminology, domains, and style conventions.

When a new translation project comes in, the AI consults the knowledge base and translates with full contextual awareness — not just fuzzy TM matching, but actual understanding of why terms were chosen, how a client prefers their texts, and what pitfalls to avoid in a given domain.

## How it works

```
1. INGEST        →  Drop raw material into 00_INBOX/
2. PROCESS INBOX →  AI reads it, writes structured articles with [[backlinks]]
3. HEALTH CHECK  →  AI periodically checks for inconsistencies and gaps
4. TRANSLATE     →  AI consults the KB, translates with full context
```

## Folder structure

| Folder | Purpose |
|--------|---------|
| `00_INBOX/` | Raw material drop zone |
| `01_CLIENTS/` | Client profiles — preferences, style rules, history |
| `02_TERMINOLOGY/` | Term articles — approved translations, rejected alternatives, reasoning |
| `03_DOMAINS/` | Domain knowledge — conventions, pitfalls, reference material |
| `04_STYLE/` | Style guides — formatting, register, localization rules |
| `05_INDICES/` | Auto-generated indexes and maps of content |
| `06_TEMPLATES/` | AI agent prompt templates |

## Getting started

1. **Copy** this folder structure into your Supervertaler user data folder:
   ```
   C:\Users\{you}\Supervertaler\supermemory\
   ```

2. **Open** the folder as a vault in [Obsidian](https://obsidian.md/).

3. **Drop** raw material (client briefs, glossaries, feedback, reference articles) into `00_INBOX/`.

4. Click **Process Inbox** in the Supervertaler Assistant toolbar to organise your raw material into structured articles. (Or use the `06_TEMPLATES/compile.md` prompt template manually with any AI chat.)

5. **Explore** your knowledge base in Obsidian's graph view — watch the connections grow.

## Agent templates

The `06_TEMPLATES/` folder contains prompt templates for the four SuperMemory agents:

- **`compile.md`** — **Process Inbox**: reads raw material, produces structured KB articles
- **`lint.md`** — **Health Check**: scans the KB for inconsistencies, broken links, stale content
- **`translate_with_kb.md`** — Translates documents using the KB as context
- **`query.md`** — Answers questions by consulting the KB

## Design philosophy

- **No vector DB, no embeddings.** At translation project scale (~100s of articles), structured Markdown + LLM reasoning outperforms RAG.
- **Human-readable and auditable.** Every translation decision can be traced to a specific `.md` file you can open and read.
- **Self-healing.** The Health Check catches inconsistencies, broken links, and stale content automatically.
- **Portable.** It's just Markdown files. If any tool disappears, your knowledge stays.

## Part of the Supervertaler ecosystem

SuperMemory integrates with:
- **Supervertaler for Trados** — Trados Studio plugin
- **Supervertaler Workbench** — Standalone desktop app
- **Supervertaler Workbench v2** — Cross-platform rewrite

## License

MIT
