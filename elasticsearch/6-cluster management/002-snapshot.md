


PUT _snapshot/cluster
{
  "type": "fs",
  "settings": {
    "location": "/home/nag/es-backups"
  }
}

PUT _snapshot/cluster/backup_1
{
  "indices": "*",
  "include_global_state": true
}

GET _snapshot/cluster/backup_1

PUT 

PUT _slm/policy/daily_snapshot
{
  "schedule": "0 0 1 * * ?",
  "name": "<daily_snapshot_{now/d}>",
  "repository": "cluster",
  "config": {
    "indices": "*",
    "include_global_state": true
  },
  "retention": {
    "expire_after": "30d",
    "min_count": 7,
    "max_count": 30
  }
}