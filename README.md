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
```javascript
{"type": "string"}
```

<br>

- number
```javascript
{"type": "number"}
```

<br>

- object
```javascript
{"type": "object"}
```

<br>

- array
```javascript
{"type": "array"}
```
<br>

- boolean
```javascript
{"type": "boolean"}

/* valid */
true
false


/* invalid */
"true"

// Values that evaluate to true or false are still not accepted by the schema:
0
```

<br>

- null
```javascript
{"type": "null"}

/* valid */
null

/* invalid */
false
0
""
```







<br><br>


## Multiple Types
```javascript
{ "type": ["number", "string"] }
```








































<br><br>
__________________________________
__________________________________
<br><br>




# string (https://json-schema.org/understanding-json-schema/reference/string.html#string)
- In Python, "string" is analogous to the unicode type on Python 2.x, and the str type on Python 3.x.

<br>

- Example:
```javascript
{ "type": "string" }
```

<br><br>


## Length (https://json-schema.org/understanding-json-schema/reference/string.html#id5)

<br>

- Example:
```javascript
{
  "type": "string",
  "minLength": 2,
  "maxLength": 3
}

// valid
"AB"
"ABC"

// invalid
"A"
"ABCD"
```




<br><br>


## Regular Expressions (https://json-schema.org/understanding-json-schema/reference/string.html#id6)
- The pattern keyword is used to restrict a string to a particular regular expression. The regular expression syntax is the one defined in JavaScript (ECMA 262 specifically). See Regular Expressions for more information.

<br>

- Example:
```javascript
{
   "type": "string",
   "pattern": "^(\\([0-9]{3}\\))?[0-9]{3}-[0-9]{4}$"
}

// valid
"555-1212"
"(888)555-1212"

// invalid
"(888)555-1212 ext. 532"
"(800)FLOWERS"
```









<br><br>


## Format (https://json-schema.org/understanding-json-schema/reference/string.html#id7)
- The format keyword allows for basic semantic validation on certain kinds of string values that are commonly used. This allows values to be constrained beyond what the other tools in JSON Schema, including Regular Expressions can do.


<br><br>

#### Dates and times (https://json-schema.org/understanding-json-schema/reference/string.html#id9)
- Dates and times are represented in RFC 3339, section 5.6. This is a subset of the date format also commonly known as ISO8601 format.
```javascript
/*
"date-time": Date and time together, for example, 2018-11-13T20:20:39+00:00.
"time": New in draft 7 Time, for example, 20:20:39+00:00
"date": New in draft 7 Date, for example, 2018-11-13.
*/
```


<br><br>

#### Email addresses (https://json-schema.org/understanding-json-schema/reference/string.html#id10)
```javascript
/*
"email": Internet email address, see RFC 5322, section 3.4.1.
"idn-email": New in draft 7 The internationalized form of an Internet email address, see RFC 6531.
*/
```



<br><br>

#### Hostnames (https://json-schema.org/understanding-json-schema/reference/string.html#id11)
```javascript
/*
"hostname": Internet host name, see RFC 1034, section 3.1.
"idn-hostname": New in draft 7 An internationalized Internet host name, see RFC5890, section 2.3.2.3.
*/
```




<br><br>

#### IP Addresses (https://json-schema.org/understanding-json-schema/reference/string.html#id12)
```javascript
/*
"ipv4": IPv4 address, according to dotted-quad ABNF syntax as defined in RFC 2673, section 3.2.
"ipv6": IPv6 address, as defined in RFC 2373, section 2.2.
*/
```




<br><br>

#### Resource identifiers (https://json-schema.org/understanding-json-schema/reference/string.html#id13)
```javascript
/*
"uri": A universal resource identifier (URI), according to RFC3986.
"uri-reference": New in draft 6 A URI Reference (either a URI or a relative-reference), according to RFC3986, section 4.1.
"iri": New in draft 7 The internationalized equivalent of a “uri”, according to RFC3987.
"iri-reference": New in draft 7 The internationalized equivalent of a “uri-reference”, according to RFC3987
If the values in the schema have the ability to be relative to a particular source path (such as a link from a webpage), it is generally better practice to use "uri-reference" (or "iri-reference") rather than "uri" (or "iri"). "uri" should only be used when the path must be absolute.
*/
```






