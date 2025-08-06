[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / Folder

# Interface: Folder

**The Folder class has been added to the DOCUMENTS PortalScripting API to gain full access to the DOCUMENTS folders by scripting means.**

## Since

ELC 3.50l01 / otrisPORTAL 5.0l01

## Properties

### allowArchive

> **allowArchive**: `boolean`

**This property specifies whether the action 'Archive' is available for the folder.**

#### Since

DOCUMENTS 4.0c

***

### allowCopyTo

> **allowCopyTo**: `boolean`

**This property specifies whether the action 'Copy to' is available for the folder.**

#### Since

DOCUMENTS 4.0c

***

### allowCreatePDF

> **allowCreatePDF**: `boolean`

**This property specifies whether the action 'PDF creation (Print)' is available for the folder.**

#### Since

DOCUMENTS 4.0c

***

### allowDelete

> **allowDelete**: `boolean`

**This property specifies whether the action 'Delete' is available for the folder.**

#### Since

DOCUMENTS 4.0c

***

### allowExport

> **allowExport**: `boolean`

**This property specifies whether the action 'Export' is available for the folder.**

#### Since

DOCUMENTS 4.0c

***

### allowForward

> **allowForward**: `boolean`

**This property specifies whether the action 'Forward' is available for the folder.**

#### Since

DOCUMENTS 4.0c

***

### allowMoveTo

> **allowMoveTo**: `boolean`

**This property specifies whether the action 'Store in' is available for the folder.**

#### Since

DOCUMENTS 4.0c

***

### comparator1

> **comparator1**: `string`

**The comparator for the first filter of the Folder object.**  

**Note:** This attribute only exists if the Folder represents a dynamic folder

***

### comparator2

> **comparator2**: `string`

**The comparator for the second filter of the Folder object.**  

**Note:** This attribute only exists if the Folder represents a dynamic folder

***

### comparator3

> **comparator3**: `string`

**The comparator for the third filter of the Folder object.**  

**Note:** This attribute only exists if the Folder represents a dynamic folder

***

### filterExpression

> **filterExpression**: `string`

**The expression of the filter of the folder.**  

**Note:** This property is only available if the Folder represents a dynamic folder and the filter style 'Extended' is used.

#### Since

DOCUMENTS 4.0c

#### See

[Filter Expressions ](../filter.html)

***

### filterfieldname1

> **filterfieldname1**: `string`

**The field to use for the first filter of the Folder object.**  

**Note:** This attribute only exists if the Folder represents a dynamic folder

***

### filterfieldname2

> **filterfieldname2**: `string`

**The field to use for the second filter of the Folder object.**  

**Note:** This attribute only exists if the Folder represents a dynamic folder

***

### filterfieldname3

> **filterfieldname3**: `string`

**The field to use for the third filter of the Folder object.**  

**Note:** This attribute only exists if the Folder represents a dynamic folder

***

### filterStyle

> **filterStyle**: `string`

**The filter style of the folder.**  

There are two filter styles available: 

+ `Standard` 
+ `Extended`

#### Since

DOCUMENTS 4.0c

***

### icon

> **icon**: `string`

**The icon to use in the folder tree.**

#### Since

DOCUMENTS 4.0c

***

### id

> **id**: `string`

**The internal id of the Folder object.**

#### Since

ELC 3.50l01 / otrisPORTAL 5.0l01

***

### invisible

> **invisible**: `boolean`

**This property specifies whether the folder is invisible to the users.**  

**Note:** This property is not operative if the folder is not released.

#### Since

DOCUMENTS 4.0c

***

### label

> **label**: `string`

**The entire label defined for the Folder object.**

#### Since

ELC 3.50l01 / otrisPORTAL 5.0l01

#### See

[Folder.getLocaleLabel](#getlocalelabel)

***

### name

> **name**: `string`

**The technical name of the Folder object.**

#### Since

ELC 3.50l01 / otrisPORTAL 5.0l01

***

### released

> **released**: `boolean`

**This property specifies whether the folder is available to the users.**

#### Since

DOCUMENTS 4.0c

***

### sortColumn

> **sortColumn**: `string`

**The column used to sort the entries in the folder.**  

The following sort columns are available: 

+ `Title`
+ `LastModifiedAt`
+ `LastEditor`
+ `CreatedAt`
+ `Owner`
+ `CustomField`

#### Since

DOCUMENTS 4.0c

***

### sortDescending

> **sortDescending**: `boolean`

**This property specifies the sort order of the entries in the folder.**

#### Since

DOCUMENTS 4.0c

***

### sortFieldName

> **sortFieldName**: `string`

**The technical name of the custom field used to sort the entries in the folder.**  

**Note:** This field is only available if the Folder.sortColumn is set to 'CustomField'.

#### Since

DOCUMENTS 4.0c

***

### systemUser

> **systemUser**: [`SystemUser`](SystemUser.md)

**Returns the owner of a private folder.**  

**Note:** If the folder is a private folder (e.g. inbox) this property returns the owning SystemUser

#### Since

DOCUMENTS 5.0d

***

### type

> **type**: `string`

**The type of the Folder object.**

#### Since

ELC 3.50l01 / otrisPORTAL 5.0l01

***

### value1

> **value1**: `string`

**The desired field value to use for the first filter of the Folder object.**  

**Note:** This attribute only exists if the Folder represents a dynamic folder

***

### value2

> **value2**: `string`

**The desired field value to use for the second filter of the Folder object.**  

**Note:** This attribute only exists if the Folder represents a dynamic folder

***

### value3

> **value3**: `string`

**The desired field value to use for the third filter of the Folder object.**  

**Note:** This attribute only exists if the Folder represents a dynamic folder

## Methods

### addAccessProfile()

> **addAccessProfile**(`accessProfileName`, `allowInsertFiles`, `allowRemoveFiles`): `boolean`

**Add a folder access right for the user group defined by an access profile to the folder.**

#### Parameters

##### accessProfileName

`string`

The technical name of the access profile.

##### allowInsertFiles

`boolean`

Flag indicating whether inserting files into the folder is allowed.

##### allowRemoveFiles

`boolean`

Flag indicating whether removing files from the folder is allowed.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var folder = context.createFolder("testFolder", "public");
var success = folder.addAccessProfile("AccessProfile1", true, false);
if (!success)
  util.out(folder.getLastError());
```

***

### addFile()

> **addFile**(`docFile`): `boolean`

**Store a reference to a desired DocFile object in the current Folder.**  

**Note:** This only works in case the Folder is a real public Folder. The Folder must not represent a dynamic folder, 
since a dynamic folder is sort of a hardcoded search, not a "real" folder.

#### Parameters

##### docFile

[`DocFile`](DocFile.md)

DocFile object which shall be available in the given Folder

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.51h / otrisPORTAL 5.1h

***

### addFilterEDAServer()

> **addFilterEDAServer**(`serverName`): `boolean`

**Add an EDA server to the filter of the folder.**  

**Note:** This function is only available for a Folder of type 'dynamicpublic'.

#### Parameters

##### serverName

`string`

The technical name of the desired EDA server.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var folder = context.createFolder("testFolder", "dynamicpublic");
var success = folder.addFilterEDAServer("eas1");
if (!success)
  util.out(folder.getLastError());
```

***

### addFilterEEiArchive()

> **addFilterEEiArchive**(`archiveKey`): `boolean`

**Add an EE.i archive to the filter of the folder.**  

**Note:** This function is only available for a Folder of type 'dynamicpublic'.

#### Parameters

##### archiveKey

`string`

The key of the desired EE.i archive.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var folder = context.createFolder("testFolder", "dynamicpublic");
var archiveKey = "$(#STANDARD)\\REGTEST@eei1";
var success = folder.addFilterEEiArchive(archiveKey);
if (!success)
  util.out(folder.getLastError());
```

***

### addFilterEExView()

> **addFilterEExView**(`viewKey`): `boolean`

**Add an EE.x view to the filter of the folder.**  

**Note:** This function is only available for a Folder of type 'dynamicpublic'.

#### Parameters

##### viewKey

`string`

The key of the desired EE.x view.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var folder = context.createFolder("testFolder", "dynamicpublic");
var viewKey = "Unit=Default/Instance=Default/View=REGTEST";
var success = folder.addFilterEExView(viewKey);
if (!success)
  util.out(folder.getLastError());
```

***

### addFilterFileType()

> **addFilterFileType**(`fileType`): `boolean`

**Add a file type to the filter of the folder.**  

**Note:** This function is only available for a Folder of type 'dynamicpublic'.

#### Parameters

##### fileType

`string`

The technical name of the desired file type.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var folder = context.createFolder("testFolder", "dynamicpublic");
var success = folder.addFilterFileType("Filetype1");
if (!success)
  util.out(folder.getLastError());
```

***

### addSystemUser()

> **addSystemUser**(`loginName`, `allowInsertFiles`, `allowRemoveFiles`): `boolean`

**Add a folder access right for a system user to the folder.**

#### Parameters

##### loginName

`string`

The login name of the system user.

##### allowInsertFiles

`boolean`

Flag indicating whether inserting files into the folder is allowed.

##### allowRemoveFiles

`boolean`

Flag indicating whether removing files from the folder is allowed.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var folder = context.createFolder("testFolder", "public");
var success = folder.addSystemUser("user1", true, false);
if (!success)
  util.out(folder.getLastError());
```

***

### addToOutbar()

> **addToOutbar**(`outbarName`): `boolean`

**Add the folder to an outbar.**

#### Parameters

##### outbarName

`string`

The technical name of the outbar.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0d HF2

#### Example

```ts
var folder = context.createFolder("testFolder", "public");
var success = folder.addToOutbar("testOutbar");
if (!success)
  util.out(folder.getLastError());
```

***

### copyFolder()

> **copyFolder**(`includeSubFolders`, `copyRights`, `copyActions`): `Folder`

**The current Folder object is duplicated to create a new Folder object.**  

The new Folder object is placed at the same hierarchical stage as the Folder used as its source object. 
After the duplication of the Folder you can change all its public attributes, e.g. to modify the filter definition of a dynamic public folder.

#### Parameters

##### includeSubFolders

`boolean`

boolean whether to duplicate any subfolders contained in the source folder as well

##### copyRights

`boolean`

boolean whether to assign the same access privileges as those assigned to the source Folder

##### copyActions

`boolean`

boolean whether to duplicate any userdefined actions attached to the source folder as well

#### Returns

`Folder`

Folder object generated by the function call

#### Since

ELC 3.50l01 / otrisPORTAL 5.0l01

***

### createSubFolder()

> **createSubFolder**(`name`, `type`): `Folder`

**Create a new subfolder of the specified folder type.**  

**Note:** There are three possible types available: 

+ `public` 
+ `dynamicpublic` 
+ `onlysubfolder`

#### Parameters

##### name

`string`

The technical name of the subfolder to be created.

##### type

`string`

The desired type of the subfolder.

#### Returns

`Folder`

New created subfolder as Folder object or `null` if failed.

#### Since

DOCUMENTS 4.0c

#### See

[context.createFolder](Context.md#createfolder)

#### Example

```ts
var parentFolder = context.createFolder("parentFolder", "public");
if (parentFolder)
{
  var subFolder = parentFolder.createSubFolder("subFolder", "dynamicpublic");
  if (subFolder)
      util.out(subFolder.type);
  else
      util.out(parentFolder.getLastError());
}
```

***

### deleteFolder()

> **deleteFolder**(): `boolean`

**Delete the folder in DOCUMENTS.**  

**Note:** All subfolders are also deleted recursively.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0c

#### See

[context.deleteFolder](Context.md#deletefolder)

#### Example

```ts
var folder = context.createFolder("testFolder", "onlysubfolder");
if (folder)
{
  var success = folder.deleteFolder();
  if (success)
  {
      var itFolder = context.getFoldersByName("testFolder", "onlysubfolder");
      util.out(itFolder.size() == 0);
  }
 }
```

***

### getAccessProfiles()

> **getAccessProfiles**(): [`AccessProfileIterator`](AccessProfileIterator.md)

**Retrieve an AccessProfileIterator representing a list of all AccessProfiles assigned to a folder access right.**

#### Returns

[`AccessProfileIterator`](AccessProfileIterator.md)

AccessProfileIterator containing a list of all AccessProfiles assigned to a folder access right.

#### Since

DOCUMENTS 5.0i HF3

***

### getActionByName()

> **getActionByName**(`actionName`): [`UserAction`](../classes/UserAction.md)

**Retrieve a user-defined action of the Folder.**

#### Parameters

##### actionName

`string`

String value containing the desired action name.

#### Returns

[`UserAction`](../classes/UserAction.md)

UserAction object representing the user-defined action.

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
  {
      action.type = "PortalScript";
      action.setPortalScript("testScript");
  }
  else
      util.out(folder.getLastError());
}
```

***

### getAttribute()

> **getAttribute**(`attribute`): `string`

**Get the String value of an attribute of the Folder.**

#### Parameters

##### attribute

`string`

String containing the name of the desired attribute

#### Returns

`string`

String containing the value of the desired attribute

#### Since

ELC 3.51b / otrisPORTAL 5.1b

***

### getFiles()

> **getFiles**(): [`FileResultset`](../classes/FileResultset.md)

**Retrieve a FileResultset of all the DocFile objects stored in the Folder.**  

**Note:** It does not matter whether the Folder is a real public folder or a dynamic folder.

#### Returns

[`FileResultset`](../classes/FileResultset.md)

FileResultset containing a list of all DocFile objects stored in the Folder

#### Since

ELC 3.51b / otrisPORTAL 5.1b

***

### getFilterFileTypes()

> **getFilterFileTypes**(): `any`[]

**Retrieve the filter file types of the folder.**

#### Returns

`any`[]

Array of strings containing the technical names of the file types.

#### Since

DOCUMENTS 5.0a HF2

#### Example

```ts
var folder = context.createFolder("testFolder", "dynamicpublic");
var success = folder.addFilterFileType("Filetype1");
if (!success)
  util.out(folder.getLastError());
var fileTypes = folder.getFilterFileTypes();
if (fileTypes)
{
  for (var i=0; i < fileTypes.length; i++)
  {
    util.out(fileTypes[i]);
  }
}
else
  util.out(folder.getLastError());
```

***

### getHitResultset()

> **getHitResultset**(`hitlist`, `sortOrder`, `fulltextFilter`, `pageSize?`): [`HitResultset`](../classes/HitResultset.md)

**Create a [HitResultset](../classes/HitResultset.md), which summarizes all DocFiles in the folder.**  

This function executes either an an empty (=unfiltered) search or a fulltext search in the folder. It creates a HitResultset,
which summarizes the Folder's files. By defaut the Resultset contains the same columns as the folder's web view.  

**Note:** The function operates on dynamic and on static folders, but not on the special folders "tasks" and "resubmission". 
On a failed search request the function does not throw errors. To detect this kind of errors scripts should call 
[HitResultset.getLastErrorCode()](../classes/HitResultset.md#getlasterrorcode) or [HitResultset.getLastError()](../classes/HitResultset.md#getlasterror) 
on the returned object.  

**Note:** When used, the hitlist parameter typically is a string with the pattern "file_type.hit_list". 
In unambiguous cases a pure hit list name is accepted, too. The hitlist parameter can instead be an array of strings, 
where each element declares an individual column (recommended pattern: "file_type.field"). Other valid array elements 
are reserved attribute column names like "DlcFile_Title". Restriction: If a folder references an EE.i or EE.x native system, 
only the plain name of a hit list of the folders's primary data source (view or archive) is accepted as the hitlist parameter. 
A few folders are incapable of fulltext searching. An example is a dynamic folder with an API-Style filter expression, 
which uses the "OR" keyword. For such folders the function returns an empty resultset with an attached error message, 
if the fulltextFilter parameter is not empty. To detect in advance, if such an operation can succeed, scripts may first 
create an unfiltered resultset and examine its property searchability. Reading from a lean HitResultset with only a few columns 
can be faster than reading from a FileResultset. Sometimes this effect outweighs the time-related costs of a search. 
If the folder addresses an archive, the time needed to create temporary DocFiles can be saved with this function.  

**Since:** DOCUMENTS 5.0f (parameters hitlist, sortOrder, fulltextFilter, pageSize)

#### Parameters

##### hitlist

`any`

Optional String or Array with a hit list template specification to override the folder's default. See remarks.

##### sortOrder

`string`

Optional sort expression to override the folder's default sort order.

##### fulltextFilter

`string`

Optional fulltext filter expression. Not applicable to all folders. See remarks.

##### pageSize?

`number`

This is a memory-saving and performance-tuning option. If the parameter is zero, Documents will load all available hits at once. 
If the parameter is a positive value, Documents will initially load only the requested number of hits as a first page. 
In order to access each further page, a call to [fetchNextPage()](../classes/HitResultset.md#fetchnextpage) is necessary. A negative 
pageSize value will be replaced by the current user's "hits per page" preference setting.  
**Default:** `0`

#### Returns

[`HitResultset`](../classes/HitResultset.md)

A HitResultset, which contains column headers and a list of [DocHit](DocHit.md) objects.

#### Since

DOCUMENTS 5.0c

#### See

[Folder.getFiles](#getfiles)  
[HitResultset.searchability](../classes/HitResultset.md#searchability)

***

### getLastError()

> **getLastError**(`shortMessage?`): `string`

**Function to get the description of the last error that occurred.**  
 
  
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

ELC 3.50l01 / otrisPORTAL 5.0l01

#### See

[DocFile.getLastError](DocFile.md#getlasterror)

***

### getLocaleLabel()

> **getLocaleLabel**(`locale?`): `string`

**Get the ergonomic label of the Folder.**

#### Parameters

##### locale?

`string`

Optional String value with the locale abbreviation (according to the principal's configuration); 
if omitted, the current user's portal language is used automatically.

#### Returns

`string`

`String` containing the ergonomic label of the Folder in the appropriate portal language.

#### Since

DOCUMENTS 4.0b HF2

***

### getOID()

> **getOID**(`oidLow?`): `string`

**Returns the object-id.**  
 
  
**Since:** DOCUMENTS 5.0 (new parameter oidLow)

#### Parameters

##### oidLow?

`boolean`

Optional flag:   
If `true` only the id of the Folder object (`m_oid`) will be returned.   
If `false` the id of the Folder object will be returned together with the id of the corresponding class in the form `class-id:m_oid`.   

**Default:** `false`

#### Returns

`string`

`String` with the object-id

#### Since

ELC 3.60c / otrisPORTAL 6.0c

***

### getParentFolder()

> **getParentFolder**(): `Folder`

**Returns the parent folder of the current folder.**

#### Returns

`Folder`

`The`Folder if successful, `null` is no parent exist

#### Since

DOCUMENTS 5.0f

***

### getPosition()

> **getPosition**(`subFolder`): `number`

**Retrieve the position of a subfolder within the subfolder list.**

#### Parameters

##### subFolder

`Folder`

Folder object whose position to be retrieved.

#### Returns

`number`

The zero-based position of the subfolder as integer or -1 in case of any error.

#### Since

DOCUMENTS 4.0c

#### See

[Folder.setPosition](#setposition)  
[context.setFolderPosition](Context.md#setfolderposition)

#### Example

```ts
var parentFolder = context.createFolder("parentFolder", "public");
if (parentFolder)
{
  var subFolder1 = parentFolder.createSubFolder("subFolder1", "dynamicpublic");
  var subFolder2 = parentFolder.createSubFolder("subFolder2", "onlysubfolder");
  if (subFolder1 && subFolder2)
  {
      var pos = parentFolder.getPosition(subFolder2);
      util.out(pos == 1);
  }
}
```

***

### getSubFolders()

> **getSubFolders**(`checkAccessRight?`): [`FolderIterator`](FolderIterator.md)

**Retrieve a [FolderIterator](FolderIterator.md) containing all Folder objects which represent subfolders of the given Folder.**  

**Note:** Until version 5.0h this method ignored the access rights of the user to the folders. 
With the optional parameter checkAccessRight this can now be done. For backward compatibility the default value is set to false.  
  
**Since:** DOCUMENTS 5.0h (new optional parameter checkAccessRight)

#### Parameters

##### checkAccessRight?

`boolean`

optional boolean value, that indicates if the access rights should be considered.  

**Default:** `false`

#### Returns

[`FolderIterator`](FolderIterator.md)

FolderIterator with all subfolders one hierarchical level below the given Folder

#### Since

ELC 3.50l01 / otrisPORTAL 5.0l01

***

### hasFiles()

> **hasFiles**(): `boolean`

**Retrieve information whether the Folder is empty or not.**

#### Returns

`boolean`

`true` if DocFile objects available inside the Folder, `false` in case the Folder is empty

#### Since

ELC 3.50l01 / otrisPORTAL 5.0l01

***

### pdo()

> **pdo**(): `PDObject`

**`Internal`**

**Function returns the PDObject of the Folder.**  

This function is for internal use only!

#### Returns

`PDObject`

PDObject, in case of an error an exception will be thrown

#### Since

DOCUMENTS 5.0f HF1

***

### removeAccessProfile()

> **removeAccessProfile**(`accessProfileName`): `boolean`

**Remove all folder access rights of the user group defined by an access profile from the folder.**

#### Parameters

##### accessProfileName

`string`

The technical name of the access profile.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var folder = context.createFolder("testFolder", "public");
var success = folder.addAccessProfile("AccessProfile1", true, false);
if (success)
{
  success = folder.removeAccessProfile("AccessProfile1");
  if (!success)
      util.out(folder.getLastError());
}
```

***

### removeFile()

> **removeFile**(`docFile`): `boolean`

**Remove the reference to a desired DocFile object out of the current Folder.**  

**Note:** This only works in case the Folder is a real public Folder. The Folder must not represent a dynamic folder, 
since a dynamic folder is sort of a hardcoded search, not a "real" folder.

#### Parameters

##### docFile

[`DocFile`](DocFile.md)

DocFile object which shall be removed from the given Folder

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.51h / otrisPORTAL 5.1h

***

### removeFilterEDAServer()

> **removeFilterEDAServer**(`serverName`): `boolean`

**Remove an EDA server from the filter of the folder.**  

**Note:** This function is only available for a Folder of type 'dynamicpublic'.

#### Parameters

##### serverName

`string`

The technical name of the desired EDA server.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var folder = context.createFolder("testFolder", "dynamicpublic");
var success = folder.addFilterEDAServer("eas1");
if (success)
{
  success = folder.removeFilterEDAServer("eas1");
  if (!success)
    util.out(folder.getLastError());
}
```

***

### removeFilterEEiArchive()

> **removeFilterEEiArchive**(`archiveKey`): `boolean`

**Remove an EE.i archive from the filter of the folder.**  

**Note:** This function is only available for a Folder of type 'dynamicpublic'.

#### Parameters

##### archiveKey

`string`

The key of the desired EE.i archive.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var folder = context.createFolder("testFolder", "dynamicpublic");
var archiveKey = "$(#STANDARD)\\REGTEST@eei1";
var success = folder.addFilterEEiArchive(archiveKey);
if (success)
{
  success = folder.removeFilterEEiArchive(archiveKey);
  if (!success)
      util.out(folder.getLastError());
}
```

***

### removeFilterEExView()

> **removeFilterEExView**(`viewKey`): `boolean`

**Remove an EE.x view from the filter of the folder.**  

**Note:** This function is only available for a Folder of type 'dynamicpublic'.

#### Parameters

##### viewKey

`string`

The key of the desired EE.x view.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var folder = context.createFolder("testFolder", "dynamicpublic");
var viewKey = "Unit=Default/Instance=Default/View=REGTEST";
var success = folder.addFilterEExView(viewKey);
if (success)
{
  success = folder.removeFilterEExView(viewKey);
  if (!success)
      util.out(folder.getLastError());
}
```

***

### removeFilterFileType()

> **removeFilterFileType**(`fileType`): `boolean`

**Remove a file type from the filter of the folder.**  

**Note:** This function is only available for a Folder of type 'dynamicpublic'.

#### Parameters

##### fileType

`string`

The technical name of the desired file type.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var folder = context.createFolder("testFolder", "dynamicpublic");
var success = folder.addFilterFileType("Filetype1");
if (success)
{
  success = folder.removeFilterFileType("Filetype1");
  if (!success)
      util.out(folder.getLastError());
}
```

***

### removeFromOutbar()

> **removeFromOutbar**(`outbarName`): `boolean`

**Remove the folder from an outbar.**

#### Parameters

##### outbarName

`string`

The technical name of the outbar.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0d HF2

#### Example

```ts
var itFolder = context.getFoldersByName("testFolder", "public");
var folder = itFolder.first();
if (folder)
{
  var success = folder.removeFromOutbar("testOutbar");
  if (!success)
      util.out(folder.getLastError());
}
```

***

### removeSystemUser()

> **removeSystemUser**(`loginName`): `boolean`

**Remove all folder access rights of a system user from the folder.**

#### Parameters

##### loginName

`string`

The login name of the system user.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var folder = context.createFolder("testFolder", "public");
var success = folder.addSystemUser("user1", true, false);
if (success)
{
  success = folder.removeSystemUser("user1");
  if (!success)
      util.out(folder.getLastError());
}
```

***

### setAllowedActionScript()

> **setAllowedActionScript**(`scriptName`): `boolean`

**Set the script containing the allowed user-defined actions.**

#### Parameters

##### scriptName

`string`

The name of the desired script; use empty string ('') if you want to remove the associated action script.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var folder = context.createFolder("testFolder", "public");
var success = folder.setAllowedActionScript("testScript");
if (!success)
  util.out(folder.getLastError());
// We can remove the action script as follows:
success = folder.setAllowedActionScript('');
```

***

### setAttribute()

> **setAttribute**(`attribute`, `value`): `boolean`

**Set the String value of an attribute of the Folder to the desired value.**

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

ELC 3.51b / otrisPORTAL 5.1b

***

### setParentFolder()

> **setParentFolder**(`parentFolder`): `boolean`

**Set the parent folder of the current folder.**

#### Parameters

##### parentFolder

`Folder`

optional Folder object being the parent folder of the current folder. If no parent folder is defined, the current folder will be moved to the top level.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var parentFolder = context.createFolder("parentFolder", "public");
if (parentFolder)
{
  var subFolder = context.createFolder("subFolder", "dynamicpublic");
  if (subFolder)
  {
      var success = subFolder.setParentFolder(parentFolder);
      if (!success)
          util.out(subFolder.getLastError());
      // We can move subFolder to the top level as follows:
      success = subFolder.setParentFolder();
  }
}
```

***

### setPosition()

> **setPosition**(`subFolder`, `position`): `boolean`

**Place a subfolder at the given position in the subfolder list.**  

**Note:** 0 at the beginning and -1 at the end.

#### Parameters

##### subFolder

`Folder`

Folder object to be placed at the given position.

##### position

`number`

The 0-based position for the subfolder.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0c

#### See

[Folder.getPosition](#getposition)  
[context.setFolderPosition](Context.md#setfolderposition)

#### Example

```ts
var parentFolder = context.createFolder("parentFolder", "public");
if (parentFolder)
{
  var subFolder1 = parentFolder.createSubFolder("subFolder1", "dynamicpublic");
  var subFolder2 = parentFolder.createSubFolder("subFolder2", "onlysubfolder");
  if (subFolder1 && subFolder2)
  {
      var pos = parentFolder.getPosition(subFolder2);
      util.out(pos == 1);
      parentFolder.setPosition(subFolder1, -1);
      pos = parentFolder.getPosition(subFolder2);
      util.out(pos == 0);
  }
}
```
