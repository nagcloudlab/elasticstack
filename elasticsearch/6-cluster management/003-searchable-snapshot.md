


POST _license/start_trial?acknowledge=true

DELETE earthquakes

POST _snapshot/cluster/backup_1/_mount
{
  "index":"earthquake",
  "renamed_index":"earthquakes_searchable_snapshot"
}


PUT _ilm/policy/my_policy
{
  "policy": {
    "phases": {
      "cold": {
       "actions": {
         "searchable_snapshot":{
           "snapshot_repository":"my-repository"
         }
       }
      }
    }
  }
}
