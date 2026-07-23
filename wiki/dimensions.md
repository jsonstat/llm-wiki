# Dimensions

**Summary**: Dimension structure, roles, categories, labels, and hierarchical relationships in JSON-stat.

**Sources**: raw/fullspec.html, raw/api.md

**Last updated**: 2026-07-23

---

## Overview

Dimensions define the axes of the data cube. Each dimension represents a classification through which data can be organized (source: fullspec.html).

## Dimension Structure

Each dimension in the `dimension` object contains:

### label
Short descriptive text for the dimension (source: fullspec.html).

- Type: String
- Should be lowercase (except dataset labels)
- Example: `"sex"`, `"time"`, `"area"`

### category
Describes the possible values (categories) of the dimension (source: fullspec.html).

Contains:
- **index** - Category IDs and their order
- **label** - Descriptive text for each category
- **child** - Hierarchical relationships (optional)
- **coordinates** - Geographic coordinates for geo role (optional)
- **unit** - Unit information for metric role (optional)

### href
URL to external dimension definition (optional) (source: fullspec.html).

### extension
Provider-specific extended information (optional) (source: fullspec.html).

### link
Related resources (optional) (source: fullspec.html).

### note
Annotations (optional) (source: fullspec.html).

## Dimension Roles

Roles assign special meaning to dimensions. A role can be shared by several dimensions (source: fullspec.html).

### time Role
Identifies dimensions containing temporal data (source: fullspec.html).

```json
"role": {
  "time": ["arrivaldate", "departuredate"]
}
```
Categories with time role are assumed to be in chronological order (source: fullspec.html).

### geo Role
Identifies dimensions containing geographic data (source: fullspec.html).

```json
"role": {
  "geo": ["origin", "destination"]
}
```
Geo role categories can include coordinates (longitude, latitude) (source: fullspec.html).

### metric Role
Identifies dimensions containing different metrics or measures (source: fullspec.html).

```json
"role": {
  "metric": ["concept"]
}
```
Metric role categories can include unit information (source: fullspec.html).

### Dimensions Without a Role
In the JSON-stat format, any dimension that is not listed under `time`, `geo`, or `metric` simply has no role (source: fullspec.html). There is no `classification` role in the format itself.

The term "classification" is a **JavaScript Toolkit convention only**: when the Toolkit exposes a dimension's role (via `Dimension().role`), it uses the string `"classification"` for dimensions that the format leaves unroled. This is not part of the JSON-stat `role` object on the wire (source: api.md).

## Categories

### index
Orders the categories of a dimension (source: fullspec.html).

- Type: Array or object
- Required unless dimension is constant (single category)
- Determines order of data in value array

**Array form**:
```json
"category": {
  "index": ["M", "F", "T"]
}
```

**Object form** (maps ID to position):
```json
"category": {
  "index": {
    "M": 0,
    "F": 1,
    "T": 2
  }
}
```
(source: fullspec.html)

### label
Descriptive text for each category (source: fullspec.html).

- Type: Object mapping category IDs to labels
- Optional - if not provided, IDs are used as labels

```json
"category": {
  "label": {
    "M": "men",
    "F": "women",
    "T": "total"
  }
}
```
(source: fullspec.html)

### child
Hierarchical relationships between categories (source: fullspec.html).

- Type: Object mapping parent IDs to arrays of child IDs
- Only references direct descendants

```json
"child": {
  "EU15": ["AT", "BE", "DE", "DK", "ES", "FI", "FR", "GR", "IE", "IT", "LU", "NL", "PT", "SE", "UK"],
  "OECD": ["EU15", "AU", "CA", "CL", "CZ", "DK", "EE", "HU", "IS", "IL", "JP", "KR", "MX", "NO", "NZ", "PL", "SK", "SI", "CH", "TR", "US"]
}
```
(source: fullspec.html)

### coordinates
Geographic coordinates for geo role dimensions (source: fullspec.html).

- Type: Object mapping category IDs to [longitude, latitude] arrays

```json
"category": {
  "coordinates": {
    "ISO-3166-2:TV": [179.1995, -8.5199]
  }
}
```
(source: fullspec.html)

### unit
Unit information for metric role dimensions (source: fullspec.html).

- Type: Object mapping category IDs to unit objects
- Unit object can include: decimals, label, symbol, position

```json
"category": {
  "unit": {
    "exp": {
      "decimals": 1,
      "label": "millions",
      "symbol": "$",
      "position": "start"
    }
  }
}
```
(source: fullspec.html)

## Constant Dimensions

A dimension with only one category is called a constant dimension. For constant dimensions, the index property is unnecessary, but if index is not provided, a category label must be included (source: fullspec.html).

## Related pages

- [[dataset-structure]]
- [[properties]]
- [[links]]
- [[api-methods]]