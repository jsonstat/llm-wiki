# JSON-stat Wiki Log

**Summary**: Append-only record of all wiki operations.

**Sources**: SKILLS.md

**Last updated**: 2026-07-23

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

## 2026-07-18

- **Re-ingested raw/tools.html** (source footer corrected by the curator to "Last update: 2026-07-18"; content otherwise unchanged versus the 2026-07-05 version already captured by the wiki).
- **Added two end-user entries** that had previously been omitted/overlooked:
  - **From CSV-stat to Excel** (`https://github.com/jsonstat/csv#importing-csv-stat-into-excel`) — imports any CSV-stat into an Excel Workbook using a set of Power Query (M) queries. A genuine gap overlooked in every prior pass (it sits in the source between "From JSON-stat dataset to Excel" and "JSON-stat Subsetter"). Added under Conversion Tools.
  - **JSON-stat LLM Wiki** (`https://github.com/jsonstat/llm-wiki`) — the structured, LLM-maintained knowledge base about JSON-stat. This is the **self-referential** entry: it describes this very wiki. Added under a new "Knowledge Base" subsection of End User Tools, reversing the prior curator decisions (2026-06-23, 2026-07-05) to omit it; the entry links to [[index]].
- **Updated pages**:
  - `wiki/tools-ecosystem.md` — added "From CSV-stat to Excel" under Conversion Tools; added a new "Knowledge Base" subsection with the JSON-stat LLM Wiki (self-reference → [[index]]); bumped date to 2026-07-18.
  - `wiki/index.md` — bumped date to 2026-07-18 (no new pages created; the `[[tools-ecosystem]]` entry description remains accurate).
- **No changes** to `wiki/programming-libraries.md` (the 14 programming libraries and jsonstat-io are unchanged) or to the other end-user tools.

## 2026-07-23

- **Re-ingested raw/tools.html** (new version; source footer "Last update: 2026-07-23").
- **Added new entry**:
  - **JSON-stat Go** (`https://github.com/jsonstat/go`) — a Go library for working with JSON-stat (by Xavier Badosa; Apache 2.0; v. 2.0). It sits in the source's left column between JSON-stat Wasm and the JavaScript Utilities Suite but had not been captured by any prior pass, introducing a new Go language category. With this addition the wiki now covers all 15 active programming libraries in the source.
- **Updated pages**:
  - `wiki/programming-libraries.md` — added a new "Go Library" section (after the Rust/WebAssembly Library, mirroring the source column order); expanded the overview to list Go; bumped date to 2026-07-23.
  - `wiki/tools-ecosystem.md` — added a "Go" subsection under Programming Libraries (after Rust/WebAssembly); bumped date to 2026-07-23.
  - `wiki/index.md` — bumped date to 2026-07-23 (no new pages created; existing entries remain accurate).
- **No changes** to the other 14 programming libraries or the 21 end-user tools — their metadata is unchanged versus the 2026-07-18 version. The commented-out CLI block in the source remains omitted.

## 2026-07-23 — Lint

- **Scope**: Full lint pass over all 16 content pages (+ `index.md`, `log.md`) against `raw/` sources (`fullspec.html` 2024-05-24, `api.md`, `tools.html` 2026-07-23, `raw/schema/*`). Per `SKILLS.md` "Lint": checked contradictions, orphan pages, missing concept pages, outdated claims, and page-format compliance.
- **Findings** (numbered, with suggested fixes):
  1. **[Contradiction — high] `api-methods.md` → `Dimension()` `instance` parameter is internally contradictory and wrong.** Line 72 states "*when true, returns category labels array*" while line 77 states "Array of category labels when *instance is false*." The two lines give opposite truth values, and both conflict with `api.md`. The source's prose (api.md L258) is itself garbled ("When a valid dimid is specified in combination with instance *true*, the return value is an array of category labels") but its example (L263, `j.Dimension("area", false)`) proves labels are returned when `instance` is **false**; `instance` defaults to **true** (return a jsonstat instance/object). *Fix*: rewrite the `Dimension()` block so the parameter reads "`instance` (optional, default `true`): when `false`, returns an array of category label strings instead of a jsonstat instance" and the Returns list reads "Array of category-label strings when `instance` is `false`". Note: the underlying typo is in the immutable `raw/api.md`, so this wiki page should document the *intended* (example-backed) behaviour rather than copy the prose typo.
  2. **[Misattribution — low] `dimensions.md` → "classification" role cited to `fullspec.html`.** The "classification" role originates in the JavaScript Toolkit (`api.md` L248, the `{ role: "classification" }` filter), not the format spec; `fullspec.html`'s `role` section only defines `time`, `geo`, and `metric` as role keys. *Fix*: change the source tag on the "classification Role" subsection (L82–83) from `(source: fullspec.html)` to `(source: api.md)`.
  3. **[Stale — low] 9 pages remain dated `2026-05-20`** (initial creation): `jsonstat.md`, `api-methods.md`, `api-reference.md`, `dataset-structure.md`, `dimensions.md`, `properties.md`, `sparse-cubes.md`, `extensions.md`, `links.md`. No concrete factual drift versus current sources was detected beyond finding #1 (the sources they cite have not been re-versioned), but a refresh pass is recommended whenever these are next edited — especially `api-methods.md`, which must be corrected per finding #1 and should have its date bumped then.
