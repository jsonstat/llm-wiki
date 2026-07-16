# JSON-stat Wiki Log

**Summary**: Append-only record of all wiki operations.

**Sources**: SKILLS.md

**Last updated**: 2026-07-16

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

## 2026-06-24

- **Ingested the JSON-stat Schema** (referenced in raw/fullspec.html, not previously captured by the wiki)
- **Downloaded** the four official JSON Schema (2020-12) files into `raw/schema/`: `index.json` (general), `dataset.json`, `collection.json`, `dimension.json` (version 1.05, dated 2025-06-13). Note: the general schema at `/format/schema/2.0/` is served as JSON despite the directory-like URL, so it was saved as `index.json` rather than `.html`.
- **Created pages**:
  - `wiki/schema.md` — the four schemas, their `oneOf` composition, self-containment, what they enforce, and the cross-field "semantic layer" gaps they cannot express
  - `wiki/sample-files.md` — the canonical sample documents and the feature each illustrates
- **Updated pages** (cross-links):
  - `wiki/format-specification.md` — added a "Validation" section; `[[schema]]`/`[[sample-files]]` links; bumped date
  - `wiki/tools-ecosystem.md` — added "Official JSON Schemas" under Validation Tools; `[[schema]]`/`[[sample-files]]` links; bumped date
  - `wiki/response-classes.md` — noted per-class required sets are codified in `[[schema]]`; `[[schema]]` link; bumped date
  - `wiki/index.md` — added `[[schema]]` and `[[sample-files]]` entries; bumped date
  - `README.md` — noted the vendored `raw/schema/` source and added a key entry point for the schema page
- **Correction**: the wiki previously implied no machine-readable schema existed; the schemas are documented in `fullspec.html` and are now captured here

## 2026-06-24 — jsonstat-validator package (Phase B implementation)

- **Planned** the `jsonstat-validator` package end to end (Architect mode) → its [DESIGN.md](https://github.com/jsonstat/validator/blob/main/DESIGN.md). Decision: Option B — one declarative `rules-manifest.json` is the single source of truth for the code vocabulary; rule *logic* is hand-written in TypeScript and Rust; a shared `corpus/cases.json` enforces behavioural parity.
- **Implemented** (now maintained in its own repository, [github.com/jsonstat/validator](https://github.com/jsonstat/validator)):
  - **TypeScript (M1/M2)**: rule engine + manifest + ajv 2020-12 structural wrapper; all rules S1–S8, D1–D7, C1–C2; `corpus/cases.json` (valid + known-invalid); Node CLI. **27/27 tests pass**; CLI verified; `tsc` build clean.
  - **Rust (M3)**: `crates/validator` (`jsonschema` crate for the structural pass; `default-features=false` since the schemas are self-contained). Full rule port; **corpus parity test passes** (both runtimes agree on all 20 cases).
  - **Wasm (M4)**: `wasm.rs` behind the `wasm` feature; **builds to `wasm32-unknown-unknown`** (`RUSTFLAGS='--cfg getrandom_backend="wasm_js"'`).
  - CI workflow (`.github/workflows/ci.yml`) and package `README.md`.
- **Created page**: `wiki/validator.md`; cross-linked from `[[schema]]`, `[[tools-ecosystem]]`, `[[index]]`.
- **Note**: the structural pass reuses the vendored 2020-12 schemas as-is (curated de-duplication deferred, design decision D1). JSON-stat's `updated` pattern uses `\-`, which ajv/the regex engine treat specially (ajv requires `unicodeRegExp:false`).
- **Pending (M5)**: npm/crates.io publish, `curated/` de-duplicated schemas with a curated≡vendored parity test, cross-validation vs the web Format Validator.
- **Repository split**: the implementation was extracted to its own repository, [github.com/jsonstat/validator](https://github.com/jsonstat/validator); the design doc moved to the project's `DESIGN.md` and `plans/` was removed from this wiki repo. This wiki references the package (see [[validator]]) and does not vendor the code.

## 2026-07-05

- **Re-ingested raw/tools.html** (new version; source footer "Last update: 2026-07-05")
- **Added new entries**:
  - **JSON-stat builder** (`jsonstat.com/builder/`) — a browser-based authoring tool that creates valid JSON-stat datasets interactively via a step-by-step wizard: define dimensions, categories, and roles to model a statistical cube, then feed it numbers from a spreadsheet, a CSV, a tidy one-row-per-observation format, or by hand; output is checked with the official, fully-offline JSON-stat tooling. Introduces a new "Authoring Tools" category under End User Tools.
  - **jsonstat-validator** — now appears in the source as a programming library (polyglot TypeScript + Rust/Wasm). This is the *developer tool* (the package behind the web app); it must not be confused with the end-user **JSON-stat Validator** web app at `/format/validator/`, which uses this package under the hood.
- **Updated pages**:
  - `wiki/tools-ecosystem.md` — added jsonstat-validator under Programming Libraries (new "TypeScript / Rust / WebAssembly" subsection); added the "Authoring Tools" subsection with the JSON-stat builder; clarified in "Validation Tools" that the JSON-stat Validator *web app* is powered by jsonstat-validator under the hood (removed the duplicate dev-tool bullet there); added `[[validator]]` to Related pages; bumped date.
  - `wiki/programming-libraries.md` — added a "TypeScript / Rust / WebAssembly Library" section for jsonstat-validator; expanded the overview to name TypeScript and the validator; added `[[validator]]` to Related pages; bumped date.
  - `wiki/index.md` — bumped date (no new pages created; existing entries remain accurate).
- **Omitted**: the self-referential "JSON-stat LLM Wiki" end-user entry, per curator decision (consistent with 2026-06-23).
- **No changes** to the other 13 programming libraries or the remaining end-user tools — their metadata is unchanged versus the 2026-06-23 version.

## 2026-07-16

- **Re-ingested raw/tools.html** (delta-only ingestion; source footer "Last update: 2026-07-05" unchanged since the 2026-07-05 pass, but the wiki had not yet captured one entry).
- **Added new entry**:
  - **jsonstat-io** (`https://github.com/jsonstat/io`) — a multi-format interop/conversion library (by Xavier Badosa; Apache 2.0; v. 2.0) that bridges JSON-stat v. 2.0 to and from Apache Arrow, Parquet, DuckDB, Polars, CSV, CSV-stat, Frictionless Data Package, and CSVW. It sits in the source's left column (Programming Libraries), immediately after jsonstat-validator. It is the *developer library* counterpart to the end-user browser/CLI Conversion Tools.
- **Updated pages**:
  - `wiki/programming-libraries.md` — added a new "Multi-Format Interop Library" section for jsonstat-io (after the TypeScript/Rust/Wasm validator section); expanded the overview paragraph to mention it; bumped date.
  - `wiki/tools-ecosystem.md` — added a "Multi-Format Interop" subsection under Programming Libraries (jsonstat-validator → jsonstat-io, mirroring the source order); added a cross-reference at the top of "Conversion Tools" pointing to jsonstat-io for programmatic/columnar conversion; bumped date.
  - `wiki/index.md` — bumped date (no new pages created; `[[programming-libraries]]` and `[[tools-ecosystem]]` entries remain accurate).
- **No changes** to the other 14 programming libraries or the end-user tools — their metadata is unchanged versus the 2026-07-05 version. The commented-out CLI block in the source remains omitted, and the self-referential "JSON-stat LLM Wiki" end-user entry continues to be omitted per prior curator decisions.