[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / ControlFlow

# Interface: ControlFlow

**The ControlFlow class has been added to the DOCUMENTS PortalScripting API to gain full control over a file's
workflow by scripting means.**  

You may access ControlFlow objects of a certain WorkflowStep by the different methods described in the WorkflowStep
chapter. The objects of this class reflect only outgoing control flows of a WorkflowStep object.  

**Note:**  
This class and all of its methods and attributes require a full workflow engine license, it does not work with pure distribution lists.

## Since

ELC 3.51e / otrisPORTAL 5.1e

## Properties

### id

> `readonly` **id**: `string`

**String value containing the unique internal ID of the ControlFlow.**  

**Note:**  
This property requires a full workflow engine license, it does not work with pure distribution lists.

#### Since

ELC 3.51e / otrisPORTAL 5.1e

***

### label

> `readonly` **label**: `string`

**String value containing the ergonomic label of the ControlFlow.**  

This is usually the label of the according button in the web surface.  

**Note:**  
This property requires a full workflow engine license, it does not work with pure distribution lists.

#### Since

ELC 3.51e / otrisPORTAL 5.1e

***

### name

> `readonly` **name**: `string`

**String value containing the technical name of the ControlFlow.**  

**Note:**  
This property requires a full workflow engine license, it does not work with pure distribution lists.

#### Since

ELC 3.51e / otrisPORTAL 5.1e

## Methods

### getAttribute()

> **getAttribute**(`attribute`): `string`

**Get the String value of an attribute of the ControlFlow.**  

**Note:**  
This function requires a full workflow engine license, it does not work with pure distribution lists.

#### Parameters

##### attribute

`string`

String containing the name of the desired attribute

#### Returns

`string`

String containing the value of the desired attribute

#### Since

ELC 3.51e / otrisPORTAL 5.1e

***

### getLastError()

> **getLastError**(): `string`

**Function to get the description of the last error that occurred.**  

**Note:**  
This function requires a full workflow engine license, it does not work with pure distribution lists.

#### Returns

`string`

Text of the last error as String

#### Since

ELC 3.51e / otrisPORTAL 5.1e

#### See

[DocFile.getLastError](DocFile.md#getlasterror)

***

### pdo()

> **pdo**(): `PDObject`

**`Internal`**

**Function returns the PDObject of the ControlFlow.**  

This function is for internal use only!

#### Returns

`PDObject`

PDObject, in case of an error an exception will be thrown

#### Since

DOCUMENTS 5.0f HF1

***

### setAttribute()

> **setAttribute**(`attribute`, `value`): `boolean`

**Set the String value of an attribute of the ControlFlow to the desired value.**  

**Note:**  
This function requires a full workflow engine license, it does not work with pure distribution lists.

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

ELC 3.51e / otrisPORTAL 5.1e
