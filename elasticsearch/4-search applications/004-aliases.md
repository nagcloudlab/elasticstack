


POST _aliases
{
  "actions": [
    {
      "add": {
        "index": "kibana_sample_data_ecommerce",
        "alias": "ecommerce1"
      }
    }
  ]
}


PUT _component_template/courses
{
  "template": {
    "aliases": {
      "courses": {}
    }
  }
}

PUT _index_template/elastic_stack
{
  "index_patterns": ["es-*"],
  "composed_of": ["courses"],
  "template": {
    "aliases": {
      "elastic_stack": {},
      "elasticsack_101":{
        "filter": {
          "term": {
            "course_name.keyword": "Elasticsearch 101"
          }
        }
      }
    }
  }
}

POST es-elasticsearch_101/_doc
{
  "course_name":"Elasticsearch 101"
}  


POST es-elasticsearch_101/_doc
{
  "course_name":"Elasticsearch 102"
}  


GET courses/_search
GET elastic_stack/_search
GET elasticsack_101/_search






