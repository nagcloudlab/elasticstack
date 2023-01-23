


GET _cat/indices?v




GET earthquakes/_search
{
  "size": 0,
  "aggs": {
    "per_month": {
      "date_histogram": {
        "field": "Date",
        "calendar_interval": "month"
      },
      "aggs": {
        "avg_magnitude": {
          "avg": {
            "field": "Magnitude"
          }
        }
      }
    }
  }
}

GET earthquakes/_search
{
  "size": 0,
  "aggs": {
    "per_year": {
      "date_histogram": {
        "field": "Date",
        "calendar_interval": "year"
      },
      "aggs": {
        "types": {
          "terms": {
            "field": "Type",
            "size": 10
          },
          "aggs": {
            "max_magnitude": {
              "max": {
                "field": "Magnitude"
              }
            }
          }
        }
      }
    }
  }
}
