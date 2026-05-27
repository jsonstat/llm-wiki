# JSON-stat

**Summary**: A simple lightweight standard for statistical data, best suited for data visualization, mobile apps, or open data initiatives.

**Sources**: raw/fullspec.html, raw/tools.html

**Last updated**: 2026-05-20

---

## Overview

JSON-stat is a lightweight standard designed for disseminating statistical data. It has been designed for all kinds of disseminators and is particularly well-suited for data visualization, mobile applications, and open data initiatives (source: fullspec.html).

## Core Principles

JSON-stat follows a cube model where values are organized in cells. A cell represents the intersection of various [[dimensions]] (source: fullspec.html). This multi-dimensional structure allows for efficient representation of complex statistical data.

## Version History

- **Version 1.0**: Initial release with bundle responses
- **Version 1.1**: Added class property, link mechanism, extension mechanism, and error handling
- **Version 1.2**: Added unit properties (decimals, symbol, position)
- **Version 2.0**: Current version with collection, dataset, and dimension [[response-classes]]

## Key Features

### Lightweight
Designed to be simple and lightweight, making it ideal for:
- Data visualization applications
- Mobile apps
- Open data initiatives (source: fullspec.html)

### Flexible Structure
Supports multiple [[response-classes]]:
- **Dataset** - Single dataset responses
- **Dimension** - Dimension-only responses
- **Collection** - References to multiple items
- **Bundle** - Pre-2.0 format with multiple datasets (deprecated) (source: fullspec.html)

### Rich Metadata
Includes comprehensive metadata through:
- Labels at multiple levels
- Dimension roles (time, geo, metric)
- Hierarchical categories
- Unit information
- Status codes for observations
- Annotations and notes (source: fullspec.html)

### Extensibility
The [[extensions]] mechanism allows providers to add custom properties for specific needs (source: fullspec.html).

### Sparse Data Support
For [[sparse-cubes]] with many empty cells, values can be stored as objects instead of arrays, reducing file size (source: fullspec.html).

## Value Ordering

Data follows the "What does not change, first" criterion (row-major order). Values are ordered by iterating through categories of the last dimension first, then moving to previous dimensions (source: fullspec.html).

For example, with dimensions A (3 categories), B (2 categories), and C (4 categories), the order is:
```
A1B1C1   A1B1C2   A1B1C3   A1B1C4
A1B2C1   A1B2C2   A1B2C3   A1B2C4
A2B1C1   A2B1C2   A2B1C3   A2B1C4
...
```
(source: fullspec.html)

## Ecosystem

A rich ecosystem of [[programming-libraries]] and tools exists for working with JSON-stat across multiple programming languages (source: tools.html).

## Related pages

- [[format-specification]]
- [[response-classes]]
- [[dataset-structure]]
- [[dimensions]]
- [[tools-ecosystem]]