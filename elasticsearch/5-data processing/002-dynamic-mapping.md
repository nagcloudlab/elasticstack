

PUT _component_template/integers_as_floats
{
  "template": {
    "mappings": {
      "dynamic_templates": [
        {
          "integers_as_floats": {
            "match_mapping_type": "long",
            "mapping": {
              "type": "double"
            }
          }
        }
      ]
    }
  }
}