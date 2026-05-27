# Programming Libraries

**Summary**: Overview of programming language libraries for working with JSON-stat data.

**Sources**: raw/tools.html, raw/api.md

**Last updated**: 2026-05-20

---

## Overview

A rich ecosystem of programming libraries exists for working with [[jsonstat]] across multiple programming languages (source: tools.html).

## JavaScript Libraries

### JSON-stat JavaScript Toolkit
The main library for working with JSON-stat in JavaScript and Node.js (source: tools.html).

- **Website**: https://github.com/jsonstat/toolkit
- **Author**: Xavier Badosa
- **License**: Apache License, Version 2.0
- **Compatibility**: v. 2.0
- **Features**:
  - Reading, traversing, and transforming methods
  - Support for typed arrays (since v1.4)
  - Promise-based URL fetching
  - See [[api-reference]] for full API documentation

### JSON-stat Javascript Utilities Suite
Additional utilities for JavaScript (source: tools.html).

- **Website**: https://github.com/jsonstat/suite
- **Author**: Xavier Badosa
- **License**: Apache License, Version 2.0
- **Compatibility**: v. 2.0

### JSON-stat for Eurostat
Specialized library for Eurostat JSON-stat data (source: tools.html).

- **Website**: https://github.com/jsonstat/euro
- **Author**: Xavier Badosa
- **License**: Apache License, Version 2.0
- **Compatibility**: v. 2.0

## Python Libraries

### pyjstat
Python library for JSON-stat (source: tools.html).

- **Website**: https://pypi.python.org/pypi/pyjstat/
- **Author**: Miguel Expósito Martín
- **License**: Apache License, Version 2.0
- **Compatibility**: v. 2.0

### jsonstat.py
Alternative Python library (source: tools.html).

- **Website**: https://github.com/26fe/jsonstat.py
- **Author**: Giovanni F.
- **License**: GNU Lesser General Public License, Version 3
- **Compatibility**: v. 2.0

## Java Library

### json-stat.java
Java library for JSON-stat (source: tools.html).

- **Website**: https://github.com/statisticsnorway/json-stat.java
- **Authors**: Erlend Hamnaberg, Hadrien Kohl, Statistics Norway
- **License**: Apache License, Version 2.0
- **Compatibility**: v. 2.0

## R Libraries

### rjstat
R package for converting JSON-stat to data frames (source: tools.html).

- **Website**: https://github.com/ajschumacher/rjstat
- **Authors**: Aaron Schumacher, Håkon Malmedal
- **License**: MIT License
- **Compatibility**: v. 2.0

### Eurostat R package
Imports Eurostat's JSON-stat v. 2.0 responses into R (source: tools.html).

- **Website**: https://ropengov.github.io/eurostat/
- **Authors**: Leo Lahti, Janne Huovari, Markus Kainu, Przemyslaw Biecek et al.
- **Compatibility**: v. 2.0

## Julia Library

### JSONStat.jl
Julia library for JSON-stat (source: tools.html).

- **Website**: https://github.com/klpn/JSONStat.jl
- **Author**: Karl Pettersson
- **License**: Simplified "2-clause" BSD License
- **Compatibility**: v. 2.0

## PHP Libraries

### JSONstat PHP Library
PHP library for JSON-stat (source: tools.html).

- **Website**: https://github.com/jsonstat/php
- **Author**: Xavier Badosa
- **License**: Apache License, Version 2.0
- **Compatibility**: v. 2.0

### Multidimensional HTML Table Renderer
Renders JSON-stat datasets as HTML tables (source: tools.html).

- **Website**: https://github.com/lfiweb/jsonstat-phpviz
- **Author**: Simon Speich
- **License**: GNU General Public License, Version 3 or later
- **Compatibility**: v. 2.0

## Common Features

Most libraries provide:
- Parsing JSON-stat responses
- Accessing data by dimension and category
- Converting to native data structures
- Handling metadata (labels, roles, etc.)

## Related pages

- [[tools-ecosystem]]
- [[api-reference]]
- [[jsonstat]]