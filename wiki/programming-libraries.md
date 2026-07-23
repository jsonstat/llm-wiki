# Programming Libraries

**Summary**: Overview of programming language libraries for working with JSON-stat data.

**Sources**: raw/tools.html, raw/api.md

**Last updated**: 2026-07-23

---

## Overview

A rich ecosystem of programming libraries exists for working with [[jsonstat]] across multiple programming languages — including JavaScript, TypeScript, Python, Java, R, Julia, PHP, Rust/WebAssembly, and Go (source: tools.html). It also includes a dedicated semantic validator, jsonstat-validator (see [[validator]]), and a multi-format interop library, jsonstat-io, that bridges JSON-stat to columnar/spreadsheet formats like Apache Arrow, Parquet, DuckDB, Polars, and CSV-stat (see below).

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

## Rust / WebAssembly Library

### JSON-stat Wasm
WebAssembly port for working with JSON-stat, written in Rust (source: tools.html).

- **Website**: https://github.com/jsonstat/wasm
- **Author**: Xavier Badosa
- **License**: MIT License
- **Compatibility**: v. 2.0

## Go Library

### JSON-stat Go
Go library for working with JSON-stat (source: tools.html).

- **Website**: https://github.com/jsonstat/go
- **Author**: Xavier Badosa
- **License**: Apache License, Version 2.0
- **Compatibility**: v. 2.0

## TypeScript / Rust / WebAssembly Library

### jsonstat-validator
Polyglot (TypeScript + Rust/WebAssembly) semantic validator for JSON-stat v. 2.0 (source: tools.html). It layers the cross-field cube invariants on top of the official [[schema|JSON Schema 2020-12]] definitions and exposes a stable, versioned error-code vocabulary. It is the *developer tool* that powers the end-user **JSON-stat Validator** web app — the two should not be confused.

- **Website**: https://github.com/jsonstat/validator
- **Author**: Xavier Badosa
- **License**: Apache License, Version 2.0
- **Compatibility**: v. 2.0
- **Features**:
  - Structural pass reusing the vendored 2020-12 schemas (via `ajv` / the `jsonschema` crate)
  - Semantic rules covering size/value counts, dimension/category consistency, roles, status, links, hierarchies, etc.
  - Available as a TypeScript package, a Rust crate, and WebAssembly
  - See [[validator]] for the full rule and error-code reference

## Multi-Format Interop Library

### jsonstat-io
Polyglot interop/conversion library that bridges JSON-stat v. 2.0 to and from modern analytics and open-data formats (source: tools.html). Rather than parsing JSON-stat into native objects, jsonstat-io translates a JSON-stat dataset into a columnar or tabular representation for use in analytical engines and pipelines, and vice versa. It complements the standalone end-user [[tools-ecosystem|Conversion Tools]] (CSV Exporter/Importer, Excel exporter, command-line conversion, etc.), which are browser/CLI tools rather than a programmable library.

- **Website**: https://github.com/jsonstat/io
- **Author**: Xavier Badosa
- **License**: Apache License, Version 2.0
- **Compatibility**: v. 2.0
- **Supported formats**:
  - Apache Arrow
  - Parquet
  - DuckDB
  - Polars
  - CSV
  - CSV-stat
  - Frictionless Data Package
  - CSVW

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
- [[validator]]
