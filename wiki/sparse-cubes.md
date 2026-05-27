# Sparse Cubes

**Summary**: Handling datasets with many empty cells using object-based value storage.

**Sources**: raw/fullspec.html, raw/api.md

**Last updated**: 2026-05-20

---

## Overview

A sparse cube is a dataset where many cube cells are empty (missing values). In such cases, storing values as an array with many nulls is inefficient (source: fullspec.html).

## Array Form (Dense)

The default form uses an array where missing values are expressed as nulls (source: fullspec.html).

```json
{
  "version": "2.0",
  "class": "dataset",
  "value": [1.3587, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, null, 1.5849]
}
```

This is inefficient when most values are null.

## Object Form (Sparse)

To avoid many nulls, the value property can take the form of an object (source: fullspec.html).

```json
{
  "version": "2.0",
  "class": "dataset",
  "value": { "0": 1.3587, "18": 1.5849 }
}
```

The object maps position indices to values, omitting null entries entirely.

## When to Use Object Form

Use object form when:
- The dataset has many missing values
- File size is a concern
- Transmission efficiency is important

Use array form when:
- Most cells have values
- Simpler parsing is preferred
- Compatibility with older implementations is needed

## Value Ordering

Regardless of form, values follow the "What does not change, first" criterion (row-major order). The position indices in object form refer to positions in the conceptual array (source: fullspec.html).

## API Support

The JavaScript Toolkit's Data() method works with both forms transparently (source: api.md).

## Related pages

- [[dataset-structure]]
- [[jsonstat]]