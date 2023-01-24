

GET shakespeare/_search

PUT _ingest/pipeline/shakespeare_words
{
  "description": "Creates the words array and word-count fields",
  "processors": [
    {
      "split": {
        "field": "text_entry",
        "separator": "\\s+",
        "target_field":"words"
      }
    },
    {
      "script": {
        "lang": "painless",
        "source": "ctx.word_count=ctx.words.length"
      }
    }
  ]
}

POST shakespeare/_update_by_query?pipeline=shakespeare_words