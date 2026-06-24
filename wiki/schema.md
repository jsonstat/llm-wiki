# JSON-stat Schema

**Summary**: The official JSON Schema (2020-12) definitions for JSON-stat 2.0 documents, which validate the *structure* of each [[response-classes|response class]] with any compliant validator.

**Sources**: raw/schema/index.json, raw/schema/dataset.json, raw/schema/collection.json, raw/schema/dimension.json, raw/fullspec.html

**Last updated**: 2026-06-24

---

## Overview

JSON-stat provides official **JSON Schema** documents so that any tool implementing the standard can validate a JSON-stat document without relying on the web [[format-specification|Format Validator]]. The full specification explicitly invites you to "use your preferred validator with the following JSON Schemas" (source: fullspec.html).

For convenience and future "improve the schemas" work, the four schemas are **vendored locally** under `raw/schema/` (immutable, alongside the other raw sources):

| Schema | `$id` | Local file | Required top-level properties |
|---|---|---|---|
| General (any class) | `https://json-stat.org/format/schema/2.0/` | `raw/schema/index.json` | `oneOf` of the three below |
| Dataset | `https://json-stat.org/format/schema/2.0/dataset.json` | `raw/schema/dataset.json` | `version`, `class`, `value`, `id`, `size`, `dimension` |
| Collection | `https://json-stat.org/format/schema/2.0/collection.json` | `raw/schema/collection.json` | `version`, `class`, `link` |
| Dimension | `https://json-stat.org/format/schema/2.0/dimension.json` | `raw/schema/dimension.json` | `version`, `class`, `category` |

All four declare the same metadata (source: dataset.json, collection.json, dimension.json, index.json):

- **Draft**: `"$schema": "https://json-schema.org/draft/2020-12/schema"` — i.e. the modern **2020-12** draft (not a legacy draft).
- **Version**: "1.05 of the JSON-stat 2.0 Schema", dated **2025-06-13**.

## Schema composition

### Per-class schemas

Each per-class schema is a self-contained document whose root is an `object` with `class` pinned to one enum value (`"dataset"`, `"collection"`, or `"dimension"`), plus the required properties listed above and `"additionalProperties": false` everywhere (source: dataset.json, collection.json, dimension.json).

### General schema

The general schema (`raw/schema/index.json`) does not add new rules; it composes the three response classes with a top-level **`oneOf`** (source: index.json):

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "JSON-stat 2.0 Schema",
  "oneOf": [
    { /* dataset branch:  class=="dataset",  required [version, class, value, id, size, dimension] */ },
    { /* dimension branch: class=="dimension", required [version, class, category] */ },
    { /* collection branch: class=="collection", required [version, class, link] */ }
  ]
}
```

### Self-containment (no shared library)

There are **no cross-file `$ref`s** between the schemas. Each file re-declares its own shared `$defs` (`strarray`, `category`, `link`, `unit`, `coordinates`, `updated`, …), so you can point a validator at a single file with no resolver or network access. The trade-off is that the shared definitions are **duplicated** across the four files, so any correction must be applied to all of them in lockstep.

## What the schemas enforce (structural layer)

The schemas encode the structural rules stated in [[format-specification]] (source: dataset.json, dimension.json, collection.json):

- **Dense vs. sparse `value`** — expressed as a `oneOf`: either an array of `number | null | string`, or an object mapping positions to `number | null | string`. A document cannot be a hybrid of the two (source: dataset.json).
- **`status`** — the three legal forms as a `oneOf`: a single string, an array of `string | null`, or an object of cell→status (source: dataset.json).
- **`role`** — only the keys `time`, `geo`, `metric` are allowed (`"additionalProperties": false`), each a unique string array (source: dataset.json).
- **`category.index`** — either a unique string array or an object of category→number (source: dataset.json).
- **`coordinates`** — fixed two-element tuple `[number, number]` (longitude, latitude) via `prefixItems` with `"items": false` (source: dataset.json).
- **`unit.position`** — enum `["start", "end"]` (source: dataset.json).
- **`updated`** — either an ISO-8601 `date-time` or a `YYYY-MM-DD` date (source: dataset.json).
- **`link` relation names** — restricted by a regex to the **IANA registered link relation names** (e.g. `item`, `alternate`, `next`, `self`, `version-history`, …), matching the design described in [[links]] (source: dataset.json).
- **`extension`** — typed as an open object (no inner constraints), consistent with [[extensions]] (source: dataset.json).

## What the schemas do NOT enforce (semantic layer)

JSON Schema — at any draft — cannot express cross-field relationships. The following invariants from [[format-specification]] and [[dimensions]] are therefore **not validated** and require a separate semantic/rules layer on top of the schema:

| Invariant | Where specified | Why the schema can't check it |
|---|---|---|
| Dense `value` array length equals the product of `size` | [[format-specification]] | No way to compare one field's length against another's value |
| Sparse `value` object keys are valid positions (`0 ≤ key < ∏size`) | [[sparse-cubes]] | Position range depends on the runtime `size` product |
| `status` array length equals the product of `size` | [[format-specification]] | Same cross-field limitation |
| `id` and `size` have the same length (and matching order) | [[format-specification]] | No field-to-field length coupling |
| `dimension` object keys exactly match the `id` array | [[dataset-structure]] | Keys-vs-array agreement |
| `role` dimension IDs actually exist in `id` | [[dimensions]] | Referential integrity across properties |
| `category.index` IDs match `category.label` keys | [[dimensions]] | Key-set agreement between siblings |
| Every metric-role dimension has a `unit` | [[dimensions]] | Conditional requirement based on a role membership |

This is the rationale for the proposed **semantic validation layer** (a rules engine or custom JSON-Schema keywords) that layers on top of these structural schemas and emits stable, named error codes (e.g. `VALUE_LEN_MISMATCH`, `ROLE_ID_UNKNOWN`). See the related discussion in [[format-specification]] and [[tools-ecosystem]].

## How to use

### Web validator

The simplest path is the **JSON-stat Format Validator** referenced in the specification, which runs these schemas server-side (source: fullspec.html). It is also listed among the [[tools-ecosystem]] validation tools.

### Any compliant library

Because the schemas are standard **2020-12**, you can validate with any compliant library (e.g. `ajv` in JavaScript/TypeScript, `jsonschema` in Python, `everit-json-schema` in Java) by loading the relevant local file from `raw/schema/`. Use the general `index.json` when the class of the incoming document is unknown.

## Improving the schemas

Potential improvements to consider (the schemas are vendored locally in `raw/schema/` precisely to support this):

1. **De-duplicate shared `$defs`** via `$ref` to a common module, so a single edit propagates to all classes.
2. **Add a semantic profile** for the cross-field invariants above — now realized as the [[validator]] package (`jsonstat-validator`), a polyglot (TypeScript + Rust/Wasm) semantic validator that layers on top of these schemas.
3. **Standardize `$id`/versioning** and publish to a schema registry for better tooling discovery.

## Related pages

- [[format-specification]]
- [[response-classes]]
- [[dataset-structure]]
- [[dimensions]]
- [[sparse-cubes]]
- [[extensions]]
- [[links]]
- [[tools-ecosystem]]
- [[sample-files]]
- [[validator]]
