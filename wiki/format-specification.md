# Format Specification

**Summary**: Full specification of the JSON-stat 2.0 format for statistical data.

**Sources**: raw/fullspec.html

**Last updated**: 2026-07-23

---

## Overview

JSON-stat is a simple lightweight standard best suited for data visualization, mobile apps, or open data initiatives. It follows a cube model where values are organized in cells, and a cell is the intersection of various [[dimensions]] (source: fullspec.html).

## Version

- **version** (required string) - Declares the JSON-stat version of the response (source: fullspec.html)
  - Current version is "2.0"
  - Helps clients parse the response correctly
  - Cannot accept values lower than 2.0 (source: fullspec.html)

## Response Classes

JSON-stat supports several [[response-classes]] (source: fullspec.html):

### Dataset Responses
Include a single dataset with the "dataset" class value. Core properties include id, size, dimension, and value (source: fullspec.html).

### Dimension Responses
Only include a dimension node with the "dimension" class value (source: fullspec.html).

### Collection Responses
Reference items in a collection using the [[links]] property with an "item" relation. Items can be of any class (datasets, dimensions, collections) (source: fullspec.html).

### Bundle Responses (Pre-2.0)
Could contain several datasets as a map where dataset IDs were keys. Replaced by collection in 2.0 (source: fullspec.html).

## Core Properties

### id
Required array containing an ordered list of dimension IDs (source: fullspec.html).

### size
Required array containing the number of categories for each dimension, same order as id (source: fullspec.html).

### role
Optional object used to assign special roles to dimensions (source: fullspec.html):
- **time** - Array of dimension IDs with time role
- **geo** - Array of dimension IDs with spatial role
- **metric** - Array of dimension IDs with metric role

### dimension
Required object containing information about dataset [[dimensions]] (source: fullspec.html). Must have properties matching each element in the id array.

### value
Required property containing data sorted according to dataset dimensions (source: fullspec.html):
- Usually an array where missing values are expressed as nulls
- For [[sparse-cubes]], can be an object to avoid many nulls
- Follows "row-major order" - "What does not change, first" criterion (source: fullspec.html)

### status
Optional property for observation-level metadata (source: fullspec.html):
- Array of the same length as `value` assigns status by position
- String assigns the same status to all data (recommended form for uniform status)
- Object provides status for specific cells

> **Deprecated:** Assigning a single uniform status via an array of size 1 is deprecated and may result in validation errors; use the string form instead.

## Dimension Structure

Each dimension ID object contains:
- **category** - Describes possible values of the dimension
- **index** - Orders categories (array or object mapping IDs to positions)
- **label** - Short descriptive text (string)
- **child** - Hierarchical relationships between categories (object)
- **coordinates** - Geographic coordinates for geo role dimensions (source: fullspec.html)

## Category Properties

Categories can have:
- **index** - Category IDs and their order
- **label** - Descriptive text for each category ID
- **child** - Hierarchical relationships (parent ID maps to array of child IDs)
- **coordinates** - Longitude/latitude for geo role categories
- **unit** - Unit of measure metadata for metric role categories (source: fullspec.html)

## Unit Properties

For metric role categories, unit can include:
- **decimals** - Number of unit decimals (required if unit present)
- **label** - Unit text displayed after values
- **symbol** - Unit symbol (e.g., "$", "%")
- **position** - "start" or "end" (default is "end") (source: fullspec.html)

## Additional Properties

- **label** - Short descriptive text at various levels
- **updated** - Update time in ISO 8601 format
- **source** - Short text describing dataset source
- **extension** - Provider-specific extended information (see [[extensions]])
- **href** - URL for the resource
- **link** - List of related resources (see [[links]])
- **note** - Annotations (array of strings)
- **error** - Error information (array of objects) (source: fullspec.html)

## Validation

The structural rules above are codified in official JSON Schema documents (JSON Schema 2020-12) — see [[schema]]. Any compliant validator can check a document's shape (per-class required properties, dense/sparse `value`, the three `status` forms, role keys, IANA link relations). JSON Schema cannot express cross-field cube invariants such as `value` length equaling the product of `size`; those require a semantic layer on top of the schema (source: fullspec.html).

## Related pages

- [[jsonstat]]
- [[response-classes]]
- [[dataset-structure]]
- [[dimensions]]
- [[sparse-cubes]]
- [[extensions]]
- [[links]]
- [[properties]]
- [[schema]]
- [[sample-files]]
