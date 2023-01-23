

GET kibana_sample_data_ecommerce/_search



PUT _security/role/products_read
{
  "cluster": [],
  "indices": [
    {
      "names": ["kibana_sample_data_ecommerce"],
      "privileges": ["read"],
      "field_security": {
        "grant":["products.*"]
      },
      "query": {
        "term": {
          "geoip.continent_name": {
            "value": "North America"
          }
        }
      }
    }
  ]
}

POST _security/user/nag
{
  "full_name": "Nag N",
  "email":"nag@mail.com",
  "password": "p@$$w0rd",
  "roles": ["products_read","kibana_user"]
}