# Dataset Structure

**Summary**: Core properties that define a JSON-stat dataset: id, size, dimension, value, and status.

**Sources**: raw/fullspec.html, raw/api.md

**Last updated**: 2026-05-20

---

## Overview

A JSON-stat dataset is organized as a multi-dimensional cube where values are cells at the intersection of [[dimensions]]. The core structure is defined by several required properties (source: fullspec.html).

## Required Properties

### id
Array of dimension IDs in the order they appear in the dataset (source: fullspec.html).

- Type: Array of strings
- Example: `["metric", "time", "geo", "sex"]`
- Dimension IDs can be any string with no special meaning in JSON-stat
- Use the [[dimensions]] role property to assign special meaning (source: fullspec.html)

### size
Array containing the number of categories for each dimension (source: fullspec.html).

- Type: Array of integers
- Must have same number of elements and same order as `id`
- Example: `[1, 12, 36, 2]` means 1 metric, 12 time periods, 36 areas, 2 sexes (source: fullspec.html)

### dimension
Object containing information about each dimension (source: fullspec.html).

- Type: Object
- Must have properties matching each element in the `id` array
- Each dimension ID object contains category information and metadata

```json
"dimension": {
  "metric": { ... },
  "time": { ... },
  "geo": { ... },
  "sex": { ... }
}
```
(source: fullspec.html)

### value
Contains the data sorted according to the dataset dimensions (source: fullspec.html).

- Type: Array or object
- Array form: Values with nulls for missing data
- Object form: Used for [[sparse-cubes]] to avoid many nulls

**Array form** (most common):
```json
"value": [105.3, 104.3, null, 177.2, ...]
```

**Object form** (for sparse data):
```json
"value": { "0": 1.3587, "18": 1.5849 }
```
(source: fullspec.html)

Values follow "row-major order" - "What does not change, first" criterion. The last dimension in `id` changes fastest (source: fullspec.html).

## Optional Properties

### status
Observation-level metadata (source: fullspec.html).

- Type: Array, string, or object
- Array: Assigns status to each value by position
- String: Assigns same status to all values
- Object: Provides status for specific cells

**Array form**:
```json
"value": [100, null, 102, 103, 104],
"status": ["a", "m", "a", "a", "p"]
```

**String form** (recommended for uniform status):
```json
"value": [100, 99, 102, 103, 104],
"status": "e"
```

**Object form** (specific cells):
```json
"value": [100, null, 102, 103, 104],
"status": { "1": "m" }
```
(source: fullspec.html)

Note: Status does not have a standard meaning or vocabulary - it's up to the provider (source: fullspec.html).

### role
Assigns special roles to dimensions (source: fullspec.html).

- Type: Object with arrays of dimension IDs
- Possible roles: time, geo, metric

```json
"role": {
  "time": ["arrivaldate", "departuredate"],
  "geo": ["origin", "destination"],
  "metric": ["concept"]
}
```
(source: fullspec.html)

## Data Access

In the JavaScript Toolkit, data can be accessed using:
- Index: `j.Data(0)` - First observation
- Array of indices: `j.Data([0, 0, 0])` - First category in each dimension
- Object of dimension IDs: `j.Data({ "concept": "UNR", "area": "GR", "year": "2014" })` (source: api.md)

## Number of Observations

The `n` property contains the total number of cells in the cube, including empty (missing) values (source: api.md).

## Related pages

- [[jsonstat]]
- [[dimensions]]
- [[sparse-cubes]]
- [[api-methods]]