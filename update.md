## Update many documents transforming array<string> from capitalized to lowercase / uppercase

```
POST /<yourIndex>/_update_by_query
{

  "query": {
    "bool": {
      "must": [
        {
          "exists": {
            "field": "tags"
          } 
        }
      ]
    }
  },
  "script": {
    "source": "ctx._source.tags = ctx._source.tags.stream().map(String::toLowerCase).toArray(String[]::new)",
    "lang": "painless"
  }
}
# other script example
# ctx._source.tags = ctx._source.tags.stream().map(t -> t.toLowerCase()).collect(Collectors.toList())
```
replace <your_field_name> and use `toLowerCase` or `toUpperCase`

`ctx._source`.<your_field_name> = `ctx._source`.<your_field_name>.stream().map(String::`toLowerCase`).toArray(String[]::new)

if you dont want filter your data before update, remove `query`.