

GET _cat/indices




GET kibana_sample_data_ecommerce/_search

POST kibana_sample_data_ecommerce/_async_search?wait_for_completion_timeout=0
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


GET _async_search/status/FjBnNW9HaTNiVFItbUY4cmRFRFNrQ2cdemttVnk4UThRRHlSRjVGbTNJYWxFQToxNTY3NTE


GET _async_search/FjBnNW9HaTNiVFItbUY4cmRFRFNrQ2cdemttVnk4UThRRHlSRjVGbTNJYWxFQToxNTY3NTE

DELETE _async_search/FjBnNW9HaTNiVFItbUY4cmRFRFNrQ2cdemttVnk4UThRRHlSRjVGbTNJYWxFQToxNTY3NTE

