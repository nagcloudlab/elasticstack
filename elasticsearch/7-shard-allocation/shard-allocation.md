

./bin/elasticsearch -Enode.attr.size=medium -Enode.attr.disk=ssd


Shard allocation filtering

PUT twitter/_settings
{
  "index.routing.allocation.require.size": "medium",
  "index.routing.allocation.require.disk": "ssd"
}


./bin/elasticsearch -Enode.attr.rack_id=rack_one


on Master Node
------------------------------------------

Shard allocation awareness

cluster.routing.allocation.awareness.attributes: rack_id

Force awareness

cluster.routing.allocation.awareness.attributes: rack_id
cluster.routing.allocation.awareness.force.rack_id.values: rack_one,rack_two


-------------------------------------------------------------

for any data,

  data
  data_content


for time-serias data (i.e data-serias),

  data
  data_hot
  data_warm
  data_cold
  data_frozen
  



