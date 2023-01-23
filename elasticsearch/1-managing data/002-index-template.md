## Index Template

PUT _index_template/logs
{
  "index_patterns": ["logs-*"],
  "template": {
    "settings": {
      "number_of_shards": 1,
      "number_of_replicas": 1
    }
  }
}


GET _index_template/logs

PUT logs-0001
GET logs-0001


## Component Template
PUT _component_template/shards
{
  "template": {
    "settings": {
      "number_of_shards": 1,
      "number_of_replicas": 2
    }
  }
}

GET _component_template/shards

PUT _index_template/weblogs
{
  "index_patterns": ["weblogs-*"],
  "composed_of": ["shards"]
}

GET _index_template/weblogs

PUT weblogs-0001
GET weblogs-0001

