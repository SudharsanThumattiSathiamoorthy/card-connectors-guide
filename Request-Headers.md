Connectors should expect the following headers with all requests from Mobile Flows. In some cases proxies may modify headers, but this is what will be issued from Mobile Flows.

Header | Description 
------------ | -------------
Authorization | The access token sent by Mobile Flows. Example value: `Bearer eyJ0eXAiOiJK`. The connector should use this header to authenticate incoming requests. It is a JWT token and should be verified using the public key at https://prod.hero.vmwservices.com/security/public-key.
Accept | The content type Mobile Flows expects to see for valid responses. In all cases this will be `application/json`.
Content-Type | The content type for requests from Mobile Flows. For card requests this will be `application/json`. For action requests this will be `application/x-www-form-urlencoded`.
Accept-Language | The requested language for the card. Connectors that don't support internationalization can ignore this header.
X-Routing-Prefix | The connector must prefix action URLs with the value of this header if action calls are to be routed via Mobile Flows. Sent only with card requests.
X-Connector-Base-Url | Connectors that support multiple backends can use this header to route traffic accordingly. Example: `X-Weather-Base-Url: https://222.wikiweather.org/weather`.
X-Connector-Authorization | The authorization header expected by the backend. Typically the connector will copy this value into the `Authorization` header before making a backend request.