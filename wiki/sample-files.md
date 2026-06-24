# Sample Files

**Summary**: The canonical JSON-stat sample documents provided on json-stat.org, each illustrating a specific feature of the 2.0 format.

**Sources**: raw/fullspec.html

**Last updated**: 2026-06-24

---

## Overview

The full specification recommends learning the format by inspecting **sample files** alongside the documentation (source: fullspec.html). These "madeup" (illustrative) documents are hosted under `https://json-stat.org/samples/` and each one targets a particular aspect of the format, making them useful as fixtures when testing [[programming-libraries]], converters, or the [[schema]].

## Canonical samples

| File | Illustrates |
|---|---|
| `oecd.json` | The main JSON-stat features in a single dataset (OECD data) |
| `canada.json` | The main JSON-stat features in a single dataset (Statistics Canada data) |
| `oecd-canada-col.json` | A [[response-classes|collection]] of **embedded** datasets (OECD + Statistics Canada) |
| `galicia.json` | A dataset with many dimensions (6): population in Galicia |
| `order.json` | A fake dataset to illustrate how `value` entries must be ordered (row-major) |
| `hierarchy.json` | A dataset with a **hierarchical** dimension (ABS Consumer Price Index Commodity Classification) |
| `us-gsp.json` | Mapping tests with several metrics and units (US States) |
| `us-unr.json` | Rich mapping tests (US Counties) |
| `us-labor.json` | A big dataset for **stress testing** |
| `collection.json` | The JSON-stat dataset sample collection |

(Source: fullspec.html)

## How to use them

- **Value ordering** — `order.json` is the reference for the "What does not change, first" row-major criterion described in [[format-specification]] and [[sparse-cubes]].
- **Hierarchies** — `hierarchy.json` exercises the `category.child` relationships documented in [[dimensions]].
- **Embedded responses** — `oecd-canada-col.json` shows full responses nested inside `link.item`, as described in [[links]].
- **Metrics and units** — `us-gsp.json` covers the metric role and the `unit` property (decimals, symbol, position) from [[dimensions]].
- **Performance** — `us-labor.json` is sized for stress testing parsers and the sparse/dense `value` handling in [[sparse-cubes]].

## Validation

Because the samples are standard 2.0 documents, they are the natural positive fixtures for the [[schema]]: a dataset sample should validate against `dataset.json`, the collection samples against `collection.json`, and any document against the general `index.json`.

## Related pages

- [[schema]]
- [[format-specification]]
- [[dimensions]]
- [[sparse-cubes]]
- [[links]]
- [[programming-libraries]]
