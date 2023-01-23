


GET earthquakes/_search

PUT _ingest/pipeline/earthquakes_refactor
{
  "description": "",
  "processors": [
    {
      "remove": {
        "field": ["Latitude","Longitude"]
      }
    },
    {
      "set": {
        "field": "timestamp",
        "value": "{{_source.Date}} {{_source.Time}}"
      }
    },
    {
      "date": {
        "field": "timestamp",
        "formats": ["MM/dd/yyyy HH:mm:ss"]
      }
    },
    {
      "remove": {
        "field": ["Date","Time","timestamp"]
      }
    }
  ]
}

POST _reindex
{
  "source": {
    "index": "earthquakes"
  },
  "dest": {
    "index": "earthquakes_refactored",
    "pipeline": "earthquakes_refactor"
  }
}


GET earthquakes_refactored/_search