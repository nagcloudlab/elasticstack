

GET earthquakes/_search
{
  "size": 0,
  "aggs": {
    "per_month": {
      "date_histogram": {
        "field": "Date",
        "calendar_interval": "month"
      }
    }
  }
}


GET earthquakes/_search
{
  "size": 0,
  "aggs": {
    "types": {
      "terms": {
        "field": "Type",
        "size": 10
      }
    }
  }
}

