The connector JSON response schema is defined using the json-schema.org syntax as follows:
```javascript
{
  "$schema": "http://json-schema.org/schema#",
  "title": "Roswell Hero Card response schema",

  "type": "object",
  "properties": {
    "cards": {"type": "array", "items": {"$ref": "#/definitions/CARD"}},
    "connector_statuses": {"type": "array"}
  },
  "additionalProperties": false,


  "definitions": {
    "CARD": {
      "type": "object",
      "properties":     {
        "id":           {"type": "string", "pattern": "^[0-9a-fA-F]{8}-([0-9a-fA-F]{4}-){3}[0-9a-fA-F]{12}$"},
        "connector_id": {"type": "string"},
        "name":         {"type": "string"},
        "creation_date": {"type": "string", "format": "date-time"},
        "expiration_date" :{"type": "string", "format": "date-time"},
        "template":     {"$ref": "#/definitions/LINK"},
        "header":       {"$ref": "#/definitions/CARD_HEADER"},
        "body":         {"$ref": "#/definitions/CARD_BODY"},
        "actions":      {"type": "array", "items": {"$ref": "#/definitions/CARD_ACTION"}}
      },
      "additionalProperties": false
    },

    "LINK": {
      "type": "object",
      "properties": {
        "href": {"type": "string"}
      },
      "required": ["href"],
      "additionalProperties": false
    },

    "CARD_HEADER": {
      "type": "object",
      "properties": {
        "title":    {"type": "string"},
        "subtitle": {"type": "string"}
      },
      "additionalProperties": false
    },

    "CARD_BODY": {
      "type": "object",
      "properties": {
        "description": {"type": "string"},
        "fields":      {"type": "array", "items": {"$ref": "#/definitions/CARD_BODY_FIELD"}}
      },
      "additionalProperties": false
    },

    "CARD_BODY_FIELD": {
      "type": "object",
      "properties": {
        "type":        {"type": "string"},
        "title":       {"type": "string"},
        "description": {"type": "string"},
        "content":     {"type": "array", "items": {"type": "object"}}
      },
      "additionalProperties": false
    },

    "CARD_ACTION": {
      "type": "object",
      "properties": {
        "id":         {"type": "string", "pattern": "^[0-9a-fA-F]{8}-([0-9a-fA-F]{4}-){3}[0-9a-fA-F]{12}$"},
        "action_key": {"type": "string"},
        "label":      {"type": "string"},
        "url":        {"$ref": "#/definitions/LINK"},
        "type":       {"$ref": "#/definitions/HTTP_METHODS"},
        "user_input": {"type": "array", "items": {"$ref": "#/definitions/CARD_ACTION_USER_INPUT"}},
        "request":    {"type": "object"}
      },
      "additionalProperties": false
    },

    "CARD_ACTION_USER_INPUT": {
      "type": "object",
      "properties": {
        "id":         {"type": "string"},
        "label":      {"type": "string"},
        "format":     {"type": "string"},
        "options":    {"type": "object"},
        "min_length": {"type": "integer", "minimum": 0},
        "max_length": {"type": "integer", "minimum": 0}
      },
      "required": ["id", "label"],
      "additionalProperties": false
    },

    "HTTP_METHODS": {
      "type": "string",
      "enum": ["DELETE", "GET", "HEAD", "OPTIONS", "PATCH", "POST", "PUT", "TRACE"]
    }

  }
}
```