



GET kibana_sample_data_flights/_search
{
  "query": {
    "term": {
      "DestCountry": {
        "value": "US"
      }
    }
  }
}


GET kibana_sample_data_flights/_search
{
  "query": {
    "terms": {
      "Carrier": [
        "Kibana Airlines",
        "Logstash Airways"
      ]
    }
  }
}


GET kibana_sample_data_flights/_search
{
  "query": {
    "range": {
      "AvgTicketPrice": {
        "gte": 200,
        "lte": 300
      }
    }
  }
}

GET kibana_sample_data_flights/_search
{
  "query": {
    "range": {
      "timestamp": {
        "gte": "now/d",
        "lte": "now"
      }
    }
  }
}