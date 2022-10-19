# JSON-Schema-cheat-sheet
JSON Schema Cheat Sheet with the most needed stuff..

<br><br>

# DOCS
- https://json-schema.org/understanding-json-schema/index.html


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




### Numeric types (https://json-schema.org/understanding-json-schema/reference/numeric.html#numeric-types)
- There are two numeric types in JSON Schema: integer and number. They share the same validation keywords.
- JSON has no standard way to represent complex numbers, so there is no way to test for them in JSON Schema.



<br><br>


#### integer (https://json-schema.org/understanding-json-schema/reference/numeric.html#id4)
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


#### number (https://json-schema.org/understanding-json-schema/reference/numeric.html#id5)
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


#### Multiples (https://json-schema.org/understanding-json-schema/reference/numeric.html#id6)
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


#### Range (https://json-schema.org/understanding-json-schema/reference/numeric.html#id7)
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
[1, 2, 2, 3]
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









<br><br>




## Enumerated values (https://json-schema.org/understanding-json-schema/reference/generic.html#id4)
- The enum keyword is used to restrict a value to a fixed set of values. It must be an array with at least one element, where each element is unique.

<br><br>

The following is an example for validating street light colors:
```javascript
{
  "type": "string",
  "enum": ["red", "amber", "green"]
}

/* valid */
"red"

/* invalid */
"blue"










/* ---- EXAMPLE #2 ---- */

// You can use enum even without a type, to accept values of different types. Let’s extend the example to use null to indicate “off”, and also add 42, just for fun.
{
  "enum": ["red", "amber", "green", null, 42]
}

/* valid */
"red"
null
42

/* invalid */
0

















/* ---- EXAMPLE #3 ---- */

// However, in most cases, the elements in the enum array should also be valid against the enclosing schema:
{
  "type": "string",
  "enum": ["red", "amber", "green", null]
}

/* valid */
"red"

/* invalid */
null
```





































## Constant values (https://json-schema.org/understanding-json-schema/reference/generic.html#id5)
- The const keyword is used to restrict a value to a single value. For example, to if you only support shipping to the United States for export reasons:

```javascript
{
  "properties": {
    "country": {
      "const": "United States of America"
    }
  }
}

/* valid */
{ "country": "United States of America" }

/* invalid */
{ "country": "Canada" }
```

<br><br> 
  
It should be noted that const is merely syntactic sugar for an enum with a single element, therefore the following are equivalent:
```javascript
{ "const": "United States of America" }
{ "enum": [ "United States of America" ] }
```












































































































<br><br>
__________________________________
__________________________________
<br><br>

# Media: string-encoding non-JSON data (https://json-schema.org/understanding-json-schema/reference/non_json_data.html#media-string-encoding-non-json-data)
- JSON schema has a set of keywords to describe and optionally validate non-JSON data stored inside JSON strings. Since it would be difficult to write validators for many media types, JSON schema validators are not required to validate the contents of JSON strings based on these keywords. At the time of this writing, it appears that most of them do not. However, these keywords are still useful for an application that consumes validated JSON.


<br><br>

## contentMediaType (https://json-schema.org/understanding-json-schema/reference/non_json_data.html#id1)
- The contentMediaType keyword specifies the MIME type of the contents of a string, as described in RFC 2046. There is a list of MIME types officially registered by the IANA, but the set of types supported will be application and operating system dependent. Mozilla Developer Network also maintains a shorter list of MIME types that are important for the web

<br><br>

## contentEncoding (https://json-schema.org/understanding-json-schema/reference/non_json_data.html#id2)
- The contentEncoding keyword specifies the encoding used to store the contents, as specified in RFC 2054, part 6.1.

<br><br>

The acceptable values are 7bit, 8bit, binary, quoted-printable and base64. If not specified, the encoding is the same as the containing JSON document.

<br><br>

Without getting into the low-level details of each of these encodings, there are really only two options useful for modern usage:
If the content is encoded in the same encoding as the enclosing JSON document (which for practical purposes, is almost always UTF-8), leave contentEncoding unspecified, and include the content in a string as-is. This includes text-based content types, such as text/html or application/xml.

<br><br>

If the content is binary data, set contentEncoding to base64 and encode the contents using Base64. This would include many image types, such as image/png or audio types, such as audio/mpeg.


<br><br>

- Example
```javascript
{
  "type": "string",
  "contentMediaType": "text/html"
}

/* valid */
"<!DOCTYPE html><html xmlns=\"http://www.w3.org/1999/xhtml\"><head></head></html>"









/* ---- EXAMPLE #2 ---- */
{
  "type": "string",
  "contentEncoding": "base64",
  "contentMediaType": "image/png"
}

/* valid */
"iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAABmJLR0QA/wD/AP+gvaeTAAAA..."
```





























































































