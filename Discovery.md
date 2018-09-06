A connector is registered with Mobile Flows Server by adding a discovery URL. This URL might point to the connector itself, or it might point to static web content (for example, Amazon S3).

Discovery tells Mobile Flows Server where to submit object requests, etc.

The content behind the discovery is JSON and its `Content-Type` should be set to `application/json`.

Discovery resources MUST be available to unauthenticated clients.

Here is an example:
```
{
  "image": {
    "href": "https://weather-connector.acme.com/images/connector.png"
  },
  "test_auth": {
    "href": "https://weather-connector.acme.com/test-auth"
  },
  "actions": [
    {
      "url": {
        "href": "https://weather-connector.acme.com/clear"
      },
      "user_input": [],
      "request": {},
      "label": "Clear Reported Data",
      "type": "POST",
      "action_key": "DIRECT"
    }
  ],
  "object_types": {
    "card": {
      "doc": {
        "href": "https://vmwaresamples.github.io/card-connectors-guide/#schema/herocard-response-schema.json"
      },
      "fields": {
        "zip": {
          "capture_group": 1,
          "regex": "([0-9]{5})(?:[- ][0-9]{4})?"
        }
      },
      "endpoint": {
        "href": "https://weather-connector.acme.com/cards/requests"
      }
    }
  }
}
```   
The `image` link tells Mobile Flows Server where to find an image to be displayed by clients.  The image should be a PNG.

The `test_auth` link offers an endpoint for testing the backend authorization. This is useful where BASIC authentication is used, and the authorization value is derived from (possibly mistyped) user input. The endpoint will be accessed with a GET request with the same headers as would be used with an object request.

The `actions` array describes any global actions offered by this connector (actions that are not related to individual objects defined in `object_types`).  The [JSON schema](http://json-schema.org/) for a connector-level action can be found [here](https://vmwaresamples.github.io/card-connectors-guide/#schema/connector-level-actions-schema.json).

The `object_types` array describes the object types supported by this connector.

Each object type has a name, some fields, an endpoint, and an optional doc link. The name identifies the object type, while the optional doc link should point to a schema so that consumers of these objects know how to parse them. The endpoint is a URL to which Mobile Flows Server will post object requests.

The `fields` object is telling Mobile Flows Server what to pass for the `tokens` in an object request. In our example, the connector is requesting `zip`, which will be extracted from some text using the supplied regular expression.

Fields can also be used to request the value of environment variables. For example:
```
"fields": {
  "user_email": {"env": "USER_EMAIL"} 
}
```
Here, the connector is requesting a token, `user_email`, which is taken from the the `USER_EMAIL` environment variable.
The full list of available environment variables is below:

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