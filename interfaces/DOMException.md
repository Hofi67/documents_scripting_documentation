[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / DOMException

# Interface: DOMException

**Many of the DOM API functions throw a DOMException, when an error has occurred.**  

**Remarks about W3C conformity**  
The class implements the DOMException exception type with the error codes specified in DOM level 2.

## Since

DOCUMENTS 4.0c

## Properties

### code

> `readonly` **code**: `number`

**An error code.**  

See the [\`Error Constants\`](../classes/DOMParser.md#errcatdom) in this class.

#### Since

DOCUMENTS 4.0c

***

### message

> `readonly` **message**: `string`

**An error message.**

#### Since

DOCUMENTS 4.0c

## Error Code Constants

All these constants are also available as properties of the constructor.  
**Since** DOCUMENTS 4.0c

### DOMSTRING\_SIZE\_ERR

> **DOMSTRING\_SIZE\_ERR**: `number`

***

### HIERARCHY\_REQUEST\_ERR

> **HIERARCHY\_REQUEST\_ERR**: `number`

***

### INDEX\_SIZE\_ERR

> **INDEX\_SIZE\_ERR**: `number`

***

### INUSE\_ATTRIBUTE\_ERR

> **INUSE\_ATTRIBUTE\_ERR**: `number`

***

### INVALID\_ACCESS\_ERR

> **INVALID\_ACCESS\_ERR**: `number`

***

### INVALID\_CHARACTER\_ERR

> **INVALID\_CHARACTER\_ERR**: `number`

***

### INVALID\_MODIFICATION\_ERR

> **INVALID\_MODIFICATION\_ERR**: `number`

***

### INVALID\_STATE\_ERR

> **INVALID\_STATE\_ERR**: `number`

***

### NAMESPACE\_ERR

> **NAMESPACE\_ERR**: `number`

***

### NO\_DATA\_ALLOWED\_ERR

> **NO\_DATA\_ALLOWED\_ERR**: `number`

***

### NO\_MODIFICATION\_ALLOWED\_ERR

> **NO\_MODIFICATION\_ALLOWED\_ERR**: `number`

***

### NOT\_FOUND\_ERR

> **NOT\_FOUND\_ERR**: `number`

***

### NOT\_SUPPORTED\_ERR

> **NOT\_SUPPORTED\_ERR**: `number`

***

### SYNTAX\_ERR

> **SYNTAX\_ERR**: `number`

***

### VALIDATION\_ERR

> **VALIDATION\_ERR**: `number`

***

### WRONG\_DOCUMENT\_ERR

> **WRONG\_DOCUMENT\_ERR**: `number`
