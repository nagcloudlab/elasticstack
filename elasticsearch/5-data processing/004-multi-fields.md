


PUT _component_template/strings
{
  "template": {
    "mappings": {
      "dynamic_template": [
        {
          "strings": {
            "match_mapping_type": "string",
            "mapping": {
              "type": "text",
              "analyzer": "standard",
              "fields": {
                "keyword": {
                  "type": "keyword"
                }
              }
            }
          }
        }
      ]
    }
  }
}