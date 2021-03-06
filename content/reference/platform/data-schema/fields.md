---
alias: teizeit5se
path: /docs/reference/platform/fields
layout: REFERENCE
description: Fields are the building blocks of a model, defining a node's shape. A field has a name and is either scalar or belongs to a relation.
tags:
  - platform
  - fields
  - data-schema
related:
  further:
    - ahwoh2fohj
    - ij2choozae
    - goh5uthoc1
    - uhieg2shio
    - oe3raifamo
  more:
    - ier7sa3eep
    - ga2ahnee2a
    - uu2xighaef
---

# Fields

*Fields* are the building blocks of a [model](!alias-ij2choozae) giving a node its shape. Every field is referenced by its name and has a type which is either a [scalar type](#scalar-types) or a [relation](!alias-goh5uthoc1).

> The `Post` model might have a `title` and a `text` field both of type String and an `id` field of type ID.

## Scalar Types

### String

A String holds text. This is the type you would use for a username, the content of a blog post or anything else that is best represented as text.

Note: String values are currently limited to 256KB in size.

In queries or mutations, String fields have to be specified using enclosing double quotes: `string: "some-string"`.

### Integer

An Integer is a number that cannot have decimals. Use this to store values such as the weight of an ingredient required for a recipe or the minimum age for an event.

Note: Int values range from -2147483648 to 2147483647.

In queries or mutations, Int fields have to be specified without any enclosing characters: `int: 42`.

### Float

A Float is a number that can have decimals. Use this to store values such as the price of an item in a store or the result of complex calculations.

Note: We store Float values as [DECIMAL(65, 30)](https://dev.mysql.com/doc/refman/5.7/en/fixed-point-types.html) inside our databases. Float value can have 65 digits in total, of which at most 35 can be in front of the decimal point, and 30 behind the decimal point.

In queries or mutations, Float fields have to be specified without any enclosing characters and an optional decimal point: `float: 42`, `float: 4.2`.

### Boolean

A Boolean can have the value `true` or `false`. This is useful to keep track of settings such as whether the user wants to receive an email newsletter or if a recipe is appropriate for vegetarians.

In queries or mutations, Boolean fields have to be specified without any enclosing characters: `boolean: true`, `boolean: false`.

### DateTime

The DateTime type can be used to store date or time values. A good example might be a person's date of birth.

In queries or mutations, DateTime fields have to be specified in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601) with enclosing double quotes: `datetime: "2015-11-22T13:57:31.123Z"`.

### Enum

Like a Boolean an Enum can have one of a predefined set of values. The difference is that you can define the possible values. For example you could specify how an article should be formatted by creating an Enum with the possible values `COMPACT`, `WIDE` and `COVER`.

Note: Enum values can at most be 191 characters long.

In queries or mutations, Enum fields have to be specified without any enclosing characters. You can only use values that you defined for the field: `enum: A`, `enum: B`.

### JSON

Sometimes you need to store arbitrary JSON values like unstructured meta information. The JSON type makes sure that it is actually valid JSON and returns the value as a parsed JSON object/array instead of a string.

Note: JSON values are currently limited to 64KB in size.

In queries or mutations, JSON fields have to be specified with enclosing double quotes. Special characters have to be escaped: `json: "[\"this\",\"is\",\"json\"]"`.

<!--
### GeoPoint

*Coming soon...*
-->

### ID

An ID value is a generated unique 25-character string based on [cuid](https://github.com/graphcool/cuid-java). Fields with ID values are system fields and just used internally, therefore it is not possible to create new fields with the ID type.

## Type Modifiers

### List

Scalar fields can be marked with the list field type. A field of a relation that has the many multiplicity will also be marked as a list.

Note: List values are currently limited to 64KB in size, independently of the [scalar type](#scalar-types) of the field.

In queries or mutations, list fields have to be enclosed by square brackets, while the separate entries of the list adhere to the same formatting rules as lined out above: `listString: ["a string", "another string"]`, `listInt: [12, 24]`.

### Required

Scalar fields can be marked as required (sometimes also referred to as "non-null"). When creating a new node, you need to supply a value for fields which are required and don't have a [default value](#default-value).

Required fields are usually marked using a `!` after the field type.

> An example for a required field on the `User` model could look like this: `name: String!`.

## Field Constraints

Fields can be configured with certain field constraints to add further semantics to your [data schema](!alias-ahwoh2fohj).

### Unique

Setting the *unique* constraint makes sure that two nodes of the model in question cannot have the same value for a certain field. The only exception is the `null` value, meaning that multiple nodes can have the value `null` without violating the constraint.

> A typical example is the `email` field on the `User` model.

Please note that only the first 191 characters in a String field are considered for uniqueness. Storing two different strings is not possible if the first 191 characters are the same.

## Default Value

You can set a default value for scalar fields. The value will be taken for new nodes when no value was supplied during creation.

## Fields in the data schema

Fields indirectly define your [data schema](!alias-ahwoh2fohj) and determine the available options for ordering and filtering when querying  multiple nodes in the [Simple API](!alias-pa2aothaec) or the [Relay API](!alias-uu4ohnaih7).
