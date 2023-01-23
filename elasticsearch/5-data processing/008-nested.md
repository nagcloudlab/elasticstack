



PUT _component_template/product_review_mappings
{
  "template": {
    "mappings": {
      "properties": {
        "product_id":{
          "type": "long"
        },
        "reviews":{
          "type": "nested", 
          "properties": {
            "first_name":{
              "type":"keyword"
            },
            "last_name":{
              "type":"keyword"
            },
            "review":{
              "type":"text",
              "analyzer":"user_reviews"
            }
          }
        }
      }
    },
    "settings": {
      "analysis": {
        "analyzer": {
          "user_reviews":{
            "type":"custom",
            "tokenizer":"classic",
            "char_filter":["social_acronyms"],
            "filters":["lowercase","english_stop"]
          }
        },
        "char_filter": {
          "social_acronyms":{
            "type":"mapping",
            "mappings":[
              "imo => in my opinion",
              "b2b => business to business",
              "roi => retun on investment"
            ]
          }
        },
        "filter": {
          "english_stop":{
            "type":"stop",
            "stopwords":["_english_"],
            "ignore_case":true
          }
        }
      }
    }
  }
}



GET _component_template/product_review_mappings

PUT _index_template/product_reviews
{
  "index_patterns": ["outdoors","kitchen","furniture"],
  "composed_of": ["integers_as_floats","product_review_mappings"],
  "template": {
    "settings": {
      "number_of_replicas": 1,
      "number_of_shards": 1
    }
  }
}

POST furniture/_doc
{
  "product_id":1,
  "product_name":"Walnut Coffee Table",
  "reviews":[
    {
      "first_name":"Myles",
      "last_name":"Young",
      "rating":5,
      "review":"Great min-century-modern coffee table, Well built, roim Should last a few generations."
    },
     {
      "first_name":"Matthew",
      "last_name":"Pearson",
      "rating":4,
      "review":"b2b custome here, Shipping took longer than expected."
    }
  ]
  
}


GET furniture/_search
{
  "query": {
    "nested": {
      "path": "reviews",
      "query": {
        "bool": {
          "must": [
            {
              "term": {
                "reviews.first_name": {
                  "value": "Myles"
                }
              }
            },
            {
              "term": {
                "reviews.last_name": {
                  "value": "Young"
                }
              }
            }
          ]
        }
      }
    }
  }
}



GET furniture/_search
{
  "query": {
    "nested": {
      "path": "reviews",
      "query": {
        "match": {
          "reviews.review": "business"
        }
      }
    }
  }
}










