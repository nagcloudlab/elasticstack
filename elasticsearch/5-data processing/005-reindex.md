

GET _cat/indices





POST _reindex
{
  "source": {
    "index": "kibana_sample_data_flights"
  },
  "dest": {
    "index": "flights_reindexed"
  }
}


DELETE flights_reindexed


POST _reindex
{
  "source": {
    "index": "kibana_sample_data_flights"
  },
  "dest": {
    "index": "flights_reindexed"
  }
}


POST _reindex
{
  "source": {
    "index": "kibana_sample_data_flights",
    "query": {
      "term": {
        "Carrier": {
          "value": "Kibana Airlines"
        }
      }
    }
  },
  "dest": {
    "index": "kibana_airlines"
  }
}

GET kibana_airlines/_search




POST _reindex
{
  "source": {
    "remote": {
      "host": "htt://:9200",
      "username": "",
      "password": ""
    },
    "index": "",
    "query": {
      "term": {
        "Carrier": {
          "value": "Logstash Airlines"
        }
      }
    }
  },
  "dest": {
    "index": "logstash_airlines"
  }
}