<br><br>

#### URI template (https://json-schema.org/understanding-json-schema/reference/string.html#id14)
```javascript
/*
"uri-template": New in draft 6 A URI Template (of any level) according to RFC6570. If you don’t already know what a URI Template is, you probably don’t need this value.
*/
```







<br><br>

#### JSON Pointer (https://json-schema.org/understanding-json-schema/reference/string.html#id15)
```javascript
/*
"json-pointer": New in draft 6 A JSON Pointer, according to RFC6901. There is more discussion on the use of JSON Pointer within JSON Schema in Structuring a complex schema. Note that this should be used only when the entire string contains only JSON Pointer content, e.g. /foo/bar. JSON Pointer URI fragments, e.g. #/foo/bar/ should use "uri-reference".
"relative-json-pointer": New in draft 7 A relative JSON pointer.
*/
```






<br><br>

#### Regular Expressions (https://json-schema.org/understanding-json-schema/reference/string.html#id16)
```javascript
/*
"regex": New in draft 7 A regular expression, which should be valid according to the ECMA 262 dialect.
Be careful, in practice, JSON schema validators are only required to accept the safe subset of Regular Expressions described elsewhere in this document.
*/
```





























































































<br><br>
__________________________________
__________________________________
<br><br>




# Numeric types (https://json-schema.org/understanding-json-schema/reference/numeric.html#numeric-types)
- There are two numeric types in JSON Schema: integer and number. They share the same validation keywords.
- JSON has no standard way to represent complex numbers, so there is no way to test for them in JSON Schema.



<br><br>


## integer (https://json-schema.org/understanding-json-schema/reference/numeric.html#id4)
- The integer type is used for integral numbers.

<br>

- Example:
```javascript
{ "type": "integer" }


/* valid */
42
-1



/* invalid */

// Floating point numbers are rejected:
3.1415926

// Numbers as strings are rejected:
"42"
```





<br><br>


## number (https://json-schema.org/understanding-json-schema/reference/numeric.html#id5)
- The number type is used for any numeric type, either integers or floating point numbers.

<br>

- Example:
```javascript
{ "type": "number" }


/* valid */
42
-1

//Simple floating point number:
5.0

// Exponential notation also works:
2.99792458e8




/* invalid */

// Numbers as strings are rejected:
"42"
```







<br><br>


## Multiples (https://json-schema.org/understanding-json-schema/reference/numeric.html#id6)
- Numbers can be restricted to a multiple of a given number, using the multipleOf keyword. It may be set to any positive number.

<br>

- Example:
```javascript
{
    "type"       : "number",
    "multipleOf" : 10
}

/* valid */
0
10
20


/* invalid */

// Not a multiple of 10:
23
```











<br><br>


## Range (https://json-schema.org/understanding-json-schema/reference/numeric.html#id7)
- Ranges of numbers are specified using a combination of the minimum and maximum keywords, (or exclusiveMinimum and exclusiveMaximum for expressing exclusive range).
- If x is the value being validated, the following must hold true:
<br> x ≥ minimum
<br> x > exclusiveMinimum
<br> x ≤ maximum
<br> x < exclusiveMaximum

<br><br>

- Example:
```javascript
/* ---- EXAMPLE #1 ---- */
{
  "type": "number",
  "minimum": 0,
  "exclusiveMaximum": 100
}


/* valid */

// minimum is inclusive, so 0 is valid:
0
10
99



/* invalid */

// Less than minimum:
-1

// exclusiveMaximum is exclusive, so 100 is not valid:
100

// Greater than maximum:
101














/* ---- EXAMPLE #2 ---- */
{
  "type": "number",
  "minimum": 0,
  "maximum": 100,
  "exclusiveMaximum": true
}


/* valid */

//exclusiveMinimum was not specified, so 0 is included:
0
10
99


/* invalid */

// Less than minimum:
-1

// exclusiveMaximum is true, so 100 is not included:
100

// Greater than maximum:
101


```








































































































<br><br>
__________________________________
__________________________________
<br><br>




