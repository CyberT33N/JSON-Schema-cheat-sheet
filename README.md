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
- Transformation (as example XML to JSON)

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

## additionalProperties
- The additionalProperties keyword is used to control the handling of extra stuff, that is, properties whose names are not listed in the properties keyword. By default any additional properties are allowed. The additionalProperties keyword may be either a boolean or an object. If additionalProperties is a boolean and set to false, no additional properties will be allowed.

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
  },
  "additionalProperties": false
}
```

<br><br>

#### allow additional Properties of specific type
- For example, one can allow additional properties, but only if they are each a string:
```javascript
{
  "type": "object",
  "properties": {
    "number":      { "type": "number" },
    "street_name": { "type": "string" },
    "street_type": { "type": "string",
                     "enum": ["Street", "Avenue", "Boulevard"]
                   }
  },
  "additionalProperties": { "type": "string" }
}
```



<br><br>

 
## Required Properties (http://json-schema.org/understanding-json-schema/reference/object.html#id3)
- By default, the properties defined by the properties keyword are not required. However, one can provide a list of required properties using the required keyword. The required keyword takes an array of zero or more strings. Each of these strings must be unique.

<br>

- In the following example schema defining a user record, we require that each user has a name and e-mail address, but we don’t mind if they don’t provide their address or telephone number:

```javascript
{
  "type": "object",
  "properties": {
    "name":      { "type": "string" },
    "email":     { "type": "string" },
    "address":   { "type": "string" },
    "telephone": { "type": "string" }
  },
  "required": ["name", "email"]
}

// valid
{
  "name": "William Shakespeare",
  "email": "bill@stratford-upon-avon.co.uk"
}

// invalid
{
  "name": "William Shakespeare",
  "address": "Henley Street, Stratford-upon-Avon, Warwickshire, England",
}
```












































<br><br>


## Property names (http://json-schema.org/understanding-json-schema/reference/object.html#id4)
- The names of properties can be validated against a schema, irrespective of their values. This can be useful if you don’t want to enforce specific properties, but you want to make sure that the names of those properties follow a specific convention. You might, for example, want to enforce that all names are valid ASCII tokens so they can be used as attributes in a particular programming language.
```javascript
{
  "type": "object",
  "propertyNames": {
    "pattern": "^[A-Za-z_][A-Za-z0-9_]*$"
  }
}

// valid
{
  "_a_proper_token_001": "value"
}

// invalid 
{
  "001 invalid": "value"
}
```
























<br><br>


## Size (http://json-schema.org/understanding-json-schema/reference/object.html#id5)
- The number of properties on an object can be restricted using the minProperties and maxProperties keywords. Each of these must be a non-negative integer.
```javascript
{
  "type": "object",
  "minProperties": 2,
  "maxProperties": 3
}

// invalid
{}
{ "a": 0 }
{ "a": 0, "b": 1, "c": 2, "d": 3 }

// valid
{ "a": 0, "b": 1 }
{ "a": 0, "b": 1, "c": 2 }
```











































<br><br>


## Dependencies (http://json-schema.org/understanding-json-schema/reference/object.html#id6)
- The dependencies keyword allows the schema of the object to change based on the presence of certain special properties. There are two forms of dependencies in JSON Schema:
<br> Property dependencies declare that certain other properties must be present if a given property is present.
<br> Schema dependencies declare that the schema changes when a given property is present.



<br><br>


#### Property dependencies (http://json-schema.org/understanding-json-schema/reference/object.html#id7)
- Let’s start with the simpler case of property dependencies. For example, suppose we have a schema representing a customer. If you have their credit card number, you also want to ensure you have a billing address. If you don’t have their credit card number, a billing address would not be required. We represent this dependency of one property on another using the dependencies keyword. The value of the dependencies keyword is an object. Each entry in the object maps from the name of a property, p, to an array of strings listing properties that are required whenever p is present.
<br><br>
In the following example, whenever a credit_card property is provided, a billing_address property must also be present:
```javascript
{
  "type": "object",

  "properties": {
    "name": { "type": "string" },
    "credit_card": { "type": "number" },
    "billing_address": { "type": "string" }
  },

  "required": ["name"],

  "dependencies": {
    "credit_card": ["billing_address"]
  }
}


// valid
{
  "name": "John Doe",
  "credit_card": 5555555555555555,
  "billing_address": "555 Debtor's Lane"
}

// This is okay, since we have neither a credit_card, or a billing_address.
{
  "name": "John Doe"
}

// Note that dependencies are not bidirectional. It’s okay to have a billing address without a credit card number.
{
  "name": "John Doe",
  "billing_address": "555 Debtor's Lane"
}

// To fix the last issue above (that dependencies are not bidirectional), you can, of course, define the bidirectional dependencies explicitly:
{
  "type": "object",

  "properties": {
    "name": { "type": "string" },
    "credit_card": { "type": "number" },
    "billing_address": { "type": "string" }
  },

  "required": ["name"],

  "dependencies": {
    "credit_card": ["billing_address"],
    "billing_address": ["credit_card"]
  }
}




// invalid
{
  "name": "John Doe",
  "credit_card": 5555555555555555
}
```











<br><br>


#### Schema dependencies (http://json-schema.org/understanding-json-schema/reference/object.html#id8)
- Schema dependencies work like property dependencies, but instead of just specifying other required properties, they can extend the schema to have other constraints. For example, here is another way to write the above:
```javascript
{
  "type": "object",

  "properties": {
    "name": { "type": "string" },
    "credit_card": { "type": "number" }
  },

  "required": ["name"],

  "dependencies": {
    "credit_card": {
      "properties": {
        "billing_address": { "type": "string" }
      },
      "required": ["billing_address"]
    }
  }
}


// valid 
{
  "name": "John Doe",
  "credit_card": 5555555555555555,
  "billing_address": "555 Debtor's Lane"
}

// This has a billing_address, but is missing a credit_card. This passes, because here billing_address just looks like an additional property:
{
  "name": "John Doe",
  "billing_address": "555 Debtor's Lane"
}




// invalid
// This instance has a credit_card, but it’s missing a billing_address:
{
  "name": "John Doe",
  "credit_card": 5555555555555555
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





