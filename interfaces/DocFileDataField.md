[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / DocFileDataField

# Interface: DocFileDataField

**The JS_DocFileDataField class represents the special comment field at the DocFile.**

## Since

DOCUMENTS 5.0d

## Properties

### fieldName

> **fieldName**: `string`

**Name of the field.**

#### Since

DOCUMENTS 5.0d

***

### hash

> **hash**: `string`

**Hash value of the last field value.**

#### Since

DOCUMENTS 5.0d

***

### readAccess

> **readAccess**: `Boolean`

**Access-right to read the field.**

#### Since

DOCUMENTS 5.0d

***

### writeAccess

> **writeAccess**: `Boolean`

**Access-right to write the field.**

#### Since

DOCUMENTS 5.0d

***

### writeAccessGui

> **writeAccessGui**: `Boolean`

**Is the field defined as readonly for the Web-Client (GUI).**

#### Since

DOCUMENTS 5.0g HF2

## Methods

### getLastError()

> **getLastError**(): `string`

**If you call a method at a DocFileDataField object and an error occurred, you can get the error description with this function.**

#### Returns

`string`

Text of the last error as String

#### Since

DOCUMENTS 5.0d

***

### getValue()

> **getValue**(): `string`

**Get the comment as String.**

#### Returns

`string`

String containing the comment

#### Since

DOCUMENTS 5.0d

***

### setValue()

> **setValue**(`value`): `boolean`

**Set the comment as String.**

#### Parameters

##### value

`string`

String containing the new comment

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0d
