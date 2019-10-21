## Request
Card actions are invoked on a connector by POSTing form data to one of its action endpoints.

The expectation for Action requests is an HTTP POST with a payload of content-type `application/x-www-form-urlencoded`. The actual payload can be of whatever the user chooses, and the client frameworks for iOS and Android offer convenience methods to encode any Dictionary/Map into an appropriately encoded payload to send to the server.

An example encoded POST body with three keys (`first_name`, `last_name`, and `contact_email`) would look like:

```
first_name=John&last_name=Smith&contact_email=JSmith@airwdemo.com
```

## Response
Generally the client expects only an HTTP status code to indicate success in a card action. We anticipate adding a status message or an object of any type that could be displayed to the user in a future version of this specification.

## Example
For example, in our [Weather sample](https://github.com/vmware-samples/card-connectors-guide/tree/master/samples/node), the action to update the current temperature is invoked thus:

```
curl -i -X POST \
   -H "Authorization:Bearer eyJ0eXAiO" \
   -H "X-Connector-Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=" \
   -H "Content-Type:application/x-www-form-urlencoded" \
   -d "zip=30360" \
   -d "temperature=90" \
 'http://localhost:3000/reports'
```

```
HTTP/1.1 200 OK
X-Powered-By: Express
Date: Wed, 18 Jul 2018 11:49:29 GMT
Connection: keep-alive
Content-Length: 0
```