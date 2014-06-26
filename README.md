sqlToJson
=========

Convert PostgreSQL dumps to streaming JSON.

# Installation
```bash
npm install sqlToJson
```

# Usage
```bash
# dump a postgres db, strip out escaped slashes, pipe to sqlToJson.js
sudo -u postgres pg_dump foo_db -a -t bar_table | sed 's/\\\\/\\/g' | sqlToJson.js
```
This results in streaming JSON where the first line is always the JSON version
of the table schema. Any additional lines are rows in the table where each
field maps to the columns specified in the first row.  Notably though, type
information is not persisted and all fields are emitted as strings.

```json
{"name": "column1", "column2", "column3", "column4"}
{"entry":["column1_value", 'column2_value", "column3_value", "column4_value"]}
{"entry":["column1_value", 'column2_value", "column3_value", "column4_value"]}
{"entry":["column1_value", 'column2_value", "column3_value", "column4_value"]}
{"entry":["column1_value", 'column2_value", "column3_value", "column4_value"]}
...
```


