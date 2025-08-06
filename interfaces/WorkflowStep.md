[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / WorkflowStep

# Interface: WorkflowStep

**The WorkflowStep class allows access to the according object type of DOCUMENTS.**  

You may access WorkflowStep objects by the different methods described in the [DocFile](DocFile.md) chapter.  

**Note:** This class and all of its methods and attributes require a full workflow engine license, it does not work with pure distribution lists.

## Properties

### executiveGroup

> `readonly` **executiveGroup**: `string`

**String value containing the locking user group of the WorkflowStep.**  

**Note:** This property requires a full workflow engine license, it does not work with pure distribution lists.

#### Since

DOCUMENTS 4.0c

***

### executiveType

> `readonly` **executiveType**: `string`

**String value containing the type of recipient of the WorkflowStep.**  

**Note:** This property requires a full workflow engine license, it does not work with pure distribution lists.

#### Since

ELC 3.50 / otrisPORTAL 5.0

***

### executiveUser

> `readonly` **executiveUser**: `string`

**String value containing the locking user of the WorkflowStep.**  

**Note:** This property requires a full workflow engine license, it does not work with pure distribution lists.

#### Since

ELC 3.50 / otrisPORTAL 5.0

***

### firstControlFlow

> `readonly` **firstControlFlow**: `string`

**String value containing the unique internal ID of the first outgoing ControlFlow.**  

**Note:** This property requires a full workflow engine license, it does not work with pure distribution lists.

#### Since

ELC 3.50 / otrisPORTAL 5.0

***

### id

> `readonly` **id**: `string`

**String value containing the unique internal ID of the WorkflowStep.**  

**Note:** This property requires a full workflow engine license, it does not work with pure distribution lists.

#### Since

ELC 3.50 / otrisPORTAL 5.0

***

### name

> `readonly` **name**: `string`

**String value containing the technical name of the WorkflowStep.**  

**Note:** This property requires a full workflow engine license, it does not work with pure distribution lists.

#### Since

ELC 3.50 / otrisPORTAL 5.0

***

### status

> `readonly` **status**: `string`

**String value containing the status of the WorkflowStep.**  

**Note:** This property requires a full workflow engine license, it does not work with pure distribution lists.

#### Since

ELC 3.50 / otrisPORTAL 5.0

***

### templateId

> `readonly` **templateId**: `string`

**String value containing the unique internal ID of the Workflow template.**  

**Note:** This property requires a full workflow engine license, it does not work with pure distribution lists.

#### Since

ELC 3.50 / otrisPORTAL 5.0

## Methods

### forwardFile()

> **forwardFile**(`controlFlowId`, `comment?`): `boolean`

**Forward the file to its next WorkflowStep.**  

This requires the internal ID (as a String value) of the [ControlFlow](ControlFlow.md) you want the file to pass through. 
The optional comment parameter will be stored as a comment in the file's monitor.  
**Note:** This function requires a full workflow engine license, it does not work with pure distribution lists. 
The current user's permissions are not checked when using this function!

#### Parameters

##### controlFlowId

`string`

String value containing the internal ID of the ControlFlow you want to pass through.

##### comment?

`string`

optional String value containing your desired comment for the file's monitor.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50e / otrisPORTAL 5.0e

***

### getAttribute()

> **getAttribute**(`attribute`): `string`

**Get the String value of an attribute of the WorkflowStep.**  

**Note:** This function requires a full workflow engine license, it does not work with pure distribution lists.

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

### getAutoText()

> **getAutoText**(`autoText`, `startTag?`, `endTag?`): `string`

**Retrieve a AutoText in the context of the WorkflowStep and the executive user.**  
 
  
**Since:** DOCUMENTS 5.0i new optional parameters startTag and endTag

#### Parameters

##### autoText

`string`

String containing the rule of the autotext

##### startTag?

`string`

optional start tag. 

**Default:** `"%"`

##### endTag?

`string`

optional end tag.

**Default:** `"%"`

#### Returns

`string`

String containing the autotext

#### Since

DOCUMENTS 5.0f HF1

***

### getControlFlows()

> **getControlFlows**(): [`ControlFlowIterator`](ControlFlowIterator.md)

**Retrieve an iterator representing a list of all outgoing ControlFlows of the WorkflowStep.**  

**Note:** This function requires a full workflow engine license, it does not work with pure distribution lists.

#### Returns

[`ControlFlowIterator`](ControlFlowIterator.md)

ControlFlowIterator containing the outgoing ControlFlows of the current WorkflowStep object.

#### Since

ELC 3.51e / otrisPORTAL 5.1e

***

### getLastError()

> **getLastError**(`shortMessage?`): `string`

**Function to get the description of the last error that occurred.**  

**Note:** This function requires a full workflow engine license, it does not work with pure distribution lists.  
  
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

ELC 3.50 / otrisPORTAL 5.0

#### See

[DocFile.getLastError](DocFile.md#getlasterror)

***

### getOID()

> **getOID**(`oidLow?`): `string`

**Returns the object-id.**  
 
  
**Since:** DOCUMENTS 5.0 (new parameter oidLow)

#### Parameters

##### oidLow?

`boolean`

Optional flag:   
If `true` only the id of the WorkflowStep object (`m_oid`) will be returned.   
If `false` the id of the WorkflowStep object will be returned together with the id of the corresponding class in the form `class-id:m_oid`.   

**Default:** `false`

#### Returns

`string`

`String` with object-id

#### Since

ELC 3.60c / otrisPORTAL 6.0c

***

### getWorkflowName()

> **getWorkflowName**(): `string`

**Retrieve the name of the workflow, the WorkflowStep belongs to.**  

**Note:** This function is only available for workflows, but not distribution lists.

#### Returns

`string`

String containing the workflow name

#### Since

ELC 3.60d / otrisPORTAL 6.0d

#### See

[WorkflowStep.getWorkflowVersion](#getworkflowversion)

***

### getWorkflowProperty()

> **getWorkflowProperty**(`propertyName`): `string`

**Retrieve a property value of the workflow action, the WorkflowStep belongs to.**  

**Note:** This function is only available for workflows, but not distribution lists.

#### Parameters

##### propertyName

`string`

String containing the name of the desired property

#### Returns

`string`

String containing the property value

#### Since

DOCUMENTS 4.0a

***

### getWorkflowVersion()

> **getWorkflowVersion**(): `string`

**Retrieve the version number of the workflow, the WorkflowStep belongs to.**  

**Note:** This function is only available for workflows, but not distribution lists.

#### Returns

`string`

String containing the workflow version number

#### Since

ELC 3.60d / otrisPORTAL 6.0d

#### See

[WorkflowStep.getWorkflowName](#getworkflowname)

***

### pdo()

> **pdo**(): `PDObject`

**`Internal`**

**Function returns the PDObject of the WorkflowStep.**  

This function is for internal use only!

#### Returns

`PDObject`

PDObject, in case of an error an exception will be thrown

#### Since

DOCUMENTS 5.0f HF1

***

### retry()

> **retry**(`comment?`): `boolean`

**`Internal`**

**Start WorkflowStep again, in cases of error.**  

This function is for internal use only!

#### Parameters

##### comment?

`string`

optional String value containing your desired comment for the file's monitor.

#### Returns

`boolean`

#### Since

ELC 3.60j / otrisPORTAL 6.0j

***

### setAttribute()

> **setAttribute**(`attribute`, `value`): `boolean`

**Set the String value of an attribute of the WorkflowStep to the desired value.**  

**Note:** This function requires a full workflow engine license, it does not work with pure distribution lists.

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

***

### setNewExecutiveGroup()

> **setNewExecutiveGroup**(`accessProfileName`): `boolean`

**Reassign the current WorkflowStep object to the given user group.**  

**Note:** This function requires a full workflow engine license, it does not work with pure distribution lists.

#### Parameters

##### accessProfileName

`string`

String containing the technical name of the access profile.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var f = context.file;
var step = f.getCurrentWorkflowStep();
if (!step)
  step = f.getFirstLockingWorkflowStep();
if (!step)
  util.out("File is not in a workflow.");
if (!step.setNewExecutiveGroup("AccessProfile1"))
  util.out(step.getLastError());
```

***

### setNewExecutiveUser()

> **setNewExecutiveUser**(`loginUser`): `boolean`

**Reassigns the current WorkflowStep object to the given user.**  

**Note:** This function requires a full workflow engine license, it does not work with pure distribution lists.

#### Parameters

##### loginUser

`string`

String containing the login name of the desired user.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50e / otrisPORTAL 5.0e
