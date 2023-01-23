

GET _cat/indices




GET kibana_sample_data_ecommerce/_search

GET kibana_sample_data_ecommerce/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "range": {
            "taxful_total_price": {
              "lte": 20
            }
          }
        }
      ]
    }
  }
}

GET kibana_sample_data_ecommerce/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "range": {
            "taxful_total_price": {
              "lte": 20
            }
          }
        }
      ],
      "should": [
        {
          "term": {
            "category.keyword": {
              "value": "Men's Shoes"
            }
          }
        },
        {
          "term": {
            "category.keyword": {
              "value": "Men's Clothing"
            }
          }
        }
      ],
      "minimum_should_match": 1,
      "must_not": [
        {
          "match": {
            "products.product_name": "sweatshirt"
          }
        }
      ],
      "filter": [
        {
          "range": {
            "order_date": {
              "gte": "now/d",
              "lte": "now"
            }
          }
        }
      ]
    }
  }
}