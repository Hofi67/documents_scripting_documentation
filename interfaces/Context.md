[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / Context

# Interface: Context

**This class can be used to access the most important attributes and methods for customizing
DOCUMENTS with PortalScripting.**  

There is exactly ONE implicit object of this class which is named [\`context\`](../variables/context.md).
This implicit object is the root object in any script. With the [\`context\`](../variables/context.md) object
you are able to access to the different DOCUMENTS objects like DocFile, Folder etc. Some
of the attributes are only available under certain conditions. It depends on the execution
context of the PortalScript, whether a certain attribute is accessible or not. For example,
[\`context.selectedFiles\`](#selectedfiles) is available in a folder userdefined
action script, but not in a script used as a signal exit.

## Properties

### actionName

> **actionName**: `string`

**Technical name of the user defined action the script is executed for.**

#### Since

DOCUMENTS 5.0f

#### Example

```ts
util.out(context.actionName);
```

***

### clientId

> **clientId**: `string`

**Id of the client / thread which is the execution context of the script.**  

This property is helpful to identify the clients at scripts running concurrently (for debugging purposes).

#### Since

ELC 3.51e / otrisPORTAL 5.1e

#### Example

```ts
util.out(context.clientId);
```

***

### currentUser

> **currentUser**: `string`

**Login of the user who has triggered the script execution.**  

If the script is running e.g. as action in the workflow the user is the logged in user, who has initiated the action.

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
util.out(context.currentUser);
```

***

### document

> **document**: [`Document`](Document.md)

**Document object representing the current document that the script is executed at.**  

**Note:** If the script is not executed in a document context then the return value is `null`.

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
var doc = context.document;
```

***

### errorMessage

> **errorMessage**: `string`

**Error message text to be returned by the script.**  

The error message will be displayed as Javascript alert box in the web client if the script is called in context of a web client.  

**Note:** You can get and set this property.

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
context.errorMessage = "You are not authorized to run this script";
return -1; // neccessary to indicate an error
```

***

### event

> **event**: [`EventType`](../type-aliases/EventType.md)

**Event which triggered the script execution.**  

According to the context where the portal script has been called this property contains a key name for this event.

#### Since

ELC 3.50n / otrisPORTAL 5.0n

#### Example

```ts
if (context.event == "fileAction")
{
    util.out("Action at the file");
}
```

***

### fieldName

> **fieldName**: `string`

**Returns in an enumeration script the name of the field where the script is executed for.**  

If the script is an enumeration script, this member contains the field name of the current field where the script is executed. 
This is particularly helpful when the script is set at more than one enumeration field and the behaviour of the script should depend on the field.

#### Since

DOCUMENTS 5.0c HF2

***

### file

> **file**: [`DocFile`](DocFile.md)

**DocFile object representing the current file that the script is executed at.**  

**Note:** If the script is not executed in a file context then the return value is `null`.

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
var file = context.file;
```

***

### fileType

> **fileType**: `string`

**Technical name of the filetype of the file which is the execution context of the script.**  

This property contains the technical name of the filetype of the file which is the execution context of the script.

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### See

[context.file](#file)

#### Example

```ts
util.out(context.fileType);
```

***

### folder

> **folder**: [`Folder`](Folder.md)

**Current folder in which context the script is running.**

#### Since

DOCUMENTS 5.0d

#### Example

```ts
var folder = context.folder;
```

***

### folderFiles

> **folderFiles**: [`FileResultset`](../classes/FileResultset.md)

**FileResultset with all files of a folder.**  

This property allows to retrieve a list of all files of a folder if this script is run as user defined action at the folder. 
You can then iterate through this list for further use of the distinct files.  

**Note:** If there is no file inside the folder you will receive a valid empty FileResultset.

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
var it = context.folderFiles;
```

***

### folderName

> **folderName**: `string`

**Technical name of the folder the script is called from.**  

This property contains the technical name of the folder which is the execution context of the script.

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
util.out(context.folderName);
```

***

### principalId

> `readonly` **principalId**: `string`

**`Internal`**

**Id of the current principal.**

***

### qsession

> **qsession**: `string`

**Session id of the current query-session.**

#### Since

DOCUMENTS 5.0d HF1

***

### register

> **register**: [`Register`](Register.md)

**Register object representing the current register that the script is executed at.**  

**Note:** If the script is not executed in a register context then the return value is `null`.

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
var reg = context.register;
```

***

### repositoryCount

> **repositoryCount**: `Number`

**Amount of documents (binaries) in documents repository for the current principal.**  

The amount includes all versions of the documents.

#### Since

DOCUMENTS 5.0h HF1

***

### repositoryPath

> **repositoryPath**: `string`

**Path to the documents repository for the current principal.**

#### Since

DOCUMENTS 5.0h HF1

***

### repositorySize

> **repositorySize**: `Number`

**Size of documents repository for the current principal in bytes.**  

The size includes all versions of the documents.

#### Since

DOCUMENTS 5.0h HF1

***

### returnType

> **returnType**: `string`

**Type of the return value that the script returns.**  

The following list shows all available types.
Return value of type object is not allowed (use `JSON.stringify()` if necessary).

| **returnType** | **return Value** | **Description** |
|---|---|---|
| `"stay"` |  | Default behaviour. Show current file.   |
| `"updateFile"` |  | Show and update current file.   |
| `"html"` | **HTML** | Show the **HTML** |
| `"htmlpopup"` | **HTML** | Show the **HTML** in a dialog   |
| `"showFile"` | **fileId[**`&dlcRegisterId=`**registerId]** | Show the file   |
| `"showEditFile"` | **fileId** | Open the file in edit mode   |
| `"showNewFile"` | **fileId** | Open the file in edit mode and delete it on cancellation   |
| `"showFolder"` | **folderId** | Show the folder   |
| `"showOverview"` |  | Show the overview page   |
| `"updateTree"` | **folderId** | Show and update the folder   |
| `"file:filename"` | string with the content of the file  | Ask the user, if they want to download the content of the return value (usually a String variable). The filename `filename` will be proposed as a default.   |
| `"download:filename"` | string with path to th blob  | Ask the user, if they want to download the blob, that is specified in the return value (server-sided path to the blob). The filename `filename` will be proposed as a default.   |
| `"checkoutDocuments"` | `JSON.stringify({"fileId": "","registerId": "","documentId": "","openLocal": false})` | Checkout document and open it in edit mode   |
| `"clientScript"` | **JavaScript** code  | Execute the code   |
| `"destroyHitTree"` |  | Remove current **HitTree** from server cache. So after logout the **HitTree** won't be available anymore.   |
| `"gadget"` | Example: `JSON.stringify({gadgetScript:"Gadget_SimpleSample", gadgetAction: "initGadget"})` | Show **Gadget** in dialog   |
| `"hitTree"` |  | Show **HitTree** outbar   |
| `"openOutbar"` | Technical name of an outbar  | Show the outbar   |
| `"openAndReloadOutbar"` | Technical name of an outbar  | Show and reload the outbar   |
| `"refreshFolder"` | `JSON.stringify({folderId: "", selectedHit: ""})` | Refresh folder with id `folderId` or current folder if not set. The file in `selectedHit` will be selected.   |
| `"refreshScriptList"` |  | Refresh scriptlist by executing the referenced script.   |
| `"scriptList"` | Created scriptlist as JSON string  | Show the scriptlist   |
| `"treeChart"` | Treechart as JSON string  | Show the treechart   |
| `"multipleAction"` | Example: `JSON.stringify([{returnType: 'showFile', returnValue : fileId}, {returnType: 'html', returnValue : 'HTML-Code'}])` | Execute all actions specified in array. |

**Note:** You may read from and write to this property. For further information and examples see "HowTo-Sammlung" on otris.software.  
  
**Since:** DOCUMENTS 4.0c showFile with return value of file-id and register-id  
**Since:** ELC 3.50c / otrisPORTAL 5.0c showNewFile, updateTree, file

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Examples

```ts
// Example 1: showFile
context.returnType = "showFile";
var idFile = docFile.getAutoText("id");
return idFile;
```

```ts
// Example 2: showFile with specific register
context.returnType = "showFile";
var idFile = docFile.getAutoText("id");
var idRegister = docFile.getRegisterByName("internal_documents").getAttribute("id");
return idFile + "&dlcRegisterId=" + idRegister;
```

```ts
// Example 3:
var itFolders = context.getFoldersByName("Invoice");
var folder = itFolders.first();
if (folder == null)
{
   context.returnType = "html";
   return "<h1>Unable to find folder Invoice</h1>";
}
context.returnType = "showFolder";
return folder.id;
```

```ts
// Example 4:
var csv = "row11;row12;row13\n";
csv += "row21;row22;row23";
context.returnType = "file:example.csv";
return csv;
```

***

### returnValue

> **returnValue**: `null` \| `string` \| `number` \| `boolean`

**Set the return value of a PortalScript.**  

Until now the PortalScripts returns their return value by the `return` statement at the end of the script.
`return retvalue;` In DOCUMENTS 6 with the V8 JS-Engine, in script mode `Module` the `return` statement
is only allowed in the context of a function. Therefore, in this case it is no longer possible to use the
return statement in the "old" way. The return value has to be set as a property at the context object.
However, in script mode `Classic` the return statement can still be used at the end of the script, but
it is not recommended.

```
context.returnValue = retvalue;
```

In DOCUMENTS 5 `context.returnValue` is now supported since 5.0h HF1 and it is recommended to use this.
This makes your scripts compatible to run in DOCUMENTS 6.

#### Since

DOCUMENTS 5.0h HF1

#### Examples

```ts
// Example 1: "old" Documents 5 return value
...
var idFile = docFile.getid();
context.returnType = "showFile";
return idFile;
```

```ts
// Example 2: "new" Documents 5/6 return value
...
var idFile = docFile.getid();
context.returnType = "showFile";
context.returnValue = idFile;
```

***

### scriptName

> **scriptName**: `string`

**Name of the executed script.**

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
util.out(context.scriptName);
```

***

### selectedArchiveFiles

> **selectedArchiveFiles**: [`ArchiveFileResultset`](../classes/ArchiveFileResultset.md)

**Iterator with the selected archive files of a folder.**  

This property allows to retrieve a list of the selected archive files of a folder if this script is run as user defined action at the folder. 
You can then iterate through this list for further use of the distinct files.  

**Note:** If there is no file selected you will receive a valid empty ArchiveFileResultset.

#### Since

ELC 3.60j / otrisPORTAL 6.0j

#### Example

```ts
var it = context.selectedArchiveFiles;
var archiveFile = it.first()
while (archiveFile)
{
   util.out(archiveFile.getAutoText("title"));
   archiveFile = it.next();
}
```

***

### selectedArchiveKeys

> **selectedArchiveKeys**: `string`[]

**Array with the keys of the selected archive files of a folder.**  

This property allows to retrieve an array with the keys of the selected archive files of a folder if this script is run as user defined action at the folder.  

**Note:** If there is no archive file selected you will receive a valid empty array.

#### Since

ELC 3.60j / otrisPORTAL 6.0j

#### Example

```ts
var keys = context.selectedArchiveKeys;
util.out(keys.length)
```

***

### selectedDocuments

> **selectedDocuments**: [`DocumentIterator`](DocumentIterator.md)

**DocumentIterator with the selected Documents (attachments) of the current document register.**  

This property allows to retrieve a list of all selected Documents of a register if this script is run as user defined action at the register.  

**Note:** If there is no document inside the Register you will receive a valid empty DocumentIterator.

#### Since

DOCUMENTS 4.0b HF1

#### Example

```ts
var it = context.selectedDocuments;
```

***

### selectedFiles

> **selectedFiles**: [`FileResultset`](../classes/FileResultset.md)

**Iterator with the selected files of a folder.**  

This property allows to retrieve a list of the selected files of a folder if this script is run as user defined action at the folder. 
You can then iterate through this list for further use of the distinct files.  

**Note:** If there is no file selected you will receive a valid empty FileResultset.

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
var it = context.selectedFiles;
```

***

### sourceCode

> **sourceCode**: `string`

**Script source code of the script after including other scripts by the #import rule.**  

This property is useful for debugging purposes, if you need to have a look for a certain line of code to find an error, 
but the script contains other imported sub scripts which mangle the line numbering.

#### Since

ELC 3.50b / otrisPORTAL 5.0b

#### Example

```ts
util.out(context.sourceCode);
```

***

### workflowActionId

> **workflowActionId**: `string`

**Id of the locking WorkflowStep for the user for the current file.**

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
util.out(context.workflowActionId);
```

***

### workflowActionName

> **workflowActionName**: `string`

**Name of the locking WorkflowStep for the user for the current file.**

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
util.out(context.workflowActionName);
```

***

### workflowControlFlowId

> **workflowControlFlowId**: `string`

**Id of the ControlFlow the current file currently passes.**

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
util.out(context.workflowControlFlowId);
```

***

### workflowControlFlowName

> **workflowControlFlowName**: `string`

**Name of the ControlFlow the current file currently passes.**

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
util.out(context.workflowControlFlowName);
```

***

### workflowStep

> **workflowStep**: [`WorkflowStep`](WorkflowStep.md)

**Returns the current workflowstep if the script is run in context of a workflow.**  

E.g. as guard or decision script.

#### Since

DOCUMENTS 5.0

## Methods

### addCustomProperty()

> **addCustomProperty**(`name`, `type`, `value`): [`CustomProperty`](CustomProperty.md)

**Creates a new global custom property.**

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

DOCUMENTS 5.0

#### See

[context.setOrAddCustomProperty](#setoraddcustomproperty)  
[context.getCustomProperties](#getcustomproperties)

#### Example

```ts
var custProp = context.addCustomProperty("favorites", "string", "peachit");
if (!custProp)
  util.out(context.getLastError());
```

***

### addTimeInterval()

> **addTimeInterval**(`ts`, `amount`, `unit?`, `useWorkCalendar?`): `Date`

**Adds a time interval to a Date object.**  

Since date manipulation in Javascript is odd sometimes, this useful function allows to conveniently add a given period of time to a given date, 
e.g. to calculate a due date based upon the current date plus `xx` days

#### Parameters

##### ts

`Date`

Date object to which the period of time should be added

##### amount

`number`

integer value of the period of time to be added

##### unit?

`string`

String value representing the time unit of the period of time.
You may use one of the following unit values:
+ `"minutes"`
+ `"hours"`
+ `"days"`
+ `"weeks"`
**Default:** `'minutes'`

##### useWorkCalendar?

`boolean`

`true` if work calendar should be taken into account, `false` if not. The work calendar has to be defined at Documents->Settings  
**Default:** `true`

#### Returns

`Date`

Date object with the new date.

#### Since

ELC 3.50e / otrisPORTAL 5.0e

#### See

[context.getDatesDiff](#getdatesdiff)  
[util.convertDateToString](Util.md#convertdatetostring)  
[util.convertStringToDate](Util.md#convertstringtodate)

#### Example

```ts
var actDate = new Date();  // actDate contains now the current date
var newDate = context.addTimeInterval(actDate, 14, "days", false);
util.out(newDate); // should  two weeks in the future
```

***

### changeScriptUser()

> **changeScriptUser**(`login`): `boolean`

**Change the user context of the PortalScript.**  

In some cases, especially if you make heavy use of access privileges both with files and file fields, 
it might be neccessary to run a script in a different user context than the user who triggered the script execution. 
For example, if the current user is not allowed to change any field values, a PortalScript running in this user's 
context will fail, if it tries to change a field value. In this case it is best practice to switch the user context 
to some superuser who is allowed to perform the restricted action before that restricted action is executed. You may 
change the script's user context as often as you need, a change only applies to the instructions following the `changeScriptUser()` call.

#### Parameters

##### login

`string`

String value containing the login name of the user to switch to. 
Since DOCUMENTS 6.2.0, an empty login makes the script user-less.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.51b / otrisPORTAL 5.1b

#### Example

```ts
var currentUserLogin = context.currentUser;
var success = context.changeScriptUser("schreiber");
// code runs now in the context of user "schreiber"
...
// switch back to the original user
success = context.changeScriptUser(currentUserLogin);
```

***

### clearEnumvalCache()

> **clearEnumvalCache**(`scriptName`): `boolean`

**Clears the cached enumval at the specified PortalScript.**

#### Parameters

##### scriptName

`string`

String with the name of the PortalScript

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0c HF1

#### Example

```ts
var ret = context.clearEnumvalCache("lcmGetAllUser");
if (!ret)
   util.out(context.getLastError());
```

***

### convertDateToString()

> **convertDateToString**(`dateOrTimeStamp`, `locale?`): `string`

**Convert a Date object representing a date into a String.**  

The output String is in the date format of the specified locale. If you leave the locale parameter away the current locale of the script context will be used.

#### Parameters

##### dateOrTimeStamp

`Date`

Date/Timestamp object representing the desired date

##### locale?

`string`

**Default:** `user locale`

#### Returns

`string`

#### Since

DOCUMENTS 4.0c HF1

#### See

[util.convertDateToString](Util.md#convertdatetostring)

#### Example

```ts
var date1 = new Date(2014, 1, 14);
util.out(context.convertDateToString(date1, "de"));
// Output: 14.02.2014
util.out(context.convertDateToString(date1));
// Output: depends on the locale of the script context
var date2 = new Date(2014, 1, 14, 12, 59);
util.out(context.convertDateToString(date2, "en"));
// Output: 02/14/2014  12:59
```

***

### convertNumericToString()

#### Call Signature

> **convertNumericToString**(`value`, `decimalSep`, `thousandSep`, `precision?`): `string`

**Converts a Number into a formatted String.**  

The output String may have any format you like. The parameters can be used to configure the format of the numeric String.

##### Parameters

###### value

`number`

Numeric object representing the number

###### decimalSep

`string`

Decimal-Separator as String

###### thousandSep

`string`

Thousand-Separator as String

###### precision?

`number`

Precision as number  
**Default:** `2`

##### Returns

`string`

String representing the desired number

##### Since

ELC 3.60c / otrisPORTAL 6.0c

##### See

[context.convertNumericToString](#convertnumerictostring)

##### Example

```ts
var numVal = 1000 * Math.PI;
util.out(context.convertNumericToString(numVal, ",", ".", 2));
Output: 3.141,59
```

#### Call Signature

> **convertNumericToString**(`value`, `locale?`, `precision?`): `string`

**Converts a Number into a formatted String.**  

The output String is formatted like the definition in the locale. If the locale is not defined by parameter, the locale of the current user will be used.

**Note:**
If the number is not formatted with a thousand-separator,
try setting the [groupingNumeric](../../../api/properties/index.html#groupingnumeric_dlcglobaloptions) property to `1`.

##### Parameters

###### value

`number`

Numeric object representing the number

###### locale?

`string`

Locale as String
**Default:** `user locale`

###### precision?

`number`

**Default:** `2`

##### Returns

`string`

String representing the desired number

##### Since

ELC 3.60c / otrisPORTAL 6.0c

##### See

[context.convertNumericToString](#convertnumerictostring)

##### Example

```ts
var numVal = 1000 * Math.PI;
util.out(context.convertNumericToString(numVal, "en", 2));
Output: 3,141.59
```

***

### convertStringToDate()

> **convertStringToDate**(`dateOrTimeStamp`, `locale?`): `Date`

**Convert a String representing a date into a Date object.**  

The output Date is in the date format of the specified locale. If you omit the locale parameter the current locale of the script context will be used.

#### Parameters

##### dateOrTimeStamp

`string`

String representing a date has to be formatted as the definition in the specified locale, e.g. "TT.MM.JJJJ" for the locale "de".

##### locale?

`string`

Optional String value with the locale abbreviation (according to the principal's configuration).

#### Returns

`Date`

#### Since

DOCUMENTS 5.0a HF2

#### See

[util.convertStringToDate](Util.md#convertstringtodate)

#### Example

```ts
var dateString = "19.09.1974";
var birthDay = context.convertStringToDate(dateString, "de");
```

***

### convertStringToNumeric()

#### Call Signature

> **convertStringToNumeric**(`numericValue`, `decimalSep`, `thousandSep`): `number`

**Converts a formated String into a number.**  

The input String may have any format you like. The following parameters defines the format to configure the format of the numeric String.

##### Parameters

###### numericValue

`string`

Formatted numeric String

###### decimalSep

`string`

Decimal-Separator as String

###### thousandSep

`string`

Thousand-Separator as String

##### Returns

`number`

the numeric number (float) or `null` if fail

##### Since

ELC 3.60c / otrisPORTAL 6.0c

##### See

[context.convertStringToNumeric](#convertstringtonumeric)

##### Example

```ts
var numString = "1.000,99";
var floatVal = context.convertStringToNumeric(numString, ",", ".");
```

#### Call Signature

> **convertStringToNumeric**(`numericValue`, `locale?`): `number`

**Converts a formated String into a number.**  

The input String has to be formatted like the definition in the locale. If the locale is not defined by parameter, the locale of the current user will be used.

##### Parameters

###### numericValue

`string`

Formatted numeric String

###### locale?

`string`

Locale as String  
**Default:** `userlocale`

##### Returns

`number`

the numeric number (float) or `null` if fail

##### Since

ELC 3.60c / otrisPORTAL 6.0c

##### See

[context.convertStringToNumeric](#convertstringtonumeric)

##### Example

```ts
var numString = "1,000.99";
var floatVal = context.convertStringToNumeric(numString, "en");
```

***

### copyFileType()

> **copyFileType**(`sourceFileTypeName`, `targetFileTypeName`, `released`): `boolean`

**Copy a file type.**

#### Parameters

##### sourceFileTypeName

`string`

String containing the technical name of the file type to be copied.

##### targetFileTypeName

`string`

Optional String containing the technical name of the file type copy. The default value is the `sourceFileTypeName` with the suffix "_copy".

##### released

`boolean`

Optional boolean indicating whether the copied file type should be released. The default value is `true`.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0f

#### Example

```ts
if (!context.copyFileType("myFileType", "fileTypeCopy"))
   util.out(contxt.getLastError());
```

***

### countPoolFiles()

> **countPoolFiles**(`fileType`): `number`

**Retrieve the amount of pool files of the specified filetype in the system.**  

**Note:** This function is only for experts.

#### Parameters

##### fileType

`string`

the technical name of the desired filetype

#### Returns

`number`

Integer amount of pool files

#### Since

ELC 3.50j / otrisPORTAL 5.0j

#### See

[context.createPoolFile](#createpoolfile)

#### Example

```ts
var fileType = "Standard"; // filetype
var poolSize = context.countPoolFiles(fileType); // amount of pool files
for (var i = poolSize; i < 3000; i++)
{
   context.createPoolFile(fileType);
}
```

***

### createAccessProfile()

> **createAccessProfile**(`profileName`): [`AccessProfile`](../classes/AccessProfile.md)

**Create a new access profile in the DOCUMENTS environment.**  

If the access profile already exist, the method returns an error.

#### Parameters

##### profileName

`string`

technical name of the access profile

#### Returns

[`AccessProfile`](../classes/AccessProfile.md)

AccessProfile object as a representation of the access profile in DOCUMENTS, `null` in case of any error

#### Since

ELC 3.60i / otrisPORTAL 6.0i

#### Example

```ts
var office = context.createAccessProfile("office");
if (!office)
   util.out(context.getLastError());
```

***

### createAlias()

> **createAlias**(`name`, `userLogin`): [`Alias`](Alias.md)

**Create a new Alias in the DOCUMENTS environment.**

#### Parameters

##### name

`string`

The name of the alias

##### userLogin

`string`

Login name of the SystemUser to be assigned to the alias.

#### Returns

[`Alias`](Alias.md)

The new created Alias object or `null` if failed.

#### Since

DOCUMENTS 5.0i HF6

***

### createArchiveServer()

> **createArchiveServer**(`name`, `type`): [`ArchiveServer`](ArchiveServer.md)

**Create a new ArchiveServer.**  

This function creates a new [ArchiveServer](ArchiveServer.md) for the specified archive software on the top level.
These types are available:
+ `EEI`
+ `EEX_native`
+ `EBIS_store`
+ `NOAH`
+ `None`

#### Parameters

##### name

`string`

The technical name of the ArchiveServer to be created.

##### type

`string`

The desired archive software of the ArchiveServer.

#### Returns

[`ArchiveServer`](ArchiveServer.md)

New created ArchiveServer object or `null` if failed.

#### Since

DOCUMENTS 5.0a

#### Example

```ts
var as = context.createArchiveServer("Invoice2016", "NOAH")   // EDA
if (as)
  util.out(as.name);
else
  util.out(context.getLastError());
```

***

### createFellow()

> **createFellow**(`loginName`, `isDlcUser`, `licenseType?`, `status?`): [`SystemUser`](SystemUser.md)

**`Internal`**

**Create a new fellow in the DOCUMENTS environment.**  

Internal: Internal Method!

#### Parameters

##### loginName

`string`

login of the fellow

##### isDlcUser

`boolean`

automatically grant DOCUMENTS access (true/false)

##### licenseType?

`string`

optional definition of the license type for that user 
(allowed values are `"named"`, `"concurrent_standard"`, `"concurrent_open"` and `"shared"` (deprecated: `"concurrent"`)  
**Default:** `'named'`

##### status?

`string`

optional definition of the status of new account (allowed value are `"released"` and `"blocked"`)  
**Default:** `'released'`

#### Returns

[`SystemUser`](SystemUser.md)

#### Since

DOCUMENTS 5.0i (new Parameter status)

***

### createFile()

> **createFile**\<`K`\>(`fileTypeName`, `jsonDefaultData?`): [`DefaultDocFileType`](../type-aliases/DefaultDocFileType.md)\<`K`\>

**Creates a new file of the specified FileType.**  

This function creates a new file object of the FileType with the given
`fileTypeName` and returns it.  
So the type of the returned object is the FileType that is specified in the parameter
`fileTypeName` and which is an extension of [DocFile](DocFile.md). In particular,
all field names of the FileType are available as properties on the returned object.

If an error occurs during creation of the file the return
value will be `null` and you can access an error message describing
the error with getLastError().  

Since the script is executed in the context of a particular user,
it is mandatory that user possesses sufficient access privileges to
create new instances of the desired FileType, otherwise the method will fail.  

**Note:**  
DOCUMENTS 5.0c HF1 and newer:  The function directly creates
a file for an EAS or EBIS store, if "@server" has been appended to the
filetype's name and if appropriate permissions are granted. In this case
the returned DocFile must be saved with
[DocFile.commit](DocFile.md#commit) instead of
[DocFile.sync](DocFile.md#sync).  
  
**Since:**  
DOCUMENTS 5.0c HF1 (support for EDA/EAS and EBIS stores)

#### Type Parameters

##### K

`K` *extends* `string`

#### Parameters

##### fileTypeName

`K`

Technincal name of the desired FileType

##### jsonDefaultData?

`string`

Optional json-String with an object with default-values for the fields of the created file

#### Returns

[`DefaultDocFileType`](../type-aliases/DefaultDocFileType.md)\<`K`\>

The new created file object or `null` if failed. The type of this object depends on the
parameter `fileTypeName` and is an extension of [DocFile](DocFile.md). See main description.

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
fileType: Person
field 1:
  Name: Lastname
  Defaultvalue: %data.foo1%
  Name: Firstname
  Defaultvalue: %data.foo2%
var defaultData = { foo1 : "Doe", foo2 : "John" };
var newFile = context.createFile("Standard", JSON.stringify(defaultData));
if (newFile)
   util.out(newFile.getAutoText("title"));
else
   util.out(context.getLastError());
```

***

### createFolder()

> **createFolder**(`name`, `type`): [`Folder`](Folder.md)

**Create a new folder of the specified type on the top level.**  

This function creates a new folder of the specified type on the top level. There are three types available:
+ `public`
+ `dynamicpublic`
+ `onlysubfolder`

#### Parameters

##### name

`string`

The technical name of the folder to be created.

##### type

`string`

The desired type of the folder.

#### Returns

[`Folder`](Folder.md)

New created folder as Folder object or `null` if failed.

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var folder = context.createFolder("myFolder", "public")
if (folder)
  util.out(folder.type);
else
  util.out(context.getLastError());
```

***

### createGlobalEnumeration()

> **createGlobalEnumeration**(`name`): [`GlobalEnumeration`](GlobalEnumeration.md)

**Create a new [GlobalEnumeration](GlobalEnumeration.md) in the DOCUMENTS environment.**

#### Parameters

##### name

`string`

The name of the GlobalEnumeration.

#### Returns

[`GlobalEnumeration`](GlobalEnumeration.md)

The new created GlobalEnumeration object or `null` if failed.

#### Since

DOCUMENTS 6.0.2

#### See

[context.deleteGlobalEnumeration](#deleteglobalenumeration)

***

### createPoolFile()

> **createPoolFile**(`fileType`): `boolean`

**Create a new pool file of the specified filetype.**  

The script must run in the context of a user who has sufficient access privileges to create new files of the specified filetype, otherwise this method will fail.

#### Parameters

##### fileType

`string`

the technical name of the desired filetype

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50j / otrisPORTAL 5.0j

#### See

[context.countPoolFiles](#countpoolfiles)

***

### createSystemUser()

> **createSystemUser**(`loginName`, `isDlcUser`, `licenseType?`, `status?`): [`SystemUser`](SystemUser.md)

**`Internal`**

**Create a new user in the DOCUMENTS environment.**  

Internal: Internal Method!

#### Parameters

##### loginName

`string`

login of the user

##### isDlcUser

`boolean`

automatically grant DOCUMENTS access (true/false)

##### licenseType?

`string`

optional definition of the license type for that user (allowed values are `"named"`, `"concurrent"` and `"shared"`)  
**Default:** `'named'`

##### status?

`string`

optional definition of the status of new account (allowed value are `"released"` and `"blocked"`)  
**Default:** `'released'`

#### Returns

[`SystemUser`](SystemUser.md)

#### Since

DOCUMENTS 5.0i (new Parameter status)

***

### deleteAccessProfile()

> **deleteAccessProfile**(`profileName`): `boolean`

**Delete a certain access profile in the DOCUMENTS environment.**

#### Parameters

##### profileName

`string`

technical name of the access profile

#### Returns

`boolean`

`true` in case of successful deletion, `false` in case of any error

#### Since

ELC 3.51b / otrisPORTAL 5.1b

#### Example

```ts
var profileName = "office"
var success = context.deleteAccessProfile(profileName);
if (success)
{
   util.out("Deletion of access profile " + profileName + " successful");
}
```

***

### deleteFolder()

> **deleteFolder**(`folderObj`): `boolean`

**Delete a folder in DOCUMENTS.**

#### Parameters

##### folderObj

[`Folder`](Folder.md)

an object of the Class Folder which represents the according folder in DOCUMENTS

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50l01 / otrisPORTAL 5.0l01

#### Example

```ts
var itFD = context.getFoldersByName("Invoice");
var fd = itFD.first();
if (fd)
{
   var success = context.deleteFolder(fd);
}
```

***

### deleteGlobalEnumeration()

> **deleteGlobalEnumeration**(`name`): `boolean`

**Delete a [GlobalEnumeration](GlobalEnumeration.md) in the DOCUMENTS environment.**

#### Parameters

##### name

`string`

The name of the GlobalEnumeration.

#### Returns

`boolean`

`true` if the deletion was successful, `false` in case of any error

#### Since

DOCUMENTS 6.0.2

#### See

[context.createGlobalEnumeration](#createglobalenumeration)

#### Example

```ts
var name = "testEnum";
var success = context.deleteGlobalEnumeration(name);
if (success)
{
   util.out("Successfully deleted GlobalEnumeration " + name);
}
```

***

### deleteSystemUser()

> **deleteSystemUser**(`loginName`): `boolean`

**Delete a user in the DOCUMENTS environment.**

#### Parameters

##### loginName

`string`

login of the user

#### Returns

`boolean`

`true` if the deletion was successful, `false` in case of any error

#### Since

ELC 3.50e / otrisPORTAL 5.0e

#### See

[context.createSystemUser](#createsystemuser)

#### Example

```ts
var login = "schreiber";
var success = context.deleteSystemUser(login);
if (success)
{
   util.out("Successfully deleted user " + login);
}
```

***

### doMaintenance()

> **doMaintenance**(`operationName`): `string`

**Calls the specified maintenance operation.**

#### Parameters

##### operationName

`string`

String with the name of the maintenance operation

#### Returns

`string`

`String` with the return message of the of the maintenance operation.

#### Since

DOCUMENTS 5.0c HF1

#### Example

```ts
var msg = context.doMaintenance("BuildAclCache lcmContract");
util.out(msg);
```

***

### enableModules()

> **enableModules**(`root?`, `flags?`): `void`

**Allow dynamic imports of other scripts as modules.**  

This function defines a function named `require()`, either in a passed object or in the global scope of the calling script.
In sequence `require`('<scriptname>') can be used to import other portal scripts, which are implemented in the style of
CommonJS (Node.js) modules.  

**Note:**  
Usually only top-level scripts call enableModules(). They should call it only once. Scripts loaded by require()
always see the function as a global parameter. DOCUMENTS exposes a generic 'module' and an initially empty 'exports'
object to each imported script. Virtually no other features of the module concept of Node.js are available.
Since DOCUMENTS 5.0i the module objects have got a readonly property "filename". In DOCUMENTS 5 this is a plain
script name. DOCUMENTS 6 will preferably return a virtual path like "/db/testPrincipal/myScriptCategory/myScriptName.js".
If the "documents.ini" contains the setting "$JSGlobalModule 1", enableModules() will create a main module object,
if no global variable 'module' is already defined. Presumably DOCUMENTS 6 will define a global module always.   
 
To customize the behaviour of the require() function the following flags may be set.
(Use one of the operators '|' or '+' to combine multiple flags.)

+ 1 = ignore ".js" or ".JS" extensions appended to the passed script name
+ 2 = ignore file paths prepended to the script name

The require() implementation saves the flags passed to enableModules() before a new module is loaded. It restores them
afterwards. This allows local overrides of the import flags, as shown in the second example. However, if require() is
called directly or indirectly from an exported function, local flag overrides generally do not work. When the importing
script calls the exported function, the embedded call of require() occurs with the flags set by the importing script,
not with the modules's local flags.  
  
**Since:** DOCUMENTS 5.0f (flags parameter)   
**Since:** DOCUMENTS 5.0i (main module creation, property "module.filename")

#### Parameters

##### root?

`Object`

An optional Object to define the require() function as a property. Use this parameter, if the name "require"
is already reserved in the script's global namespace.

##### flags?

`number`

An optional integer number containing a bit mask with special options. Defaults to 0.  
**Default:** `0`

#### Returns

`void`

undefined.

#### Since

DOCUMENTS 5.0d

#### Examples

```ts
// The main script
context.enableModules();
var mymath = require('MyMath');
var test = mymath.square(42);
util.out("square(42) is " + test);
// End of main script
// The 'MyMath' module script
// "module.exports" is initially an empty object.
// require() will return whatever the script places here.
//
// "exports" is a shortcut reference to "module.exports".
// This works as long as only properties need to be added.
// Directly assigning a new value to "exports" or
// "module.exports" would break the reference.
exports.square = function(x) { return x*x; };
// End of module script
```

```ts
// Excerpt from main script
context.enableModules(undefined, 1);
var firstModule = require('Module1.js'); // extension ".js" will be ignored
var someOtherModule = require('Module2.js'); // ".js" will be ignored again
// Excerpt from 'Module1' module script
// override import flags for local imports of this module
// DOCUMENTS will reset them after initialization of the module.
context.enableModules(undefined, 2);
var submodule1 = require("C:/anywhere/Module3"); // Path will be ignored
exports.square = function(x) { return x*x; };
// But don't rely on overridden flags within an exported function!
// This is a negative example.
exports.error_prone = function {
  // This raises an error when called from the main script: path is not ignored.
  var otherMod = require("C:/anywhere/Module4");
  // any more code ...
}
// End of module script
```

***

### exportList()

> **exportList**(`inJSON`): `string`

**Creates an xlsx from the given JSON-Data and returns the path to the xlsx.**

The JSON-String represents a table and has the following structure:
```json
{
   "exporttype" : export-format,
   "labels" : [column1-label, column2-label, ...],
   "datatypes" : [column1-datatype, column2-datatype, ...],
   "data" : [
     	       [data11, data12, ...],
     	       [data21, data22, ...],
                ...
            ]
}
```

+ `exporttype`: type of the exported format, currently only the type `xlsx` is available
+ `labels`: array of labels for columns
+ `datatypes`: array of data types for columns. The following types are avaiable: `string`, `date`, `timestamp` and `numeric`.
+ `data`: array of arrays - each array specify one line in the table

#### Parameters

##### inJSON

`string`

JSON-String containing the data to be exported.

#### Returns

`string`

String containing the path to the xlsx file, an empty string in case of any error.

#### Since

DOCUMENTS 5.0i HF5

#### Example

```ts
var inJSON = {};
inJSON.exporttype = "xlsx";
inJSON.labels    = ["Title", "Date", "Time", "Amount", "Comment"];
inJSON.datatypes = ["string", "date", "timestamp", "numeric", "string"];
inJSON.data = [
     	       ["Title1", "12/01/2023", "12/01/2023  15:01", "1.000,99", "Comment 1"],
     	       ["Title2", "12/02/2023", "12/02/2023  15:02", "2.000", "Comment 2"],
     	       ["Title3", "12/03/2023", "12/03/2023  15:03", "3000", "Comment 3"]
              ];

var filepath = context.exportList(JSON.stringify(inJSON));
if (filepath == "")
   throw context.getLastError();

context.returnValue = filepath;
```

***

### extCall()

> **extCall**(`workDir`, `cmd`, `synced`): `number`

**Perform an external command shell call on the Portalserver.**  

Executes an external command shell call (usually a batch file or shell script) in the context of the given work directory. 
With the `synced` parameter, you can specify if the scripting engine should wait for the external call to complete or 
if the script execution should continue asynchonously. If the script waits for the external call to complete, this method 
returns the errorcode of the external call as an integer value (see note for Linux).  

**Note:** On Linux, the return value contains some more information. You can see in the example, how you can get the exit status on Linux.

#### Parameters

##### workDir

`string`

String containing a complete directory path which should be used as the working directory

##### cmd

`string`

String containing the full path and filename to the file to execute

##### synced

`boolean`

boolean value that defines, if the script should wait for the external call to finish (`true`) or not (`false`)

#### Returns

`number`

number containing the errorcode (ERRORLEVEL) of the call (see note for Linux).

#### Since

ELC 3.51 / otrisPORTAL 5.1

#### Example

```ts
// execute testrun.bat in "c:\tmp" and wait for the call to complete
var errorLevel = context.extCall("c:\\tmp", "c:\\tmp\\testrun.bat", true);
util.out(errorLevel);
// get exit status on linux
var ret = context.extCall("/tmp", "/tmp/testrun", true);
var exitStatus = (ret & 0xff00) >> 8;
```

***

### extProcess()

> **extProcess**(`cmd`, `timeout?`): `string`[]

**Perform an external process call on the Portalserver and returns the exitcode of the external process and the standard output.**  

An external process call is executed, e.g. a batch file. The methods returns a string array of the size 2. 
The first array value is the exit code (converted to its equivalent string representation) of the external process. 
The second array value contains the content that the external process has written to the standard output.  
  
**Since:** DOCUMENTS 5.0i new optional parameter timeout

#### Parameters

##### cmd

`string`

String containing the full path and filename to the program which shall be executed

##### timeout?

`number`

Number in milliseconds  
**Default:** `0`

#### Returns

`string`[]

a string array with the exit code and the content of the standard output; at timeout the exitcode = -99

#### Since

ELC 3.60g / otrisPORTAL 6.0g

#### Example

```ts
// execute testrun.bat and wait for the call to complete
var res = context.extProcess("c:\\tmp\\testrun.bat");
var exitcode = res[0];
var stdout = res[1];
if (exitcode !== "0")
  util.out(exitcode + ": " + stdout);
```

***

### findAccessProfile()

> **findAccessProfile**(`profileName`): [`AccessProfile`](../classes/AccessProfile.md)

**Find a certain access profile in the DOCUMENTS environment.**

#### Parameters

##### profileName

`string`

technical name of the access profile

#### Returns

[`AccessProfile`](../classes/AccessProfile.md)

AccessProfile object as a representation of the access profile in DOCUMENTS, `null` in case of any error

#### Since

ELC 3.50b / otrisPORTAL 5.0b

#### Example

```ts
var office = context.findAccessProfile("office");
```

***

### findCustomProperties()

> **findCustomProperties**(`filter`): [`CustomPropertyIterator`](CustomPropertyIterator.md)

**Searches for CustomProperties.**

#### Parameters

##### filter

`string`

Optional String value defining the search filter (specification see example)

#### Returns

[`CustomPropertyIterator`](CustomPropertyIterator.md)

CustomPropertyIterator

#### Since

DOCUMENTS 5.0

#### See

[context.getCustomProperties](#getcustomproperties)  
[AccessProfile.getCustomProperties](../classes/AccessProfile.md#getcustomproperties)  
[SystemUser.getCustomProperties](SystemUser.md#getcustomproperties)

#### Example

```ts
// Specification of the filter:
// ----------------------------
// Possible filter-columns:
// name: String - name of the custom property
// type: String - type of the custom property
// to_Systemuser:    Integer (oid-low) - connected SystemUser
// to_AccessProfile: Integer (oid-low) - connected AccessProfile
// to_DlcFile      : Integer (oid-low) - connected Filetype
//
// Operators:
// &&: AND
// ||: OR
var oidUser = context.findSystemUser("schreiber").getOID(true);
var oidAP1 = context.findAccessProfile("Service").getOID(true);
var oidAP2 = context.findAccessProfile("Customer").getOID(true);
var oidFileType = context.getFileTypeOID("ftRecord", true);
var filter = "name='Prop1'";
filter += "&& to_Systemuser=" + oidUser;
filter += "&& (to_AccessProfile=" + oidAP1 + " || to_AccessProfile=" + oidAP2 + ")";
filter += "&& to_DlcFile =" + oidFileType;
var it = context.findCustomProperties(filter);
for (var cp=it.first(); cp; cp=it.next())
{
   util.out(cp.value);
}
```

***

### findLogBookEntries()

> **findLogBookEntries**(`filter?`, `sortOrder?`): `string`

**Searches for log book entries.**  

**Since:** DOCUMENTS 5.0i HF10 (optional parameter `sortOrder`)

#### Parameters

##### filter?

`string`

Optional String value defining the search filter (specification see example)

##### sortOrder?

`string`

String containing an optional sort order; use empty String ('') if you don't want to sort at all

#### Returns

`string`

String containing the JSON string with all log book entries matching the filter

#### Since

DOCUMENTS 5.0h HF1

#### See

[context.writeLogBook](#writelogbook)

#### Example

```ts
// Specification of the filter:
// ----------------------------
// Possible filter-columns:
// Ts: Timestamp - Timestamp of the creation of the entry (using special format 'fyyyymmddHHMMSS' for the filter value)
// UserLogin: String - Login of the responsible user
// TitleFile: String - Title of the file
// IdFile: String - Id of the file
// FieldValues: String - A log book entry defined on the file type
// TitleFileType: String - Title of the file type
// IdFileType: String - Id of the file type
// IdWorkflow: String - Id of the workflow within the file being circulated
// MainContextName: String - Name of the workflow template
// IdMainContext: String - Id of the workflow template
// IdStep: String - Id of the workflow step
// ContextName: String - Display name of the workflow action
// IdContext: String - Id of the workflow action
// ActionCode : Integer - Integer code of the executed action (see Context.writeLogBook() for more information)
// ActionDescription: String - Description of the executed action (see Context.writeLogBook() for more information)
// ActionDetail1: String - Additional information
// ActionDetail2: String - Additional information
// ActionDetail3: String - Additional information
//
// Operators:
// &&: AND
// ||: OR
var filter = "Ts <= 'f20220121092256'";
filter += "&& Ts >= 'f20220111092256'";
filter += "&& IdFile = 'peachitreg_fi20220000000193'";
filter += "&& (ActionCode = 7 || ActionCode = 6)";
var jsonStr = context.findLogBookEntries(filter, "Ts-");
var jsonArr = JSON.parse(jsonStr);
for (var entry of jsonArr)
{
    util.out("-------------------");
    for (var prop in entry)
    {
        util.out(prop + ": " + entry[prop]);
    }
    util.out("-------------------");
}
```

***

### findSystemUser()

> **findSystemUser**(`login`): [`SystemUser`](SystemUser.md)

**Retrieve a user by his/her login.**  

If the user does not exist, then the return value will be `null`.

#### Parameters

##### login

`string`

name of the user

#### Returns

[`SystemUser`](SystemUser.md)

User as SystemUser object

#### Since

ELC 3.50b / otrisPORTAL 5.0b

#### See

[context.findSystemUserByAlias](#findsystemuserbyalias)  
[context.getSystemUser](#getsystemuser)  
[context.getSystemUsers](#getsystemusers)  
[AccessProfile.getSystemUsers](../classes/AccessProfile.md#getsystemusers)

#### Example

```ts
var myUser = context.findSystemUser("schreiber");
```

***

### findSystemUserByAlias()

> **findSystemUserByAlias**(`alias`): [`SystemUser`](SystemUser.md)

**Retrieve a user by an alias name.**  

If the alias does not exist or is not connected to a user then the return value will be `null`.

#### Parameters

##### alias

`string`

technical name of the desired alias

#### Returns

[`SystemUser`](SystemUser.md)

User as SystemUser object

#### Since

ELC 3.51c / otrisPORTAL 5.1c

#### See

[context.findSystemUser](#findsystemuser)  
[context.getSystemUser](#getsystemuser)  
[context.getSystemUsers](#getsystemusers)

#### Example

```ts
var myUser = context.findSystemUserByAlias("CEO");
```

***

### findSystemUserByLoginAlias()

> **findSystemUserByLoginAlias**(`loginAlias`): [`SystemUser`](SystemUser.md)

**Retrieve a user by a login alias.**  
A login alias for a user can be set via the Systemuser property `loginAlias`.
If the login alias does not exist then the return value will be `null`.

#### Parameters

##### loginAlias

`string`

The desired login alias for a user.

#### Returns

[`SystemUser`](SystemUser.md)

User as SystemUser object or `null` if no user found.

#### Since

DOCUMENTS 5.0i HF5

#### See

[context.findSystemUserByAlias(alias)](#findsystemuserbyalias)

#### Example

```ts
var myUser = context.findSystemUserByLoginAlias("myLoginAlias");
```

***

### getAccessProfiles()

> **getAccessProfiles**(`includeInvisibleProfiles?`): [`AccessProfileIterator`](AccessProfileIterator.md)

**Get an iterator with all access profiles of in the DOCUMENTS environment.**  

**Note:** This method can only return access profiles which are checkmarked as being visible in DOCUMENTS lists.  
  
**Since:** ELC 3.60e / otrisPORTAL 6.0e (new parameter includeInvisibleProfiles)

#### Parameters

##### includeInvisibleProfiles?

`boolean`

optional boolean value to define, if access profiles that are not checkmarked as being visible in DOCUMENTS lists should be included  
**Default:** `false`

#### Returns

[`AccessProfileIterator`](AccessProfileIterator.md)

AccessProfileIterator object with all AccessProfile in DOCUMENTS

#### Since

ELC 3.51g / otrisPORTAL 5.1g

#### Example

```ts
var itAP = context.getAccessProfiles(false);
for (var ap = itAP.first(); ap; ap = itAP.next())
{
   util.out(ap.name);
}
```

***

### getActionByName()

> **getActionByName**(`actionName`): [`UserAction`](../classes/UserAction.md)

**Retrieve a global user-defined action.**

#### Parameters

##### actionName

`string`

String value containing the desired action name.

#### Returns

[`UserAction`](../classes/UserAction.md)

UserAction object representing the user-defined action.

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var action = context.getActionByName("testAction");
if (action)
{
   action.type = "PortalScript";
   action.setPortalScript("testScript");
}
else
   util.out(context.getLastError());
```

***

### getAliasByName()

> **getAliasByName**(`name`): [`Alias`](Alias.md)

**Get an Alias object by its name.**

#### Parameters

##### name

`string`

The name of the desired Alias.

#### Returns

[`Alias`](Alias.md)

An Alias object if successful, `null` in case of any error.

#### Since

DOCUMENTS 5.0i HF7

***

### getAllAliases()

> **getAllAliases**(): [`AliasIterator`](AliasIterator.md)

**Get an AliasIterator with all aliases in DOCUMENTS.**

#### Returns

[`AliasIterator`](AliasIterator.md)

AliasIterator

#### Since

DOCUMENTS 5.0i HF7

#### Example

```ts
var it = context.getAllAliases();
for (var alias of it)
{
   // do something
}
```

***

### getAllLockedDocumentsInfo()

> **getAllLockedDocumentsInfo**(): `string`

**Retrieve the information of all locked documents as JSON string.**

#### Returns

`string`

JSON string containing the information of all locked documents

#### Since

DOCUMENTS 6.0

***

### getAllWorkflows()

> **getAllWorkflows**(`typeFlags?`): [`WorkflowIterator`](WorkflowIterator.md)

**List all available Workflows.**  

Create a [WorkflowIterator](WorkflowIterator.md), which contains references to all available Workflows and distribution lists.  

**Note:**  
typeFlags Parameter supports any combination of the following values.

| Bit # | Value | Meaning                              |
|-------|-------|--------------------------------------|
| 0     | 1     | Enumerate simple distribution lists  |
| 1     | 2     | Enumerate complete workflows         |

The bits not listed above should remain zero for upward compatibility. Hint for beginners: flag values
are always powers of 2. They can be combined with "|" or with "+". The expression (1|2|8) evaluates
to 11 for example.  

**Note:**  
See the WorkflowIterator class description for an example.

#### Parameters

##### typeFlags?

`number`

An optional integer number, which specifies the requested types of Workflow objects (see remarks). The default value is 2.

#### Returns

[`WorkflowIterator`](WorkflowIterator.md)

A new WorkflowIterator.

#### Since

DOCUMENTS 6.0

***

### getArchiveConnection()

> **getArchiveConnection**(`archiveServerName`): [`ArchiveConnection`](ArchiveConnection.md)

**Get an [ArchiveConnection](ArchiveConnection.md) object.**  

With this method you can get an ArchiveConnection object. This object offers several methods to use the EAS Interface, EBIS or the EASY ENTERPRISE XML-Server.

#### Parameters

##### archiveServerName

`string`

Optional string containing the archive server name; If the archive server is not defined, then the main archive server will be used

#### Returns

[`ArchiveConnection`](ArchiveConnection.md)

ArchiveConnection-Object or `null`, if failed

#### Since

DOCUMENTS 5.0a

#### See

[ArchiveServer.getArchiveConnection](ArchiveServer.md#getarchiveconnection)

#### Example

```ts
var xmlserver = context.getArchiveConnection("myeex")
if (!xmlserver) // failed
   util.out(context.getLastError());
else
{
   ...
}
```

***

### getArchiveFile()

> **getArchiveFile**(`key`): [`DocFile`](DocFile.md)

**Get a file from the archive.**  

With this method you can get a file from the archive using the archive key. You need the necessary access rights on the archive side.

#### Parameters

##### key

`string`

#### Returns

[`DocFile`](DocFile.md)

`DocFile` or `null`, if failed

#### Since

ELC 3.60e / otrisPORTAL 6.0e

#### Example

```ts
var key = "Unit=Default/Instance=Default/Pool=DEMO/Pool=PRESSE/Document=Waz.4E1D1F7E28C611DD9EE2000C29FACDC2@eex1";
var file = context.getArchiveFile(key)
if (!file) // failed
   util.out(context.getLastError());
else
{
   ...
}
```

***

### getArchiveServer()

> **getArchiveServer**(`name`): [`ArchiveServer`](ArchiveServer.md)

**Get an [ArchiveServer](ArchiveServer.md) identified by its name.**

#### Parameters

##### name

`string`

The technical name of the ArchiveServer.

#### Returns

[`ArchiveServer`](ArchiveServer.md)

ArchiveServer object or `null` if failed.

#### Since

DOCUMENTS 5.0a

#### Example

```ts
var as = context.getArchiveServer("ebis1");
if (as)
   util.out(as.name);
```

***

### getArchiveServers()

> **getArchiveServers**(): [`ArchiveServerIterator`](ArchiveServerIterator.md)

**Get an iterator with all ArchiveServers in the DOCUMENTS environment.**

#### Returns

[`ArchiveServerIterator`](ArchiveServerIterator.md)

#### Since

DOCUMENTS 5.0a

#### Example

```ts
var itAS = context.getArchiveServers();
for (var as = itAS.first(); as; as = itAS.next())
{
   util.out(as.name);
}
```

***

### getAutoText()

> **getAutoText**(`autoText`, `startTag?`, `endTag?`): `string`

**Get the String value of a DOCUMENTS autotext.**  
 
  
**Since:** DOCUMENTS 5.0i new optional parameters startTag and endTag

#### Parameters

##### autoText

`string`

the rule to be parsed

##### startTag?

`string`

optional start tag.  
**Default:** `"%"`

##### endTag?

`string`

otional end tag.  
**Default:** `"%"`

#### Returns

`string`

String containing the parsed value of the autotext

#### Since

ELC 3.50e / otrisPORTAL 5.0e

#### Example

```ts
util.out(context.getAutoText("currentDate"));
```

***

### getClientLang()

> **getClientLang**(): `string`

**Get the abbreviation of the current user's portal language.**  

If you want to return output messages through scripting, taking into account that your users might use different portal languages, 
this function is useful to gain knowledge about the portal language used by the current user, who is part of the script's runtime context. 
This function returns the current language as the two letter abbreviation as defined in the principal's settings in the Windows Portal Client (e.g. "de" for German).

#### Returns

`string`

String containing the abbreviation of the current user's portal language

#### Since

ELC 3.51 / otrisPORTAL 5.1

#### See

[context.setClientLang](#setclientlang)   
[context.getEnumErgValue](#getenumergvalue)   
[context.getFieldErgName](#getfieldergname)  
[context.getFileTypeErgName](#getfiletypeergname)  
[context.getEnumValues](#getenumvalues)   
[context.getFromSystemTable](#getfromsystemtable)

#### Example

```ts
util.out(context.getClientLang());
```

***

### getClientSystemLang()

> **getClientSystemLang**(): `number`

**Get the script's execution context portal language index.**

#### Returns

`number`

integer value of the index of the current system language

#### Since

ELC 3.51g / otrisPORTAL 5.1g

#### See

[context.getEnumErgValue](#getenumergvalue)  
[context.getFieldErgName](#getfieldergname)   
[context.getFileTypeErgName](#getfiletypeergname)   
[context.getEnumValues](#getenumvalues)  
[context.getFromSystemTable](#getfromsystemtable)

#### Example

```ts
util.out(context.getClientSystemLang());
var erg = context.setClientSystemLang(0); // first portal language
```

***

### getClientType()

> **getClientType**(): `string`

**Get the connection info of the client connection.**  

You can analyze the connection info to identify e.g. a client thread of the HTML5 Web-Client 
` HTML5-Client:   CL[Windows 7/Java 1.7.0_76], POOL[SingleConnector], INF[SID[ua:docsclient, 
dca:2.0, docs_cv:5.0]] Classic-Client: CL[Windows 7/Java 1.7.0_76], POOL[SingleConnector] SOAP-Client:    
Documents-SOAP-Proxy (In-Server-Client-Library) on Win32 `

#### Returns

`string`

String containing the connection info

#### Since

DOCUMENTS 5.0

#### Example

```ts
function isHTML5Client()
{
    return context.getClientType().indexOf("docs_cv:5.0") > -1;
}
if (isHTML5Client())
   util.out("HTML5-Client");
else
   util.out("NO HTML5-Client");
```

***

### getCurrentUserAttribute()

> **getCurrentUserAttribute**(`attributeName`): `string`

**Get the String value of an attribute of the current user.**

#### Parameters

##### attributeName

`string`

the technical name of the desired attribute

#### Returns

`string`

String containing the value of the attribute

#### Since

ELC 3.50f / otrisPORTAL 5.0f

#### See

[context.getPrincipalAttribute](#getprincipalattribute)  
[context.setPrincipalAttribute](#setprincipalattribute)

#### Example

```ts
util.out(context.getCurrentUserAttribute("particulars.lastName"));
```

***

### getCustomProperties()

> **getCustomProperties**(`nameFilter?`, `typeFilter?`): [`CustomPropertyIterator`](CustomPropertyIterator.md)

**Get a CustomPropertyIterator with global custom properties.**

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

DOCUMENTS 5.0

#### See

[context.findCustomProperties](#findcustomproperties)   
[context.setOrAddCustomProperty](#setoraddcustomproperty)   
[context.addCustomProperty](#addcustomproperty)

#### Example

```ts
var itProp = context.getCustomProperties();
for (var prop = itProp.first(); prop; prop = itProp.next())
{
   util.out(prop.name + ": " + prop.value);
}
```

***

### getDatesDiff()

> **getDatesDiff**(`earlierDate`, `laterDate`, `unit?`, `useWorkCalendar?`): `number`

**Subtract two Date objects to get their difference.**  

This function calculates the time difference between two Date objects, for example if you need to know how many days a business trip takes. 
By default this function takes the work calendar into account if it is configured and enabled for the principal.

#### Parameters

##### earlierDate

`Date`

Date object representing the earlier date

##### laterDate

`Date`

Date object representing the later date

##### unit?

`string`

optional String value defining the unit, allowed values are `"minutes"`, `"hours"` and `"days"` (default)  
**Default:** `'days'`

##### useWorkCalendar?

`boolean`

optional boolean to take office hours into account or not (requires enabled and configured work calendar)  
**Default:** `true`

#### Returns

`number`

integer value representing the difference between the two dates

#### Since

ELC 3.51b / otrisPORTAL 5.1b

#### Example

```ts
var start = util.convertStringToDate("01.04.2006", "dd.mm.yyyy");
var end = util.convertStringToDate("05.04.2006", "dd.mm.yyyy");
var duration = context.getDatesDiff(start, end) ;
util.out("Difference: " + duration); // should be 4
```

***

### getDocumentById()

> **getDocumentById**(`idFile`, `idDocument`): [`Document`](Document.md)

**Get the Document by its unique file-id.**  

If the Document does not exist or the user in whose context the script is executed is not allowed to access the file, then the return value will be `null`.

#### Parameters

##### idFile

`string`

Unique id of the file

##### idDocument

`string`

Unique id of the document

#### Returns

[`Document`](Document.md)

Document as Document object.

#### Since

DOCUMENTS 5.0e

#### Example

```ts
var doc = context.getDocumentById("dopaag_fi20160000000423", "dopaagdc0000000000000256");
if (!doc)
   util.out(context.getLastError());
else
  util.out(doc.fullname)
```

***

### getDocumentTemplateFromFileType()

> **getDocumentTemplateFromFileType**(`fileTypeName`, `templateName`, `content?`): `string`

**Retrieve the content or the path of a document template from a file type.**

#### Parameters

##### fileTypeName

`string`

String containing the technical name of the file type.

##### templateName

`string`

String containing the technical name of the document template.

##### content?

`boolean`

**Default:** `false`.  
Optional boolean indicating whether the path of the template file is wanted or the content of the file as String.

#### Returns

`string`

`String` with the path to the template or the content of the template, an exception in case of any error

#### Since

DOCUMENTS 5.0f

#### Example

```ts
try {
   var templatePath    = context.getDocumentTemplateFromFileType("crmUser", "TemplateOrder");
   var templateContent = context.getDocumentTemplateFromFileType("crmUser", "TemplateOrder", true);
} catch (err) {
   util.out(err)
}
```

***

### getEnumAutoText()

> **getEnumAutoText**(`autoText`): `string`[]

**Get an array with the values of an enumeration autotext.**

#### Parameters

##### autoText

`string`

to be parsed

#### Returns

`string`[]

Array containing the values for the autotext

#### Since

ELC 3.60e / otrisPORTAL 6.0e

#### Example

```ts
var values = context.getEnumAutoText("%accessProfile%")
if (values)
{
  for (var i = 0; i < values.length; i++)
  {
      util.out(values[i]);
  }
}
```

***

### getEnumErgValue()

> **getEnumErgValue**(`fileType`, `field`, `techEnumValue`, `locale?`): `string`

**Get the ergonomic label of a multilanguage enumeration list value.**  

Enumeration lists in multilanguage DOCUMENTS installations usually are translated into the different portal languages as well. 
This results in the effect that only a technical value for an enumeration is stored in the database. 
So, if you need to display the label which is usually visible instead in the enumeration field through scripting, 
this function is used to access that ergonomic label.

#### Parameters

##### fileType

`string`

String value containing the technical name of the desired filetype

##### field

`string`

String value containing the technical name of the desired enumeration field

##### techEnumValue

`string`

String value containing the desired technical value of the enumeration entry

##### locale?

`string`

optional String value with the locale abbreviation (according to the principal's configuration); 
if omitted, the current user's portal language is used automatically

#### Returns

`string`

String containing the ergonomic value of the enumeration value in the appropriate portal language

#### Since

ELC 3.51 / otrisPORTAL 5.1

#### See

[context.getEnumErgValue](#getenumergvalue)  
[context.getFieldErgName](#getfieldergname)   
[context.getFileTypeErgName](#getfiletypeergname)   
[context.getEnumValues](#getenumvalues)  
[context.getFromSystemTable](#getfromsystemtable)

#### Example

```ts
util.out(context.getEnumErgValue("Standard", "Priority", "1", "de"));
```

***

### getEnumLocaleValues()

> **getEnumLocaleValues**(`fileTypeOrScript`, `fieldOrParamName`, `enumKeys`, `enumLocales`, `locale?`, `enumSource?`): `string`

**Retrieve the technical and ergonomic values of an enumeration list.**  

**Since:** DOCUMENTS 6.1.0 (new parameter `enumSource`)

#### Parameters

##### fileTypeOrScript

`string`

The technical name of the desired file type or script.

##### fieldOrParamName

`string`

The technical name of the desired enumeration field or script parameter.

##### enumKeys

`string`[]

Empty array for the technical values.

##### enumLocales

`string`[]

Empty array for the ergonomic values.

##### locale?

`string`

The locale abbreviation (according to the principal's configuration).  
**Default:** the current user's portal language

##### enumSource?

`number`

Constant indicating the source of the enumeration. Currently only the following values are available:

+ [context.FILETYPE\_FIELD](#filetype_field): The source is a field in a file type;
+ [context.SCRIPT\_PARAM](#script_param): The source is a script parameter;
+ [context.SOURCE\_UNKNOWN](#source_unknown): The source is not specified.

**Default:** context.SOURCE_UNKNOWN
  
**Note:**  
If this parameter is not specified or `context.SOURCE_UNKNOWN`, the method first checks whether the specification (`fileTypeOrScript`) 
is a file type name. If no file type is found, it searches for a script.

#### Returns

`string`

Empty String if successful, the error message in case of any error.

#### Since

DOCUMENTS 6.0.1

#### See

[context.getEnumErgValue](#getenumergvalue)  
[context.getEnumValues](#getenumvalues)

#### Example

```ts
var enumKeys = new Array();
var enumLocales = new Array();
var msg = context.getEnumLocaleValues("Standard", "Priority", enumKeys, enumLocales, "en", context.FILETYPE_FIELD);
if (msg.length == 0)
{
   for (var i = 0; i < enumKeys.length; i++)
   {
      util.out(enumKeys[i]);
      util.out(enumLocales[i]);
      util.out("---------");
   }
}
else
   util.out(msg);
```

***

### getEnumValues()

> **getEnumValues**(`fileType`, `field`): `false` \| `string`[]

**Get an array with enumeration list entries.**  

In some cases it might be useful not only to access the selected value of an enumeration file field, 
but the list of all possible field values as well. This function creates an Array of String values (zero-based), 
and each index is one available value of the enumeration field. If the enumeration field is configured to sort the values 
alphabetically, this option is respected.

#### Parameters

##### fileType

`string`

The technical name of the desired filetype

##### field

`string`

The technical name of the desired enumeration field

#### Returns

`false` \| `string`[]

Array containing all possible values of the enumeration field, or false if the field does not exist.

#### Since

ELC 3.51 / otrisPORTAL 5.1

#### See

[context.getEnumErgValue](#getenumergvalue)  
[context.getFieldErgName](#getfieldergname)  
[context.getFileTypeErgName](#getfiletypeergname)  
[context.getEnumValues](#getenumvalues)  
[context.getFromSystemTable](#getfromsystemtable)

#### Example

```ts
var valueList = context.getEnumValues("Standard", "Priority");
if (valueList && valueList.length > 0)
{
   for (var i = 0; i < valueList.length; i++)
   {
      util.out(valueList[i]);
   }
}
```

***

### getFieldErgName()

> **getFieldErgName**(`fileType`, `field`, `locale?`): `string`

**Get the ergonomic label of a file field.**  

In multilanguage DOCUMENTS environments, usually the file fields are translated to the different locales by using the well known ergonomic label hack. 
The function is useful to output scripting generated information in the appropriate portal language of the web user who triggered the script execution.

#### Parameters

##### fileType

`string`

The technical name of the desired filetype

##### field

`string`

The technical name of the desired field

##### locale?

`string`

The locale abbreviation (according to the principal's configuration); if omitted, the current user's portal language is used automatically

#### Returns

`string`

String containing the ergonomic description of the file field in the appropriate portal language

#### Since

ELC 3.51 / otrisPORTAL 5.1

#### See

[context.getEnumErgValue](#getenumergvalue)  
[context.getFieldErgName](#getfieldergname)  
[context.getFileTypeErgName](#getfiletypeergname)   
[context.getEnumValues](#getenumvalues)   
[context.getFromSystemTable](#getfromsystemtable)

#### Example

```ts
util.out(context.getFieldErgName("Standard", "Prioritaet", "de"));
```

***

### getFileById()

> **getFileById**(`idFile`): [`DocFile`](DocFile.md)

**Get the file by its unique file-id.**  

If the file does not exist or the user in whose context the script is executed is not allowed to access the file, then the return value will be `null`.

#### Parameters

##### idFile

`string`

Unique id of the file

#### Returns

[`DocFile`](DocFile.md)

File as DocFile object.

#### Since

ELC 3.51b / otrisPORTAL 5.1b

#### See

[context.file](#file)

#### Example

```ts
var file = context.getFileById("toastupfi_20070000002081");
if (file)
   util.out(file.getAutoText("title"));
else
   util.out(context.getLastError());
```

***

### getFilesWithScratchCopy()

> **getFilesWithScratchCopy**(): [`FileResultset`](../classes/FileResultset.md)

**Retrieve a FileResultset of all the active files related with a scratch copy.**

#### Returns

[`FileResultset`](../classes/FileResultset.md)

FileResultset containing a list of the DocFile objects.

#### Since

DOCUMENTS 5.0i HF5

#### See

[DocFile.deleteScratchCopy](DocFile.md#deletescratchcopy)

***

### getFileTypeErgName()

> **getFileTypeErgName**(`fileType`, `locale?`): `string` \| `boolean`

**Get the ergonomic label of a filetype.**  

In multilanguage DOCUMENTS environments, usually the filetypes are translated to the different locales by using the well known ergonomic label hack. 
The function is useful to output scripting generated information in the appropriate portal language of the web user who triggered the script execution.

#### Parameters

##### fileType

`string`

String value containing the technical name of the desired filetype

##### locale?

`string`

optional String value with the locale abbreviation (according to the principal's configuration); if omitted, the current user's portal language is used automatically

#### Returns

`string` \| `boolean`

String containing the ergonomic description of the filetype in the appropriate portal language. `false` in case of an error

#### Since

ELC 3.51 / otrisPORTAL 5.1

#### See

[context.getEnumErgValue](#getenumergvalue)  
[context.getFieldErgName](#getfieldergname)  
[context.getFileTypeErgName](#getfiletypeergname)  
[context.getEnumValues](#getenumvalues)  
[context.getFromSystemTable](#getfromsystemtable)

#### Example

```ts
util.out(context.getFileTypeErgName("Standard", "de"));
```

***

### getFileTypeOID()

> **getFileTypeOID**(`nameFiletype`, `oidLow?`): `string`

**Returns the object-id of a filetype.**

#### Parameters

##### nameFiletype

`string`

String value containing the technical name of the filetype.

##### oidLow?

`boolean`

**Default:** `false`.  
Optional flag:   
If `true` only the id of the filetype object (`m_oid`) will be returned.   
If `false` the id of the filetype object will be returned together with the id of the corresponding class in the form `class-id:m_oid`.

#### Returns

`string`

`String` with the object-id or `false` if filetype does not exist

#### Since

DOCUMENTS 5.0

***

### getFolderPosition()

> **getFolderPosition**(`folder`): `number`

**Retrieve the position of a top level folder in the global context.**  

This method can be used to get the position of a top level folder (public, public dynamic or only subfolders folder with no parent) in the global context.

#### Parameters

##### folder

[`Folder`](Folder.md)

Folder object whose position to be retrieved.

#### Returns

`number`

internal position number of the folder as integer or -1 in case of any error.

#### Since

DOCUMENTS 5.0a

#### See

[context.setFolderPosition](#setfolderposition)  
[Folder.getPosition](Folder.md#getposition)  
[Folder.setPosition](Folder.md#setposition)

#### Example

```ts
var folder = context.getFoldersByName("MyPublicFolder").first();
var pos = context.getFolderPosition(folder);
if (pos < 0)
   throw context.getLastError();
```

***

### getFoldersByName()

> **getFoldersByName**(`folderPattern`, `type?`, `checkAccessRight?`): [`FolderIterator`](FolderIterator.md)

**Retrieve a list of folders with identical name.**  

Different folders might match an identical pattern, e.g. `"DE_20*"` for each folder like `"DE_2004"`, `"DE_2005"` and so on. 
If you need to perform some action with the different folders or their contents, it might be useful to retrieve an iterator (a list) 
of all these folders to loop through that list.  

**Note:** Until version 5.0h this method ignored the access rights of the user to the folders. With the optional parameter 
checkAccessRight this can now be done. For backward compatibility the default value is set to false.  
  
**Since:** DOCUMENTS 5.0h (new optional parameter checkAccessRight)

#### Parameters

##### folderPattern

`string`

the name pattern of the desired folder(s)

##### type?

`string`

optional parameter, a String value defining the type of folders to look for; allowed values are `"public"`, `"dynamicpublic"` and `"onlysubfolder"`

##### checkAccessRight?

`boolean`

**Default:** `false`.  
optional boolean value, that indicates if the access rights should be considered

#### Returns

[`FolderIterator`](FolderIterator.md)

FolderIterator containing a list of all folders matching the specified name pattern

#### Since

ELC 3.50l01 / otrisPORTAL 5.0l01

#### Example

```ts
var folderIter = context.getFoldersByName("Inv*");
```

***

### getFromSystemTable()

> **getFromSystemTable**(`identifier`, `locale?`): `string`

**Retrieve the desired entry of the system messages table.**  

It might be inconvenient to maintain the different output Strings of localized PortalScripts, if this requires to edit the scripts themselves. 
This function adds a convenient way to directly access the system messages table which you may maintain in the Windows Portal Client. 
This enables you to add your own system message table entries in your different portal languages and to directly access them in your scripts.
**Since:** DOCUMENTS 5.0i HF5 (new parameter locale)

#### Parameters

##### identifier

`string`

String value containing the technical identifer of a certain system message table entry

##### locale?

`string`

String value containing the locale (de, en,...)
optional String value, that indicates the wanted language

#### Returns

`string`

String containing the value of the desired entry in the current user's portal language

#### Since

ELC 3.50o / otrisPORTAL 5.0o

#### See

[context.getEnumErgValue](#getenumergvalue)  
[context.getFieldErgName](#getfieldergname)  
[context.getFileTypeErgName](#getfiletypeergname)  
[context.getEnumValues](#getenumvalues)  
[context.getFromSystemTable](#getfromsystemtable)

#### Example

```ts
// requires an entry with that name in your system message table
util.out(context.getFromSystemTable("myOwnTableEntry"));
```

***

### getGlobalAttribute()

> **getGlobalAttribute**(`attributeName`): `string`

**Get the string value of an attribute of the DOCUMENTS global settings.**

#### Parameters

##### attributeName

`string`

The name of the desired attribute

#### Returns

`string`

String with the value of the attribute, an exception in case of using an invalid attribute and an empty string in case of 
using a not existing property starting with '$', respectively.

#### Since

DOCUMENTS 5.0g

#### See

[context.setGlobalAttribute](#setglobalattribute)

#### Example

```ts
// Retrieve a global attribute
try {
   var value = context.getGlobalAttribute("StandardUser");
   util.out(value);
} catch (err) {
   util.out(err);
}
// Retrieve a global property whose name starts with '$'
var propValue = context.getGlobalAttribute("$decreaseSearchArchivesScript");
if (propValue == "")
  util.out("$decreaseSearchArchivesScript not set");
else
  util.out(propValue);
```

***

### getGlobalEnumerations()

> **getGlobalEnumerations**(): [`GlobalEnumerationIterator`](GlobalEnumerationIterator.md)

**Get a [GlobalEnumerationIterator](GlobalEnumerationIterator.md) with all GlobalEnumerations in DOCUMENTS.**

#### Returns

[`GlobalEnumerationIterator`](GlobalEnumerationIterator.md)

GlobalEnumerationIterator

#### Since

DOCUMENTS 6.0.2

#### Example

```ts
var it = context.getGlobalEnumerations();
for (var gEnum of it)
{
   // do something
}
```

***

### getJSObject()

> **getJSObject**(`oid`): `object`

**Get a JS_Object by object id.**  

With this method you can get a JS-Object by the object id. Depending of the class of the object you get a JS-Object of the classes AccessProfile, 
DocFile, Document, Folder, Register, SystemUser or WorkflowStep

#### Parameters

##### oid

`string`

String containing the id of the object

#### Returns

`object`

JS-Object or `null`, if failed

#### Since

ELC 3.60c / otrisPORTAL 6.0c

#### Example

```ts
var docFile1 = context.file;
var objectId = docFile1.getOID();
var docFile2 = context.getJSObject(objectId);
// docFile1 and docFile2 are both of the class DocFile
// and reference the same ELC-file object
```

***

### getLastError()

> **getLastError**(`shortMessage?`): `string`

**Function to get the description of the last error that occurred.**  

**Note:** All classes have their own error functions. Only global errors are available through the context getLastError() method.  
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files   
**Since:** DOCUMENTS 5.0g (new parameter shortMessage)

#### Parameters

##### shortMessage?

`boolean`

**Default:** `false`.  
optional Boolean; removes "Error in function: class.method(): " from the message.

#### Returns

`string`

Text of the last error as String

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### See

[DocFile.getLastError](DocFile.md#getlasterror)

#### Example

```ts
util.out(context.getLastError());
```

***

### getLicenseInfo()

> **getLicenseInfo**(): `string`

**Retrievs license infos for the actual principal as json-String.**

#### Returns

`string`

String with license restrictions and current usage.

#### Since

DOCUMENTS 5.0h HF1

#### Example

```ts
try {
   var json = context.getLicenseInfo();
   var obj = JSON.parse(json);
    .....
} catch (err) {
   util.out(err)
}
```

***

### getLocaleValue()

> **getLocaleValue**(`value`, `locale?`): `string`

**Get the value/label of a String with the format "de:rot;en:red;fr:rouge" in the current or defined portal language.**

#### Parameters

##### value

`string`

String with the complete value string

##### locale?

`string`

Optional String value with the locale abbreviation (according to the principal's configuration); if omitted, the current user's portal language is used automatically.

#### Returns

`string`

`String` containing the valuein the appropriate portal language.

#### Since

DOCUMENTS 5.0c HF1

#### Example

```ts
var title = "de:Rechnung 001; en:Invoice 001"
var deVal = context.getLocaleValue(title, "de");
util.out(deVal);    // deVal = Rechnung 001
var valInCurrentLanguage = context.getLocaleValue(title);
```

***

### getMails()

> **getMails**(): [`EmailIterator`](EmailIterator.md)

**Get an EmailIterator with all emails in DOCUMENTS.**

#### Returns

[`EmailIterator`](EmailIterator.md)

EmailIterator

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var it = context.getMails();
for (var mail of it)
{
   // do something
}
```

***

### getPrincipalAttribute()

> **getPrincipalAttribute**(`attributeName`): `string`

**Get the String value of an attribute of the DOCUMENTS principal.**

#### Parameters

##### attributeName

`string`

the technical name of the desired attribute

#### Returns

`string`

String containing the value of the attribute

#### Since

ELC 3.50f / otrisPORTAL 5.0f

#### See

[context.getCurrentUserAttribute](#getcurrentuserattribute)  
[context.setPrincipalAttribute](#setprincipalattribute)

#### Example

```ts
util.out(context.getPrincipalAttribute("executive.eMail"));
```

***

### getPrincipalStatus()

> **getPrincipalStatus**(): `string`

**Get the status of the principal.**

#### Returns

`string`

String with the value of the status

#### Since

DOCUMENTS 5.0g

#### See

[context.setPrincipalStatus](#setprincipalstatus)

***

### getProgressBar()

> **getProgressBar**(): `number`

**Gets the current progress value in % of the progress bar in the Documents-Manager during the PortalScript execution.**

#### Returns

`number`

`progress` as float (value >= 0 and value <= 100)

#### Since

DOCUMENTS 5.0c

#### See

[context.setProgressBarText](#setprogressbartext)  
[context.setProgressBar](#setprogressbar)

***

### getQueryParams()

> **getQueryParams**(): [`DocQueryParams`](DocQueryParams.md)

**Get the actual search parameters within an "OnSearch" or "FillSearchScript" exit.**  

**Note:** The return value is `null`, if the calling script is not running as an "OnSearch" or "FillSearchMask" handler. 
It can also be `null`, if the script has called changeScriptUser(). In order to access the search parameters, 
the script needs to restore the original user context.

#### Returns

[`DocQueryParams`](DocQueryParams.md)

A DocQueryParams object on success, otherwise `null`.

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var queryParams = context.getQueryParams();
```

***

### getRegisterErgName()

> **getRegisterErgName**(`fileTypeName`, `registerName`, `locale?`): `string`

**Get the ergonomic label of a register.**

#### Parameters

##### fileTypeName

`string`

String value containing the technical name of the desired filetype

##### registerName

`string`

String value containing the technical name of the desired register

##### locale?

`string`

optional String value with the locale abbreviation (according to the principal's configuration); if omitted, the current user's portal language is used automatically

#### Returns

`string`

String containing the ergonomic description of the register in the appropriate portal language

#### Since

DOCUMENTS 4.0d HF1

#### See

[context.getFieldErgName](#getfieldergname)  
[context.getFileTypeErgName](#getfiletypeergname)

#### Example

```ts
util.out(context.getRegisterErgName("Standard", "Reg1", "de"));
```

***

### getScriptOrigin()

> **getScriptOrigin**(`scriptName`): `number`

**Function to declare where a script comes from.**

#### Parameters

##### scriptName

`string`

The name of the desired script.

#### Returns

`number`

One of `Script Origin Constants`:
<ul> 
<li>[context.SCRIPT\_FROM\_DB](#script_from_db) if the script comes from DB</li> 
<li>[context.SCRIPT\_FROM\_LIBS](#script_from_libs) if the script comes from the server directory [...]\server\scriptlibs</li> 
<li>[context.SCRIPT\_UNKNOWN](#script_unknown) otherwise</li>
</ul>

#### Since

DOCUMENTS 5.0i HF5

***

### getServerInstallPath()

> **getServerInstallPath**(): `string`

**Create a String containing the installation path of the portal server.**

#### Returns

`string`

String containing the portal server installation path

#### Since

ELC 3.60a / otrisPORTAL 6.0a

#### Example

```ts
var installDir = context.getServerInstallPath();
util.out(installDir);
```

***

### getSkillLicense()

> **getSkillLicense**(`type`, `skill`): `number`

**`Internal`**

**Returns the license value of the wanted skill.**

#### Parameters

##### type

`string`

String value containing the type of the skill
(allowed values are `"named"`, `"concurrent_standard"`, `"concurrent_open"`)

##### skill

`string`

String value containing the name of the skill

#### Returns

`number`

Number containing the value from the license file

#### Since

DOCUMENTS 6.1.1

#### Example

```ts
var amount = context.getSkillLicense("named", "AI");
util.out(amount);
```

***

### getSkillUse()

> **getSkillUse**(`type`, `skill`): `number`

**`Internal`**

**Returns the number of users to whom a skill is assigned.**

#### Parameters

##### type

`string`

String value containing the type of the skill
(allowed values are `"named"`, `"concurrent_standard"`, `"concurrent_open"`)

##### skill

`string`

String value containing the name of the skill

#### Returns

`number`

Number containing the amount of users  to whom a skill is assigned

#### Since

DOCUMENTS 6.1.1

#### See

[context.getSkillLicense](#getskilllicense)

#### Example

```ts
var license = context.getSkillLicense("named", "AI");
var used = context.getSkillUse("named", "AI");
util.out("Free licenses: " + (license - used));
```

***

### getSuperMode()

> **getSuperMode**(): `boolean`

**Get the "setSuperMode"-flag of the current PortalScript-Session.**

#### Returns

`boolean`

`true` or `false`

#### Since

DOCUMENTS 5.0e HF2

#### See

[context.setSuperMode](#setsupermode)

***

### getSystemUser()

> **getSystemUser**(): [`SystemUser`](SystemUser.md)

**Get the current user as a SystemUser object.**

#### Returns

[`SystemUser`](SystemUser.md)

SystemUser object representing the current user.

#### Since

ELC 3.51b / otrisPORTAL 5.1b

#### See

[context.findSystemUser](#findsystemuser)  
[context.findSystemUserByAlias](#findsystemuserbyalias)  
[context.getSystemUsers](#getsystemusers)

#### Example

```ts
var su = context.getSystemUser();
if (su)
   util.out(su.login); // output login name of current user
```

***

### getSystemUsers()

> **getSystemUsers**(`includeLockedUsers?`, `includeInvisibleUsers?`): [`SystemUserIterator`](SystemUserIterator.md)

**Get a list of users created in the system.**  
 
  
**Since:** DOCUMENTS 4.0c new optional parameter includeLockedUsers   
**Since:** DOCUMENTS 5.0f HF2 new optional parameter includeInvisibleUsers

#### Parameters

##### includeLockedUsers?

`boolean`

**Default:** `false`.  
optional definition, if locked users also should be returned.

##### includeInvisibleUsers?

`boolean`

**Default:** `false`.  
Optional flag indicating whether the method also should return users for which the option "Display user in DOCUMENTS lists" in the Documents Manager is not checkmarked.

#### Returns

[`SystemUserIterator`](SystemUserIterator.md)

SystemUserIterator object containing a list of users created in the system.

#### Since

ELC 3.50b / otrisPORTAL 5.0b

#### See

[context.findSystemUser](#findsystemuser)  
[context.getSystemUser](#getsystemuser)  
[context.findSystemUserByAlias](#findsystemuserbyalias)

#### Example

```ts
var itSU = context.getSystemUsers();
for (var su = itSU.first(); su; su = itSU.next())
{
   util.out(su.login);
}
```

***

### getTempPathByToken()

> **getTempPathByToken**(`accessToken`, `dropToken?`): `string`

**Returns the temporary server path, that was ordered by the gadget API for the token.**

#### Parameters

##### accessToken

`string`

String value with the token

##### dropToken?

`boolean`

**Default:** `true`.  
Optional Boolean value that indicates the server to forget the token

#### Returns

`string`

String with temporary path or Emptystring if accessToken is unknown

#### Since

DOCUMENTS 5.0d

***

### getTimestampsDiff()

> **getTimestampsDiff**(`earlierDate`, `laterDate`, `unit?`, `useWorkCalendar?`): `number`

**Subtract two Date objects to get their difference.**  

This function calculates the time difference between two Date objects, for example if you need to know how many days a business trip takes. 
By default this function takes the work calendar into account if it is configured and enabled for the principal.

#### Parameters

##### earlierDate

`Date`

Date object representing the earlier date

##### laterDate

`Date`

Date object representing the later date

##### unit?

`string`

**Default:** `'days'`.  
optional String value defining the unit, allowed values are `"minutes"`, `"hours"` and `"days"` (default)

##### useWorkCalendar?

`boolean`

**Default:** `true`.  
optional boolean to take office hours into account or not (requires enabled and configured work calendar)

#### Returns

`number`

integer value representing the difference between the two dates

#### Since

DOCUMENTS 5.0i HF3

#### Example

```ts
var start = util.convertStringToDate("01.04.2006 12:30", "dd.mm.yyyy HH:MM");
var end = util.convertStringToDate("05.04.2006 12:30", "dd.mm.yyyy HH:MM");
var duration = context.getTimestampsDiff(start, end) ;
util.out("Difference: " + duration); // should be 4
```

***

### getTmpFilePath()

> **getTmpFilePath**(): `string`

**Create a String containing a complete path and filename to a temporary file.**  

The created file path may be used without any danger of corrupting any important data by accident, because DOCUMENTS assures that there is no such file with the created filename yet.

#### Returns

`string`

String containing the complete "safe" path and filename

#### Since

ELC 3.50n / otrisPORTAL 5.0n

#### Example

```ts
var tmpFilePath = context.getTmpFilePath();
util.out(tmpFilePath);
```

***

### getWorkflowByName()

> **getWorkflowByName**(`name`): [`Workflow`](Workflow.md)

**Get a Workflow object by its technical name.**  

The name parameter may be composed of `name + "-" + version`. Otherwise the function seeks the newest available version of the workflow.  

**Note:** This function requires a full workflow engine license. It does not seek pure distribution lists.

#### Parameters

##### name

`string`

A string which contains the technical name of a workflow and optionally a version appendix

#### Returns

[`Workflow`](Workflow.md)

The requested Workflow object or `null`, if the given name is unknown.

#### Since

DOCUMENTS 6.0

***

### getWorkflowsFromFileType()

> **getWorkflowsFromFileType**(`fileTypeName`, `onlyReleased?`): `String`[]

**Retrieve the allowed workflows for a file type.**

#### Parameters

##### fileTypeName

`string`

String value containing the desired file type name.

##### onlyReleased?

`boolean`

**Default:** `true`.  
Optional flag indicating whether only released workflows should be returned.

#### Returns

`String`[]

Array of strings containing the technical names of the allowed workflows.

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var workflows = context.getWorkflowsFromFileType("testFileType");
if (workflows)
{
  for (var wf of workflows)
  {
      util.out(wf);
  }
}
```

***

### ~~getXMLServer()~~

> **getXMLServer**(`archiveServerName?`): [`ArchiveConnection`](ArchiveConnection.md)

**Get an ArchiveConnection object.**  

With this method you can get an ArchiveConnection object. This object offers several methods to use the EAS Interface, EBIS or the EASY ENTERPRISE XML-Server.  
  
**Since:** archiveServerName: Documents 4.0

#### Parameters

##### archiveServerName?

`string`

Optional string containing the archive server name; If the archive server is not defined, then the main archive server will be used

#### Returns

[`ArchiveConnection`](ArchiveConnection.md)

ArchiveConnection-Object or `null`, if failed

#### Since

ELC 3.60d / otrisPORTAL 6.0d

#### Deprecated

since DOCUMENTS 5.0a - Use [Context.getArchiveConnection(archiveServerName)](#getarchiveconnection) instead

***

### hasPEMModule()

> **hasPEMModule**(`moduleConst`): `Boolean`

**Function to check if a module is licenced in the pem.**

#### Parameters

##### moduleConst

`number`

from [\`PEM Module Constants\`](#pem_module_business_units).

#### Returns

`Boolean`

`true` if licenced, otherwise `false`

#### Since

DOCUMENTS 5.0c HF2

#### Example

```ts
util.out(context.hasPEMModule(context.PEM_MODULE_GADGETS));
```

***

### reloadCurrentPrincipal()

> **reloadCurrentPrincipal**(`pemReload?`): `boolean`

**Reloads the current principal.**  

This function invalidates or clears caches (e.g. `PortalScriptCache` and `ScriptEnumCache`) in order to reload them. If necessary, 
you can also use this method to reload the pem-file for the current principal using the parameter `pemReload`.

#### Parameters

##### pemReload?

`boolean`

**Default:** `false`.  
Optional boolean indicating whether the pem-file for the current principal to be reloaded.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0e

#### See

[context.reloadPrincipal](#reloadprincipal)

#### Example

```ts
if (!context.reloadCurrentPrincipal(true))
   util.out(context.getLastError());
```

***

### reloadPrincipal()

> **reloadPrincipal**(`principalName`, `pemReload?`): `boolean`

**Reloads the desired principal.**  

This function invalidates or clears caches (e.g. `PortalScriptCache` and `ScriptEnumCache`) in order to reload them. If necessary, 
you can also use this method to reload the pem-file for the desired principal using the parameter `pemReload`.

#### Parameters

##### principalName

`string`

String containing the name of the principal to be reloaded.

##### pemReload?

`boolean`

**Default:** `false`.  
Optional boolean indicating whether the pem-file for the desired principal to be reloaded.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0e

#### See

[context.reloadCurrentPrincipal](#reloadcurrentprincipal)

#### Example

```ts
if (!context.reloadPrincipal("peachit", true))
   util.out(context.getLastError());
```

***

### runScriptFromFile()

> **runScriptFromFile**(`filePath`, `paramNames?`, `paramValues?`): `string`

**`Internal`**

**Executes a PortalScript source code from a file in the file system.**  

This function is for internal use only!

#### Parameters

##### filePath

`string`

String Path to the PortalScript file in the file system

##### paramNames?

`any`[]

**Default:** `null`.  
Array with parameter names

##### paramValues?

`any`[]

**Default:** `null`.  
Array with parameter values

#### Returns

`string`

#### Since

DOCUMENTS 4.0b HF2

***

### sendTCPStringRequest()

> **sendTCPStringRequest**(`server`, `port`, `request`, `responseTimeout?`): `string`

**Send a String as TCP-Request to a server.**  

With this method it is possible to send a String via TCP to a server. The return value of the function is the response of the server. 
Optional you can define a timeout in ms this function waits for the response of a server  

**Note:** The responseTimeout is effective only after a request has successfully been sent. Timeouts for connecting and sending are determined by the underlying OS.

#### Parameters

##### server

`string`

String containing the IP address or server host

##### port

`number`

int containing the port on which the server is listening

##### request

`string`

String with the request that should be sent to the server

##### responseTimeout?

`number`

**Default:** `3000`.  
int with the timeout for the response in ms. Default value is 3000ms

#### Returns

`string`

String containing the response and `null` on error

#### Since

ELC 3.60b / otrisPORTAL 6.0b

#### Example

```ts
var response = context.sendTCPStringRequest("192.168.1.1", "4010", "Hello World", 5000);
if (!response)
   util.out(context.getLastError());
else
   util.out(response);
```

***

### setClientLang()

> **setClientLang**(`locale`): `string`

**Set the abbreviation of the current user's portal language.**  

If you want to set the portal language different from the current users language, you can use this method. As parameter you have to use 
the two letter abbreviation as defined in the principal's settings in the Windows DOCUMENTS Manager (e.g. "de" for German).

#### Parameters

##### locale

`string`

String containing the two letter abbreviation for the locale

#### Returns

`string`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 4.0c

#### See

[context.getClientLang](#getclientlang)

#### Example

```ts
context.setClientLang("en");
```

***

### ~~setClientSystemLang()~~

> **setClientSystemLang**(`langIndex`): `boolean`

**Set the script's execution context portal language to the desired language.**

#### Parameters

##### langIndex

`number`

integer value of the index of the desired system language

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.51g / otrisPORTAL 5.1g

#### Deprecated

since DOCUMENTS 4.0c use setClientLang(String locale) instead

#### Example

```ts
util.out(context.getClientSystemLang());
var erg = context.setClientSystemLang(0); // first portal language
```

***

### setFolderPosition()

> **setFolderPosition**(`folder`, `position`): `boolean`

**Place a top level folder a at given position in the global context.**  

This method can be used to set the position of a top level folder (public, public dynamic or only subfolders folder with no parent) in the global context.

#### Parameters

##### folder

[`Folder`](Folder.md)

Folder object whose position to be set.

##### position

`number`

new internal position number of folder.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0a

#### See

[context.getFolderPosition](#getfolderposition)  
[Folder.getPosition](Folder.md#getposition)  
[Folder.setPosition](Folder.md#setposition)

#### Example

```ts
// Create a folder B and place it before a folder A
var folderA = context.getFoldersByName("folderA").first();
var posA = context.getFolderPosition(folderA);
var folderB = context.createFolder("folderB", "public");
if (!context.setFolderPosition(folderB, posA - 1))
   throw context.getLastError();
```

***

### setGlobalAttribute()

> **setGlobalAttribute**(`attributeName`, `value`): `boolean`

**Set an attribute of the DOCUMENTS global settings to the desired value.**

#### Parameters

##### attributeName

`string`

The name of the desired attribute

##### value

`string`

The value that should be assigned

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0g

#### See

[context.getGlobalAttribute](#getglobalattribute)

#### Example

```ts
var ret = context.setGlobalAttribute("$decreaseSearchArchivesScript", "myDecreaseSearchArchivesScript");
if (!ret)
  throw context.getLastError();
```

***

### setOrAddCustomProperty()

> **setOrAddCustomProperty**(`name`, `type`, `value`): [`CustomProperty`](CustomProperty.md)

**Creates or modifies a global custom property according the name and type.**

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

DOCUMENTS 5.0

#### See

[context.getCustomProperties](#getcustomproperties)  
[context.addCustomProperty](#addcustomproperty)

#### Example

```ts
var custProp = context.setOrAddCustomProperty("favorites", "string", "peachit");
if (!custProp)
  util.out(context.getLastError());
```

***

### setPrincipalAttribute()

> **setPrincipalAttribute**(`attributeName`, `value`): `boolean`

**Set an attribute of the DOCUMENTS principal to the desired value.**

#### Parameters

##### attributeName

`string`

the technical name of the desired attribute

##### value

`string`

the value that should be assigned

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.51b / otrisPORTAL 5.1b

#### See

[context.getCurrentUserAttribute](#getcurrentuserattribute)  
[context.getPrincipalAttribute](#getprincipalattribute)

#### Example

```ts
context.setPrincipalAttribute("executive.eMail", "test@mail.de");
util.out(context.getPrincipalAttribute("executive.eMail"));
```

***

### setPrincipalStatus()

> **setPrincipalStatus**(`status`): `boolean`

**Set the status of the principal.**

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

[context.getPrincipalStatus](#getprincipalstatus)

#### Example

```ts
if (!context.setPrincipalStatus("released"))
  throw context.getLastError();
```

***

### setProgressBar()

> **setProgressBar**(`value`): `void`

**Sets the progress (%) of the progress bar in the Documents-Manager during the PortalScript execution.**

#### Parameters

##### value

`number`

Float with in % of the execution (value >= 0 and value <= 100)

#### Returns

`void`

#### Since

DOCUMENTS 5.0c

#### See

[context.setProgressBarText](#setprogressbartext)  
[context.getProgressBar](#getprogressbar)

#### Example

```ts
context.setProgressBarText("Calculating...");
context.setProgressBar(0.0);  // set progress bar to 0.0%
for (var i = 1; i<100; i++) {
   // do something
   context.setProgressBar(i);
}
```

***

### setProgressBarText()

> **setProgressBarText**(`text`): `void`

**Sets the progress bar text in the Documents-Manager during the PortalScript execution.**

#### Parameters

##### text

`string`

String with the text to displayed in the progress bar

#### Returns

`void`

#### Since

DOCUMENTS 5.0c

#### See

[context.setProgressBar](#setprogressbar)  
[context.getProgressBar](#getprogressbar)

#### Example

```ts
context.setProgressBarText("Calculating...");
context.setProgressBar(0.0);  // set progress bar to 0.0%
for (var i = 1; i<100; i++) {
   // do something
   context.setProgressBar(i);
}
```

***

### setSuperMode()

> **setSuperMode**(`value`): `void`

**Set and unset "setSuperMode"-flag for the current PortalScript-Session.**  

The method gives "superrights" to the session and overrules the DOCUMENTS right management e.g. if you use (G)ACL in a filetype, 
in supermode a FileResultset / HitResultset in the script will find all files, independed of the access rights of the current user. 
The supermode will be inhertited to sub-scripts (e.g. implicit running enum scripts), but not to ScriptCalls.

#### Parameters

##### value

`boolean`

boolean to set / unset setSuperMode-flag

#### Returns

`void`

#### Since

DOCUMENTS 5.0e HF2

#### See

[context.getSuperMode](#getsupermode)

#### Example

```ts
try {
   context.setSuperMode(true);
   // do something with superrights
   // ...... new HitResultset(.....)
} finally {
  context.setSuperMode(false);
}
```

***

### submitFileChanges()

> **submitFileChanges**(`fileTypeName`, `withStatusEntry?`): `boolean`

**Change the structure of files of a file type.**

#### Parameters

##### fileTypeName

`string`

String containing the technical name of the file type.

##### withStatusEntry?

`boolean`

**Default:** `true`.  
Optional boolean indicating whether the status entries for the changed files should be suppressed.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0g HF2

#### Example

```ts
try {
   context.submitFileChanges("TestFileType", false);
} catch (err) {
   util.out(err)
}
```

***

### updateSearchFieldCache()

> **updateSearchFieldCache**(`fileTypeName?`): `boolean`

**Updates the server sided search field cache for file types.**

#### Parameters

##### fileTypeName?

`string`

Optional string containing the technical name of the file type. If the parameter is missing or empty, 
this function updates the search field cache for all file types.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0g HF2

#### Example

```ts
try {
   context.updateSearchFieldCache("TestFileType");
} catch (err) {
   util.out(err)
}
```

***

### writeLogBook()

> **writeLogBook**(`actionCode`, `detail1`, `detail2`, `detail3`, `logObject`): `boolean`

**Logs an executed action to the logbook.**

#### Parameters

##### actionCode

`number`

The integer code of the executed action to be logged. Range: 0 to n described as follows:

+ `0` : Create file
+ `1` : Start edit file
+ `2` : Cancel edit file
+ `3` : Save file
+ `4` : Archive file
+ `5` : Delete file
+ `6` : Start workflow
+ `7` : Receive file
+ `8` : Forward file
+ `9` : Change filetype
+ `10` : Workflow escalation
+ `11` : Workflow decision
+ `12` : XML-Export
+ `13` : Workflow receive-signal
+ `14` : Workflow finished
+ `15` : Filetype created
+ `16` : Filetype changed
+ `17` : Filetype deleted
+ `18` : Filetype-field created
+ `19` : Filetype-field changed
+ `20` : Filetype-field deleted
+ `21` : Filetype-register created
+ `22` : Filetype-register changed
+ `23` : Filetype-register deleted
+ `24` : User created
+ `25` : User changed
+ `26` : User deleted
+ `27` : Access profile created
+ `28` : Access profile changed
+ `29` : Access profile deleted
+ `30` : Added user to access profile
+ `31` : Removed user from access profile
+ `32` : Delete file to trash
+ `33` : Recovery from trash
+ `34` : Delete archive file
+ `35` : Maintenance operation performed
+ `36` : Life cycle action performed
+ `255`: Custom action

##### detail1

`string`

Optional String with length <= 255 containing additional information of the action. if the string length > 255, only the first 255 characters will be displayed.

##### detail2

`string`

Optional String with length <= 60 containing additional information of the action. if the string length > 60, only the first 60 characters will be displayed.

##### detail3

`string`

Optional String with length <= 60 containing additional information of the action. if the string length > 60, only the first 60 characters will be displayed.

##### logObject

`any`

Optional object to be logged. Currently only DocFile object is allowed.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0e

#### See

[context.findLogBookEntries](#findlogbookentries)

#### Example

```ts
context.writeLogBook(32, "info1", "info2", "info3");
```

## Script Origin Constants

These constants build an enumeration of the possible values indicating where a script comes from.  
**Since** DOCUMENTS 5.0i HF5  
**See** [context.getScriptOrigin(scriptName)](#getscriptorigin)

### SCRIPT\_FROM\_DB

> `readonly` **SCRIPT\_FROM\_DB**: `number`

***

### SCRIPT\_FROM\_LIBS

> `readonly` **SCRIPT\_FROM\_LIBS**: `number`

***

### SCRIPT\_UNKNOWN

> `readonly` **SCRIPT\_UNKNOWN**: `number`

## PEM Module Constants

These constants build an enumeration of the possible values of the pem license.  
**Since** DOCUMENTS 5.0c HF2  
**See** [Context.hasPEMModule(moduleConst)](#haspemmodule)

### PEM\_MODULE\_BUSINESS\_UNITS

> `readonly` **PEM\_MODULE\_BUSINESS\_UNITS**: `number`

***

### PEM\_MODULE\_CGC

> `readonly` **PEM\_MODULE\_CGC**: `number`

***

### PEM\_MODULE\_CGC\_ENT

> `readonly` **PEM\_MODULE\_CGC\_ENT**: `number`

***

### PEM\_MODULE\_CGC\_ENT\_PLUS

> `readonly` **PEM\_MODULE\_CGC\_ENT\_PLUS**: `number`

***

### PEM\_MODULE\_CONTRACT

> `readonly` **PEM\_MODULE\_CONTRACT**: `number`

***

### PEM\_MODULE\_CONTRACT\_SAP

> `readonly` **PEM\_MODULE\_CONTRACT\_SAP**: `number`

***

### PEM\_MODULE\_CONTROLLING

> `readonly` **PEM\_MODULE\_CONTROLLING**: `number`

***

### PEM\_MODULE\_CREATOR

> `readonly` **PEM\_MODULE\_CREATOR**: `number`

***

### PEM\_MODULE\_DOC\_TREE

> `readonly` **PEM\_MODULE\_DOC\_TREE**: `number`

***

### PEM\_MODULE\_DRIVECONNECT

> `readonly` **PEM\_MODULE\_DRIVECONNECT**: `number`

***

### PEM\_MODULE\_DROP

> `readonly` **PEM\_MODULE\_DROP**: `number`

***

### PEM\_MODULE\_EASYHR

> `readonly` **PEM\_MODULE\_EASYHR**: `number`

***

### PEM\_MODULE\_FP\_HENR

> `readonly` **PEM\_MODULE\_FP\_HENR**: `number`

***

### PEM\_MODULE\_GADGETS

> `readonly` **PEM\_MODULE\_GADGETS**: `number`

***

### PEM\_MODULE\_IFRS16

> `readonly` **PEM\_MODULE\_IFRS16**: `number`

***

### PEM\_MODULE\_IMS

> `readonly` **PEM\_MODULE\_IMS**: `number`

***

### PEM\_MODULE\_INBOX

> `readonly` **PEM\_MODULE\_INBOX**: `number`

***

### PEM\_MODULE\_INVOICE

> `readonly` **PEM\_MODULE\_INVOICE**: `number`

***

### PEM\_MODULE\_IP\_MANAGEMENT

> `readonly` **PEM\_MODULE\_IP\_MANAGEMENT**: `number`

***

### PEM\_MODULE\_LDAP

> `readonly` **PEM\_MODULE\_LDAP**: `number`

***

### PEM\_MODULE\_MATTER

> `readonly` **PEM\_MODULE\_MATTER**: `number`

***

### PEM\_MODULE\_MOBILE

> `readonly` **PEM\_MODULE\_MOBILE**: `number`

***

### PEM\_MODULE\_OUTLOOK\_SYNC

> `readonly` **PEM\_MODULE\_OUTLOOK\_SYNC**: `number`

***

### PEM\_MODULE\_OUTLOOK\_WEB

> `readonly` **PEM\_MODULE\_OUTLOOK\_WEB**: `number`

***

### PEM\_MODULE\_REPORTING

> `readonly` **PEM\_MODULE\_REPORTING**: `number`

***

### PEM\_MODULE\_RISK\_MANAGEMENT

> `readonly` **PEM\_MODULE\_RISK\_MANAGEMENT**: `number`

***

### PEM\_MODULE\_SIGN

> `readonly` **PEM\_MODULE\_SIGN**: `number`

***

### PEM\_MODULE\_WORDML

> `readonly` **PEM\_MODULE\_WORDML**: `number`

## Enumeration Source Constants

These constants build an enumeration of the possible values of the enumeration source.  
**Since** DOCUMENTS 6.1.0 
**See** [context.getEnumLocaleValues()](#getenumlocalevalues)

### FILETYPE\_FIELD

> `readonly` **FILETYPE\_FIELD**: `number`

***

### SCRIPT\_PARAM

> `readonly` **SCRIPT\_PARAM**: `number`

***

### SOURCE\_UNKNOWN

> `readonly` **SOURCE\_UNKNOWN**: `number`
