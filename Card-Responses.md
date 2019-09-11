The [JSON schema](http://json-schema.org/) for a card response can be found [here](https://vmware-samples.github.io/card-connectors-guide/#schema/herocard-response-schema.json).

Here is an example response:

```javascript
{
  "objects": [
    {
      "body": {
        "fields": [
          {
            "type": "GENERAL",
            "title": "Temperature",
            "description": "75"
          },
          {
            "type": "GENERAL",
            "title": "Conditions",
            "description": "Sunny"
          }
        ],
        "description": "The weather is rather nice at the moment"
      },
      "id": "583ff582-0c09-40ab-b8ae-d366a7b95958",
      "hash": "faa939f5556317bd3cff7e92e6ee4eb6cb3af737",
      "backend_id": "98593717fc9133253e588783c7b3ca94d9afa617",
      "header": {
        "title": "Weather forecast for 30332",
        "links": {
          "title": "http://<link-to-weather-forecast-webapp-page-for-30332>"
        }
      },
      "actions": [
        {
          "url": {
            "href": "https://hero.vmwservices.com/connectors/<weather-connector-id>/card/reports"
          },
          "id": "75befd7f-99f0-4980-90a6-8daf6270770f",
          "user_input": [
            {
              "id": "temperature",
              "label": "Please enter temperature for 30332"
            }
          ],
          "request": {
            "zip": "30332"
          },
          "label": "Report weather",
          "type": "POST",
          "completed_label": "Weather reported successfully",
          "action_key": "USER_INPUT"
        }
      ]
    },
    {
      "body": {
        "fields": [
          {
            "type": "GENERAL",
            "title": "Temperature",
            "description": "75"
          },
          {
            "type": "GENERAL",
            "title": "Conditions",
            "description": "Sunny"
          }
        ],
        "description": "The weather is rather nice at the moment"
      },
      "id": "f299ea76-1f71-4ec0-af12-8caced30aff5",
      "hash": "8798a78bd7b150837ef108a12c73466465ce01b7",
      "backend_id": "240817bf03355899a52a616f51b452d9f181d56c",
      "header": {
        "title": "Weather forecast for 30067",
        "links": {
          "title": "http://<link-to-weather-forecast-webapp-page-for-30067>"
        }
      },
      "actions": [
        {
          "url": {
            "href": "https://hero.vmwservices.com/connectors/<weather-connector-id>/card/reports"
          },
          "id": "6d8caf05-e93d-4521-b603-c5a4dffc5176",
          "user_input": [
            {
              "id": "temperature",
              "label": "Please enter temperature for 30067"
            }
          ],
          "request": {
            "zip": "30067"
          },
          "label": "Report weather",
          "type": "POST",
          "completed_label": "Weather reported successfully",
          "action_key": "USER_INPUT"
        }
      ]
    },
    {
      "body": {
        "fields": [
          {
            "type": "GENERAL",
            "title": "Temperature",
            "description": "75"
          },
          {
            "type": "GENERAL",
            "title": "Conditions",
            "description": "Sunny"
          }
        ],
        "description": "The weather is rather nice at the moment"
      },
      "id": "c046c0ab-3dc7-4c5a-905e-8b3cdde4d9a1",
      "hash": "360748ccb74419fe459db0963c6441853d88a957",
      "backend_id": "ebdc977aea6d3ec02c7c6a176073580bf836875b",
      "header": {
        "title": "Weather forecast for 00100",
        "links": {
          "title": "http://<link-to-weather-forecast-webapp-page-for-00100>"
        }
      },
      "actions": [
        {
          "url": {
            "href": "https://hero.vmwservices.com/connectors/<weather-connector-id>/card/reports"
          },
          "id": "5ede58dc-c479-46e0-a70e-03b772fb78fd",
          "user_input": [
            {
              "id": "temperature",
              "label": "Please enter temperature for 00100"
            }
          ],
          "request": {
            "zip": "00100"
          },
          "label": "Report weather",
          "type": "POST",
          "completed_label": "Weather reported successfully",
          "action_key": "USER_INPUT"
        }
      ]
    },
    {
      "body": {
        "fields": [
          {
            "type": "GENERAL",
            "title": "Temperature",
            "description": "75"
          },
          {
            "type": "GENERAL",
            "title": "Conditions",
            "description": "Sunny"
          }
        ],
        "description": "The weather is rather nice at the moment"
      },
      "id": "2a9531c4-3cf3-4494-af30-21c9a99cd636",
      "hash": "9af7b47ffdf4288d992f4a384dd166c8e3585ac3",
      "backend_id": "63ada17e679e155906da48b90166544b38c0e89e",
      "header": {
        "title": "Weather forecast for 30080",
        "links": {
          "title": "http://<link-to-weather-forecast-webapp-page-for-30080>"
        }
      },
      "actions": [
        {
          "url": {
            "href": "https://hero.vmwservices.com/connectors/<weather-connector-id>/card/reports"
          },
          "id": "2274b789-7179-44e9-8c11-941cfa58c9b0",
          "user_input": [
            {
              "id": "temperature",
              "label": "Please enter temperature for 30080"
            }
          ],
          "request": {
            "zip": "30080"
          },
          "label": "Report weather",
          "type": "POST",
          "completed_label": "Weather reported successfully",
          "action_key": "USER_INPUT"
        }
      ]
    }
  ]
}
``` 