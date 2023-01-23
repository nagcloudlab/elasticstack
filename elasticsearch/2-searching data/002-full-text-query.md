

GET _cat/indices




GET shakespeare/_search
{
  "query": {
    "match": {
      "text_entry": "King"
    }
  }
}


GET shakespeare/_search
{
  "query": {
    "match": {
      "text_entry": "wherefore art thou romeo"
    }
  }
}

GET shakespeare/_search
{
  "query": {
    "match_phrase": {
      "text_entry": "wherefore art thou romeo"
    }
  }
}


