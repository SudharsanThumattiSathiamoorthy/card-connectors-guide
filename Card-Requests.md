A card request consists of one or more tokens. These tokens might be pulled from the text of an email, or they might be from the client's environment &mdash; for example, the user's email address.

The [JSON schema](http://json-schema.org/) for a card request can be found [here](https://vmware-samples.github.io/card-connectors-guide/#schema/herocard-request-schema.json).

Here is an example request:

```javascript
{
  "config": {
    "foo": "bar"
  },
  "tokens": {
    "zip": [
      "30080",
      "30067",
      "30332",
      "00100"
    ]
  },
  "connector_id": "238ff136-1f49-4c88-8acd-aa4c3749a75c"
}
``` 