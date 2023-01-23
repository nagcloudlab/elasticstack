

POST _snapshot/cluster/backup_1/_restore
{
  "indices": "earthquakes",
  "rename_pattern": "(.+)",
  "rename_replacement": "$1_restored"
}
