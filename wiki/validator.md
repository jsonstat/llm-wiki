# jsonstat-validator

**Summary**: A polyglot (TypeScript + Rust/WebAssembly) semantic validator for JSON-stat 2.0 that layers cross-field cube invariants on top of the official [[schema|JSON Schema 2020-12]] definitions, with a stable, versioned error-code vocabulary. It is a standalone project — referenced here, not embedded.

**Sources**: https://github.com/jsonstat/validator (code + DESIGN.md), raw/fullspec.html

**Last updated**: 2026-06-24

---

## Overview

The official [[schema]] validates a document's *shape*, but JSON Schema cannot express relationships between fields — e.g. that the `value` array length must equal the product of [[dataset-structure|`size`]], or that `role.metric` IDs must exist in `id`. `jsonstat-validator` implements exactly these cross-field invariants (the **S/D/C catalogue**) on top of the structural schemas, so a document must pass *both* the structural and semantic passes to be considered valid.

It **reuses — never reimplements** — the structural pass: `ajv` (TypeScript) and the `jsonschema` crate (Rust). The two runtimes share one [`rules-manifest.json`](https://github.com/jsonstat/validator/blob/main/rules-manifest.json) (the code/severity/message vocabulary) and one [`corpus/cases.json`](https://github.com/jsonstat/validator/blob/main/corpus/cases.json) (the behavioural parity gate). The architecture is documented in the project's [DESIGN.md](https://github.com/jsonstat/validator/blob/main/DESIGN.md).

> **Repository:** the project lives at [github.com/jsonstat/validator](https://github.com/jsonstat/validator) — it is its own repository, separate from this LLM-Wiki.

## What it checks (selected)

| Code | Checks | Source |
|---|---|---|
| `VALUE_LEN_MISMATCH` (S3) | dense `value` length == product(`size`) | [[format-specification]] |
| `SPARSE_KEY_OUT_OF_RANGE` (S4) | sparse `value` keys in `[0, product(size)-1]` | [[sparse-cubes]] |
| `STATUS_LEN_MISMATCH` (S6) | array `status` length == product(`size`) | [[dataset-structure]] |
| `DIM_KEY_ID_MISMATCH` (S2) | `dimension` keys == `id` values | [[dataset-structure]] |
| `ID_SIZE_LEN_MISMATCH` (S1) | `len(id) == len(size)` | [[dataset-structure]] |
| `ROLE_ID_UNKNOWN` (S5) | `role.{time,geo,metric}` ⊆ `id` | [[dimensions]] |
| `INDEX_COUNT_MISMATCH` / `INDEX_POSITIONS_INVALID` (D1/D2) | per-dimension index vs `size` | [[dimensions]] |
| `LABEL/UNIT/COORD/NOTE_KEY_UNKNOWN` (D3–D6) | category sub-property keys ⊆ index ids | [[dimensions]] |
| `CHILD_ID_UNKNOWN` / `CHILD_CYCLE` (D7) | `category.child` ids valid and acyclic | [[dimensions]] |
| `METRIC_UNIT_MISSING` (S8, warning) | metric dims carry a `unit` | [[dimensions]] |
| `BUNDLE_DEPRECATED` (C2, info) | pre-2.0 bundle detected | [[response-classes]] |
| `STRUCTURAL_VIOLATION`, `PARSE_ERROR`, `CUBE_SIZE_OVERFLOW` | shape, JSON parse, overflow guard | [[schema]] |

The full, append-only catalogue lives in [`rules-manifest.json`](https://github.com/jsonstat/validator/blob/main/rules-manifest.json) and is versioned independently (`meta.ruleSetVersion`) from the package SemVer.

## Status

- **M1/M2 (TypeScript)** ✅ — rule engine, full rule set, corpus, Node CLI; 27/27 tests pass; `tsc` build clean.
- **M3 (Rust)** ✅ — `crates/validator` (lib + example CLI); corpus parity test passes (identical findings to the TS surface on the shared corpus).
- **M4 (Wasm)** ✅ — `wasm.rs` behind the `wasm` feature; builds to `wasm32-unknown-unknown`.
- **M5** ⏳ — npm/crates.io publish, `curated/` de-duplicated schemas (with curated≡vendored parity test), cross-validation vs the web [[tools-ecosystem|Format Validator]].

## How it relates to the wiki

This page is the realization of the "semantic validation layer" proposed in [[schema]]. The package is maintained in its own repository — [github.com/jsonstat/validator](https://github.com/jsonstat/validator) — and designed in its [DESIGN.md](https://github.com/jsonstat/validator/blob/main/DESIGN.md); this wiki references it but does not vendor the code.

## Related pages

- [[schema]]
- [[format-specification]]
- [[dataset-structure]]
- [[dimensions]]
- [[sparse-cubes]]
- [[response-classes]]
- [[tools-ecosystem]]
- [[sample-files]]
