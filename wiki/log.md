# JSON-stat Wiki Log

**Summary**: Append-only record of all wiki operations.

**Sources**: SKILLS.md

**Last updated**: 2026-06-23

---

## 2026-05-20

- **Initial wiki creation**: Ingested raw/api.md, raw/fullspec.html, and raw/tools.html
- **Created pages**:
  - wiki/index.md - Table of contents
  - wiki/log.md - Operation log
  - Source summaries: wiki/api-reference.md, wiki/format-specification.md, wiki/tools-ecosystem.md
  - Concept pages: wiki/jsonstat.md, wiki/response-classes.md, wiki/dataset-structure.md, wiki/dimensions.md, wiki/api-methods.md, wiki/properties.md, wiki/sparse-cubes.md, wiki/extensions.md, wiki/links.md, wiki/programming-libraries.md
- **Wiki-links**: All pages include [[wiki-links]] to related concepts

## 2026-06-23

- **Re-ingested raw/tools.html** (new version; source footer "Last update: 2026-06-23")
- **Added new entries**:
  - JSON-stat Wasm — a Rust/WebAssembly library (introduces a new Rust/WebAssembly language category)
  - JSON-stat WebMCP Explorer — an end-user tool that browses any JSON-stat endpoint via a web UI or natural language (WebMCP-enabled browser)
- **Updated pages**:
  - wiki/tools-ecosystem.md — added a "Rust / WebAssembly" section; added JSON-stat WebMCP Explorer under "Viewing and Filtering Tools"; bumped date
  - wiki/programming-libraries.md — added a "Rust / WebAssembly Library" section; expanded the overview to list the supported languages; bumped date
  - wiki/index.md — bumped date (no new pages were created; existing entries remain accurate)
- **Omitted**: the self-referential "JSON-stat LLM Wiki" end-user entry, per curator decision
- **Cross-links**: existing bidirectional links between [[tools-ecosystem]] and [[programming-libraries]] already cover the new items