<br><br>
__________________________________
__________________________________
<br><br>

# Combining schemas (https://json-schema.org/understanding-json-schema/reference/combining.html#combining-schemas)
- JSON Schema includes a few keywords for combining schemas together. Note that this doesn’t necessarily mean combining schemas from multiple files or JSON trees, though these facilities help to enable that and are described in Structuring a complex schema. Combining schemas may be as simple as allowing a value to be validated against multiple criteria at the same time.

<br><br>

For example, in the following schema, the anyOf keyword is used to say that the given value may be valid against any of the given subschemas. The first subschema requires a string with maximum length 5. The second subschema requires a number with a minimum value of 0. As long as a value validates against either of these schemas, it is considered valid against the entire combined schema.
```javascript
{
  "anyOf": [
    { "type": "string", "maxLength": 5 },
    { "type": "number", "minimum": 0 }
  ]
}

/* valid */
"short"
12

/* invalid */
"too long"
-5
```


<br><br>

The keywords used to combine schemas are:
- allOf: Must be valid against all of the subschemas
- anyOf: Must be valid against any of the subschemas
- oneOf: Must be valid against exactly one of the subschemas











<br><br><br><br>

## allOf (https://json-schema.org/understanding-json-schema/reference/combining.html#id5)
- To validate against allOf, the given data must be valid against all of the given subschemas.
```javascript
{
  "allOf": [
    { "type": "string" },
    { "maxLength": 5 }
  ]
}

/* valid */
"short"

/* invalid */
"too long"






/* ---- EXAMPLE #2 ---- */
{
  "allOf": [
    { "type": "string" },
    { "type": "number" }
  ]
}

```




<br><br><br><br>

## allOf (https://json-schema.org/understanding-json-schema/reference/combining.html#id5)
- To validate against allOf, the given data must be valid against all of the given subschemas.
```javascript
{

/* invalid */
"No way"
-1











/* ---- EXAMPLE #3 ---- */
// It is important to note that the schemas listed in an allOf, anyOf or oneOf array know nothing of one another. While it might be surprising, allOf can not be used to “extend” a schema to add more details to it in the sense of object-oriented inheritance. For example, say you had a schema for an address in a definitions section, and want to extend it to include an address type:
{
  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street_address": { "type": "string" },
        "city":           { "type": "string" },
        "state":          { "type": "string" }
      },
      "required": ["street_address", "city", "state"]
    }
  },

  "allOf": [
    { "$ref": "#/definitions/address" },
    { "properties": {
        "type": { "enum": [ "residential", "business" ] }
      }
    }
  ]
}

/* valid */
{
   "street_address": "1600 Pennsylvania Avenue NW",
   "city": "Washington",
   "state": "DC",
   "type": "business"
}
































/* ---- EXAMPLE #4 ---- */
// This works, but what if we wanted to restrict the schema so no additional properties are allowed? One might try adding the highlighted line below:
{
  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street_address": { "type": "string" },
        "city":           { "type": "string" },
        "state":          { "type": "string" }
      },
      "required": ["street_address", "city", "state"]
    }
  },

  "allOf": [
    { "$ref": "#/definitions/address" },
    { "properties": {
        "type": { "enum": [ "residential", "business" ] }
      }
    }
  ],

  "additionalProperties": false
}

/* invalid */
{
   "street_address": "1600 Pennsylvania Avenue NW",
   "city": "Washington",
   "state": "DC",
   "type": "business"
}
```














<br><br>

## anyOf (https://json-schema.org/understanding-json-schema/reference/combining.html#anyof)
- To validate against anyOf, the given data must be valid against any (one or more) of the given subschemas.
```javascript
{
  "anyOf": [
    { "type": "string" },
    { "type": "number" }
  ]
}

/* valid */
"Yes"
42

/* invalid */
{ "Not a": "string or number" }
```



















<br><br>

## oneOf (https://json-schema.org/understanding-json-schema/reference/combining.html#oneof)
- To validate against oneOf, the given data must be valid against exactly one of the given subschemas.
```javascript
{
  "oneOf": [
    { "type": "number", "multipleOf": 5 },
    { "type": "number", "multipleOf": 3 }
  ]
}

/* valid */
10
9



/* invalid */

// Not a multiple of either 5 or 3.
2

// Multiple of both 5 and 3 is rejected.
15
```















<br><br>

## not (https://json-schema.org/understanding-json-schema/reference/combining.html#id8)
- This doesn’t strictly combine schemas, but it belongs in this chapter along with other things that help to modify the effect of schemas in some way. The not keyword declares that a instance validates if it doesn’t validate against the given subschema.
<br><br>
For example, the following schema validates against anything that is not a string:
```javascript
{ "not": { "type": "string" } }
/* valid */
10
9



/* invalid */

// Not a multiple of either 5 or 3.
42
{ "key": "value" }

// Multiple of both 5 and 3 is rejected.
"I am a string"
```























































































































