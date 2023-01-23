


PUT diagnostic
GET diagnostic

GET _cat/shards/diagnostic?v
GET _cluster/allocation/explain
{
  "index":"diagnostic",
  "shard":0,
  "primary":false
}

PUT diagnostic/_settings
{
  "number_of_replicas": 0
}