
GET kibana_sample_data_ecommerce/_search
{
  "from": 0, 
  "size": 20, 
  "query": {
    "match": {
      "products.product_name": "sweatshirt"
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