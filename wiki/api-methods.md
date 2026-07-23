# API Methods

**Summary**: Methods in the JSON-stat JavaScript Toolkit organized by function: reading, traversing, and transforming.

**Sources**: raw/api.md

**Last updated**: 2026-07-23

---

## Overview

The JSON-stat JavaScript Toolkit provides methods for working with [[jsonstat]] data. Methods are organized into three categories: reading, traversing, and transforming (source: api.md).

## Reading Methods

### JSONstat()
Creates a jsonstat instance from an external input (source: api.md).

**Signature**: `JSONstat(res [, init] [, typedArray])`

**Parameters**:
- `res` (required): Object in JSON-stat format, string "version", or URL string
- `init` (optional): Options object for fetch when res is a URL
- `typedArray` (optional): TypedArray constructor for value storage (since v1.4)

**Returns**:
- String version when res is "version"
- jsonstat instance when res is an object
- Promise resolving to jsonstat instance when res is a URL

**Examples**:
```javascript
// From object
var j = JSONstat({ ... });

// Get version
var version = JSONstat("version");

// From URL
JSONstat("https://json-stat.org/samples/oecd.json").then(function(j) { ... });

// With typed array
JSONstat("https://json-stat.org/samples/oecd.json", Float32Array).then(function(j) { ... });
```
(source: api.md)

## Traversing Methods

### Dataset()
Gets dataset information from a jsonstat instance (source: api.md).

**Signature**: `Dataset([dsid])`

**Parameters**:
- `dsid` (optional): Integer (index) or string (ID)

**Returns**:
- jsonstat instance when dsid is valid
- Array of jsonstat instances when dsid is not specified
- null when dsid is invalid

**Works on**: bundle, collection, and dataset instances (source: api.md)

### Dimension()
Gets dimension information from a dataset (source: api.md).

**Signature**: `Dimension([dimid] [, instance])`

**Parameters**:
- `dimid` (optional): Integer, string, or object `{ role: "geo" }`
- `instance` (optional, default `true`): when `false`, returns an array of category-label strings instead of a jsonstat instance

**Returns**:
- jsonstat instance when dimid is valid (and `instance` is `true` or omitted)
- Array of category-label strings when dimid is valid and `instance` is `false`
- Array of jsonstat instances when dimid is not specified
- null when dimid is invalid

### Category()
Gets category information from a dimension (source: api.md).

**Signature**: `Category([catid])`

**Parameters**:
- `catid` (optional): Integer (index) or string (ID)

**Returns**:
- jsonstat instance when catid is valid
- Array of jsonstat instances when catid is not specified
- null when catid is invalid

### Data()
Gets data information from a dataset (source: api.md).

**Signature**: `Data([dataid] [, status])`

**Parameters**:
- `dataid` (optional): Integer, array of indices, or object of dimension IDs
- `status` (optional): Boolean - include status (default true)

**Returns**:
- Array of value-status objects when no parameters
- Value-status object when dataid is valid and status is true
- Simple value when dataid is valid and status is false
- null when dataid is invalid

**Examples**:
```javascript
// By index
j.Data(0).value;

// By array of indices
j.Data([0, 0, 0]).value;

// By dimension IDs
j.Data({ "concept": "UNR", "area": "GR", "year": "2014" }).value;

// Without status
j.Data(0, false);
```
(source: api.md)

### Item()
Gets item information from collection instances (source: api.md).

**Signature**: `Item([itemid])`

**Parameters**:
- `itemid` (optional): Integer or filter object with "class" property

**Returns**:
- Item object when itemid is valid
- Array of items when itemid is not specified
- null when itemid is invalid

## Transforming Methods

### Unflatten()
Converts dataset to data array with associated metadata (source: api.md).

**Signature**: `Unflatten(callback)`

**Parameters**:
- `callback` (required): Function defining output structure

**Callback receives**:
- coordinates: Object of dimension ID to category ID
- datapoint: Object with value and status
- n: Cell counter (integer)
- row: Cells array

**Returns**: Array built by callback (source: api.md)

### Transform()
Converts dataset to tabular form (source: api.md).

**Signature**: `Transform([opts])`

**Parameters**:
- `opts` (optional): Object with options

**Options**:
- `type`: "array", "arrobj", "objarr", "object" (default: "array")
- `status`: Boolean (default: false)
- `content`: "id" or "label" (default: "label")
- `field`: "id" or "label" (default: "id" except for array type)
- `vlabel`: Value field label (default: "Value")
- `slabel`: Status field label (default: "Status")
- `meta`: Boolean - include metadata (default: false)
- `by`: Dimension ID for transposition
- `prefix`: String prefix for transposed properties
- `drop`: Array of dimension IDs to exclude
- `comma`: Boolean - use comma decimal mark (default: false)

**Returns**: Array or object depending on type (source: api.md)

### Dice()
Creates a subset by filtering dimension categories (source: api.md).

**Signature**: `Dice([filter] [, opts])`

**Parameters**:
- `filter` (optional): Object or array of dimension/category pairs
- `opts` (optional): Object with options

**Options**:
- `clone`: Boolean - keep original (default: false)
- `drop`: Boolean - filter is antifilter (default: false)
- `stringify`: Boolean - return JSON string (default: false)
- `ovalue`: Boolean - value as object when stringify (default: false)
- `ostatus`: Boolean - status as object when stringify (default: false)

**Returns**: jsonstat instance or string (source: api.md)

### toTable()
Deprecated method for converting to tabular form (source: api.md).

**Status**: Deprecated, planned removal in version 3.0.0

**Use**: Transform() instead

### Slice()
Deprecated method for creating subsets (source: api.md).

**Status**: Deprecated in version 1.1

**Use**: Dice() instead

## Related pages

- [[api-reference]]
- [[dataset-structure]]
- [[dimensions]]