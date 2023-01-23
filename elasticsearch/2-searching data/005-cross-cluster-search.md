



// # remote cluster IP 172.31.47.49
PUT _cluster/settings
{
  "persistent": {
    "cluster": {
      "remote":{
        "cluster2":{
          "seeds":["172.31.47.49:9300"]
        }
      }
    }
  }
}

GET cluster_2:filebeat-7.13.4/_search
{
  "query": {
    "range": {
      "@timestamp": {
        "gte": "now-1h",
        "lte": "now"
      }
    }
  }
}


GET filebeat-7.13.4,cluster_2:filebeat-7.13.4/_search
{
  "query": {
    "range": {
      "@timestamp": {
        "gte": "now-1h",
        "lte": "now"
      }
    }
  }
}