

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

GET _async_search/status/FjBnNW9HaTNiVFItbUY4cmRFRFNrQ2cdemttVnk4UThRRHlSRjVGbTNJYWxFQToxNTY3NTE


GET _async_search/FjBnNW9HaTNiVFItbUY4cmRFRFNrQ2cdemttVnk4UThRRHlSRjVGbTNJYWxFQToxNTY3NTE

DELETE _async_search/FjBnNW9HaTNiVFItbUY4cmRFRFNrQ2cdemttVnk4UThRRHlSRjVGbTNJYWxFQToxNTY3NTE

