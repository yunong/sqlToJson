sqlToJson
=========

Convert PostgreSQL dumps to [streaming
JSON](https://dev.twitter.com/docs/streaming-apis/processing).

# Installation
```bash
npm install sqlToJson
```

# Usage
```bash
# dump a postgres db, strip out escaped slashes, pipe to sqlToJson.js
# note postgres will escape every '\' with an additional '\' resulting in '\\'
# for each '\'. Hence an original row value of '\\' will get converted to
# '\\\\'. We therefore have to transform '\\\\' back to '\\'
sudo -u postgres pg_dump foo_db -a -t bar_table | sed 's/\\\\/\\/g' | sqlToJson.js
```
This results in streaming JSON where the first line is always the JSON version
of the table schema. Any additional lines are rows in the table where each
field maps to the columns specified in the first row.  Notably though, type
information is not persisted and all fields are emitted as strings.

```
{"name": "column1", "column2", "column3", "column4"}
{"entry":["column1_value", 'column2_value", "column3_value", "column4_value"]}
{"entry":["column1_value", 'column2_value", "column3_value", "column4_value"]}
{"entry":["column1_value", 'column2_value", "column3_value", "column4_value"]}
{"entry":["column1_value", 'column2_value", "column3_value", "column4_value"]}
...
```

# Contributions

Contributions welcome. Please ensure `npm test` runs cleanly.

# License

The MIT License (MIT)

Copyright (c) 2014 Yunong J Xiao

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.

