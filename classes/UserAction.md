[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / UserAction

# Class: UserAction

The UserAction class represents the user-defined action of DOCUMENTS.

## Properties

### label

> **label**: `string`

**The entire label defined for the UserAction object.**

#### Since

DOCUMENTS 4.0d

***

### name

> **name**: `string`

**The technical name of the UserAction object.**

#### Since

DOCUMENTS 4.0d

***

### scope

> **scope**: `string`

**The scope of the UserAction object.**

#### Since

DOCUMENTS 4.0d

***

### type

> **type**: `string`

**The type of the UserAction object.**

#### Since

DOCUMENTS 4.0d

***

### widget

> **widget**: `string`

**The widget identifier of the UserAction object.**

#### Since

DOCUMENTS 4.0d

## Methods

### addToFolder()

> **addToFolder**(`folder`): `boolean`

**Add the user action to a [Folder](../interfaces/Folder.md).**

#### Parameters

##### folder

[`Folder`](../interfaces/Folder.md)

Folder object representing the desired Folder.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 4.0d

#### Example

```ts
var it = context.getFoldersByName("testFolder");
var folder = it.first();
if (folder)
{
  var action = new UserAction("testAction");
  if (action)
  {
      if (!action.addToFolder(folder))
          util.out(action.getLastError());
  }
}
```

***

### getAttribute()

> **getAttribute**(`attribute`): `string`

**Get the String value of an attribute of the user action.**

#### Parameters

##### attribute

`string`

String containing the name of the desired attribute.

#### Returns

`string`

String containing the value of the desired attribute.

#### Since

DOCUMENTS 4.0d

***

### getLastError()

> **getLastError**(): `string`

**Get the description of the last error that occurred.**

#### Returns

`string`

Text of the last error as String

#### Since

DOCUMENTS 4.0d

***

### getOID()

> **getOID**(`oidLow?`): `string`

**Returns the object-id.**  
 
  
**Since:** DOCUMENTS 5.0 (new parameter oidLow)

#### Parameters

##### oidLow?

`boolean`

Optional flag:   
If `true` only the id of the user action object (`m_oid`) will be returned.   
If `false` the id of the user action object will be returned together with the id of the corresponding class in the form `class-id:m_oid`.   

**Default:** `false`

#### Returns

`string`

`String` with the object-id or an empty string in case of any error.

#### Since

DOCUMENTS 4.0d

***

### getPosition()

> **getPosition**(): `number`

**Retrieve the position of the user action within the user-defined action list of the parent object.**

#### Returns

`number`

The zero-based position of the user action as integer or -1 in case of any error.

#### Since

DOCUMENTS 4.0d

#### Example

```ts
var it = context.getFoldersByName("testFolder");
var folder = it.first();
if (folder)
{
  var action = folder.getActionByName("testAction");
  if (action)
      util.out(action.getPosition());
}
```

***

### pdo()

> **pdo**(): `PDObject`

**`Internal`**

**Function returns the PDObject of the UserAction.**  

This function is for internal use only!

#### Returns

`PDObject`

PDObject, in case of an error an exception will be thrown

#### Since

DOCUMENTS 5.0f HF1

***

### remove()

> **remove**(): `boolean`

**Remove the user-defined action from DOCUMENTS.**

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 4.0d

#### Example

```ts
var it = context.getFoldersByName("testFolder");
var folder = it.first();
if (folder)
{
  var action = folder.getActionByName("testAction");
  if (action)
      action.remove();
}
```

***

### setAttribute()

> **setAttribute**(`attribute`, `value`): `boolean`

**Set the String value of an attribute of the user action to the desired value.**

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

DOCUMENTS 4.0d

***

### setContext()

> **setContext**(`context`): `boolean`

**Set the context for a user action of type JSP.**  

**Note:** This function is only available for a user action of type JSP.

#### Parameters

##### context

`string`

String containing the desired context.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 4.0d

#### Example

```ts
var action = new UserAction("testAction");
action.type = "JSP";
if (!action.setContext("myContext"))
  util.out(action.getLastError());
```

***

### setCreateDefaultWorkflow()

> **setCreateDefaultWorkflow**(`createDefaultWorkflow`): `boolean`

**Set the flag whether to create the default workflow for a user action of type NewFile.**  

**Note:** This function is only available for a user action of type NewFile.

#### Parameters

##### createDefaultWorkflow

`boolean`

Flag indicating whether to create the default workflow for a new file.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 4.0d

#### Example

```ts
var action = new UserAction("testAction");
if (!action.setCreateDefaultWorkflow(false))
  util.out(action.getLastError());
```

***

### setFileTypeForNewFile()

> **setFileTypeForNewFile**(`fileType`): `boolean`

**Set the file type for a user action of type NewFile.**  

**Note:** This function is only available for a user action of type NewFile.

#### Parameters

##### fileType

`string`

The technical name of the desired file type; use empty string ('') if you want to remove the associated file type.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 4.0d

#### Example

```ts
var action = new UserAction("testAction");
if (!action.setFileTypeForNewFile("Filetype1"))
  util.out(action.getLastError());
// You can remove the file type as follows:
action.setFileTypeForNewFile('');
```

***

### setPortalScript()

> **setPortalScript**(`scriptName`): `boolean`

**Set the portal script for a user action of type PortalScript.**  

**Note:** This function is only available for a user action of type PortalScript.

#### Parameters

##### scriptName

`string`

The name of the desired portal script; use empty string ('') if you want to remove the associated script.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 4.0d

#### Example

```ts
var action = new UserAction("testAction");
action.type = "PortalScript";
if (!action.setPortalScript("testScript"))
  util.out(action.getLastError());
// You can remove the script as follows:
action.setPortalScript('');
```

***

### setPosition()

> **setPosition**(`position`): `boolean`

**Place the user action at the given position in the user-defined action list of the parent object.**  

**Note:** 0 at the beginning and -1 at the end.

#### Parameters

##### position

`number`

The 0-based position for the user action.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0d

#### Example

```ts
var it = context.getFoldersByName("testFolder");
var folder = it.first();
if (folder)
{
  var action = folder.getActionByName("testAction");
  if (action)
      action.setPosition(-1);
}
```

## Constructors

### Constructor

> **new UserAction**(`name`, `label?`, `widget?`, `type?`, `scope?`): `UserAction`

**Create a new instance of the UserAction class.**  
 
  
**Since:** DOCUMENTS 4.0d   
**Since:** DOCUMENTS 5.0i a global user-defined action will be created.

#### Parameters

##### name

`string`

String value containing the desired user action name.

##### label?

`string`

String value containing the desired user action label.

##### widget?

`string`

String value containing the desired user action widget.  

**Default:** `"Button"`

##### type?

`string`

String value containing the desired user action type.  

**Default:** `"NewFile"`

##### scope?

`string`

String value containting the desired user action scope.  

**Default:** `"Unrestricted"`

#### Returns

`UserAction`

#### Since

DOCUMENTS 4.0d

#### Examples

```ts
var folder = context.createFolder("test", "public");
var action = new UserAction("testAction");
action.widget = "DropdownList";
action.setFileTypeForNewFile("FileType1");
if (!action.addToFolder(folder))
  util.out(action.getLastError());
```

```ts
var action = new UserAction("testAction", "de:Aktion;en:Action", "DropdownList", "PortalScript", "ProcessesOnly");
```

#### See

[UserAction.widget](#widget)  
[UserAction.type](#type)  
[UserAction.scope](#scope)
