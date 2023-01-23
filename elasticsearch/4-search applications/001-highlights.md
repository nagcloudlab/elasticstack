
GET kibana_sample_data_ecommerce/_search
{
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
  }
}