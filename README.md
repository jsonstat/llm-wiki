# JSON-stat LLM Wiki

A structured, LLM-maintained knowledge base about the [JSON-stat](https://json-stat.org/) format, built following [Andrej Karpathy's LLM Wiki pattern](https://karpathy.ai/blog/llmwiki.html).

## What is this

### The LLM Wiki pattern

In April 2026, Andrej Karpathy proposed an alternative to traditional Retrieval-Augmented Generation (RAG) for managing knowledge with LLMs. The core idea is **"compile, don't retrieve"**:

- **Traditional RAG** retrieves raw document chunks on every query — stateless and repetitive, like interpreting source code from scratch every time.
- **LLM Wiki** pre-processes raw sources into a structured, interlinked wiki — stateful and compounding, like compiling source code into an optimized binary.

The result is a plain-Markdown knowledge base that an LLM maintains and a human curates. Knowledge **compounds over time**: every new source strengthens existing pages, adds cross-links, and surfaces contradictions — instead of being silently forgotten after a single query.

### This repository

This repo applies the LLM Wiki pattern to **JSON-stat**, a lightweight standard for disseminating statistical data. It covers the format specification (up to version 2.0), the JavaScript Toolkit API, and the broader ecosystem of tools and libraries.

The wiki is **not written by hand**. An LLM reads the raw sources, creates and updates structured Markdown pages, and keeps everything cross-linked and consistent. The human's role is to add sources, ask questions, and guide the analysis.

## Repository structure

```
.
├── SKILLS.md       ← Editorial guide for the LLM (the "schema" layer)
├── raw/            ← Original source documents (immutable)
│   ├── api.md
│   ├── fullspec.html
│   └── tools.html
└── wiki/           ← Compiled knowledge base (LLM-maintained)
    ├── index.md    ← Table of contents for the entire wiki
    ├── log.md      ← Append-only record of all operations
    └── *.md        ← One page per concept or source summary
```

### `SKILLS.md` — The schema layer

This is the operating manual for the LLM. It defines:

- **Folder structure** — Where raw sources live and where wiki pages go.
- **Ingest workflow** — Step-by-step instructions for processing a new source (read → discuss → create/update pages → cross-link → update index and log).
- **Page format** — A consistent template every wiki page must follow (summary, sources, last-updated date, content, related pages).
- **Citation rules** — How to attribute claims to sources and handle contradictions.
- **Question-answering protocol** — How to look up information in the wiki and when to file answers back as new pages.
- **Lint / audit checklist** — How to find contradictions, orphan pages, missing concept pages, and outdated claims.

Think of it as the `.editorconfig` of the knowledge base: it ensures consistency regardless of which LLM session touches the wiki.

### `raw/` — The source layer

Contains the original, **immutable** source documents. Nothing in this folder is ever modified. Current sources:

| File | Description |
|---|---|
| `fullspec.html` | JSON-stat 2.0 format specification |
| `api.md` | JSON-stat JavaScript Toolkit API reference |
| `tools.html` | Ecosystem of tools and libraries |

To add new knowledge, drop a document here and ask the LLM to ingest it.

### `wiki/` — The compiled knowledge layer

Contains structured Markdown pages maintained by the LLM. Each page covers a single concept or source summary and follows a consistent format:

- **Summary** — One to two sentences.
- **Sources** — Which raw files the page draws from.
- **Last updated** — Date of the most recent update.
- **Content** — Clear headings, short paragraphs, `[[wiki-links]]` to related concepts.
- **Related pages** — Explicit cross-links.

Key entry points:

| Page | Description |
|---|---|
| `index.md` | Table of contents — start here |
| `log.md` | Chronological record of every change |
| `jsonstat.md` | Top-level overview of the JSON-stat format |
| `format-specification.md` | The 2.0 spec in detail |
| `dataset-structure.md` | Core dataset properties (id, size, value, status…) |
| `dimensions.md` | Dimension roles, categories, hierarchies |
| `response-classes.md` | Collection, bundle, dataset, dimension classes |
| `api-methods.md` | JavaScript Toolkit reading/traversal methods |
| `programming-libraries.md` | Libraries across languages |
| `tools-ecosystem.md` | Converters, explorers, and other tools |

## How to install

This is a plain-text knowledge base — there is nothing to build or compile.

### 1. Clone the repository

```bash
git clone https://github.com/jsonstat/llm-wiki.git
cd llm-wiki
```

### 2. Point your LLM at it

The wiki is designed to work with any LLM that can read files. How you do this depends on your setup:

**With an AI coding assistant (Claude Code, Antigravity CLI, Windsurf, Cline, Cursor, etc.)**

Open the repository as your workspace. The assistant will automatically see `SKILLS.md` and follow its instructions when you ask questions or request an ingestion.

**With a chat-based LLM (ChatGPT, Claude, Gemini, Qwen Studio, etc.)**

1. Copy the contents of `SKILLS.md` into your system prompt (or paste it at the start of the conversation).
2. Attach or paste the relevant `wiki/` pages as context.
3. Ask your question or request an ingestion.

### 3. Use it

| Task | How |
|---|---|
| **Ask a question** | *"What response classes does JSON-stat 2.0 support?"* — The LLM reads the wiki and answers with citations. |
| **Ingest a new source** | Drop a file in `raw/`, then ask: *"Ingest raw/new-source.pdf"*. The LLM reads it, creates/updates wiki pages, and logs the change. |
| **Audit the wiki** | Ask: *"Lint the wiki"*. The LLM checks for contradictions, orphan pages, missing concepts, and format issues. |

### Requirements

- An LLM with file-reading capabilities (or the ability to paste file contents).
- Optionally, [Obsidian](https://obsidian.md/) to browse the wiki with rendered `[[wiki-links]]` and a live graph view.

## How it works

The following diagram summarizes the three-phase lifecycle:

```
┌─────────────────────────────────────────────────────────┐
│                      INGEST                             │
│                                                         │
│   raw/new-doc.pdf ──► LLM reads & extracts ──► wiki/    │
│                        ┌──────────────┐                 │
│                        │ Create pages │                 │
│                        │ Update pages │                 │
│                        │ Cross-link   │                 │
│                        │ Update index │                 │
│                        │ Append log   │                 │
│                        └──────────────┘                 │
├─────────────────────────────────────────────────────────┤
│                      QUERY                              │
│                                                         │
│   User question ──► LLM reads wiki/ ──► Cited answer    │
│                                                         │
│   (Valuable answers are filed back into the wiki)       │
├─────────────────────────────────────────────────────────┤
│                      LINT                               │
│                                                         │
│   LLM audits wiki/ ──► Contradictions                   │
│                     ──► Orphan pages                    │
│                     ──► Missing concepts                │
│                     ──► Outdated claims                 │
│                     ──► Format violations               │
└─────────────────────────────────────────────────────────┘
```

## License

MIT License

Copyright (c) 2026 Xavier Badosa

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
