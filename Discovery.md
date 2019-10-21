A connector is registered with Mobile Flows Server by adding a discovery URL. This URL might point to the connector itself, or it might point to static web content (for example, Amazon S3).

Discovery tells Mobile Flows Server where to submit object requests, etc.

The content behind the discovery is JSON and its `Content-Type` should be set to `application/json`. The JSON schema for the discovery can be found [here](https://vmware-samples.github.io/card-connectors-guide/#schema/connector-discovery-schema.json)

Discovery resources MUST be available to unauthenticated clients.

Here is an example:
```
{ 
   "image":{ 
      "href":"https://weather-connector.acme.com/images/connector.png"
   },
   "test_auth":{ 
      "href":"https://weather-connector.acme.com/test-auth"
   },
   "actions":{ 
      "clear":{ 
         "url":{ 
            "href":"https://weather-connector.acme.com/clear"
         },
         "user_input":[ 

         ],
         "label":{ 
            "en-US":"Clear Reported Data",
            "es-ES":"..."
         },
         "type":"POST",
         "action_key":"DIRECT"
      },
      "report_rain_status":{ 
         "url":{ 
            "href":"https://weather-connector.acme.com/report"
         },
         "user_input":[ 
            { 
               "id":"rain_status",
               "label":{ 
                  "en-US":"Is it raining now ?",
                  "es-ES":"..."
               },
               "format":"select",
               "select":[ 
                  { 
                     "value":"High",
                     "label":{ 
                        "en-US":"Yes, raining heavily.",
                        "es-ES":"..."
                     }
                  },
                  { 
                     "value":"Medium",
                     "label":{ 
                        "en-US":"Yes, it is.",
                        "es-ES":"..."
                     }
                  },
                  { 
                     "value":"No",
                     "label":{ 
                        "en-US":"No, its not raining.",
                        "es-ES":"..."
                     }
                  }
               ]
            }
         ],
         "fields":{ 
            "user_zip":{ 
               "env":"USER_ZIP_CODE"
            }
         },
         "label":{ 
            "en-US":"Report rain information.",
            "es-ES":"..."
         },
         "type":"POST",
         "action_key":"USER_INPUT"
      }
   },
   "config":{ 
      "foo":{ 
         "default":"bar",
         "type":"STRING",
         "label":{ 
            "en-US":"Foo",
            "es-ES":"Foo"
         },
         "description":{ 
            "en-US":"This ...",
            "es-ES":"Este ..."
         },
         "validators":[ 
            { 
               "type":"required",
               "description":{ 
                  "en-US":"Foo is required",
                  "es-ES":"..."
               }
            },
            { 
               "type":"regex",
               "value":"^\\w+$",
               "description":{ 
                  "en-US":"Foo must be only letters and numbers",
                  "es-ES":"..."
               }
            },
            { 
               "type":"max_length",
               "value":"10",
               "description":{ 
                  "en-US":"Foo must not be more than 10 characters",
                  "es-ES":"..."
               }
            }
         ]
      }
   },
   "object_types":{ 
      "card":{ 
         "doc":{ 
            "href":"https://vmware-samples.github.io/card-connectors-guide/#schema/herocard-response-schema.json"
         },
         "fields":{ 
            "zip":{ 
               "capture_group":1,
               "regex":"([0-9]{5})(?:[- ][0-9]{4})?"
            }
         },
         "pollable":false,
         "endpoint":{ 
            "href":"https://weather-connector.acme.com/cards/requests"
         }
      }
   }
}
```   
The `image` link tells Mobile Flows Server where to find an image to be displayed by clients.  The image should be a PNG.

The `test_auth` link offers an endpoint for testing the backend authorization. This is useful where BASIC authentication is used, and the authorization value is derived from (possibly mistyped) user input. The endpoint will be accessed with a GET request with the same headers as would be used with an object request.

The `actions` object (map/dictionary) describes any global actions (a.k.a connector level actions) offered by this connector These actions are not related to individual objects defined in `object_types`. Each action can ask user inputs (`user_input`) as well as some input `fields`.
Action key (`action_key`) gives a hint to the client about how to perform the action. A value called "USER_INPUT" indicates there are some input parameters to be collected from the user, in order to perform the action. In the example `rain_status` is a user input of format called "select".
For this input format, connector should also provide select options. 

The `config` object describes the config properties to prompt an admin for when configuring a connector in Mobile Flows.  The values that the admin configures will be sent in to your deployed connector in the object requests from Mobile Flows.  This allows a connector to be customized by an admin without requiring deploying custom connector code.

The `object_types` describes the object types supported by this connector.

Each object type has a name, some fields, an endpoint and optionally defines if it is pollable. Additionally it could contain a doc link and a metadata property. The name identifies the object type, while the optional doc link should point to a schema so that consumers of these objects know how to parse them. The endpoint is a URL to which Mobile Flows Server will post object requests.

A pollable object type can be registered for polling with Mobile Flows.  Pollable object types should not require tokens.

The `fields` object is telling what to pass for the `tokens` in an object request. In the example above, "card" object is requesting `zip`, which will be extracted from some text using the supplied regular expression.
The action `report_rain_status` requests a field input `user_zip`, which client app would be providing from its environment variables. As long as the target client app understands it, connector can describe and expect any environmental variables. 

To request client device OS name, connector could describe as below:
```
"fields": {
  "device_system_name": {"env": "DEVICE_SYSTEM_NAME"} 
}
```
Here, the connector is requesting a token, `device_system_name`, which is taken from the the `DEVICE_SYSTEM_NAME` environment variable.
The full list of available environment variables (Known to the VMware email app) is below:

| Variable | Description|
-----------|------------------------|
| USER_EMAIL | The user's email address|
| ENROLLMENT_IDENTIFIER | MDM unique enrollment identifier |
| ENROLLMENT_USERNAME | MDM enrollment username |
| ENROLLMENT_GROUP_IDENTIFIER | MDM enrollment group |
| ENROLLMENT_DEVICE_UDID | MDM enrollment device unique identifier |
| DEVICE_IDENTIFIER | Operating system device unique identifier |
| DEVICE_MODEL | Operating system device model |
| DEVICE_NAME | Operating system device name |
| DEVICE_SYSTEM_NAME | Operating system system name (‘iOS’) |
| DEVICE_SYSTEM_VERSION | Operating system version (‘10.0’) |
| DEVICE_UI_IDIOM | Operating system device idiom (‘tablet’)|