# Array (https://json-schema.org/understanding-json-schema/reference/array.html#array)
- Arrays are used for ordered elements. In JSON, each element in an array may be of a different type.

<br>

- Example:
```javascript
{ "type": "array" }

/* valid */
[1, 2, 3, 4, 5]
[3, "different", { "types" : "of values" }]

/* invalid */
{"Not": "an array"}
```







<br><br>





# Items (https://json-schema.org/understanding-json-schema/reference/array.html#id4)
- By default, the elements of the array may be anything at all. However, it’s often useful to validate the items of the array against some schema as well. This is done using the items, additionalItems, and contains keywords. There are two ways in which arrays are generally used in JSON:
<br> List validation: a sequence of arbitrary length where each item matches the same schema.
<br> Tuple validation: a sequence of fixed length where each item may have a different schema. In this usage, the index (or location) of each item is meaningful as to how the value is interpreted. (This usage is often given a whole separate type in some programming languages, such as Python’s tuple).

<br><br>





## List validation (https://json-schema.org/understanding-json-schema/reference/array.html#id5)
- List validation is useful for arrays of arbitrary length where each item matches the same schema. For this kind of array, set the items keyword to a single schema that will be used to validate all of the items in the array.

<br>

- Example:
```javascript
{
  "type": "array",
  "items": {
    "type": "number"
  }
}

// valid
[1, 2, 3, 4, 5]
[]

// invalid
[1, 2, "3", 4, 5]








/* contains */
{
   "type": "array",
   "contains": {
     "type": "number"
   }
}

// valid
["life", "universe", "everything", 42]
[1, 2, 3, 4, 5]

// invalid
["life", "universe", "everything", "forty-two"]
```










## Tuple validation (https://json-schema.org/understanding-json-schema/reference/array.html#id6)
- Tuple validation is useful when the array is a collection of items where each has a different schema and the ordinal index of each item is meaningful. For example, you may represent a street address such as:
<br> **1600 Pennsylvania Avenue NW**

<br><br>

Each of these fields will have a different schema:
<br> number: The address number. Must be a number.
<br> street_name: The name of the street. Must be a string.
<br> street_type: The type of street. Should be a string from a fixed set of values.
<br> direction: The city quadrant of the address. Should be a string from a different set of values.

<br><br>


- Example:
```javascript
{
  "type": "array",
  "items": [
    {
      "type": "number"
    },
    {
      "type": "string"
    },
    {
      "type": "string",
      "enum": ["Street", "Avenue", "Boulevard"]
    },
    {
      "type": "string",
      "enum": ["NW", "NE", "SW", "SE"]
    }
  ]
}



/* valid */
[1600, "Pennsylvania", "Avenue", "NW"]

// It’s okay to not provide all of the items:
[10, "Downing", "Street"]

// And, by default, it’s also okay to add additional items to end:
[1600, "Pennsylvania", "Avenue", "NW", "Washington"]





/* invalid */

// “Drive” is not one of the acceptable street types:
[24, "Sussex", "Drive"]

// This address is missing a street number
["Palais de l'Élysée"]




















/* ---- additionalItems ---- */
{
  "type": "array",
  "items": [
    {
      "type": "number"
    },
    {
      "type": "string"
    },
    {
      "type": "string",
      "enum": ["Street", "Avenue", "Boulevard"]
    },
    {
      "type": "string",
      "enum": ["NW", "NE", "SW", "SE"]
    }
  ],
  "additionalItems": false
}


/* valid */
[1600, "Pennsylvania", "Avenue", "NW"]

// It’s ok to not provide all of the items:
[1600, "Pennsylvania", "Avenue"]



/* invalid */
// But, since additionalItems is false, we can’t provide extra items:
[1600, "Pennsylvania", "Avenue", "NW", "Washington"]
```























<br><br>




## Length (https://json-schema.org/understanding-json-schema/reference/array.html#id7)
- The length of the array can be specified using the minItems and maxItems keywords. The value of each keyword must be a non-negative number. These keywords work whether doing List validation or Tuple validation.

<br>

