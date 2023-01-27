

GET _cat/nodes



PUT _index_template/user-template
{
  "index_patterns": ["user-*"],
  "template": {
    "settings": {
      "number_of_shards": 1,
      "number_of_replicas": 1
    },
    "mappings": {
      "dynamic":"false",
      "properties": {
        "name":{
          "type":"keyword"
        }
      }
    },
    "aliases": {
      "all_users": {}
    }
  }
}

PUT user-000001
{
  "aliases": {
    "user_writable_alias": {
      "is_write_index": true
    }
  }
}


# When is re-index required 

# intial index
GET user-000001/_settings


# try to increase primary shards
PUT user-000001/_settings
{
  "index.number_of_shards":2
}



# reindexing approach

PUT user-000002
{
  "settings": {
    "index.number_of_shards":2,
    "index.number_of_replicas":1
  }
}


POST _reindex
{
  "source": {
    "index": "user-000001"
  },
  "dest": {
    "index":"user-000002"
  }
}



POST _aliases
{
  "actions": [
    {
      "remove": {
        "index": "user-000001",
        "alias": "user_writable_alias"
      }
    },
    {
      "add": {
        "index": "user-000002",
        "alias": "user_writable_alias",
        "is_write_index":true
      }
    }
  ]
}

DELETE user-000001

GET user-000002/_settings


// #rollover
POST user_writable_alias/_rollover


