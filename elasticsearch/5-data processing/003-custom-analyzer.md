




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