# JSON-Schema-cheat-sheet
JSON Schema Cheat Sheet with the most needed stuff..

<br><br>

Example:
```javascript
{
  "price": {
    "type": "number",
    "description": "Price of the good",
    "example": 0.98
  }
}
```

<br><br>

# For what we use JSON Schema?
- Validate JSON Documents.

<br><br>

# How does JSON Schema work?
- You import the JSON Documents & JSON Schema into a Schema Parser which will validate the JSON Document based on the JSON Schema.














<br><br>
__________________________________
__________________________________
<br><br>

# Schema Validator

## Online
- https://jsonschemalint.com/#!/version/draft-07/markup/json



























<br><br>
__________________________________
__________________________________
<br><br>

# Types (https://json-schema.org/understanding-json-schema/reference/type.html)

<br>

- Example:
```javascript
{"type": "object"}
```
<br><br>

## Basic Types:
- string
- number
- object
- array
- boolean
- null

<br><br>


## Multiple Types
```javascript
{ "type": ["number", "string"] }
```


































<br><br>





















<br><br>
__________________________________
__________________________________
<br><br>

# Properties (http://json-schema.org/understanding-json-schema/reference/object.html#properties)
- The properties (key-value pairs) on an object are defined using the properties keyword. The value of properties is an object, where each key is the name of a property and each value is a JSON schema used to validate that property.

<br>

- Example:
```javascript
{
  "type": "object",
  "properties": {
    "number":      { "type": "number" },
    "street_name": { "type": "string" },
    "street_type": { "type": "string",
                     "enum": ["Street", "Avenue", "Boulevard"]
                   }
  }
}
```



















































<br><br>
__________________________________
__________________________________
<br><br>

# Enumerated values (https://json-schema.org/understanding-json-schema/reference/generic.html#id4)
- The enum keyword is used to restrict a value to a fixed set of values. It must be an array with at least one element, where each element is unique.

<br><br>

The following is an example for validating street light colors:
```javascript
{
  "type": "string",
  "enum": ["red", "amber", "green"]
}
```