- Example:
```javascript
{
  "type": "array",
  "minItems": 2,
  "maxItems": 3
}

// valid
[1, 2]
[1, 2, 3]

// invalid
[]
[1]
[1, 2, 3, 4]
```











<br><br>




## Uniqueness (https://json-schema.org/understanding-json-schema/reference/array.html#id8)
- A schema can ensure that each of the items in an array is unique. Simply set the uniqueItems keyword to true.

<br>

- Example:
```javascript
{
  "type": "array",
  "uniqueItems": true
}

// valid
[1, 2, 3, 4, 5]
[]

// invalid
[]
[1]
[1, 2, 3, 4]
```





















































<br><br>
__________________________________
__________________________________
<br><br>




# Object (https://json-schema.org/understanding-json-schema/reference/object.html#object)
- Objects are the mapping type in JSON. They map “keys” to “values”. In JSON, the “keys” must always be strings. Each of these pairs is conventionally referred to as a “property”.

<br>

- Example:
```javascript
{ "type": "object" }


/* valid */
{
   "key"         : "value",
   "another_key" : "another_value"
}

{
    "Sun"     : 1.9891e30,
    "Jupiter" : 1.8986e27,
    "Saturn"  : 5.6846e26,
    "Neptune" : 10.243e25,
    "Uranus"  : 8.6810e25,
    "Earth"   : 5.9736e24,
    "Venus"   : 4.8685e24,
    "Mars"    : 6.4185e23,
    "Mercury" : 3.3022e23,
    "Moon"    : 7.349e22,
    "Pluto"   : 1.25e22
}



/* invalid */

// Using non-strings as keys is invalid JSON:
{
    0.01 : "cm"
    1    : "m",
    1000 : "km"
}

"Not an object"

["An", "array", "not", "an", "object"]
```




<br><br>


## Properties (http://json-schema.org/understanding-json-schema/reference/object.html#properties)
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

#### additionalProperties
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

 
#### Required Properties (http://json-schema.org/understanding-json-schema/reference/object.html#id3)
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


#### Property names (http://json-schema.org/understanding-json-schema/reference/object.html#id4)
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


#### Size (http://json-schema.org/understanding-json-schema/reference/object.html#id5)
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


#### Dependencies (http://json-schema.org/understanding-json-schema/reference/object.html#id6)
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

































































<br><br>
__________________________________
__________________________________
<br><br>

# Generic keywords (https://json-schema.org/understanding-json-schema/reference/generic.html)
- This chapter lists some miscellaneous properties that are available for all JSON types.


<br><br>


## Annotations (https://json-schema.org/understanding-json-schema/reference/generic.html#id2)
- JSON Schema includes a few keywords, title, description, default, examples that aren’t strictly used for validation, but are used to describe parts of a schema.

<br><br>

None of these “annotation” keywords are required, but they are encouraged for good practice, and can make your schema “self-documenting”.

<br><br>

The title and description keywords must be strings. A “title” will preferably be short, whereas a “description” will provide a more lengthy explanation about the purpose of the data described by the schema.

<br><br>

The default keyword specifies a default value for an item. JSON processing tools may use this information to provide a default value for a missing key/value pair, though many JSON schema validators simply ignore the default keyword. It should validate against the schema in which it resides, but that isn’t required.

<br><br>

The examples keyword is a place to provide an array of examples that validate against the schema. This isn’t used for validation, but may help with explaining the effect and purpose of the schema to a reader. Each entry should validate against the schema in which is resides, but that isn’t strictly required. There is no need to duplicate the default value in the examples array, since default will be treated as another example.:
```javascript
{
  "title" : "Match anything",
  "description" : "This is a schema that matches anything.",
  "default" : "Default value",
  "examples" : [
    "Anything",
    4035
  ]
}
```







<br><br>


## Comments (https://json-schema.org/understanding-json-schema/reference/generic.html#comments)
- The $comment keyword is strictly intended for adding comments to the JSON schema source. Its value must always be a string. Unlike the annotations title, description and examples, JSON schema implementations aren’t allowed to attach any meaning or behavior to it whatsoever, and may even strip them at any time. Therefore, they are useful for leaving notes to future editors of a JSON schema, (which is quite likely your future self), but should not be used to communicate to users of the schema.



