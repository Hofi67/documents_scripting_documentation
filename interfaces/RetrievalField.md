[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / RetrievalField

# Interface: RetrievalField

**This class represents one search field or one conditon within a DOCUMENTS search request.**

## Since

DOCUMENTS 4.0c HF2

## See

[DocQueryParams](DocQueryParams.md)

## Properties

### compOp

> **compOp**: `string`

**The comparison operator / relational operator as a String.**  

For a list of valid operators see the page: [Filter Expressions](../filter.html).  

**Note:** The access to this property is restricted. Only the "OnSearchScript" can effectively modify it. 
Modifying the operator is risky, since it can produce unexpected results from the user's point of view.

#### Since

DOCUMENTS 4.0c HF2

***

### defaultValue

> **defaultValue**: `string`

**The actual default value of the field (read-only).**  

**Note:** Actually only the "FillSearchMask" exit can attach default values (see setDefault()). 
There might exist another method in a future version. To improve upward compatibility a "FillSearchMask" script 
may check for external default values, and leave them unmodified.

#### Since

DOCUMENTS 4.0d

***

### defValWriteProt

> **defValWriteProt**: `boolean`

**The UI write protection state of the defautValue (read-only) **

#### Since

DOCUMENTS 4.0d

#### See

[setDefault](#setdefault)

***

### label

> **label**: `string`

**The localized label of the field. Maybe an empty String.**  

**Note:** If the field has not got a label, DOCUMENTS falls back to the technical name. So there is no need to specify a label always. 
A few reserved internal fields, which are usualli never displayed on a search mask or a hit list, also come along without any label. 
An example is the special field "Search_EEIFileNr", which DOCUMENTS uses internally to implement a version listing for an ENTERPRISE.i file.

#### Since

DOCUMENTS 4.0c HF2

***

### name

> **name**: `string`

**The name of the look-up field (read-only).**

#### Since

DOCUMENTS 4.0c HF2

***

### type

> **type**: `number`

**The field type coded as an integer (read-only).**  

See the enumeration constants in this class.

#### Since

DOCUMENTS 4.0c HF2

***

### valueExpr

> **valueExpr**: `string`

**The value sought after. If the operator is "~", it can be a composed value expression.**  

**Note:** The access to this property is restricted. Only the "OnSearchScript" can effectively modify it. Modifying the value is risky, 
because it can produce unexpected results from the user's point of view. Within a "FillSearchMask" exit this property contains always an empty string.

#### Since

DOCUMENTS 4.0c HF2

## Methods

### setDefault()

> **setDefault**(`value`, `writeProtect`): `any`

**Place a default value in a search field.**  

A "FillSearchMask" script-exit can call this function to place default values in an extended search formular. Calls from other scripts will 
rather deposit a "LastError" message in the superior [DocQueryParams](DocQueryParams.md) object.  

**Note:** The DocumentsServer only forwards these parameters to the client application. If a special client implementation will ignore them, 
the server would not enforce the defaults, because such a behaviour would confuse users. Calling this function does not modify the "empty" state 
in terms of [DocQueryParams.getSearchField()](DocQueryParams.md#getsearchfield).

#### Parameters

##### value

`string`

The initial text in the search field. Dates and numbers must be formatted with the current user's locale settings.

##### writeProtect

`boolean`

Indicates, if the user interface shall write-protect the field.

#### Returns

`any`

No return value.

#### Since

DOCUMENTS 4.0d

## Field Types

These constants are equally available in each instance of RetrievalField and in the constructor object.

### FT\_BOOL

> `readonly` **FT\_BOOL**: `number`

Integer code for the field type "boolean"

***

### FT\_CHECKBOX

> `readonly` **FT\_CHECKBOX**: `number`

Integer code for the field type "Checkbox"

***

### FT\_DATE

> `readonly` **FT\_DATE**: `number`

Integer code for the field type "Date"

***

### FT\_DOUBLE\_LIST

> `readonly` **FT\_DOUBLE\_LIST**: `number`

Integer code for the field type "Double select list"

***

### FT\_E\_MAIL

> `readonly` **FT\_E\_MAIL**: `number`

Integer code for the field type "E-mail address"

***

### FT\_ENUM

> `readonly` **FT\_ENUM**: `number`

Integer code for the field type "Enumeration" (not extensible)

***

### FT\_FILING\_PLAN

> `readonly` **FT\_FILING\_PLAN**: `number`

Integer code for the field type "Filing plan"

***

### FT\_FILING\_STRUCTURE

> `readonly` **FT\_FILING\_STRUCTURE**: `number`

Reserved constant for a possible future use.

***

### FT\_GADGET

> `readonly` **FT\_GADGET**: `number`

Integer code for the field type "Gadget" (actually ignored by the retrieval system)

***

### FT\_HISTORY

> `readonly` **FT\_HISTORY**: `number`

Integer code for the field type "History"

***

### FT\_HTML

> `readonly` **FT\_HTML**: `number`

Integer code for the field type "HTML"

***

### FT\_NUMERIC

> `readonly` **FT\_NUMERIC**: `number`

Integer code for the field type "Numeric"

***

### FT\_REFERENCE

> `readonly` **FT\_REFERENCE**: `number`

Integer code for the field type "File reference"

***

### FT\_SEPARATOR

> `readonly` **FT\_SEPARATOR**: `number`

Integer code for the field type "Horizontal seperator" (actually ignored by the retrieval system)

***

### FT\_STRING

> `readonly` **FT\_STRING**: `number`

Integer code for the field type "String" (single line)

***

### FT\_TEXT

> `readonly` **FT\_TEXT**: `number`

Integer code for the field type "Text" (multiple lines)

***

### FT\_TEXT\_FIXED\_FONT

> `readonly` **FT\_TEXT\_FIXED\_FONT**: `number`

Integer code for the field type "Text (fixed font)"

***

### FT\_TIMESTAMP

> `readonly` **FT\_TIMESTAMP**: `number`

Integer code for the field type "Time stamp"

***

### FT\_UNDEFINED

> `readonly` **FT\_UNDEFINED**: `number`

Integer code for fields with an unspecified data type.  
This constant has been added for completeness. Fields in this state should never appear in the retrieval system.

***

### FT\_URL

> `readonly` **FT\_URL**: `number`

Integer code for the field type "URL"

***

### FT\_USER\_DEFINED

> `readonly` **FT\_USER\_DEFINED**: `number`

Integer code for the field type "User defeined"
