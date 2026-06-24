# Tools Ecosystem

**Summary**: Overview of programming libraries and end-user tools for working with JSON-stat.

**Sources**: raw/tools.html

**Last updated**: 2026-06-24

---

## Programming Libraries

### JavaScript

- **JSON-stat JavaScript Toolkit** - Main library for working with JSON-stat in JavaScript and Node.js (source: tools.html)
  - Website: https://github.com/jsonstat/toolkit
  - Author: Xavier Badosa
  - License: Apache License, Version 2.0
  - Compatibility: v. 2.0

- **JSON-stat Javascript Utilities Suite** - Additional utilities for JavaScript (source: tools.html)
  - Website: https://github.com/jsonstat/suite
  - Author: Xavier Badosa
  - License: Apache License, Version 2.0
  - Compatibility: v. 2.0

- **JSON-stat for Eurostat** - Specialized library for Eurostat JSON-stat data (source: tools.html)
  - Website: https://github.com/jsonstat/euro
  - Author: Xavier Badosa
  - License: Apache License, Version 2.0
  - Compatibility: v. 2.0

### Python

- **pyjstat** - Python library for JSON-stat (source: tools.html)
  - Website: https://pypi.python.org/pypi/pyjstat/
  - Author: Miguel Expósito Martín
  - License: Apache License, Version 2.0
  - Compatibility: v. 2.0

- **jsonstat.py** - Alternative Python library (source: tools.html)
  - Website: https://github.com/26fe/jsonstat.py
  - Author: Giovanni F.
  - License: GNU Lesser General Public License, Version 3
  - Compatibility: v. 2.0

### Java

- **json-stat.java** - Java library for JSON-stat (source: tools.html)
  - Website: https://github.com/statisticsnorway/json-stat.java
  - Authors: Erlend Hamnaberg, Hadrien Kohl, Statistics Norway
  - License: Apache License, Version 2.0
  - Compatibility: v. 2.0

### R

- **rjstat** - R package for converting JSON-stat to data frames (source: tools.html)
  - Website: https://github.com/ajschumacher/rjstat
  - Authors: Aaron Schumacher, Håkon Malmedal
  - License: MIT License
  - Compatibility: v. 2.0

- **Eurostat R package** - Imports Eurostat's JSON-stat v. 2.0 responses into R (source: tools.html)
  - Website: https://ropengov.github.io/eurostat/
  - Authors: Leo Lahti, Janne Huovari, Markus Kainu, Przemyslaw Biecek et al.
  - Compatibility: v. 2.0

### Julia

- **JSONStat.jl** - Julia library for JSON-stat (source: tools.html)
  - Website: https://github.com/klpn/JSONStat.jl
  - Author: Karl Pettersson
  - License: Simplified "2-clause" BSD License
  - Compatibility: v. 2.0

### PHP

- **JSONstat PHP Library** - PHP library for JSON-stat (source: tools.html)
  - Website: https://github.com/jsonstat/php
  - Author: Xavier Badosa
  - License: Apache License, Version 2.0
  - Compatibility: v. 2.0

- **Multidimensional HTML Table Renderer** - Renders JSON-stat datasets as HTML tables (source: tools.html)
  - Website: https://github.com/lfiweb/jsonstat-phpviz
  - Author: Simon Speich
  - License: GNU General Public License, Version 3 or later
  - Compatibility: v. 2.0

### Rust / WebAssembly

- **JSON-stat Wasm** - WebAssembly port for working with JSON-stat, written in Rust (source: tools.html)
  - Website: https://github.com/jsonstat/wasm
  - Author: Xavier Badosa
  - License: MIT License
  - Compatibility: v. 2.0

## End User Tools

### Conversion Tools

- **From JSON-stat API to JSON/CSV API** - Converts dataset API URLs to JSON or CSV format (source: tools.html)
- **From JSON-stat dataset to Excel** - Downloads dataset information as Excel file (source: tools.html)
- **JSON-stat CSV Exporter** - Converts local JSON-stat dataset to CSV (source: tools.html)
- **JSON-stat CSV Batch Exporter** - Batch converts multiple datasets to CSV (source: tools.html)
- **JSON-stat CSV Importer** - Converts CSV to JSON-stat (source: tools.html)
- **JSON-stat Command Line Conversion Tools** - Command line conversion supporting JSON, CSV, and SDMX-JSON (source: tools.html)

### Viewing and Filtering Tools

- **JSON-stat WebMCP Explorer** - Fetch any JSON-stat endpoint and browse its data through a web interface or natural language using a WebMCP-enabled browser (may require enabling experimental features in Chrome and installing a WebMCP extension) (source: tools.html)
  - Website: https://jsonstat.com/webmcp/
- **JSON-stat Subsetter** - Retrieve, view, filter, and save subsets of JSON-stat/CSV-stat/SDMX-JSON datasets (source: tools.html)
- **JSON-stat Explorer** - View and filter JSON-stat queries or pasted JSON-stat content (source: tools.html)
- **Idescat JSON-stat Viewer** - Fully interactive table viewer for dataset queries (source: tools.html)
- **JSON-stat Viewer** - View contents of JSON-stat queries of any kind (source: tools.html)
- **JSON-stat Table Browser** - Browse contents in tabular form (source: tools.html)
- **JSON-stat Input Table Browser** - Browse pasted JSON-stat or SDMX-JSON text in tabular form (source: tools.html)

### Validation Tools

- **JSON-stat Validator** - Validate JSON-stat 2.0 documents or queries (source: tools.html)
- **Official JSON Schemas** - JSON Schema 2020-12 definitions (general, dataset, collection, dimension) usable with any compliant validator; vendored in this repo's `raw/schema/` (see [[schema]])
- **jsonstat-validator** - Semantic validator (polyglot TypeScript + Rust/Wasm) that adds the cross-field cube invariants the schemas cannot express, with a stable error-code vocabulary (see [[validator]])

### Specialized Tools

- **Eurostat's Swiss Army Knife** - Browse, filter, convert, and download Eurostat datasets (source: tools.html)
- **JSON-stat Web Data Connector for Tableau** - Import datasets into Tableau (source: tools.html)
- **Power BI custom connector** - Import datasets into Power BI (source: tools.html)
- **Free Power Query (M) generator** - Generate Power Query scripts for PowerBI/Excel from PXWeb API (source: tools.html)

## Related pages

- [[jsonstat]]
- [[api-reference]]
- [[programming-libraries]]
- [[schema]]
- [[sample-files]]