- **No issues found** in the following dimensions:
  - **Orphan pages**: none. All 16 content pages receive at least one inbound `[[link]]` from another page (verified via full link-map).
  - **Missing concept pages**: none required. Concepts without a dedicated page (`bundle`, `status`, `unit`, `coordinates`, `hierarchy`, `classification`, `constant dimension`) are each covered as subsections of existing pages (`response-classes.md`, `dataset-structure.md`, `dimensions.md`), which matches the wiki's chosen granularity.
  - **Page-format compliance**: all 16 content pages have the required `# Title`, `**Summary**`, `**Sources**`, `**Last updated**`, `---` separator, and `## Related pages` block. `index.md` and `log.md` omit `## Related pages` by design (they are the table of contents and append-only log respectively) — not a violation.
  - **Source/footer accuracy**: wiki/log.md date claims for `fullspec.html` (2024-05-24) and `tools.html` (2026-07-23) match the actual source footers.
- **No files modified** in this pass (lint reports only; fixes are suggested for a follow-up edit pass). Bumped `log.md` date is implicit in this entry's heading.

## 2026-07-23 — Lint fixes (curator follow-up)

- Applied the fixes from the lint pass above, plus an additional deprecation surfaced during review.
- **Fix 1 — `Dimension().instance` contradiction.**
  - `raw/api.md` — corrected the source typo in the `instance` parameter description ("in combination with **instance** *true*" → "*false*"), so the prose now matches its own example (`j.Dimension("area", false)` returns labels).
  - `wiki/api-methods.md` — rewrote the `Dimension()` block so the parameter reads "`instance` (optional, default `true`): when `false`, returns an array of category-label strings instead of a jsonstat instance" and the Returns list lists the label-array outcome only under `instance === false`. Removed the self-contradicting lines (old L72 vs L77). Bumped date to 2026-07-23.
- **Fix 2 — "classification" is not a JSON-stat format role.** `wiki/dimensions.md` — replaced the misleading "classification Role" subsection (mis-cited to `fullspec.html`) with a "Dimensions Without a Role" subsection clarifying that the format defines only `time`, `geo`, `metric`; any other dimension is simply unroled. The string `"classification"` is documented as a **JavaScript Toolkit convention only** (used by `Dimension().role` for unroled dimensions, per `api.md`), not a value that appears in the on-the-wire `role` object. Bumped date to 2026-07-23.
- **Fix 4 — `status` array-of-size-1 is deprecated.** Curator note: assigning a single uniform status via an array of size 1 (e.g. `"status": ["e"]`) is deprecated; the string form (`"status": "e"`) must be used for this case.
  - `wiki/dataset-structure.md` — clarified that the array form is "one entry per value" (same length as `value`), marked the string form as the recommended uniform-status form, and added a deprecation note for the size-1 array. Bumped date to 2026-07-23.
  - `wiki/format-specification.md` — aligned the `status` bullet list (array same length as `value`, string recommended for uniform status, object for specific cells) and added the matching deprecation note. Bumped date to 2026-07-23.
- **No changes** to the remaining 8 of the 9 originally-stale pages (`jsonstat.md`, `api-reference.md`, `properties.md`, `sparse-cubes.md`, `extensions.md`, `links.md`, and the unaffected `index.md`/`log.md`); only the four pages touched by fixes 1/2/4 were re-dated.

## 2026-07-23 — Re-ingest api.md and fullspec.html (curator typo/explanation fixes)

- **Re-ingested `raw/api.md` and `raw/fullspec.html`** (curator updates: a typo correction and an improved explanation). Per the curator's note, the changes are already coherent with the wiki's content; this pass verified that and captured the one new substantive nuance.
- **`raw/api.md`** — The `Dimension()` `instance` parameter description (L258) now reads "in combination with **instance** *false*" (returning an array of category labels). This is exactly the typo the wiki flagged in the 2026-07-23 Lint (finding #1) and that the curator had already corrected in `raw/api.md` as part of "Lint fixes, Fix 1". The wiki's `Dimension()` documentation (`api-methods.md`) already describes the corrected, example-backed behaviour — no wiki change required.
- **`raw/fullspec.html`** — Footer "Last update" is now **2026-07-04** (the 2026-07-23 Lint had recorded 2024-05-24; the source has since been re-versioned). The `status` section (L436) now states that the single-element-array form "is deprecated and **may result in validation errors**" — a consequence not previously captured in the wiki's deprecation notes.
- **Updated pages** (status deprecation nuance — "may result in validation errors"):
  - `wiki/dataset-structure.md` — extended the deprecation blockquote (L98) to note the size-1 array form may result in validation errors; dates already 2026-07-23.
  - `wiki/format-specification.md` — extended the deprecation blockquote (L67) likewise; date already 2026-07-23.
- **Coherence scan**: all 16 content pages citing `api.md`/`fullspec.html` were checked against the updated sources — no contradictions found (Dimension `instance` behaviour, value ordering/row-major, the three `status` forms, role keys `time`/`geo`/`metric`, link/unit/note sections, embedded responses). The wiki's "classification is a Toolkit convention only" note (`dimensions.md`) remains consistent with both sources.
- **Source-footer accuracy correction**: `log.md` now records `fullspec.html` as 2026-07-04 (was 2024-05-24 in the 2026-07-23 Lint entry); the lint's source/footer-accuracy claim had gone stale.
- **No changes** to `index.md` (no new pages created; existing entries remain accurate).