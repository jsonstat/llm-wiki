# Links

**Summary**: Link mechanism for referencing related resources using IANA link relations.

**Sources**: raw/fullspec.html, raw/api.md

**Last updated**: 2026-05-20

---

## Overview

The link property provides a list of links related to a dataset or dimension, sorted by relation (source: fullspec.html). Relations are identified by IANA link relation names.

## Structure

**Type**: Object mapping relation IDs to arrays (source: fullspec.html)

**Location**: Can be included at:
- Root level (dataset, collection, dimension)
- Relation ID array element (collection items)

## IANA Link Relations

Relation IDs must be IANA link relation names that describe the relationship between the linked resources and the parent (source: fullspec.html).

Common relations include:
- **item** - Items in a collection
- **alternate** - Alternate representations
- **next** - Next page in a sequence
- **prev** - Previous page in a sequence
- **first** - First page in a sequence
- **last** - Last page in a sequence

## Linking to Non-JSON-stat Documents

When linking to non-JSON-stat documents, elements are objects with type and href properties (source: fullspec.html).

```json
{
  "version": "2.0",
  "class": "dataset",
  "link": {
    "alternate": [
      {
        "type": "text/csv",
        "href": "https://example.com/2002/population/sex.csv"
      },
      {
        "type": "text/html",
        "href": "https://example.com/2002/population/sex.html"
      }
    ]
  }
}
```
(source: fullspec.html)

## Linking to JSON-stat Documents

When linking to JSON-stat documents, elements can contain common JSON-stat properties (source: fullspec.html).

```json
{
  "version": "2.0",
  "class": "collection",
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

## Embedded Responses

JSON-stat documents can also embed full responses of any class (source: fullspec.html).

```json
{
  "version": "2.0",
  "class": "collection",
  "link": {
    "item": [
      {
        "class": "dataset",
        "href": "https://json-stat.org/samples/oecd.json",
        "label": "Unemployment rate in the OECD countries 2003-2014",
        "source": "Economic Outlook No 92 - December 2012 - OECD Annual Projections",
        "updated": "2012-11-27",
        "value": [5.943826289, 5.39663128, ...],
        "id": ["concept", "area", "year"],
        "size": [1, 36, 12],
        "dimension": { ... }
      }
    ]
  }
}
```
(source: fullspec.html)

## href Property

The href property specifies a URL (source: fullspec.html). It can be used to:
- Avoid sending shared information between requests
- Point to external dimension definitions
- Reference related resources

When href is a descendant of link, it points to related resources (source: fullspec.html).

## type Property

Describes the media type of the accompanying href (source: fullspec.html).

**Type**: String

**Required**: When resource is not a JSON-stat resource

```json
{
  "type": "text/csv",
  "href": "https://example.com/data.csv"
}
```
(source: fullspec.html)

## Related pages

- [[properties]]
- [[response-classes]]
- [[format-specification]]