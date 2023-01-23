PUT _ilm/policy/logs-policy
{
  "policy": {
    "phases": {
      "hot": {
        "actions": {
          "rollover": {
            "max_age": "30d",
            "max_size": "50gb"
          }
        }
      },
      "warm": {
        "min_age": "1d",
        "actions": {}
      },
      "delete": {
        "min_age": "10d",
        "actions": {}
      }
    }
  }
}

PUT /_index_template/logs-datastream
{
  "priority": 200,
  "index_patterns": [ "logs-datastream*" ],
  "data_stream": { },
  "template": {
    "settings": {
      "index.lifecycle.name": "logs-policy"
    }
  }
}

PUT /_data_stream/logs-datastream-web-server
GET _data_stream/logs-datastream-web-server