# Properties

**Summary**: Common properties used across JSON-stat responses for metadata and descriptive information.

**Sources**: raw/fullspec.html, raw/api.md

**Last updated**: 2026-05-20

---

## Overview

JSON-stat uses various properties to provide metadata and descriptive information at different levels of the response tree (source: fullspec.html).

## label

Short descriptive text assigned to IDs at different levels (source: fullspec.html).

**Type**: String or object

**Usage**:
- As root property or child of dimension/unit: string
- As child of category: object mapping category IDs to labels

**Examples**:
```json
// Dataset label
{
  "version": "2.0",
  "class": "dataset",
  "label": "Tuvalu population by sex in the 2002 Census"
}

// Dimension label
"sex": {
  "label": "sex"
}

// Category labels
"category": {
  "label": {
    "M": "men",
    "F": "women",
    "T": "total"
  }
}
```
(source: fullspec.html)

**Guidelines**:
- Should be lowercase except for dataset labels
- Language-dependent
- Client's job to capitalize for display (source: fullspec.html)

## source

Short text describing the source of the dataset or collection (source: fullspec.html).

**Type**: String

**Example**:
```json
{
  "source": "Economic Outlook No 92 - December 2012 - OECD Annual Projections"
}
```
(source: fullspec.html)

## updated

Update time of the dataset or collection (source: fullspec.html).

**Type**: String in ISO 8601 format

**Example**:
```json
{
  "updated": "2012-01-22T12:30:02Z"
}
```
(source: fullspec.html)

## note

Annotations at various levels (source: fullspec.html).

**Type**: Array of strings (dataset, dimension) or object (category)

**Usage**:
- Dataset/dimension: array of annotation strings
- Category: object mapping category IDs to annotation arrays

**Example**:
```json
{
  "note": ["Most data are from national correspondents."],
  "dimension": {
    "country": {
      "note": ["Data refer to actual territory."],
      "category": {
        "note": {
          "DEU": ["Germany was created 3 October 1990."]
        }
      }
    }
  }
}
```
(source: fullspec.html)

**Difference from label**:
- note is for annotations, label is for descriptive text
- note uses array, label uses string (source: fullspec.html)

## href

URL of the resource (source: fullspec.html).

**Type**: String

**Usage**:
- Avoid sending shared information between requests
- Point to external dimension definitions
- Point to related resources when descendant of link

**Example**:
```json
{
  "dimension": {
    "sex": {
      "href": "https://example.com/dimension/sex"
    }
  }
}
```
(source: fullspec.html)

## link

List of links related to a dataset or dimension (source: fullspec.html).

**Type**: Object of IANA link relation names to arrays

**Example**:
```json
{
  "link": {
    "alternate": [
      {
        "type": "text/csv",
        "href": "https://example.com/2002/population/sex.csv"
      }
    ]
  }
}
```
(source: fullspec.html)

See [[links]] for more details.

## extension

Provider-specific extended information (source: fullspec.html).

**Type**: Object with open children

**Purpose**: Allows JSON-stat to be extended for particular needs

**Example**:
```json
{
  "extension": {
    "contact": "EcoOutlook@oecd.org",
    "metadata": [
      {
        "title": "Economic Outlook Policy",
        "href": "https://www.oecd.org/eco/economicoutlookanalysisandforecasts/EO92macroeconomicsituation.pdf"
      }
    ]
  }
}
```
(source: fullspec.html)

See [[extensions]] for more details.

## error

Error information in responses (source: fullspec.html).

**Type**: Array of objects

**Status**: Suggested but not mandatory in version 1.1

**Possible elements**:
- status: HTTP status code
- id: Provider's internal error code
- href: Link to error information page
- label: Descriptive text about the error (source: fullspec.html)

## Related pages

- [[extensions]]
- [[links]]
- [[dimensions]]
- [[response-classes]]