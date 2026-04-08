# Supervertaler-SuperMemory (archived)

> **This repository has moved.**
>
> It is now part of [**Supervertaler/supervertaler-assistant**](https://github.com/Supervertaler/supervertaler-assistant).

## What happened

"SuperMemory" has been retired as a product name. What used to be called
"the SuperMemory vault" is now called a **memory bank** – the long-term
memory of the **Supervertaler Assistant**, a cross-platform AI assistant
for professional translators.

Everything that used to live here has a new home in the unified
`supervertaler-assistant` repo:

| What it was | Where to find it now |
|---|---|
| Vault format specification (`SPEC.md`) | [`SPEC.md`](https://github.com/Supervertaler/supervertaler-assistant/blob/main/SPEC.md) – now titled *Supervertaler Memory Bank Format – Specification* (v1.1) |
| Starting vault skeleton (`00_INBOX/` … `06_TEMPLATES/`) | [`skeleton/`](https://github.com/Supervertaler/supervertaler-assistant/tree/main/skeleton) |
| Agent prompt templates | [`skeleton/06_TEMPLATES/`](https://github.com/Supervertaler/supervertaler-assistant/tree/main/skeleton/06_TEMPLATES) and bundled in [`supervertaler_assistant/templates/`](https://github.com/Supervertaler/supervertaler-assistant/tree/main/supervertaler_assistant/templates) |
| The standalone desktop app (used to live in a separate `SuperMemory/` repo) | [`supervertaler_assistant/`](https://github.com/Supervertaler/supervertaler-assistant/tree/main/supervertaler_assistant) |

## The format is unchanged

The wire format (folder layout, frontmatter schema, `### FILE:` output
markers, scoring rules, code-fence tolerance) is byte-for-byte compatible.
Any conformant v1.0 SuperMemory vault is also a conformant v1.1 memory
bank – just rename the folder if you want, and point the
Supervertaler Assistant or Supervertaler for Trados at it.

## Hosts that read the memory-bank format

- [**Supervertaler Assistant**](https://github.com/Supervertaler/supervertaler-assistant) – the standalone cross-platform Python/PyQt6 app (this repo's successor)
- [**Supervertaler for Trados**](https://github.com/Supervertaler/Supervertaler-for-Trados) – Trados Studio plugin

Please update any bookmarks, clones or references to point at the new
repo. This one will remain available as a read-only archive for history.
