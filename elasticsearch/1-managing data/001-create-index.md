GET _license
GET _cat/health?v
GET _cat/nodes?v
GET _cat/indices?v

HEAD myindex
PUT myindex
GET myindex
DELETE myindex



PUT /myindex
{
    "settings": {
        "index": {
            "number_of_shards": 1,
            "number_of_replicas": 1
        }
    }
}


//https://www.elastic.co/guide/en/elasticsearch/reference/current/index-modules.html#index-modules-settings