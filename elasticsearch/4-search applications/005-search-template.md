



PUT _scripts/ecommerce_template
{
  "script": {
    "lang": "mustache",
    "source": {
      "from": "{{from}}{{^from}}0{{/from}}",
      "size": "{{size}}{{^size}}15{{/size}}",
      "query": {
        "match": {
          "products.product_name": "{{product_name}}"
        }
      },
      "highlight": {
        "pre_tags": "<b>",
        "post_tags": "</b>",
        "fields": {
          "products.product_name": {}
        }
      },
      "sort": [
        {
          "customer_last_name.keyword": {
            "order": "asc"
          }
        },
        {
          "customer_first_name.keyword": {}
        },
        {
          "products.price": {
            "mode": "avg",
            "order": "asc"
          }
        },
        "_score"
      ]
    }
  }
}


POST _render/template
{
  "id":"ecommerce_template",
  "params": {
    "product_name":"boots"
  }
}



GET ecommerce/_search/template
{
  "id": "ecommerce_template",
  "params": {
    "from":0,
    "size":2,
    "product_name": "boots"
  }
}
