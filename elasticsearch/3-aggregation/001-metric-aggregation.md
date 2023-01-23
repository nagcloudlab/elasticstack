




GET _cat/indices?v


GET earthquakes/_search?size=0
{
  //"size": 0, 
  "aggs": {
    "avg_magnitude": {
      "avg": {
        "field": "Magnitude"
      }
    }
  }
}


GET earthquakes/_search?size=0
{
  //"size": 0, 
  "aggs": {
    "max_magnitude": {
      "max": {
        "field": "Magnitude"
      }
    }
  }
}


GET earthquakes/_search?size=0
{
  //"size": 0, 
  "aggs": {
    "stats": {
      "stats": {
        "field": "Magnitude"
      }
    }
  }
}



GET earthquakes/_search
{
  "size": 0,
  "aggs": {
    "types": {
      "cardinality": {
        "field": "Type"
      }
    }
  }
}