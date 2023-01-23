

GET earthquakes


PUT _component_template/product_review_mappings
{
  "template": {
    "mappings": {
      "properties": {
        "product_id":{
          "type": "long"
        },
        "reviews":{
          "properties": {
            "first_name":{
              "type":"keyword"
            },
            "last_name":{
              "type":"keyword"
            },
            "review":{
              "type":"text",
              "analyzer":"english"
            }
          }
        }
      }
    }
  }
}

GET _component_template/product_review_mappings