<br><br>
__________________________________
__________________________________
<br><br>

# Applying subschemas conditionally (https://json-schema.org/understanding-json-schema/reference/conditionals.html#applying-subschemas-conditionally)
- The if, then and else keywords allow the application of a subschema based on the outcome of another schema, much like the if/then/else constructs you’ve probably seen in traditional programming languages. If if is valid, then must also be valid (and else is ignored.) If if is invalid, else must also be valid (and then is ignored).

<br><br>

- For example, let’s say you wanted to write a schema to handle addresses in the United States and Canada. These countries have different postal code formats, and we want to select which format to validate against based on the country. If the address is in the United States, the postal_code field is a “zipcode”: five numeric digits followed by an optional four digit suffix. If the address is in Canada, the postal_code field is a six digit alphanumeric string where letters and numbers alternate.
```javascript
{
  "type": "object",
  "properties": {
    "street_address": {
      "type": "string"
    },
    "country": {
      "enum": ["United States of America", "Canada"]
    }
  },
  "if": {
    "properties": { "country": { "const": "United States of America" } }
  },
  "then": {
    "properties": { "postal_code": { "pattern": "[0-9]{5}(-[0-9]{4})?" } }
  },
  "else": {
    "properties": { "postal_code": { "pattern": "[A-Z][0-9][A-Z] [0-9][A-Z][0-9]" } }
  }
}

/* valid */
{
  "street_address": "1600 Pennsylvania Avenue NW",
  "country": "United States of America",
  "postal_code": "20500"
}

{
  "street_address": "24 Sussex Drive",
  "country": "Canada",
  "postal_code": "K1M 1M4"
}

/* invalid */
{
  "street_address": "24 Sussex Drive",
  "country": "Canada",
  "postal_code": "10000"
}
```





<br><br>



- Unfortunately, this approach above doesn’t scale to more than two countries. You can, however, wrap pairs of if and then inside an allOf to create something that would scale. In this example, we’ll use United States and Canadian postal codes, but also add Netherlands postal codes, which are 4 digits followed by two letters. It’s left as an exercise to the reader to expand this to the remaining postal codes of the world.
```javascript
{
  "type": "object",
  "properties": {
    "street_address": {
      "type": "string"
    },
    "country": {
      "enum": ["United States of America", "Canada", "Netherlands"]
    }
  },
  "allOf": [
    {
      "if": {
        "properties": { "country": { "const": "United States of America" } }
      },
      "then": {
        "properties": { "postal_code": { "pattern": "[0-9]{5}(-[0-9]{4})?" } }
      }
    },
    {
      "if": {
        "properties": { "country": { "const": "Canada" } }
      },
      "then": {
        "properties": { "postal_code": { "pattern": "[A-Z][0-9][A-Z] [0-9][A-Z][0-9]" } }
      }
    },
    {
      "if": {
        "properties": { "country": { "const": "Netherlands" } }
      },
      "then": {
        "properties": { "postal_code": { "pattern": "[0-9]{4} [A-Z]{2}" } }
      }
    }
  ]
}

/* valid */
{
  "street_address": "1600 Pennsylvania Avenue NW",
  "country": "United States of America",
  "postal_code": "20500"
}

{
  "street_address": "24 Sussex Drive",
  "country": "Canada",
  "postal_code": "K1M 1M4"
}

{
  "street_address": "Adriaan Goekooplaan",
  "country": "Netherlands",
  "postal_code": "2517 JX"
}


/* invalid */
{
  "street_address": "24 Sussex Drive",
  "country": "Canada",
  "postal_code": "10000"
}
```































































<br><br>
__________________________________
__________________________________
<br><br>

# The $schema keyword (https://json-schema.org/understanding-json-schema/reference/schema.html#the-schema-keyword)
- The $schema keyword is used to declare that a JSON fragment is actually a piece of JSON Schema. It also declares which version of the JSON Schema standard that the schema was written against. It is recommended that all JSON Schemas have a $schema entry, which must be at the root. Therefore most of the time, you’ll want this at the root of your schema:
```javascript
"$schema": "http://json-schema.org/draft/2019-09/schema#"
```


<br><br>

## Advanced (https://json-schema.org/understanding-json-schema/reference/schema.html#advanced)
- You should declare that your schema was written against a specific version of the JSON Schema standard and include the draft name in the path, for example:
<br> http://json-schema.org/draft/2019-09/schema#
<br> http://json-schema.org/draft-07/schema#
<br> http://json-schema.org/draft-06/schema#
<br> http://json-schema.org/draft-04/schema#

