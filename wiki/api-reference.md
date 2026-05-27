# API Reference

**Summary**: Documentation of the JSON-stat JavaScript Toolkit API for working with JSON-stat responses.

**Sources**: raw/api.md

**Last updated**: 2026-05-20

---

## Overview

The JSON-stat JavaScript Toolkit provides methods for reading, traversing, and transforming [[jsonstat]] data. It supports [[response-classes]] including collection, bundle, dataset, and dimension.

## Method Categories

### Reading Methods

- **JSONstat()** - Creates a jsonstat instance from an external input in JSON-stat format (source: api.md)
  - Accepts: object in JSON-stat format, string "version", or URL string
  - When a URL is specified, returns a promise that resolves to a jsonstat instance
  - Supports typed arrays since version 1.4 (source: api.md)

### Traversing Methods

- **Dataset()** - Gets dataset information from a jsonstat instance (source: api.md)
  - Can access by index (integer) or ID (string)
  - Returns jsonstat instance, array of instances, or null
  - Works on bundle, collection, and dataset instances (source: api.md)

- **Dimension()** - Gets dimension information from a jsonstat instance (source: api.md)
  - Access by index, ID, or role object (e.g., `{ role: "geo" }`)
  - Optional `instance` parameter returns category labels array instead of instance

- **Category()** - Gets category information from a dimension (source: api.md)
  - Access by index or ID
  - Returns jsonstat instance, array of instances, or null

- **Data()** - Gets data information from a dataset (source: api.md)
  - Access by index, array of dimension indices, or object of dimension IDs
  - Optional `status` parameter (default true) determines if status is included
  - Returns value-status object, array, or null

- **Item()** - Gets item information from collection instances (source: api.md)
  - Access by index or filter object with "class" property
  - Returns item object or array of items

### Transforming Methods

- **Unflatten()** - Converts dataset to data array with associated metadata (source: api.md)
  - Added in version 1.6
  - More efficient and flexible than toTable()
  - Exposes coordinates, datapoint, cell counter, and cells array to callback (source: api.md)

- **Transform()** - Converts dataset to tabular form (source: api.md)
  - Added in version 2.1.0 as future replacement for toTable()
  - Supports types: array, arrobj, objarr, object
  - Options include: type, status, content, field, vlabel, slabel, meta, by, prefix, drop, comma (source: api.md)

- **toTable()** - Deprecated method for converting to tabular form (source: api.md)
  - Planned removal in version 3.0.0
  - Use Transform() instead

- **Dice()** - Creates a subset by filtering dimension categories (source: api.md)
  - Added in version 1.1
  - Filter specified as object or array of dimension/category pairs
  - Options: clone, drop, stringify, ovalue, ostatus (source: api.md)

- **Slice()** - Deprecated method for creating subsets (source: api.md)
  - Deprecated in version 1.1
  - Use Dice() instead

## Public Properties

Common properties available on jsonstat instances include:
- class, length, id, label, size, value, status, updated, source, role, note, href, link, extension (source: api.md)

## Related pages

- [[response-classes]]
- [[dataset-structure]]
- [[dimensions]]
- [[api-methods]]
- [[properties]]