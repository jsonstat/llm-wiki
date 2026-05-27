# Extensions

**Summary**: Extension mechanism for adding provider-specific properties to JSON-stat responses.

**Sources**: raw/fullspec.html, raw/api.md

**Last updated**: 2026-05-20

---

## Overview

The extension property allows JSON-stat to be extended for particular needs. Providers are free to define where they include this property and what children are allowed in each case (source: fullspec.html).

## Purpose

Extensions enable data providers to:
- Add custom metadata not covered by standard properties
- Include provider-specific information
- Extend the format for specialized use cases
- Maintain backward compatibility while adding new features

## Structure

**Type**: Object with open children (source: fullspec.html)

**Location**: Can be included at:
- Root level (dataset, collection)
- Dimension level
- Relation ID array element (collection items)

## Example

```json
{
  "version": "2.0",
  "class": "dataset",
  "label": "Unemployment rate in the OECD countries 2003-2014",
  "source": "Economic Outlook No 92 - December 2012 - OECD Annual Projections",
  "updated": "2012-11-27",

  "extension": {
    "contact": "EcoOutlook@oecd.org",
    "metadata": [
      {
        "title": "Economic Outlook Policy and other assumptions",
        "href": "https://www.oecd.org/eco/economicoutlookanalysisandforecasts/EO92macroeconomicsituation.pdf"
      },
      {
        "title": "Economic Outlook Sources and Methods",
        "href": "https://www.oecd.org/document/22/0,3343,en_2649_34109_33702486_1_1_1_1,00.html"
      }
    ]
  },

  "value": [ ... ],
  "id": [ ... ],
  "size": [ ... ],
  "dimension": { ... }
}
```
(source: fullspec.html)

## API Access

Client libraries should provide a general way to retrieve extension contents (source: fullspec.html).

**JavaScript Toolkit example**:
```javascript
// Get entire extension object
J.Dataset(0).extension;

// Get specific extension property
J.Dataset(0).extension.contact;
```
(source: fullspec.html)

## Best Practices

1. **Document extensions**: Clearly document custom extension properties
2. **Use meaningful names**: Choose descriptive property names
3. **Consider standardization**: If an extension becomes widely used, consider proposing it as a standard property
4. **Namespace if needed**: For conflicting names, use provider-specific prefixes
5. **Version extensions**: Include version information for extensions that may change

## Related pages

- [[properties]]
- [[format-specification]]
- [[api-reference]]