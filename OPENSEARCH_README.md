# Set a policy to delete data after 3 days in Opensearch

PUT _plugins/_ism/policies/delete_after_3_days
{
  "policy": {
    "policy_id": "delete_after_3_days",
    "description": "Deletes indexes older than 3 days",
    "schema_version": 1,
    "default_state": "hot",
    "states": [
      {
        "name": "hot",
        "actions": [],
        "transitions": [
          {
            "state_name": "delete",
            "conditions": {
              "min_index_age": "3d"
            }
          }
        ]
      },
      {
        "name": "delete",
        "actions": [
          {
            "delete": {}
          }
        ],
        "transitions": []
      }
    ],
    "ism_template": [
      {
        "index_patterns": [
          "logstash*"
        ],
        "priority": 100
      }
    ]
  }
}