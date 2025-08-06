[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / Workflow

# Interface: Workflow

**A DOCUMENTS Workflow object.**  

This class provides read-only access to DOCUMENTS Workflow objects.  

**Note:** This class is designed for usage with a full workflow engine license. Its capability in representing pure distribution lists is 
very limited. For the most part it is only possible to read the name of a distribution list.

## Since

DOCUMENTS 6.0

## Properties

### name

> `readonly` **name**: `string`

**The technical name of the Workflow.**

#### Since

DOCUMENTS 6.0

***

### version

> `readonly` **version**: `string`

**The version string of the Workflow.**

#### Since

DOCUMENTS 6.0

## Methods

### getAllActiveFiles()

> **getAllActiveFiles**(`actionId`): [`FileResultset`](../classes/FileResultset.md)

**Find DocFiles, which are traversing this workflow or a specific descendant step.**  

Given a valid actionId the function retrieves only the DocFiles, which actually pass the workflow step with this id. If the actionId parameter 
is empty or missing, the function retrieves DocFiles at arbitrary positions in the worflow.   
The function lists neither DocFiles, which have reached the end of the workflow nor DocFiles in a different version of the workflow.  

**Note:** This function requires a full workflow engine license. Each call on a distribution list creates only an empty [FileResultset](../classes/FileResultset.md).

#### Parameters

##### actionId

`string`

Optional string holding the actionId or nodeId of a specific workflow step.

#### Returns

[`FileResultset`](../classes/FileResultset.md)

A new FileResultset object, which is capable of enumerating the found DocFiles.

#### Since

DOCUMENTS 6.0

***

### getAttribute()

> **getAttribute**(`attribute`): `string`

**Get the String value of an attribute of the Workflow.**  

**Note:** Workflows and distribution lists share one scripting class, but they are internally separate classes with different sets of attributes.

#### Parameters

##### attribute

`string`

String containing the name of the desired attribute

#### Returns

`string`

String containing the value of the attribute

#### Since

DOCUMENTS 6.0

***

### pdo()

> **pdo**(): `PDObject`

**`Internal`**

**The function returns the PDObject of the Workflow.**  

This function is for internal use only!

#### Returns

`PDObject`

PDObject, in case of an error an exception will be thrown

#### Since

DOCUMENTS 6.0
