


GET earthquakes/_search

POST earthquakes/_update/nUYW2IUBAfLo03StriQV
{
  "doc": {
    "Type":"Natural"
  }
}

GET earthquakes/_doc/nUYW2IUBAfLo03StriQV


POST earthquakes/_update_by_query
{
  "script": {
    "source": "ctx._source.Type = 'Natural'",
    "lang": "painless"
  },
  "query": {
    "term": {
      "Type": {
        "value": "Earthquake"
      }
    }
  }
}f