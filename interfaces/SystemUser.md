[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / SystemUser

# Interface: SystemUser

**The SystemUser class has been added to the DOCUMENTS PortalScripting API to gain full access to the DOCUMENTS users by scripting means.**  

There are several functions implemented in different classes to retrieve a SystemUser object.

## Since

ELC 3.50b / otrisPORTAL 5.0b

## Properties

### ANNOTATIONS

> **ANNOTATIONS**: `number`

**Annotations right flag in the access mask.**  

**Note:** The access mask is returned by SystemUser.getAccess(DocFile)

#### See

[SystemUser.getAccess](#getaccess)

***

### ARCHIVE

> **ARCHIVE**: `number`

**Archive right flag in the access mask.**  

The bit that specifies the right to archive files.  

**Note:** The access mask is returned by SystemUser.getAccess(DocFile)

#### See

[SystemUser.getAccess](#getaccess)

***

### CHANGE\_TYPE

> **CHANGE\_TYPE**: `number`

**Change filetype right flag in the access mask.**  

The bit that specifies the right to change the filetype of a file.  

**Note:** The access mask is returned by SystemUser.getAccess(DocFile)

#### See

[SystemUser.getAccess](#getaccess)

***

### CHANGE\_WORKFLOW

> **CHANGE\_WORKFLOW**: `number`

**Change workflow right flag in the access mask.**  

The bit that specifies the right to change a workflow assigned to a file.  

**Note:** The access mask is returned by SystemUser.getAccess(DocFile)

#### See

[SystemUser.getAccess](#getaccess)

***

### COPY

> **COPY**: `number`

**Copy right flag in the access mask.**  

The bit that specifies the right to copy files to a personal or public folder.  

**Note:** The access mask is returned by SystemUser.getAccess(DocFile)

#### See

[SystemUser.getAccess](#getaccess)

***

### CREATE

> **CREATE**: `number`

**Create right flag in the access mask.**  

The bit that specifies the right to create new files.  

**Note:** The access mask is returned by SystemUser.getAccess(DocFile)

#### See

[SystemUser.getAccess](#getaccess)

***

### CREATE\_WORKFLOW

> **CREATE\_WORKFLOW**: `number`

**Create workflow right flag in the access mask.**  

**Note:** The access mask is returned by SystemUser.getAccess(DocFile)

#### See

[SystemUser.getAccess](#getaccess)

***

### email

> **email**: `string`

**String value containing the email address of the SystemUser.**

#### Since

DOCUMENTS 5.0a

***

### firstName

> **firstName**: `string`

**String value containing the first name of the SystemUser.**

#### Since

ELC 3.50b / otrisPORTAL 5.0b

***

### lastName

> **lastName**: `string`

**String value containing the last name of the SystemUser.**

#### Since

ELC 3.50b / otrisPORTAL 5.0b

***

### login

> **login**: `string`

**String value containing the unique login name of the SystemUser.**

#### Since

ELC 3.50b / otrisPORTAL 5.0b

***

### MAIL

> **MAIL**: `number`

**Mail right flag in the access mask.**  

The bit that specifies the right to send files via an e-mail system.  

**Note:** The access mask is returned by SystemUser.getAccess(DocFile)

#### See

[SystemUser.getAccess](#getaccess)

***

### MOVE

> **MOVE**: `number`

**Move right flag in the access mask.**  

The bit that specifies the right to move files to a personal or public folder.  

**Note:** The access mask is returned by SystemUser.getAccess(DocFile)

#### See

[SystemUser.getAccess](#getaccess)

***

### PDF

> **PDF**: `number`

**Create PDF right flag in the access mask.**  

The bit that specifies the right to create a PDF of a file.  

**Note:** The access mask is returned by SystemUser.getAccess(DocFile)

#### See

[SystemUser.getAccess](#getaccess)

***

### propCache

> **propCache**: [`PropertyCache`](PropertyCache.md)

**Access to the property cache of the SystemUser.**

#### Since

DOCUMENTS 5.0

#### See

[PropertyCache](PropertyCache.md)  
[AccessProfile.propCache](../classes/AccessProfile.md#propcache)

#### Example

```ts
var user = context.getSystemUser();
if (!user.propCache.hasProperty("Contacts"))
{
   util.out("Creating cache");
   user.propCache.Contacts = ["Peter", "Paul", "Marry"];
}
```

***

### READ

> **READ**: `number`

**Read right flag in the access mask.**  

The bit that specifies the right to see files.  

**Note:** the access mask is returned by SystemUser.getAccess(DocFile)

#### See

[SystemUser.getAccess](#getaccess)

***

### REMOVE

> **REMOVE**: `number`

**Remove right flag in the access mask.**  

The bit that specifies the right to delete files.  

**Note:** the access mask is returned by SystemUser.getAccess(DocFile)

#### See

[SystemUser.getAccess](#getaccess)

***

### START\_WORKFLOW

> **START\_WORKFLOW**: `number`

**Start workflow flag in the access mask.**  

**Note:** The access mask is returned by SystemUser.getAccess(DocFile)

#### See

[SystemUser.getAccess](#getaccess)

***

### VERSION

> **VERSION**: `number`

**Versioning right flag in the access mask.**  

**Note:** The access mask is returned by SystemUser.getAccess(DocFile)

#### See

[SystemUser.getAccess](#getaccess)

***

### WRITE

> **WRITE**: `number`

**Write right flag in the access mask.**  

The bit that specifies the right for changing index fields or documents in files.

**Note:** the access mask is returned by SystemUser.getAccess(DocFile)

#### See

[SystemUser.getAccess](#getaccess)

## Methods

### addCustomProperty()

> **addCustomProperty**(`name`, `type`, `value`): [`CustomProperty`](CustomProperty.md)

**Creates a new CustomProperty for the user.**

#### Parameters

##### name

`string`

String value defining the name

##### type

`string`

String value defining the type

##### value

`string`

String value defining the value

#### Returns

[`CustomProperty`](CustomProperty.md)

CustomProperty

#### Since

DOCUMENTS 4.0a

#### See

[SystemUser.setOrAddCustomProperty](#setoraddcustomproperty)  
[SystemUser.getCustomProperties](#getcustomproperties)

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser) throw "currentUser is NULL";
var custProp = currentUser.addCustomProperty("favorites", "string", "peachit");
if (!custProp)
  util.out(currentUser.getLastError());
```

***

### addFileTypeAgent()

> **addFileTypeAgent**(`fileTypes`, `loginNames`): `boolean`

**Create file type agents for the user.**

#### Parameters

##### fileTypes

The desired file types may be passed as follows: 
<ul> 
<li>String containing the technical name of the desired file type; </li> 
<li>Array of strings containing the technical names of the desired file types; </li> 
<li>String constant "*" indicating all file types. </li> 
</ul>

`string` | `string`[]

##### loginNames

`string`[]

Array of strings containing the login names of the agents.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0a

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser) throw "currentUser is NULL";
var loginNames = new Array();
loginNames.push("user1");
loginNames.push("user2");
if (!currentUser.addFileTypeAgent("testFileType", loginNames))
   util.out("Error: " + currentUser.getLastError());
else
   util.out("OK.");
```

***

### addFileTypeAgentScript()

> **addFileTypeAgentScript**(`fileTypes`, `scriptName`): `boolean`

**Create file type agents for the user, whereby the agents are specified by the desired script.**

#### Parameters

##### fileTypes

The desired file types may be passed as follows: 
<ul> 
<li>String containing the technical name of the desired file type; </li> 
<li>Array of strings containing the technical names of the desired file types; </li> 
<li>String constant "*" indicating all file types. </li> 
</ul>

`string` | `string`[]

##### scriptName

`string`

String containing the name of the script specifying the file type agents.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0a

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser) throw "currentUser is NULL";
if (!currentUser.addFileTypeAgentScript("*", "testScript"))
   util.out("Error: " + currentUser.getLastError());
else
   util.out("OK.");
```

***

### addToAccessProfile()

> **addToAccessProfile**(`ap`): `boolean`

**Make the SystemUser a member of the desired AccessProfile.**  

**Note:** If the user is already logged in, it is necessary to invalidate the cache of the user 
s. [SystemUser.invalidateAccessProfileCache()](#invalidateaccessprofilecache)  
  
**Since:** ELC 3.50b / otrisPORTAL 5.0b for PartnerAccounts  
**Since:** DOCUMENTS 4.0b HF1 for Fellows

#### Parameters

##### ap

[`AccessProfile`](../classes/AccessProfile.md)

AccessProfile the user should be a member of

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50b / otrisPORTAL 5.0b

***

### checkPassword()

> **checkPassword**(`passwd`): `boolean`

**Evaluate if the password is correct.**

#### Parameters

##### passwd

`string`

String value containing the plain password

#### Returns

`boolean`

`true` if correct, otherwise `false`

#### Since

ELC 3.60d / otrisPORTAL 6.0d

***

### delegateFilesOfAbsentUser()

> **delegateFilesOfAbsentUser**(): `boolean`

**Move the files from the inbox of an absent user to his agent.**  

If a Systemuser is set to absent, then all new files are redirected to his agent. The currently existing files 
(that came into the inbox before the was absent) can be moved to the agent with this method. If the user is 
not absent this method returns an error.

#### Returns

`boolean`

`true` if succeeded, otherwise `false` - an error message describing the error with getLastError().

#### Since

ELC 3.60g / otrisPORTAL 6.0g

#### See

[setAbsent](#setabsent)  
[setAbsentMail](#setabsentmail)  
SystemUserIteratorgetAgents

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser) throw "currentUser is NULL";
if (!currentUser.delegateFilesOfAbsentUser())
   util.out("Error: " + currentUser.getLastError());
else
   util.out("OK.");
```

***

### delegateFilesToUser()

> **delegateFilesToUser**(`login`): `number`

**Move the files from the inbox of a user to another user.**

#### Parameters

##### login

`string`

String containing the login name of the user the files moved to.

#### Returns

`number`

Count of the files moved to the desired user or -1 in case of any error.

#### Since

DOCUMENTS 6.0

#### See

[delegateFilesOfAbsentUser](#delegatefilesofabsentuser)

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser) throw "currentUser is NULL";
var count = currentUser.delegateFilesToUser("anotherUser");
if ( count == -1)
   util.out("Error: " + currentUser.getLastError());
else
   util.out("Count of delegated files: " + count);
```

***

### generateAPIKey()

> **generateAPIKey**(`label`, `deviceInfo`): `object`

Creates an API key.

#### Parameters

##### label

`any`

An arbitrary name for the client application.

##### deviceInfo

`any`

An arbitrary description for the client device.

#### Returns

`object`

***

### getAbsentFrom()

> **getAbsentFrom**(): `Date`

**Retrieve the configured start date of absence.**

#### Returns

`Date`

Date object representing when the absence begins.

#### Since

DOCUMENTS 5.0g

#### See

[setAbsent](#setabsent)

***

### getAbsentMessage()

> **getAbsentMessage**(): `string`

**Get the absence message.**

#### Returns

`string`

String with the absence message.

#### Since

DOCUMENTS 5.0g

#### See

[setAbsentMail](#setabsentmail)  
[setAbsent](#setabsent)

***

### getAbsentUntil()

> **getAbsentUntil**(): `Date`

**Retrieve the configured end date of absence.**

#### Returns

`Date`

Date object representing when the absence ends.

#### Since

DOCUMENTS 5.0g

#### See

[setAbsent](#setabsent)

***

### getAccess()

> **getAccess**(`docFile`): `number`

**Retrieve an access mask whose bits correspond to the user's access rights supported by the given DocFile or filetype.**  

**Note:** There is a constant for any right flag in the access mask (e.g. SystemUser.READ specifies the read right).

#### Parameters

##### docFile

[`DocFile`](DocFile.md)

DocFile object to which the access rights should be retrieved.

#### Returns

`number`

32-bit value whose bits correspond to the user's access rights.

#### Since

DOCUMENTS 5.0a HF2

#### See

e.g. [SystemUser.READ](#read)

#### Example

```ts
var docFile = context.file;
var currentUser = context.getSystemUser();
if (!currentUser)
    throw "currentUser is NULL";
var accessMask = currentUser.getAccess(docFile);
if(SystemUser.READ & accessMask)
    util.out("The user " + currentUser.login + " has read access!");
```

***

### getAccessProfiles()

> **getAccessProfiles**(): [`AccessProfileIterator`](AccessProfileIterator.md)

**Retrieve an [AccessProfileIterator](AccessProfileIterator.md) representing a list of all AccessProfiles the user is a member of.**

#### Returns

[`AccessProfileIterator`](AccessProfileIterator.md)

AccessProfileIterator containing a list of all AccessProfiles which are assigned to the user; `null` in case of any error

#### Since

ELC 3.50b / otrisPORTAL 5.0b

***

### getAgents()

> **getAgents**(): [`SystemUserIterator`](SystemUserIterator.md)

**Get a [SystemUserIterator](SystemUserIterator.md) with the agents of the user.**  

This method returns a SystemUserIterator with the agents of the user, if the user is absent.

#### Returns

[`SystemUserIterator`](SystemUserIterator.md)

SystemUserIterator

#### Since

ELC 3.60g / otrisPORTAL 6.0g

#### See

[setAbsent](#setabsent)  
[setAbsentMail](#setabsentmail)  
[delegateFilesOfAbsentUser](#delegatefilesofabsentuser)

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser) throw "currentUser is NULL";
var itSU = currentUser.getAgents();
for (var su = itSU.first(); su; su = itSU.next())
{
   util.out(su.login);
}
```

***

### getAllFolders()

> **getAllFolders**(): [`FolderIterator`](FolderIterator.md)

**Retrieve a list of private and public Folders of the Systemuser.**

#### Returns

[`FolderIterator`](FolderIterator.md)

FolderIterator containing a list of the folders.

#### Since

DOCUMENTS 5.0c

#### See

[SystemUser.getAllFolders](#getallfolders)

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser)
  throw "currentUser is null";
var folderIter = currentUser.getAllFolders();
```

***

### getAPIKeyLevel()

> **getAPIKeyLevel**(): `string`

Returns the value of the property ApiKeyAuthentication.

#### Returns

`string`

***

### getAPIKeys()

> **getAPIKeys**(): `object`[]

Returns all API keys as array.

#### Returns

`object`[]

***

### getAttribute()

> **getAttribute**(`attribute`): `string`

**Get the String value of an attribute of the SystemUser.**

#### Parameters

##### attribute

`string`

String containing the name of the desired attribute

#### Returns

`string`

String containing the value of the desired attribute

#### Since

ELC 3.50b / otrisPORTAL 5.0b

***

### getBackDelegatedFiles()

> **getBackDelegatedFiles**(`removeFromAgentInbox`): `boolean`

**Get back the delegated files.**  

If the user is not present this method returns an error.

#### Parameters

##### removeFromAgentInbox

`boolean`

Optional boolean indicating whether the files are removed from agent inbox after getting back by the user. 
If this parameter is not specified, the value from the user settings in the absent dialog on the web is used.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0d

#### See

[setAbsent](#setabsent)  
[delegateFilesOfAbsentUser](#delegatefilesofabsentuser)

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser) throw "currentUser is NULL";
if (!currentUser.getBackDelegatedFiles(true))
   util.out("Error: " + currentUser.getLastError());
else
   util.out("OK.");
```

***

### getCustomProperties()

> **getCustomProperties**(`nameFilter?`, `typeFilter?`): [`CustomPropertyIterator`](CustomPropertyIterator.md)

**Get a [CustomPropertyIterator](CustomPropertyIterator.md) with all [CustomProperty](CustomProperty.md) of the user.**  

This method returns a CustomPropertyIterator with the CustomProperty of the user.

#### Parameters

##### nameFilter?

`string`

String value defining an optional filter depending on the name

##### typeFilter?

`string`

String value defining an optional filter depending on the type

#### Returns

[`CustomPropertyIterator`](CustomPropertyIterator.md)

CustomPropertyIterator

#### Since

DOCUMENTS 4.0a

#### See

[context.findCustomProperties](Context.md#findcustomproperties)  
[SystemUser.setOrAddCustomProperty](#setoraddcustomproperty)  
[SystemUser.addCustomProperty](#addcustomproperty)

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser) throw "currentUser is NULL";
var itProp = currentUser.getCustomProperties();
for (var prop = itProp.first(); prop; prop = itProp.next())
{
   util.out(prop.name + ": " + prop.value);
}
```

***

### getIndividualFolders()

> **getIndividualFolders**(): [`FolderIterator`](FolderIterator.md)

**Retrieve a list of individual Folders of the Systemuser.**

#### Returns

[`FolderIterator`](FolderIterator.md)

FolderIterator containing a list of all individual folders.

#### Since

DOCUMENTS 4.0d

#### See

[SystemUser.getPrivateFolder](#getprivatefolder)

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser)
  throw "currentUser is null";
var folderIter = currentUser.getIndividualFolders();
```

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

ELC 3.50b / otrisPORTAL 5.0b

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
If `true` only the id of the Systemuser object (`m_oid`) will be returned.   
If `false` the id of the Systemuser object will be returned together with the id of the corresponding class in the form `class-id:m_oid`.   

**Default:** `false`

#### Returns

`string`

`String` with the object-id

#### Since

ELC 3.60c / otrisPORTAL 6.0c

***

### getPrivateFolder()

> **getPrivateFolder**(`folderType`): [`Folder`](Folder.md)

**Try to retrieve a particular private [Folder](Folder.md) of the Systemuser.**  

In addition to the public folders you may define in DOCUMENTS, each DOCUMENTS user has a set of private folders. 
You might need to access a particular private folder to access its contents, for example.

#### Parameters

##### folderType

`string`

String value defining the kind of private folder you want to access.  
You may choose between 

+ `"individual"` individual folder   

  **Note:** This function returns only the first individual folder on the top level. Using 
  [SystemUser.getIndividualFolders()](#getindividualfolders) to retrieve all individual folders.
+ `"favorites"` favorites folder
+ `"inbox"` the user's inbox
+ `"sent"` the user's sent folder
+ `"sendingfinished"` user's folder containing files which finished their workflow
+ `"inwork"` folder containing the files the SystemUser created himself 
+ `"resubmission"` folder containing files with a resubmission defined for the SystemUser
+ `"trash"` folder containing files the user has deleted 
+ `"tasks"` folder containing all files the user has a task to perform to
+ `"lastused"` folder containing the files the SystemUser accessed latest, sorted in descending chronological order 
+ `"introuble"` folder containing files which ran into some workflow error. This folder is only available for editors 
  and only if it has been added manually by the administrator.

#### Returns

[`Folder`](Folder.md)

Folder object representing the desired folder, `null` in case of any error

#### Since

ELC 3.51b / otrisPORTAL 5.1b

#### See

[SystemUser.getIndividualFolders](#getindividualfolders)

***

### getSendAbsenceMail()

> **getSendAbsenceMail**(): `boolean`

**Gather information whether an absence mail will be sent.**  

If the Systemuser is absent and get a file in the inbox, an absence mail to the sender of this file can be send.

#### Returns

`boolean`

`true` if an absence mail will be sent, otherwise `false`.

#### Since

DOCUMENTS 5.0g

#### See

[setAbsentMail](#setabsentmail)  
[setAbsent](#setabsent)

***

### getSkill()

> **getSkill**(`skill`): `number`

**`Internal`**

**Returns, if a skill is assigned to a user.**

#### Parameters

##### skill

`string`

String value containing the name of the skill

#### Returns

`number`

Number (0/1) if a skill is assigend

#### Since

DOCUMENTS 6.1.1

#### Example

```ts
var currentUser = context.getSystemUser();
const userHasAI = user.getSkill("AI") == 1;
```

***

### getStatus()

> **getStatus**(): `string`

**Get the status of the SystemUser.**

#### Returns

`string`

String with the value of the status

#### Since

DOCUMENTS 5.0g

#### See

[SystemUser.setStatus](#setstatus)

***

### getSuperior()

> **getSuperior**(): `SystemUser`

**Get the SystemUser object representing the superior of the user.**

#### Returns

`SystemUser`

SystemUser object representing the superior or `null` if no superior available

#### Since

ELC 3.50b / otrisPORTAL 5.0b

***

### getUserdefinedInboxFolders()

> **getUserdefinedInboxFolders**(): [`FolderIterator`](FolderIterator.md)

**Retrieve a list of userdefined inbox Folders of the Systemuser.**

#### Returns

[`FolderIterator`](FolderIterator.md)

FolderIterator containing a list of all userdefined inbox folders.

#### Since

DOCUMENTS 4.0d

#### See

[SystemUser.getPrivateFolder](#getprivatefolder)

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser)
  throw "currentUser is null";
var folderIter = currentUser.getUserdefinedInboxFolders();
```

***

### hasAccessProfile()

> **hasAccessProfile**(`profileName`): `boolean`

**Retrieve information whether the SystemUser is a member of a particular [AccessProfile](../classes/AccessProfile.md) which is identified by its technical name.**

#### Parameters

##### profileName

`string`

String value containing the technical name of an AccessProfile

#### Returns

`boolean`

`true` if the SystemUser is a member of the desired profile, otherwise `false`

#### Since

ELC 3.50e / otrisPORTAL 5.0e

***

### invalidateAccessProfileCache()

> **invalidateAccessProfileCache**(): `boolean`

**Invalidates the server sided cache of the access profiles for the SystemUser.**

#### Returns

`boolean`

`true` if successful, otherwise `false`

#### Since

DOCUMENTS 4.0 (HF1)

***

### invalidateFolderCache()

> **invalidateFolderCache**(): `boolean`

**Invalidates the server sided cache of the folders for the SystemUser.**

#### Returns

`boolean`

`true` if successful, otherwise `false`

#### Since

DOCUMENTS 5.0g (HF2)

***

### isAbsent()

> **isAbsent**(): `boolean`

**Gather information whether the current user is absent.**

#### Returns

`boolean`

`true` if the user is absent, otherwise `false`.

#### Since

DOCUMENTS 5.0g

#### See

[setAbsent](#setabsent)

***

### ~~isSuperUser()~~

> **isSuperUser**(): `boolean`

**Returns, if the "Superuser"-flag is actually set at the SystemUser.**

#### Returns

`boolean`

`true` or `false`

#### Since

DOCUMENTS 5.0b HF2

#### See

[SystemUser.setSuperUser](#setsuperuser)

#### Deprecated

since DOCUMENTS 5.0e HF2 - Use Context.setSuperMode(boolean value) / Context.getSuperMode() instead

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser) throw "currentUser is NULL";
util.out(currentUser.isSuperUser());
```

***

### listAgentFileTypes()

> **listAgentFileTypes**(): `string`[]

**Retrieve a list of file types for that an agent exists.**

#### Returns

`string`[]

The technical names of the file types. If the agent was set for all filetypes 
by calling `SystemUser.addFileTypeAgent`, the returned array only contains the string "&#42;".

#### Since

DOCUMENTS 5.0a

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser) throw "currentUser is NULL";
var fileTypes = currentUser.listAgentFileTypes();
if (fileTypes)
{
   for (var i=0; i < fileTypes.length; i++)
   {
      util.out(fileTypes[i]);
    }
}
else
   util.out("Error: " + currentUser.getLastError());
```

***

### listFileTypeAgents()

> **listFileTypeAgents**(`fileType`): `string`[]

**Retrieve a list of all agents for the desired file type of the user.**

#### Parameters

##### fileType

String containing the technical name of the file type.

`string` | `string`[]

#### Returns

`string`[]

Array of strings containing login names of all agents for the desired file type.

#### Since

DOCUMENTS 5.0a

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser) throw "currentUser is NULL";
var loginNames = currentUser.listFileTypeAgents("testFileType");
if (loginNames)
{
   for (var i=0; i < loginNames.length; i++)
   {
      util.out(loginNames[i]);
    }
}
else
   util.out("Error: " + currentUser.getLastError());
```

***

### notifyFileReturnedFromSending()

> **notifyFileReturnedFromSending**(`notifying?`): `boolean`

**Define whether to notify the user by e-mail of files returned from sending.**

#### Parameters

##### notifying?

`boolean`

boolean indicating whether files returned from sending are to be notified to the user.  

**Default:** `true`

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0a

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser) throw "currentUser is NULL";
if (!currentUser.notifyFileReturnedFromSending(true))
   util.out("Error: " + currentUser.getLastError());
else
   util.out("OK.");
```

***

### notifyNewFileInInbox()

> **notifyNewFileInInbox**(`notifying?`): `boolean`

**Define whether to notify the user by e-mail of new files in inbox.**

#### Parameters

##### notifying?

`boolean`

boolean indicating whether new files in inbox are to be notified to the user.

**Default:** `true`

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0a

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser) throw "currentUser is NULL";
if (!currentUser.notifyNewFileInInbox(true))
   util.out("Error: " + currentUser.getLastError());
else
   util.out("OK.");
```

***

### pdo()

> **pdo**(): `PDObject`

**`Internal`**

**Function returns the PDObject of the SystemUser.**  

This function is for internal use only!

#### Returns

`PDObject`

PDObject, in case of an error an exception will be thrown

#### Since

DOCUMENTS 5.0f HF1

***

### removeAPIKey()

> **removeAPIKey**(`id`): `void`

removes the API-Key with the given id

#### Parameters

##### id

`string`

The id of the API-Key that should be removed

#### Returns

`void`

***

### removeFileTypeAgent()

> **removeFileTypeAgent**(`fileTypes`): `boolean`

**Remove file type agents from the user.**

#### Parameters

##### fileTypes

The desired file types may be passed as follows: 
<ul> 
<li>String containing the technical name of the desired file type; </li> 
<li>Array of strings containing the technical names of the desired file types; </li> 
<li>String constant "*" indicating all file types. </li> 
</ul>

`string` | `string`[]

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0a

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser) throw "currentUser is NULL";
var fileTypes = new Array();
fileTypes.push("Filetype1");
fileTypes.push("Filetype2");
if (!currentUser.removeFileTypeAgent(fileTypes))
   util.out("Error: " + currentUser.getLastError());
else
   util.out("OK.");
```

***

### removeFromAccessProfile()

> **removeFromAccessProfile**(`ap`): `boolean`

**Clear the SystemUser's membership in the given AccessProfile.**  

**Note:** If the user is already logged in, it is necessary to invalidate the cache of the user 
s. [SystemUser.invalidateAccessProfileCache()](#invalidateaccessprofilecache)  

**Since:** ELC 3.50b / otrisPORTAL 5.0b for PartnerAccounts  
**Since:** DOCUMENTS 4.0b HF1 for Fellows

#### Parameters

##### ap

[`AccessProfile`](../classes/AccessProfile.md)

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50b / otrisPORTAL 5.0b

***

### resetSuperior()

> **resetSuperior**(): `boolean`

**Clear the user's relation to a superior.**

#### Returns

`boolean`

true if successful, false in case of any error

#### Since

ELC 3.50b / otrisPORTAL 5.0b

***

### setAbsent()

> **setAbsent**(`absent`, `filesDueAbsenceToInfo?`, `agents?`, `removeFromAgentInbox?`, `from?`, `until?`): `boolean`

**Set a Systemuser absent or present.**  

If a Systemuser is on holiday with this function it is possible to set the user absent. After his return you can set him present. 
You can also define one or more agents for the absent user. The agent will get new files for the absent user in substitution. 
With the agent list you set the agents for the user (you overwrite the existing agents!). With an empty agent list you remove all agents.  
  
**Since:** DOCUMENTS 4.0d (Option: removeFromAgentInbox)   
**Since:** DOCUMENTS 5.0a (Option: from and until)

#### Parameters

##### absent

`boolean`

boolean `true`, if the user should be set absent, `false`, if the user is present

##### filesDueAbsenceToInfo?

`boolean`

boolean set to `true`, if the user should get the files due absence to info in his inbox  

**Default:** `true`

##### agents?

`string`[]

Array with the login-names of the agents  

**Default:** `[]`

##### removeFromAgentInbox?

`boolean`

Optional boolean indicating whether the files are removed from agent inbox after getting back by the user. If this parameter is not specified, 
the value from the user settings in the absent dialog on the web is used.  

**Default:** `false`

##### from?

`Date`

Optional Date object specifying when the absence begins.

##### until?

`Date`

Optional Date object specifying when the absence ends.

#### Returns

`boolean`

`true` if correct, otherwise `false` an error message describing the error with getLastError().

#### Since

ELC 3.60g / otrisPORTAL 6.0g

#### See

[setAbsentMail](#setabsentmail)  
[delegateFilesOfAbsentUser](#delegatefilesofabsentuser)  
[getBackDelegatedFiles](#getbackdelegatedfiles)  
[SystemUserIterator](SystemUserIterator.md)  
[getAgents](#getagents)

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser) throw "currentUser is NULL";
// set user absent
var agents = new Array();
agents.push("oppen");
agents.push("buch");
var from = new Date();
var until = context.addTimeInterval(from, 3, "days", false);
if (!currentUser.setAbsent(true, false, agents, true, from, until))
   util.out("Error: " + currentUser.getLastError());
else
   util.out("OK.");
// set user present
if (!currentUser.setAbsent(false))
   util.out("Error: " + currentUser.getLastError());
else
   util.out("OK.");
```

***

### setAbsentMail()

> **setAbsentMail**(`sendMail`, `message?`): `boolean`

**Define if an absence mail for the absent user will be sent to the sender of the file.**  

If a Systemuser is absent and get a file in the inbox, an absence mail to the sender of this file can be send.

#### Parameters

##### sendMail

`boolean`

boolean `true`, if an absent mail should be sent, otherwise `false`

##### message?

`string`

String with an additional e-mail message from the absent user

#### Returns

`boolean`

`true` if succeeded, otherwise `false` - an error message describing the error with getLastError().

#### Since

ELC 3.60g / otrisPORTAL 6.0g

#### See

[setAbsent](#setabsent)  
[delegateFilesOfAbsentUser](#delegatefilesofabsentuser)  
[SystemUserIterator](SystemUserIterator.md)  
[getAgents](#getagents)

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser) throw "currentUser is NULL";
if (!currentUser.setAbsentMail(true, "I will be back on 12/31 2009"))
   util.out("Error: " + currentUser.getLastError());
else
   util.out("OK.");
```

***

### setAccessProfiles()

> **setAccessProfiles**(`apNames1`, `apNames2`, ...`restParams`): `boolean`

**Set the AccessProfiles for an user.**  

All existing AccessProfiles will be removed and the AccessProfiles from the parameters will be set.

#### Parameters

##### apNames1

`any`

String or Array with the names of the AccessProfiles

##### apNames2

`any`

String or Array with the names of the AccessProfiles

##### restParams

...`any`[]

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0c HF2

#### Example

```ts
var val1 = ["AP1", "AP2"];
var val2 = "AP3\r\nAP4";
var user = context.getSystemUser();
if (!user.setAccessProfiles(val1, val2))
   throw user.getLastError();
```

***

### setAttribute()

> **setAttribute**(`attribute`, `value`): `boolean`

**Set the String value of an attribute of the SystemUser to the desired value.**

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

ELC 3.50b / otrisPORTAL 5.0b

***

### setEasywareAuthentication()

> **setEasywareAuthentication**(`value`): `boolean`

**Turn EASYWARE Authentication on or off.**

#### Parameters

##### value

`boolean`

boolean `true` to turn authentication on `false` to turn it off.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0c HF2

***

### setOrAddCustomProperty()

> **setOrAddCustomProperty**(`name`, `type`, `value`): [`CustomProperty`](CustomProperty.md)

**Creates a new CustomProperty or modifies a CustomProperty according the name and type for the user.**  

This method creates or modifies a unique CustomProperty for the user. The combination of the name and the type make the CustomProperty unique for the user.

#### Parameters

##### name

`string`

String value defining the name

##### type

`string`

String value defining the type

##### value

`string`

String value defining the value

#### Returns

[`CustomProperty`](CustomProperty.md)

CustomProperty

#### Since

DOCUMENTS 4.0a

#### See

[SystemUser.getCustomProperties](#getcustomproperties)  
[SystemUser.addCustomProperty](#addcustomproperty)

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser) throw "currentUser is NULL";
var custProp = currentUser.setOrAddCustomProperty("superior", "string", "oppen");
if (!custProp)
  util.out(currentUser.getLastError());
```

***

### setPassword()

> **setPassword**(`newPwd`, `checkRestriction?`): `boolean`

**Set the password of the user represented by the SystemUser object to the desired new value.**

#### Parameters

##### newPwd

`string`

String containing the plaintext new password

##### checkRestriction?

`boolean`

boolean if true, check if password is strong (see property StrongPasswords)

**Default:** `false`

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50b / otrisPORTAL 5.0b

***

### setSkill()

> **setSkill**(`skill`, `value`): `boolean`

**`Internal`**

**Assign or remove a skill to a user.**

#### Parameters

##### skill

`string`

String value containing the name of the skill

##### value

`number`

Number (0/1) containing the value

#### Returns

`boolean`

true if successful, false in case of any error

#### Since

DOCUMENTS 6.1.1

#### See

[SystemUser.getSkill](#getskill)  
[context.getSkillLicense](Context.md#getskilllicense)

#### Example

```ts
var currentUser = context.getSystemUser();
const succ = currentUser.setSkill("AI", 1);
if (!succ)
   throw currentUser.getLastError();   // maybe there is no more free license
```

***

### setStatus()

> **setStatus**(`status`): `boolean`

**Set the status of the SystemUser.**

#### Parameters

##### status

`string`

String with the desired value of the status. There are following values available: 
 
+ `inherited`
+ `released` 
+ `registered` 
+ `blocked` 
+ `removable`

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0g

#### See

[SystemUser.getStatus](#getstatus)

#### Example

```ts
var currUser = context.getSystemUser();
if (!currUser.setStatus("released"))
  throw currUser.getLastError();
```

***

### setSuperior()

> **setSuperior**(`sup`): `boolean`

**Set the SystemUser object representing the superior of the user to the desired object.**

#### Parameters

##### sup

`SystemUser`

Systemuser object representing the new superior of the user

#### Returns

`boolean`

true if successful, false in case of any error

#### Since

ELC 3.50b / otrisPORTAL 5.0b

***

### ~~setSuperUser()~~

> **setSuperUser**(`value`): `void`

**Set and unset "Superuser"-flag at the SystemUser.**  

The method gives "superrights" to the user and overrules the DOCUMENTS right management. e.g. if you use (G)ACL in a filetype, 
the Superuser will find all files, independed from the content of the ACL field...

#### Parameters

##### value

`boolean`

boolean to set / unset superuser-flag

#### Returns

`void`

#### Since

DOCUMENTS 4.0a HF2

#### Deprecated

since DOCUMENTS 5.0e HF2 - Use Context.setSuperMode(boolean value) instead

#### Example

```ts
var currentUser = context.getSystemUser();
if (!currentUser) throw "currentUser is NULL";
currentUser.setSuperUser(true);
// do something with super rights
currentUser.setSuperUser(false);  // Important: unset the rights!
```
