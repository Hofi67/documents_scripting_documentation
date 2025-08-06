[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / ArchiveServer

# Interface: ArchiveServer

**The ArchiveServer class has been added to the DOCUMENTS PortalScripting API to gain full access to the DOCUMENTS ArchiveServer by scripting means.**

## Since

DOCUMENTS 5.0a

## Properties

### name

> **name**: `string`

**The technical name of the ArchiveServer.**

#### Since

DOCUMENTS 5.0a

## Methods

### getArchiveConnection()

> **getArchiveConnection**(): [`ArchiveConnection`](ArchiveConnection.md)

**Retrieve the archive connection object for EAS, EBIS or EASY Enterprise XML-Server.**  

The ArchiveConnection object can be used for low level call directly on the archive interface.

#### Returns

[`ArchiveConnection`](ArchiveConnection.md)

`ArchiveConnection` object if successful, `null` in case of any error

#### Since

DOCUMENTS 5.0a

***

### getAttribute()

> **getAttribute**(`attribute`): `string`

**Get the String value of an attribute of the ArchiveServer.**  

**Note:** This function is only for experts. Knowledge about the DOCUMENTS-database schema is necessary!

#### Parameters

##### attribute

`string`

String containing the name of the desired attribute

#### Returns

`string`

String containing the value of the desired attribute

#### Since

DOCUMENTS 5.0a

***

### getLastError()

> **getLastError**(`shortMessage?`): `string`

**If you call a method at an ArchiveServer object and an error occurred, you can get the error description with this function.**  
 
  
**Since:** DOCUMENTS 5.0g (new parameter shortMessage)

#### Parameters

##### shortMessage?

`boolean`

optional Boolean; removes "Error in function: class.method(): " from the message.  
**Default:** `false`

#### Returns

`string`

Text of the last error as String

#### Since

DOCUMENTS 5.0a

***

### getOID()

> **getOID**(`oidLow?`): `string`

**Returns the object-id.**

#### Parameters

##### oidLow?

`boolean`

Optional flag:   
If `true` only the id of the ArchiveServer object (`m_oid`) will be returned.   
If `false` the id of the ArchiveServer object will be returned together with the id of the corresponding class in the form `class-id:m_oid`.   
**Default:** `false`

#### Returns

`string`

`String` with the object-id

#### Since

DOCUMENTS 5.0a

***

### getRetentionPolicies()

> **getRetentionPolicies**(): `string`

**Returns a json string with the retention policies of the ArchiveServer.**  

**Note:** Only available for EAS ArchiveServer

#### Returns

`string`

`json-String`; throws an exception in case of an error

#### Since

DOCUMENTS 5.0i

#### Example

```ts
try {
  var as = context.getArchiveServer("EDA_2022");
  var policiesString = as.getRetentionPolicies()
  util.out(policiesString);
} catch (err) {
  util.out(err)
}
```

***

### pdo()

> **pdo**(): `PDObject`

**`Internal`**

**Function returns the PDObject of the ArchiveServer.**  

This function is for internal use only!

#### Returns

`PDObject`

PDObject, in case of an error an exception will be thrown

#### Since

DOCUMENTS 5.0f HF1

***

### setAttribute()

> **setAttribute**(`attribute`, `value`): `boolean`

**Set the String value of an attribute of the ArchiveServer to the desired value.**  

**Note:** This function is only for experts. Knowledge about the DOCUMENTS-database schema is necessary!

#### Parameters

##### attribute

`string`

String containing the name of the desired attribute

##### value

`string`

String containing the desired value of the attribute

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0a

***

### submitChanges()

> **submitChanges**(): `void`

**After changes on the ArchiveServer with scripting methods, it is necessary to submit them to make them immediately valid.**  

The settings of the ArchiveServer will be cached in a connection pool to the archive system. The pool does not recognize 
changes in the ArchiveServer object automatically, therefore it is necessary to call this method after all.

#### Returns

`void`

#### Since

DOCUMENTS 5.0c

#### Example

```ts
var as = context.getArchiveServer("EDA_2017");
if (as)
{
  as.setAttribute("Host", "127.0.0.1");
  as.submitChanges();
}
```
