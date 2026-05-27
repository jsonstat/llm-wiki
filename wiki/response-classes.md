# Response Classes

**Summary**: The different types of JSON-stat responses: collection, bundle, dataset, and dimension.

**Sources**: raw/fullspec.html, raw/api.md

**Last updated**: 2026-05-20

---

## Overview

JSON-stat supports several classes of responses, each serving different purposes. The class is specified using the `class` property (source: fullspec.html).

## Dataset Class

**Purpose**: Include a single dataset with all its data and metadata (source: fullspec.html).

**Properties**:
- version (required)
- class: "dataset"
- label (optional)
- source (optional)
- updated (optional)
- id (required) - Array of dimension IDs
- size (required) - Array of category counts
- dimension (required) - Object describing dimensions
- value (required) - Data values
- status (optional) - Observation metadata
- role (optional) - Dimension roles
- extension (optional) - Provider-specific data
- link (optional) - Related resources
- note (optional) - Annotations (source: fullspec.html)

**Example**:
```json
{
  "version": "2.0",
  "class": "dataset",
  "label": "Unemployment rate in the OECD countries 2003-2014",
  "id": ["concept", "area", "year"],
  "size": [1, 36, 12],
  "dimension": { ... },
  "value": [ ... ]
}
```
(source: fullspec.html)

## Dimension Class

**Purpose**: Include only a dimension node without full dataset data (source: fullspec.html).

**Properties**:
- version (required)
- class: "dimension"
- label (optional)
- category (required) - Describes dimension categories
- extension (optional) - Provider-specific data
- link (optional) - Related resources (source: fullspec.html)

**Example**:
```json
{
  "version": "2.0",
  "class": "dimension",
  "label": "sex",
  "category": {
    "index": ["T", "M", "F"],
    "label": {
      "T": "total",
      "M": "male",
      "F": "female"
    }
  }
}
```
(source: fullspec.html)

## Collection Class

**Purpose**: Reference items in a collection using the [[links]] property with an "item" relation (source: fullspec.html).

**Properties**:
- version (required)
- class: "collection"
- href (optional) - URL of the collection
- label (optional)
- updated (optional)
- link (required) - Contains "item" array
- extension (optional) - Provider-specific data (source: fullspec.html)

Items in the collection can be of any class: datasets, dimensions, or other collections. Items can be referenced by href or embedded with full content (source: fullspec.html).

**Example**:
```json
{
  "version": "2.0",
  "class": "collection",
  "href": "https://json-stat.org/samples/collection.json",
  "label": "JSON-stat Dataset Sample Collection",
  "link": {
    "item": [
      {
        "class": "dataset",
        "href": "https://json-stat.org/samples/oecd.json",
        "label": "Unemployment rate in the OECD countries 2003-2014"
      }
    ]
  }
}
```
(source: fullspec.html)

## Bundle Class (Pre-2.0)

**Purpose**: Contain several datasets in a single response (source: fullspec.html).

**Status**: Deprecated in version 2.0, replaced by collection class.

**Structure**: A map where dataset IDs are keys and values are objects containing dataset information (source: fullspec.html).

For backward compatibility, properties id, size, and role were children of dimension before 2.0. Data providers using pre-2.0 libraries are advised to include these properties at both the root level (2.0 style) and as children of dimension (<2.0 style) (source: fullspec.html).

## Error Class (Proposed)

**Purpose**: Communicate response errors (source: fullspec.html).

**Status**: Suggested but not mandatory. A specific error response class makes more sense in 2.0 (source: fullspec.html).

**Structure**: Array of objects with error information such as:
- status: HTTP status code
- id: Provider's internal error code
- href: Link to error information page
- label: Descriptive text about the error (source: fullspec.html)

## Related pages

- [[jsonstat]]
- [[dataset-structure]]
- [[dimensions]]
- [[links]]