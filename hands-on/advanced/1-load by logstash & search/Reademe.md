
Load data

> head web.log
> cat web-logs-template.json
> ./load.sh

> /usr/share/bin/logstash -f web-logs-logstash.conf < web.log

> GET web-logs/_count
> GET web-logs/_search



Running queries on your data

1. Find all the HTTP events with an HTTP response code of 200.

GET web-logs/_search
{
 "query": {
    "term": {
      "http.response.status_code": { "value": "200" }
    }
  }
}


2. Find all HTTP events where the request method was of the POST type and resulted in a non-200 response code.


GET web-logs/_search
{
  "query": {
    "bool": {
      "must_not": [
        { "term": {
            "http.response.status_code": { "value": "200" }
          }
        
      ], 
      "must": [
        { "term": {
            "http.request.method": { "value": "POST" }
          }
        }
      ]
    }
  }
}

3. Find all HTTP events referencing the terms refrigerator and windows anywhere in the document.

GET web-logs/_search
{
  "query": {
    "match": {
      "event.original":{
        "query": "refrigerator windows",
        "operator": "and"
      }
    }
  }
}

4. Look for all requests where users on Windows machines were looking at refrigerator-related pages on the website.

GET web-logs/_search
{
  "query": {
    "bool": {
      "must": [
        { "match": { "url.original.text": "refrigerator" }},
        { "match": { "user_agent.os.full.text": "windows" }}
      ]
    }
  }
}

5. Look for all events originating from either South Africa, Ireland, or Hong Kong.

GET web-logs/_search
{
  "query": {
    "terms": {
      "source.geo.country_name": [
        "South Africa",
        "Ireland",
        "Hong Kong"
      ]
    }
  }
}

6. Find all the events originating from IP addresses belonging to the Pars Online PJS and Respina Networks & Beyond PJSC telecommunication providers.


PUT telcos-list
{
  "mappings": {
    "properties": { "name": { "type": "keyword" }}
  }
}

PUT telcos-list/_doc/1
{
  "name":   ["Pars Online PJS", "Respina Networks & Beyond PJSC"]
}

GET web-logs/_search
{
  "query": {
    "terms": {
        "source.as.organization.name": {
            "index" : "telcos-list",
            "id" : "1",
            "path" : "name"
        }
    }
  }
}

7. Find all HTTP GET events with response bodies of more than 100,000 bytes.

GET web-logs/_search
{
  "query": {
    "bool": {
      "must": [
        { "term": { "http.request.method": { "value": "GET" }}},
        { "range": { "http.response.body.bytes": { "gte": 100000 }}}
      ]
    }
  }
}