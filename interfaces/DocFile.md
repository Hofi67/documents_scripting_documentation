[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / DocFile

# Interface: DocFile

**The DocFile class implements the file object of DOCUMENTS.**  

You may access a single DocFile with the help of the attribute `context.file` or by creating a [FileResultset](../classes/FileResultset.md). 
There are no special properties available, but each field of a file is mapped to an according property. 
You can access the different field values with their technical names.  
For this reason it is mandatory to use programming language friendly technical names, meaning 
<ul> 
<li>only letters, digits and the underscore "_" are allowed. </li> 
<li>no whitespaces or any special characters are allowed. </li> 
<li>the technical name must not start with a digit. </li> 
<li>only the first 32 characters of the technical name are significant to identify the field.</li> 
</ul>

## Example

```ts
var myFile = context.file;
var priority = myFile.Priority; // read a field value
myFile.Remark = "Just a remark"; // assign a value to a field
myFile.sync(); // apply changes in field values to the file
```

## Properties

### fieldName

> **fieldName**: `any`

**The technical name of a field.**  

Each field of a DocFile is mapped to an according property. You can access the field value with the technical name.

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
var myFile = context.file;
var strValue = myFile.stringField;
myFile.dateField = new Date();
myFile.sync();
```

## Methods

### abort()

> **abort**(): `boolean`

**Cancel edit mode for a file.**  

If you switched a file to edit mode with the [startEdit()](#startedit) method and if you want to cancel this 
(e.g. due to some error that has occurred in the mean time) this function should be used to destroy 
the scratch copy which has been created by the startEdit() instruction.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### See

[DocFile.startEdit](#startedit)  
[DocFile.commit](#commit)

#### Example

```ts
var myFile = context.file;
myFile.startEdit();
myFile.Field = "value";
if(!myFile.abort()) { // effect: "value" is not applied!
     throw myFile.getLastError();
}
```

***

### addCustomProperty()

> **addCustomProperty**(`name`, `type`, `value`): [`CustomProperty`](CustomProperty.md)

**Creates a new [CustomProperty](CustomProperty.md) for an active file.**

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

DOCUMENTS 6.1.0

#### See

[DocFile.setOrAddCustomProperty](#setoraddcustomproperty)  
[DocFile.getCustomProperties](#getcustomproperties)

#### Example

```ts
var docFile = context.file;
var custProp = docFile.addCustomProperty("favorites", "string", "peachit");
if (!custProp)
  util.out(docFile.getLastError());
```

***

### addDocumentFromFileSystem()

> **addDocumentFromFileSystem**(`pathDocument`, `targetRegister`, `targetFileName`, `deleteDocumentAtFileSystem?`, `parseAutoText?`, `referencFileToParse?`): [`Document`](Document.md)

**Add a file as a new [Document](Document.md) from the server's filesystem to a given Register.**  

It is possible to parse Autotexts inside the source file to fill the Document with the contents of index fields of a DocFile object. 
The max. file size for the source file is 512 KB.  
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Parameters

##### pathDocument

`string`

String value containing the complete filepath with file-extension to the source file on the server

##### targetRegister

`string`

String value containing the technical name of the desired Register

##### targetFileName

`string`

String value containing the desired filename of the uploaded Document

##### deleteDocumentAtFileSystem?

`boolean`

**Default:** `false`.  
optional boolean value to decide whether to delete the source file on the server's filesystem

##### parseAutoText?

`boolean`

**Default:** `false`.  
optional boolean value to decide whether to parse the AutoText values inside the source file. 
The param pathDocument must have included an extension, otherwise parsing of Autotext will not work!

**Note:** if you want to make use of AutoTexts in this kind of template files, 
you need to use double percentage signs instead of single ones, e.g. %%Field1%% instead of %Field1%!

##### referencFileToParse?

`DocFile`

**Default:** `this`.  
optional DocFile object to be used to parse the AutoTexts inside the template. If you omit this parameter, 
the current DocFile object is used as the data source.

#### Returns

[`Document`](Document.md)

`Document` if successful, `null` in case of any error

#### Since

ELC 3.51f / otrisPORTAL 5.1f

#### Example

```ts
var f = context.file;
var success = f.addDocumentFromFileSystem("c:\\temp\\test.rtf", "Documents", "parsedRTFFile.rtf", false, true);
```

***

### addPDF()

> **addPDF**(`pathCoverXML`, `createCover`, `pdfFileName`, `targetRegister`, `sourceRegisterNames`): `boolean`

**Create a PDF file containing the current DocFile's contents and store it on a given document register.**  

The different document types of your documents on your different tabs require the appropriate PDF filter programs to be installed and configured in DOCUMENTS. 
To successfully add the created PDF file to a register the DocFile needs to be in edit mode (via [startEdit()](#startedit) method), 
and the changes have to be applied via [DocFile.commit()](#commit).  
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Parameters

##### pathCoverXML

`string`

String containing full path and filename of the template xml file to parse

##### createCover

`boolean`

boolean whether to create a field list or to only take the documents

##### pdfFileName

`string`

String value for the desired file name of the created PDF

##### targetRegister

`string`

String value containing the technical name of the target document register

##### sourceRegisterNames

`any`[]

Array with the technical names of the document registers you want to include

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50a / otrisPORTAL 5.0a

#### Example

```ts
var source = new Array();
source.push("FirstRegister");
source.push("SecondRegister");
var docFile = context.file;
docFile.startEdit();
docFile.addPDF("c:\\tmp\\cover.xml",
   true,
   "GeneratedPDF.pdf",
   "MyTargetRegister",
   source
);
docFile.commit();
```

***

### archive()

#### Call Signature

> **archive**(): `boolean`

**Archive the DocFile object.**  

The target archive has to be configured in the filetype definition (in the Windows Portal Client) as the default archive. 
If no default archive is defined, the execution of this operation will fail.

##### Returns

`boolean`

`true` if successful, `false` in case of any error

##### Since

ELC 3.50 / otrisPORTAL 5.0

##### See

[DocFile.archive(archiveKey)](./DocFile.html#archive.archive-2)  
[DocFile.archive(ArchivingDescription)](./DocFile.html#archive.archive-3)

##### Example

```ts
var myFile = context.file;
myFile.archive();
```

#### Call Signature

> **archive**(`archiveKey`): `boolean`

**Archive the DocFile object to the desired archive.**  

If the target archive key is misspelled or if the target archive does not exist, the operation will fall back to the default archive, 
as long as it is configured in the filetype definition. So the function will only fail if both the target archive and the default archive are missing.  
**Note:** For EE.i: It is important to know that the target archive String must use the socalled XML-Server syntax. The old EAG syntax is not supported. 
It is as well neccessary to use a double backslash (\\) if you define your target archive as an ECMAScript String value, because a single backslash is a special character.  
  
**Since:** EE.i: ELC 3.51c / otrisPORTAL 5.1c  
**Since:** EE.x: ELC 3.60a / otrisPORTAL 6.0a   
**Since:** EAS: Documents 4.0

##### Parameters

###### archiveKey

`string`

String value containing the complete archive key for EE.i or schema|view for EE.x of the desired target archive

##### Returns

`boolean`

`true` if successful, `false` in case of any error

##### Since

ELC 3.51c / otrisPORTAL 5.1c

##### See

[DocFile.archive()](./DocFile.html#archive.archive-1)  
[DocFile.archive(ArchivingDescription)](./DocFile.html#archive.archive-3)

##### Examples

```ts
// Example for EE.i:
var myFile = context.file;
var targetArchive = "$(#TOASTUP)\\STANDARD";
targetArchive += "@myeei";  // since Documents 4.0 using multi archive server
myFile.archive(targetArchive);
```

```ts
// Example for EE.x:
var myFile = context.file;
var view = "Unit=Default/Instance=Default/View=DeliveryNotes";
var schema = "Unit=Default/Instance=Default/DocumentSchema=LIEFERSCHEINE";
var target = schema + "|" + view;
target += "@myeex";  // since Documents 4.0 using multi archive server
myFile.archive(target);
```

```ts
// Example for EAS:
var myFile = context.file;
myFile.archive("@myeas");  // using multi archive server
```

#### Call Signature

> **archive**(`desc`): `boolean`

**Archive the DocFile object according to the given [ArchivingDescription](../classes/ArchivingDescription.md) object.**  

This is the most powerful way to archive a file through scripting, since the ArchivingDescription object supports 
a convenient way to influence which parts of the DocFile should be archived.  
  
**Since:** EE.i: ELC 3.51c / otrisPORTAL 5.1c  
**Since:** EE.x: ELC 3.60a / otrisPORTAL 6.0a   
**Since:** EAS: Documents 4.0

##### Parameters

###### desc

[`ArchivingDescription`](../classes/ArchivingDescription.md)

ArchivingDescription object that configures several archiving options

##### Returns

`boolean`

`true` if successful, `false` in case of any error

##### Since

ELC 3.51c / otrisPORTAL 5.1c

##### See

 - [ArchivingDescription](../classes/ArchivingDescription.md)
 - [DocFile.archive()](./DocFile.html#archive.archive-1)
 - [DocFile.archive(archiveKey)](./DocFile.html#archive.archive-2)

##### Examples

```ts
// Example for EE.i:
var myFile = context.file;
var ad = new ArchivingDescription();
ad.targetArchive = "$(#TOASTUP)\\STANDARD";
ad.archiveServer = "myeei";  // since Documents 4.0 using multi archive server
ad.archiveStatus = true;
ad.archiveMonitor = true;
ad.addRegister("all_docs");  // archive all attachments
var success = myFile.archive(ad);
if (success)
{
   context.returnType = "html";
   return ("<p>ArchiveFileID: " + myFile.getAttribute("Key") + "<p>");
}
```

```ts
// Example for EE.x:
var myFile = context.file;
var ad = new ArchivingDescription();
ad.targetView = "Unit=Default/Instance=Default/View=DeliveryNotes";
ad.targetSchema = "Unit=Default/Instance=Default/DocumentSchema=LIEFERSCHEINE";
ad.archiveServer = "myeex";  // since Documents 4.0 using multi archive server
ad.archiveStatus = true;
ad.archiveMonitor = true;
ad.addRegister("all_docs");  // archive all attachments
var success = myFile.archive(ad);
if (success)
{
   context.returnType = "html";
   return ("<p>ArchiveFileID: " + myFile.getArchiveKey() + "</p>");
}
```

```ts
// Example for EAS:
var myFile = context.file;
var ad = new ArchivingDescription();
ad.archiveServer = "myeas";  // using multi archive server
ad.archiveStatus = true;
ad.archiveMonitor = true;
ad.addRegister("all_docs");  // archive all attachments
var success = myFile.archive(ad);
if (success)
{
   context.returnType = "html";
   return ("<p>ArchiveFileID: " + myFile.getArchiveKey() + "</p>");
}
```

***

### archiveAndDelete()

> **archiveAndDelete**(): `boolean`

**Archive the DocFile object and remove the DOCUMENTS file.**  

The target archive has to be configured in the filetype definition (in the Windows Portal Client) as the default archive. 
It depends on the filetype settings as well, whether Status and Monitor will be archived as well. 
If no default archive is defined, the execution of this operation will fail.  
**Note:** It is strictly forbidden to access the DocFile object after this function has been executed successfully; 
if you try to access it, your script will fail, because the DocFile does not exist any longer in DOCUMENTS. 
For the same reason it is strictly forbidden to execute this function in a signal exit PortalScript.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
var myFile = context.file;
myFile.archiveAndDelete();
```

***

### asJSON()

> **asJSON**(`fieldList?`, `jsonMode?`): `string`

**Creates a JSON string of this file.**  
 
  
**Since:** DOCUMENTS 5.0c HF2 (new parameter fieldList)   
**Since:** DOCUMENTS 5.0F (new parameter jsonMode)

#### Parameters

##### fieldList?

`String`[]

**Default:** `[]`.  
optional String array to specify the JSON output. The array must contain field names and DocFile attributes from the following list 

+ `"DlcFile_Title"`
+ `"DlcFile_Owner"`
+ `"DlcFile_Created"` 
+ `"DlcFile_LastEditor"` 
+ `"DlcFile_LastModified"`

##### jsonMode?

`number`

**Default:** `0`.  
optional Integer bit mask to specify the JSON output structure. The jsonMode can be combined by the following values 
 
+ [\`util.JSON\_RAW\`](Util.md#json_raw) 
+ [\`util.JSON\_LABEL\`](Util.md#json_label) 
+ [\`util.JSON\_LOCALE\`](Util.md#json_locale)

#### Returns

`string`

`string` with JSON content.

#### Since

DOCUMENTS 5.0 HF1

#### See

[DocFile.fromJSON](#fromjson)

#### Example

```ts
var file = context.file;
util.out(file.asJSON());
// {
//    "DlcFile_Title": "Rechnung 17",
//    "DlcFile_Owner": "Schreiber, Willi",
//    "DlcFile_Created": "2019-11-08T10:42:42.000Z",
//    "DlcFile_LastEditor": "Schreiber, Willi",
//    "DlcFile_LastModified": "2019-11-08T10:45:10.000Z",
//    "company": "otris software AG",
//    "invoice_ts": "2019-11-08T10:45:10.000Z",     Zulu Time
//    "invoice_ok": true,
//    "invoice_no": 17,
//    "amount": 3.14,
// }
var file = context.file;
var fields = ["DlcFile_Title", "company"];
util.out(file.asJSON(fields));
// {
//    "DlcFile_Title": "Rechnung 17",
//    "company":"otris software AG"
// }
var file = context.file;
util.out(file.asJSON([], util.JSON_LOCALE));
// {
//    "DlcFile_Title": "Rechnung 17",
//    "DlcFile_Owner": "Schreiber, Willi",
//    "DlcFile_Created": "08.11.2019  11:42",
//    "DlcFile_LastEditor": "Schreiber, Willi",
//    "DlcFile_LastModified": "08.11.2019  11:45",
//    "company": "otris software AG",
//    "invoice_date": "08.11.2019  11:45",
//    "invoice_ok": true,
//    "invoice_no": 17,
//    "amount": "3,14",
// }
//
var file = context.file;
util.out(file.asJSON([], util.JSON_RAW | util.JSON_LABEL | util.JSON_LOCALE));
// {
//    "DlcFile_Title": "Rechnung 17",
//    "DlcFile_Owner": "Schreiber, Willi",
//    "DlcFile_Created": "08.11.2019  11:42",
//     ....
//     "raw":  {
//                "DlcFile_Title": "Rechnung 17",
//                "DlcFile_Created": "2019-11-08T10:42:42.000Z",
//                "company": "otris software AG",
//                ...
//              },
//     "label": {
//                "DlcFile_Title": "Titel",
//                "DlcFile_Created": "Erstellt am"",
//                "company": "Kundenname",
//                ...
//               }
// }
```

***

### cancelWorkflow()

> **cancelWorkflow**(`deleteSteps?`): `boolean`

**Cancel the current workflow for the file.**  

**Since:** DOCUMENTS 6.1.0 (new parameter `deleteSteps`)

#### Parameters

##### deleteSteps?

`boolean`

Optional flag indicating whether all workflow steps should be deleted.  
**Default:** `false`

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.51e / otrisPORTAL 5.1e

#### Example

```ts
var f = context.file;
f.cancelWorkflow();
```

***

### changeFiletype()

> **changeFiletype**(`nameFiletype`): `boolean`

**Change the filetype of this file.**

#### Parameters

##### nameFiletype

`string`

String containing the technical name of the filetype.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0e

#### Example

```ts
var file = context.file;
if (!file.changeFiletype("newFiletype"))
  util.out(file.getLastError());
```

***

### checkLifeCycleScript()

> **checkLifeCycleScript**(`event?`): `boolean`

**Executes the global otrLifeCycle_OnMasterExit Script-Exit If the property LifeCycleEnabled is set at the filetype the global otrLifeCycle_OnMasterExit Script will be started.**

#### Parameters

##### event?

`string`

optional String with en event name.

#### Returns

`boolean`

`true` if successful or in case of an error an exception will be thrown

#### Since

DOCUMENTS 5.0i

#### See

parameter 'checkLifeCyleScript' in [DocFile.sync()](#sync)

#### Example

```ts
try {
   var docFile = context.file;
   ... do something
   docFile.checkLifeCycleScript();
} catch (err) {
   util.out("Error: ") + err;
}
```

***

### checkRule()

> **checkRule**(`jsonRule`): `boolean`

**Function to check a DocFile rule.**

#### Parameters

##### jsonRule

`string`

String json-String with the rule

#### Returns

`boolean`

`true` if the rule is fulfilled, otherwise `false`

#### Since

DOCUMENTS 5.0h

***

### checkWorkflowReceiveSignal()

> **checkWorkflowReceiveSignal**(): `boolean`

**Checks the receive signals of the workflow for the DocFile object.**  

This method can only be used for a DocFile, that runs in a workflow and the workflow has receive signals. 
Usually the receive signals of the workflow step will be checked by a periodic job. 
Use this method to trigger the check of the receive signals for the DocFile.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 4.0a

#### Example

```ts
var myFile = context.file;
var succ = myFile.checkWorkflowReceiveSignal();
if (!succ)
   util.out(myFile.getLastError());
```

***

### clearFollowUpDate()

> **clearFollowUpDate**(`pUser`): `boolean`

**Clear a followup date for a desired user.**

#### Parameters

##### pUser

[`SystemUser`](SystemUser.md)

SystemUser object of the desired user

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.51b / otrisPORTAL 5.1b

#### See

[DocFile.setFollowUpDate](#setfollowupdate)

#### Example

```ts
var docFile = context.file;
var su = context.getSystemUser();
docFile.clearFollowUpDate(su);
```

***

### commit()

> **commit**(): `boolean`

**Commit any changes to the DocFile object.**  

This method is mandatory to apply changes to a file that has been switched to edit mode with the [DocFile.startEdit()](#startedit) method. 
It is strictly prohibited to execute the [DocFile.commit()](#commit) method in a script which is attached to the onSave scripting hook.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### See

[DocFile.startEdit](#startedit)  
[DocFile.sync](#sync)  
[DocFile.abort](#abort)

#### Example

```ts
var myFile = context.file;
if (!myFile) {
   throw "file undefined";
}
if (!myFile.startEdit()) {
   throw myFile.getLastError();
}
myFile.Field = "value";
if (!myFile.commit()) {
   var errorMsg = myFile.getLastError(); // Stores error message of commit(), if abort() does not work its error message is appended
   if (!myFile.abort()) {
      errorMsg += '\n' + myFile.getLastError();
   }
   throw errorMsg;
}
```

***

### connectFolder()

> **connectFolder**(`fObj`): `boolean`

**Store a reference to the current file in the desired target folder.**  

The (public) folder must be a real folder, it must not be a dynamic filter, nor a "only subfolder" object.

#### Parameters

##### fObj

[`Folder`](Folder.md)

Folder object representing the desired target public folder

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

ELC 3.51h / otrisPORTAL 5.1h

#### See

[DocFile.disconnectFolder](#disconnectfolder)

#### Example

```ts
var f = context.file;
var fObj = context.getFoldersByName("Invoices").first();
var success = f.connectFolder(fObj);
```

***

### countFields()

> **countFields**(`fieldName`): `number`

**Count fields with a desired name in the file.**  

**Note:** When this function is called on an EE.x DocFile with an empty field name, the return value may be greater than expected. 
The DOCUMENTS image of such a file can include EE.x system fields and symbolic fields for other imported scheme attributes (blob content, notice content).

#### Parameters

##### fieldName

`string`

String containing the technical name of the fields to be counted.

#### Returns

`number`

The number of fields als an Integer.

#### Since

DOCUMENTS 4.0c HF2

#### Example

```ts
var key = "Unit=Default/Instance=Default/Pool=DEMO/Pool=RECHNUNGEN/Document=RECHNUNGEN.41D3694E2B1E11DD8A9A000C29FACDC2@eex1"
var docFile = context.getArchiveFile(key);
if (!docFile)
   throw "archive file does not exist: " + key;
else
   util.out(docFile.countFields("fieldName"));
```

***

### createDocumentFromTemplate()

> **createDocumentFromTemplate**(`templateName`): `string`

**Creates a document using a document template, that was defined at the file type.**

#### Parameters

##### templateName

`string`

String name of the filetypes template that must be used

#### Returns

`string`

`string` with path to the created document object or an empty string, if failed.

#### Since

DOCUMENTS 5.0f

***

### createMonitorFile()

> **createMonitorFile**(`asPDF?`, `locale?`): `string`

**Creates a workflow monitor file in the server's file system.**  

This method creates a monitor file in the server's file system with the workflow monitor content of the DocFile. The file will be created as a html-file.  
**Note:** This generated file will no be automatically added to the DocFile

#### Parameters

##### asPDF?

`boolean`

**Default:** `false`.  
boolean parameter that indicates that a pdf-file must be created instead of a html-file

##### locale?

`string`

String (de, en,..) in which locale the file must be created (empty locale = log-in locale)

#### Returns

`string`

String containing the path of the created file

#### Since

DOCUMENTS 4.0a HF2

***

### createStatusFile()

> **createStatusFile**(`asPDF?`, `locale?`): `string`

**Creates a status file in the server's file system.**  

This method creates a status file in the server's file system with the status content of the DocFile. The file will be created as a html-file.  
**Note:** This generated file will no be automatically added to the DocFile

#### Parameters

##### asPDF?

`boolean`

**Default:** `false`.  
boolean parameter that indicates that a pdf-file must ge created instead of a html-file

##### locale?

`string`

String (de, en,..) in which locale the file must be created (empty locale = log-in locale)

#### Returns

`string`

String containing the path of the created file

#### Since

DOCUMENTS 4.0a HF2

***

### deleteFile()

> **deleteFile**(`moveTrash?`, `movePool?`, `allVersions?`, `easDeleteMode?`): `boolean`

**Delete the DocFile object.**  

If there's another PortalScript attached to the onDelete scripting hook, it will be executed right before the deletion takes place.  
**Note:** It is strictly forbidden to access the DocFile object after this function has been executed successfully; 
if you try to access it, your script will fail, because the DocFile does not exist any longer in DOCUMENTS. 
For the same reason it is strictly forbidden to execute this function in a signal exit PortalScript.  
**Note:** The parameters moveTrash, movePool are ignored for archive files. The parameters allVersions and easDeleteMode require an EAS/EDA file and are ignored otherwise.  
**Note:** The parameter easDeleteMode is interpreted in the following way. 
<ul>
<li> 0 = Use default setting (property "EASDeleteMode" of the archive store or factory setting); </li> 
<li> 1 = quick delete (restorable from WORM directory with archive administration tools); </li> 
<li> 2 = full delete (requires archive maintenance login "eas_keeper"). </li> 
</ul>
The last option ist occasionally needed to make a solution compliant with EU-GDPR. If a script tries to delete the actual "context.file", 
the server usually enforces "movePool = true". This is controlled by the common DOCUMENTS property "ContextFileDeleteProtection".  
  
**Since:** ELC 3.50n / otrisPORTAL 5.0n (moveTrash parameter)   
**Since:** ELC 3.51f / otrisPORTAL 5.1f (movePool parameter)   
**Since:** DOCUMENTS 4.0a HF1 (available for archive files)   
**Since:** DOCUMENTS 4.0e (all versions)   
**Since:** DOCUMENTS 5.0e (easDeleteMode)

#### Parameters

##### moveTrash?

`boolean`

**Default:** `false`.  
optional boolean parameter to decide whether to move the deleted file to the trash folder

##### movePool?

`boolean`

**Default:** `true`.  
optional boolean parameter to decide whether to move the deleted file's object to the file pool

##### allVersions?

`boolean`

**Default:** `false`.  
optional boolean parameter to delete all versions of an EAS archive file at once.

##### easDeleteMode?

`number`

**Default:** `0`.  
opional integer specifying the delete mode for an EAS archive file. See remarks.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
var myFile = context.file;
myFile.deleteFile(false, true);
```

***

### deleteScratchCopy()

> **deleteScratchCopy**(): `boolean`

**Delete the scratch copy related to a DocFile.**  

If there's another PortalScript attached to the `afterCancelEdit` scripting hook, it will be executed after the deletion takes place.  
**Note:** This function is only available for active files.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0i HF5

#### See

[context.getFilesWithScratchCopy](Context.md#getfileswithscratchcopy)

#### Example

```ts
var file = context.file;
if (!file.deleteScratchCopy())
	 util.out(file.getLastError());
```

***

### deleteWorkflowSteps()

> **deleteWorkflowSteps**(): `boolean`

**Delete all workflow steps for the file.**

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 6.1.0

#### Example

```ts
var f = context.file;
f.deleteWorkflowSteps();
```

***

### disconnectArchivedFile()

> **disconnectArchivedFile**(): `boolean`

**Uncouple an active file from the archived version.**

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0d

#### See

[DocFile.archive](#archive)

#### Example

```ts
var f = context.file;
var f.archive();
var success = f.disconnectArchivedFile();
```

***

### disconnectFolder()

> **disconnectFolder**(`fObj`): `boolean`

**Remove a reference to the current file out of the desired target folder.**  

The (public) folder must be a real folder, it must not be a dynamic filter, nor a "only subfolder" object.

#### Parameters

##### fObj

[`Folder`](Folder.md)

Folder object representing the desired target public folder

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

ELC 3.51h / otrisPORTAL 5.1h

#### See

[DocFile.connectFolder](#connectfolder)

#### Example

```ts
var f = context.file;
var fObj = context.getFoldersByName("Invoices").first();
var success = f.disconnectFolder(fObj);
```

***

### exportXML()

> **exportXML**(`pathXML`, `withDocuments`, `withStatus?`, `withMonitor?`): `boolean`

**Export the file as an XML file.**  
 
  
**Since:** ELC 3.60e / otrisPORTAL 6.0e (Option: export of status & monitor)

#### Parameters

##### pathXML

`string`

String containing full path and filename of the desired target xml file

##### withDocuments

`boolean`

boolean value to include the documents. The value must be set to `true` in case status or monitor information are to be inserted.

##### withStatus?

`boolean`

**Default:** `false`.  
boolean value to include status information. The value must be set to `true` in order to add the status. Status Information will then be generated into 
a file which will be added to the documents. Please note that therefore `withDocuments` must be set to true in order to get Status information.

##### withMonitor?

`boolean`

**Default:** `false`.  
boolean value to include Monitor information. The value must be set to `true` in order to add the monitor. Monitor Information will then be generated into 
a file which will be added to the documents. Please note that therefore `withDocuments` must be set to true in order to get Monitor information.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50a / otrisPORTAL 5.0a

#### Example

```ts
var docFile = context.file;
docFile.exportXML("c:\\tmp\\myXmlExport.xml", true, false, true);
```

***

### forwardFile()

> **forwardFile**(`controlFlowId`, `comment?`): `boolean`

**Forward file in its workflow via the given control flow.**  

This method only works if the file is inside a workflow and inside a workflow action that is accessible by a user of the web interface. Based on that 
current workflowstep you need to gather the ID of one of the outgoing control flows of that step. The access privileges of the current user who tries 
to execute the script are taken into account. Forwarding the file will only work if that control flow is designed to forward without query.  
**Note:** This function requires a full workflow engine license, it does not work with pure distribution lists.

#### Parameters

##### controlFlowId

`string`

String containing the technical ID of the outgoing control flow that should be passed

##### comment?

`string`

optional String value containing a comment to be automatically added to the file's monitor

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
var docFile = context.file;
var step = docFile.getCurrentWorkflowStep();
var flowId = step.firstControlFlow;
docFile.forwardFile(flowId);
```

***

### fromJSON()

> **fromJSON**(`jsonstring`): `boolean`

**Updates a file from a JSON-String.**  

**Note:** Only JSON-Strings that are created by DocFile.asJSON() with jsonMode = 0 can be imported Must be followed by `sync()`

#### Parameters

##### jsonstring

`string`

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0 HF1

#### See

[DocFile.asJSON](#asjson)

***

### getAllLockingWorkflowSteps()

> **getAllLockingWorkflowSteps**(): [`WorkflowStepIterator`](WorkflowStepIterator.md)

**Get a list of all locking workflow step that currently lock the file.**  

The locking workflow steps do not need to be locked by the current user executing the script, this function as well returns all locking steps which refer to different users.  
**Note:** This function requires a full workflow engine license, it does not work with pure distribution lists.

#### Returns

[`WorkflowStepIterator`](WorkflowStepIterator.md)

WorkflowStepIterator object which represents a list of all locking workflow steps for the file

#### Since

ELC 3.51e / otrisPORTAL 5.1e

#### See

[DocFile.getCurrentWorkflowStep](#getcurrentworkflowstep)  
[DocFile.getFirstLockingWorkflowStep](#getfirstlockingworkflowstep)

#### Example

```ts
var f = context.file;
var stepIter = f.getAllLockingWorkflowSteps();
if (stepIter.size() > 0)
   util.out("File is locked by " + stepIter.size() + " workflow steps");
```

***

### getAllWorkflowSteps()

> **getAllWorkflowSteps**(): [`WorkflowStepIterator`](WorkflowStepIterator.md)

**Get a list of all workflow step of the file.**  

The methd will return all workflow steps, the currently locking and the previous ones.  
**Note:** This function requires a full workflow engine license, it does not work with pure distribution lists.

#### Returns

[`WorkflowStepIterator`](WorkflowStepIterator.md)

WorkflowStepIterator object which represents a list of all workflow steps for the file

#### Since

DOCUMENTS 5.0b

#### See

[DocFile.getCurrentWorkflowStep](#getcurrentworkflowstep)   
[DocFile.getFirstLockingWorkflowStep](#getfirstlockingworkflowstep)

#### Example

```ts
var f = context.file;
var stepIter = f.getAllWorkflowSteps();
```

***

### getArchiveKey()

> **getArchiveKey**(`withServer?`): `string`

**After archiving of a file this method returns the key of the file in the archive.**  

**Note:** If the file is not archived or archived without versioning or uncoupled from the achived file the key is empty.  
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Parameters

##### withServer?

`boolean`

**Default:** `true`.  
optional boolean value to indicate, if the key should include an "@archiveServerName" appendix

#### Returns

`string`

String containing the key.

#### Since

ELC 3.60a / otrisPORTAL 6.0a

#### See

[DocFile.archive](#archive)

#### Example

```ts
var f = context.file;
if (f.archive())
   util.out(f.getArchiveKey());
else
   util.out(f.getLastError());
```

***

### getAsPDF()

> **getAsPDF**(`nameCoverTemplate`, `createCover`, `sourceRegisterNames`): `string`

**Create a PDF file containing the current DocFile's contents and returns the path in the file system.**  

The different document types of your documents on your different tabs require the appropriate PDF filter programs to be installed and configured in DOCUMENTS.

#### Parameters

##### nameCoverTemplate

`string`

String containing the name of the pdf cover template defined at the filetype

##### createCover

`boolean`

boolean whether to create a field list or to only take the documents

##### sourceRegisterNames

`any`[]

Array with the technical names of the document registers you want to include

#### Returns

`string`

`String` with file path of the pdf, an empty string in case of any error

#### Since

DOCUMENTS 4.0b

#### Example

```ts
var source = new Array();
source.push("FirstRegister");
source.push("SecondRegister");
var docFile = context.file;
var pathPdfFile = docFile.getAsPDF("pdfcover", true, source);
if (pathPdfFile == "")
   throw docFile.getLastError();
util.out("Size: " + util.fileSize(pathPdfFile))
```

***

### getAttribute()

#### Call Signature

> **getAttribute**(`attribute`): `string`

**Get the String value of an attribute of the file.**  
 
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

##### Parameters

###### attribute

`string`

String containing the name of the desired attribute

##### Returns

`string`

String containing the value of the desired attribute

##### Since

ELC 3.50 / otrisPORTAL 5.0

##### Example

```ts
var myFile = context.file;
util.out(myFile.getAttribute("Title"));
```

#### Call Signature

> **getAttribute**(`attribute`): `string`

**`Internal`**

**Get the String value of an attribute of the file.**  

This function is for internal use only!

##### Parameters

###### attribute

`string`

String containing the name of the desired attribute

##### Returns

`string`

##### Since

DOCUMENTS 5.0f HF1 (Support for file type attributes / properties)

##### Example

```ts
var myFile = context.file;
util.out(myFile.getAttribute("Title"));  // Title of the DocFile
util.out(myFile.getAttribute("filetype.Title"));  // Title of the file type of the DocFile
util.out(myFile.getAttribute("filetype.$showBlobAsPdf"));  // Property showBlobAsPdf from the file type
```

***

### getAutoText()

> **getAutoText**(`autoText`, `startTag?`, `endTag?`): `string`

**Get the String value of a DOCUMENTS autotext.**  
 
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files   
**Since:** DOCUMENTS 5.0i new optional parameters startTag and endTag

#### Parameters

##### autoText

`string`

the rule to be parsed

##### startTag?

`string`

**Default:** `"%"`.  
optional start tag.

##### endTag?

`string`

**Default:** `"%"`.  
otional end tag.

#### Returns

`string`

String containing the parsed value of the autotext

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
var myFile = context.file;
util.out(myFile.getAutoText("fileOwner"));
```

***

### getCopy()

> **getCopy**(`copyMode`): `DocFile`

**Duplicate a file.**  

This function creates a real 1:1 copy of the current file which may be submitted to its own workflow. The function returns the copied file. 
If an error occurrs, the function returns `null` and `getLastError()` can be called on the calling object.

#### Parameters

##### copyMode

defines how to handle the documents of the originating file.  
There are three different parameter values allowed: 

+ `"NoDocs"` copied DocFile does not contain any documents  
+ `"ActualVersion"` copied DocFile contains only the latest (published) version of each document 
+ `"AllVersions"` copied DocFile contains all versions (both published and locked) of each document

`"NoDocs"` | `"ActualVersion"` | `"AllVersions"`

#### Returns

`DocFile`

DocFile object representing the copied file, `null` in case of error

#### Since

ELC 3.51c / otrisPORTAL 5.1c

#### Example

```ts
var docFile = context.file;
var newFile = docFile.getCopy("AllVersions");
if (!newFile)
  util.out(docFile.getLastError());
```

***

### getCreationDate()

> **getCreationDate**(): `Date`

**Returns the creation date (timestamp) of a DocFile.**

#### Returns

`Date`

`Date` object, if the date is valid, `null` for an invalid data.

#### Since

DOCUMENTS 5.0c

#### See

[DocFile.getCreator](#getcreator)  
[DocFile.getLastModificationDate](#getlastmodificationdate)

#### Example

```ts
var file = context.file;
var c_ts = file.getCreationDate();
if (c_ts)
   util.out(c_ts);
```

***

### getCreator()

> **getCreator**(`asObject?`): `any`

**Returns the SystemUser object or fullname as String of the creator of the DocFile.**

#### Parameters

##### asObject?

`boolean`

**Default:** `false`.  
optional boolean value, that specifies, if the SystemUser object or the fullname should be returned.

#### Returns

`any`

`asObject=true:``SystemUser` object or `null` (if user does not exist anymore)

#### Since

DOCUMENTS 5.0c

#### See

[DocFile.getLastModifier](#getlastmodifier)  
[DocFile.getCreationDate](#getcreationdate)

#### Example

```ts
var file = context.file;
var su = file.getCreator(true);
if (su)
   util.out(su.login);
else
   util.out(file.getCreator());
```

***

### getCurrentWorkflowStep()

> **getCurrentWorkflowStep**(): [`WorkflowStep`](WorkflowStep.md)

**Get the current workflow step of the current user locking the file.**  

The function returns a valid [WorkflowStep](WorkflowStep.md) object if there exists one for the current user. If the current user does not lock the file, the function returns `null` instead.  
**Note:** This function requires a full workflow engine license, it does not work with pure distribution lists.

#### Returns

[`WorkflowStep`](WorkflowStep.md)

WorkflowStep object

#### Since

ELC 3.51e / otrisPORTAL 5.1e

#### See

[DocFile.getFirstLockingWorkflowStep](#getfirstlockingworkflowstep)

#### Example

```ts
var f = context.file;
var step = f.getCurrentWorkflowStep();
if (!step)
   step = f.getFirstLockingWorkflowStep();
// still no workflow steps found? File not in workflow
if (!step)
   util.out("File is not in a workflow");
```

***

### getCustomProperties()

> **getCustomProperties**(`nameFilter?`, `typeFilter?`): [`CustomPropertyIterator`](CustomPropertyIterator.md)

**Get a [CustomPropertyIterator](CustomPropertyIterator.md) with all [CustomProperty](CustomProperty.md) of an active file.**  

This method returns a CustomPropertyIterator with the CustomProperty of the file.

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

DOCUMENTS 6.1.0

#### See

[DocFile.setOrAddCustomProperty](#setoraddcustomproperty)  
[DocFile.addCustomProperty](#addcustomproperty)

#### Example

```ts
var docFile = context.file;
var itProp = docFile.getCustomProperties();
for (var prop = itProp.first(); prop; prop = itProp.next())
{
   util.out(prop.name + ": " + prop.value);
}
```

***

### getDocFileComment()

> **getDocFileComment**(): [`DocFileDataField`](DocFileDataField.md)

**Returns the comment value for a DocFile.**

#### Returns

[`DocFileDataField`](DocFileDataField.md)

`DocFileDataField` object or `null`.

#### Since

DOCUMENTS 5.0d

***

### getDoubleSelectListValues()

> **getDoubleSelectListValues**(`fieldName`, `resolved?`): `string`[]

**Get the enumeration values of the desired double select list field.**

#### Parameters

##### fieldName

`string`

String containing the technical field name can be followed by the desired instance number in form techFieldName[i] 
for multi-instance fields of an EE.i/EE.x archive file.  

**Note:** The index `i` is zero-based. The specification of field instance is olny available for an EE.i/EE.x archive file, 
it will be ignored for other files. If the parameter contains no instance information, the first field instance is used. 
The field instance order is determined by the field order in the file.

##### resolved?

`boolean`

**Default:** `false`.  
Optional boolean value indicating whether to return the full multi language enumeration values (e.g. "key;de:Wert;en:Value") instead of only the keys (e.g. "key").

#### Returns

`string`[]

Array of strings containing the multi language enumeration values or only the keys.

#### Since

DOCUMENTS 5.0e HF2

#### Example

```ts
var myFile = context.file;
var values = myFile.getDoubleSelectListValues("DoubleListfield", true);
if (values)
{
  for (var i = 0; i < values.length; i++)
  {
      util.out(values[i]);
  }
}
```

***

### getEnumAutoText()

> **getEnumAutoText**(`autoText`): `any`[]

**Get an array with the values of an enumeration autotext.**

#### Parameters

##### autoText

`string`

to be parsed

#### Returns

`any`[]

Array containing the values for the autotext

#### Since

ELC 3.60e / otrisPORTAL 6.0e

#### Example

```ts
var values = context.getEnumAutoText("%accessProfile%")
if (values)
{
  for (var i=0; i < values.length; i++)
  {
      util.out(values[i]);
  }
}
```

***

### getFieldAttribute()

> **getFieldAttribute**(`fieldName`, `attrName`): `string`

**Get the String value of an attribute of the desired file field.**  
 
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Parameters

##### fieldName

`string`

String containing the technical name of the desired field

##### attrName

`string`

String containing the name of the desired attribute

#### Returns

`string`

String containing the value of the desired field attribute

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
var myFile = context.file;
util.out(myFile.getFieldAttribute("Samplefield", "Value"));
```

***

### getFieldAutoText()

> **getFieldAutoText**(`fieldName`, `autoText?`): `string`

**Returns an AutoText value of a specified field of the DocFile.**  

The following AutoTexts are available 
 
+ `"[locale]"` - field value in the user locale or specified locale. 
+ `"key"` - key value (e.g. at refence fields, enumeration fields, etc.). 
+ `"fix"` - fix format value (e.g. at numeric fields, date fields, etc.).
+ `"pos"` - order position of the field value at enumeration fields.
+ `"raw"` - database field value. 
+ `"label[.locale]"` - label of the field in user locale or specified locale.

#### Parameters

##### fieldName

`string`

Name of the field as string

##### autoText?

`string`

**Default:** `"[locale]"`.  
The desired AutoText (see list) as string (default = "[locale]" returns field value in the user locale)

#### Returns

`string`

`String` with the AutoText.

#### Since

DOCUMENTS 5.0c

#### Example

```ts
var file = context.file;
util.out(file.getFieldAutoText("erpInvoiceDate"));             // => 31.12.2017
util.out(file.getFieldAutoText("erpInvoiceDate", "en"));       // => 12/31/2017
util.out(file.getFieldAutoText("erpInvoiceDate", "fix"));      // => 20171231
util.out(file.getFieldAutoText("erpInvoiceDate", "label"));    // => Rechnungsdatum
util.out(file.getFieldAutoText("erpInvoiceDate", "label.en")); // => Invoice date
```

***

### getFieldName()

> **getFieldName**(`index`): `string`

**Get the technical name of the n-th field of the file.**  

This allows generic scripts to be capable of different versions of the same filetype, e.g. if you changed details of the filetype, 
but there are still older files of the filetype in the system.  
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Parameters

##### index

`number`

index of the desired field

#### Returns

`string`

string containing the technical name of the file field, `false` if index is out of range

#### Since

ELC 3.50e / otrisPORTAL 5.0e

#### Example

```ts
var myFile = context.file;
var fieldName = "Samplefield";
var fields = new Array();
var i = 0;
// get all field names
while (myFile.getFieldName(i))
{
   fields[i] = myFile.getFieldName(i)
   i++;
}
// check for field existance
var found = false;
for (var j = 0; j < fields.length; j++)
{
   if (fields[j] == fieldName)
   {
      found = true;
      break;
   }
}
```

***

### getFieldValue()

> **getFieldValue**(`fieldName`, `returnType?`): `any`

**Get the value of the desired file field.**  
 
  
**Since:** DOCUMENTS 4.0c HF2 available for multi-instance fields of an EE.i/EE.x archive file   
**Since:** DOCUMENTS 5.0e HF2 (optional parameter `returnType`)   
**Since:** DOCUMENTS 5.0i HF6 (`Nullable` for parameter `returnType`)

#### Parameters

##### fieldName

`string`

String containing the technical field name can be followed by the desired instance number in form techFieldName[i] 
for multi-instance fields of an EE.i/EE.x archive file.   

**Note:** The index `i` is zero-based. The specification of field instance is olny available for an EE.i/EE.x archive file, 
it will be ignored for other files. If the parameter contains no instance information, the first field instance is used. 
The field instance order is determined by the field order in the file.

##### returnType?

`string`

Optional string specified the type of the return value. Currently only the following values are available:

+ `"Array"` for a double select list field
+ `"Nullable"` for a numeric field: the function returns `null`, if the field empty, otherwise the field value.

#### Returns

`any`

The field value, its type depends on the field type (such as a Date object returned for a field of type 'Timestamp') 
or the specified return type if applicable.

#### Since

DOCUMENTS 4.0c

#### See

 - [DocFile.setFieldValue](#setfieldvalue)
 - [Field Access Methods](../fieldmethods.html)

#### Example

```ts
var myFile = context.file;
util.out(myFile.getFieldValue("Samplefield"));
// Since DOCUMENTS 4.0c HF2
var key = "Unit=Default/Instance=Default/Pool=FeldZ/Document=Feldzahlen.86C94C30438011E2B925080027B22D11@eex1";
var eexFile = context.getArchiveFile(key);
util.out(eexFile.getFieldValue("multiInstanceField[2]"));
// Since DOCUMENTS 5.0e HF2
var myFile = context.file;
var values = myFile.getFieldValue("doubleListfield", "Array");
if (values)
{
  for (var i = 0; i < values.length; i++)
  {
      util.out(values[i]);
  }
}
```

***

### getFileOwner()

> **getFileOwner**(): [`SystemUser`](SystemUser.md)

**Get the file owner of the file.**

#### Returns

[`SystemUser`](SystemUser.md)

SystemUser object representing the user who owns the file

#### Since

ELC 3.51d / otrisPORTAL 5.1d

#### Example

```ts
var docFile = context.file;
var su = docFile.getFileOwner();
util.out(su.login);
```

***

### getFirstLockingWorkflowStep()

> **getFirstLockingWorkflowStep**(): [`WorkflowStep`](WorkflowStep.md)

**Get the first locking workflow step that currently locks the file.**  

The first locking workflow step does not need to be locked by the current user executing the script, 
this function as well returns the first locking step if it is locked by a different user. 
If no locking step is found at all, the function returns `null` instead.  

**Note:** This function requires a full workflow engine license, it does not work with pure distribution lists.

#### Returns

[`WorkflowStep`](WorkflowStep.md)

WorkflowStep object

#### Since

ELC 3.50e / otrisPORTAL 5.0e

#### See

[DocFile.getCurrentWorkflowStep](#getcurrentworkflowstep)

#### Example

```ts
var f = context.file;
var step = f.getCurrentWorkflowStep();
if (!step)
{
   step = f.getFirstLockingWorkflowStep();
}
// still no workflow steps found? File not in workflow
if (!step)
{
   util.out("File is not in a workflow");
}
```

***

### getid()

> **getid**(): `string`

**Returns the file id of the DocFile.**

#### Returns

`string`

`String` with the file id.

#### Since

DOCUMENTS 5.0c

#### Example

```ts
var file = context.file;
util.out(file.getid());
```

***

### getLastError()

> **getLastError**(`shortMessage?`): `string`

**Function to get the description of the last error that occurred.**  
 
  
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

#### Example

```ts
var myFile = context.file;
// do something which may go wrong
if (!myFile.setUserStatus("user_notExist", "standard"))
{
   util.out(myFile.getLastError());
}
```

***

### getLastModificationDate()

> **getLastModificationDate**(): `Date`

**Returns the last modification date (timestamp) of a DocFile.**

#### Returns

`Date`

`Date` object, if the date is valid, `null` for an invalid data.

#### Since

DOCUMENTS 5.0c

#### See

[DocFile.getLastModifier](#getlastmodifier)  
[DocFile.getCreationDate](#getcreationdate)

#### Example

```ts
var file = context.file;
var c_ts = file.getLastModificationDate();
if (c_ts)
   util.out(c_ts);
```

***

### getLastModifier()

> **getLastModifier**(): `string`

**Returns the fullname as String of the last editor of the DocFile.**

#### Returns

`string`

`String` with the fullname.

#### Since

DOCUMENTS 5.0c

#### See

[DocFile.getCreator](#getcreator)  
[DocFile.getLastModificationDate](#getlastmodificationdate)

#### Example

```ts
var file = context.file;
util.out(file.getLastModifier());
```

***

### getLockedBy()

> **getLockedBy**(): `string`

**Returns the login of the user the DocFile locked by.**

#### Returns

`string`

`String` with the login.

#### Since

DOCUMENTS 5.0i HF5

#### Example

```ts
var file = context.file;
util.out(file.getLockedBy());
```

***

### getOID()

> **getOID**(`oidLow?`): `string`

**Returns the object-id.**  
 
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files   
**Since:** DOCUMENTS 5.0 (new parameter oidLow)

#### Parameters

##### oidLow?

`boolean`

**Default:** `false`.  
Optional flag:   
If `true` only the id of the DocFile object (`m_oid`) will be returned.   
If `false` the id of the DocFile object will be returned together with the id of the corresponding class in the form `class-id:m_oid`.

#### Returns

`string`

`String` with the object-id

#### Since

ELC 3.60c / otrisPORTAL 6.0c

***

### getOriginal()

> **getOriginal**(): `DocFile`

**Get the orginal file for a scratch copy.**  

If you run a scipt on a scratch copy (e.g. a onSave script), you can get the orginal file with this function.

#### Returns

`DocFile`

DocFile

#### Since

DOCUMENTS 4.0 (EAS)

#### Example

```ts
var scratchCopy = context.file;
var origFile = scratchCopy.getOriginal();
if (!origFile)
   util.out(scratchFile.getLastError();
else
{
   if (scratchCopy.FieldA != origFile.FieldA)
      util.out("Field A changed");
   else
      util.out("Field A not changed");
}
```

***

### getReferenceFile()

> **getReferenceFile**(`referenceFileField`): `null` \| `DocFile`

**Get the file referred by a reference field in the current file.**  

If the current file's filetype is connected to a superior filetype by a reference field, 
this function allows to easily access the referred file, e.g. if you are in an invoice file 
and you want to access data of the referring company.  
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Parameters

##### referenceFileField

`string`

String value containing the technical name of the file field contianing the definition to the referred filetype

#### Returns

`null` \| `DocFile`

DocFile object representing the referred file if successful, `null` in case of any error

#### Since

ELC 3.51c / otrisPORTAL 5.1c

#### Example

```ts
var docFile = context.file;
var company = docFile.getReferenceFile("crmCompany"); 
if(!company) { 
     if(!docFile.crmCompany) { 
         throw "No company set in the reference field";
     } else {
         throw "The function 'getReferenceFile' failed";
     }
}
util.out(company.crmCompanyName);
```

***

### getRegisterByName()

> **getRegisterByName**(`registerName`, `checkAccessRight?`): `null` \| [`Register`](Register.md)

**Note:** Until version 5.0c this method ignored the access rights of the user to the register. 
With the optional parameter checkAccessRight this can now be done. For backward compatibility the default value is set to false.  
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files   
**Since:** DOCUMENTS 5.0c (new optional parameter checkAccessRight)

#### Parameters

##### registerName

`string`

String value containing the technical name of the desired register

##### checkAccessRight?

`boolean`

**Default:** `false`.  
optional boolean value, that indicates if the access rights should be considered.

#### Returns

`null` \| [`Register`](Register.md)

Register object representing the desired register or null in case of any error

#### Since

ELC 3.50n / otrisPORTAL 5.0n

#### See

[DocFile.getRegisters](#getregisters)

#### Example

```ts
var docFile = context.file;
var reg = docFile.getRegisterByName("Documents");
if (reg) {
  // ...
} else {
  throw new Error(docFile.getLastError());
}
```

***

### getRegisters()

> **getRegisters**(`type?`, `checkAccessRight?`): [`RegisterIterator`](RegisterIterator.md)

**Get an iterator with the registers of the file for the specified type.**  

**Note:** Until version 5.0c this method ignored the access rights of the user to the register. 
With the optional parameter checkAccessRight this can now be done. For backward compatibility the default value is set to false.  
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files   
**Since:** DOCUMENTS 5.0c (new optional parameter checkAccessRight)

#### Parameters

##### type?

`string`

**Default:** `"documents"`.  
optional String value to filter for a desired register type. Default type is `documents`  
Allowed values: 
 
+ `documents` 
+ `fields` 
+ `links` 
+ `archiveddocuments`
+ `externalcall` 
+ `all` (returns all registers independent of the type)

##### checkAccessRight?

`boolean`

**Default:** `false`.  
optional boolean value, that indicates if the access rights should be considered.

#### Returns

[`RegisterIterator`](RegisterIterator.md)

RegisterIterator with all registers (matching the filter)

#### Since

ELC 3.50n / otrisPORTAL 5.0n

#### See

[RegisterIterator](RegisterIterator.md)  
[DocFile.getRegisterByName](#getregisterbyname)

#### Example

```ts
var docFile = context.file;
var regIter = docFile.getRegisters("documents");
```

***

### getRuleValue()

> **getRuleValue**(`value`, `type?`): `any`

**Function to get a value of DocFile rule.**

#### Parameters

##### value

`string`

String value of the rule value

##### type?

`string`

**Default:** `"auto"`.  
Optional data type of the value (number, boolean, date, timestamp, auto)

#### Returns

`any`

The rule value in the desired type or `null`, if failed

#### Since

DOCUMENTS 5.0h

***

### getStatusAsJSON()

> **getStatusAsJSON**(`locale?`): `string`

**Get the status of the DocFile as a JSON string.**

#### Parameters

##### locale?

`string`

String (`"de"`, `"en"`, ...) in which locale the status has to be returned (empty locale = log-in locale)

#### Returns

`string`

String containing the JSON string with the status in the following structure: 
 
```json
 [ 
    { "Action": "File edited", 
      "Comment": "test", 
      "Time": "01/18/2022 15:39", 
      "User": "Schreiber, Willi", 
    }, 
     ... 
 ]
```

#### Since

DOCUMENTS 5.0h HF1

#### Example

```ts
var docFile = context.file;
var jsonStr = docFile.getStatusAsJSON("en");
var jsonArr = JSON.parse(jsonStr);
for (var status of jsonArr)
{
  util.out("-------------------");
  for (var prop in status)
  {
      util.out(prop + ": " + status[prop]);
  }
  util.out("-------------------");
}
```

***

### getTitle()

> **getTitle**(`locale?`): `string`

**Returns the title of the DocFile.**  

**Note:** the special locale raw returns the title in all locales

#### Parameters

##### locale?

`string`

**Default:** `user locale`.  
Locale as String (default = user locale)

#### Returns

`string`

`String` with the title.

#### Since

DOCUMENTS 5.0c

#### Example

```ts
var file = context.file;
util.out(file.getTitle("en"));
```

***

### getUserRead()

> **getUserRead**(`login`): `boolean`

**Gather information whether the file is marked as read or unread for a desired user.**  

**Note:** This function requires a full workflow engine license, it does not work with pure distribution lists.

#### Parameters

##### login

`string`

String containing the login name of the desired user

#### Returns

`boolean`

boolean value whether the file is marked as read for the desired user.

#### Since

DOCUMENTS 5.0h

#### See

[DocFile.setUserRead](#setuserread)

#### Example

```ts
var docFile = context.file;
var fileRead = docFile.getUserRead("schreiber");
```

***

### getUserStatus()

> **getUserStatus**(`login`): `string`

**Get the status of the file for a desired user.**

#### Parameters

##### login

`string`

String containing the login name of the desired user

#### Returns

`string`

String with the status. Possible values: 

+ `standard` 
+ `new` 
+ `fromFollowup` 
+ `toForward` 
+ `forInfo`
+ `task` 
+ `workflowCanceled` 
+ `backFromDistribution` 
+ `consultation`

#### Since

DOCUMENTS 4.0c HF1

#### See

[DocFile.setUserStatus](#setuserstatus)

#### Example

```ts
var docFile = context.file;
util.out(docFile.getUserStatus("schreiber"));
```

***

### getVisibleFields()

> **getVisibleFields**(`options?`): `boolean` \| `string`[]

**`Internal`**

**List all visible fields.**

#### Parameters

##### options?

`number`

An optional integer number (bitmask) supports any combination of the following values:

| Bit # | Value             | Meaning                              |
|-------|-------------------|--------------------------------------|
| 0     | 1 (2<sup>0</sup>) | Consider workflow rights             |
| 1     | 2 (2<sup>1</sup>) | Consider standard fields             |
| 2     | 4 (2<sup>2</sup>) | Consider comment field               |

The bits not listed above should remain zero for upward compatibility. Hint for beginners: bitmask values
are always powers of 2. They can be combined with "|" or with "+". The expression (1|2|4) evaluates
to 7 for example.

The default value is 1.

#### Returns

`boolean` \| `string`[]

An array with the names of all visible fields or `false` in case of any error.

#### Since

DOCUMENTS 5.0i HF5

***

### getWebKey()

> **getWebKey**(): `string`

**Function to get webkey to use in the WebClient.**

#### Returns

`string`

String with key

#### Since

DOCUMENTS 5.0f

***

### hasField()

> **hasField**(`fieldName`): `boolean`

**Gather information whether the current file has the field with the desired name.**

#### Parameters

##### fieldName

`string`

String containing the technical name of the field.

#### Returns

`boolean`

`true` if the file has the field, `false` if not

#### Since

DOCUMENTS 4.0d

#### Example

```ts
var file = context.file;
if (file.hasField("address"))
  util.out(file.address);
```

***

### insertStatusEntry()

> **insertStatusEntry**(`action`, `comment`): `boolean`

**Add an entry to the status tab of the file.**  

This function is especially useful in connection with PortalScripts being used as decision guards in workflows, 
because this allows to comment and describe the decisions taken by the scripts. This increases transparency concerning the life cycle of a file in DOCUMENTS.

#### Parameters

##### action

`string`

String containing a brief description

##### comment

`string`

optional String containing a descriptive comment to be added to the status entry

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.51b / otrisPORTAL 5.1b

#### Example

```ts
var docFile = context.file;
docFile.insertStatusEntry("Executed Guard Script","all conditions met");
```

***

### isArchiveFile()

> **isArchiveFile**(): `boolean`

**Gather information whether the current file is an archive file.**

#### Returns

`boolean`

`true` if is an archive file, `false` if not

#### Since

ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Example

```ts
var key = "Unit=Default/Instance=Default/Pool=DEMO/Pool=RECHNUNGEN/Document=RECHNUNGEN.41D3694E2B1E11DD8A9A000C29FACDC2"
var docFile = context.getArchiveFile(key);
if (docFile)
  util.out(docFile.isArchiveFile());
```

***

### isDeletedFile()

> **isDeletedFile**(): `boolean`

**Gather information whether the current file is a deleted file of a trash folder.**

#### Returns

`boolean`

`true` if is a deleted file, `false` if not

#### Since

ELC 3.60e / otrisPORTAL 6.0e

#### Example

```ts
...
var trashFolder = user.getPrivateFolder("trash");
if (trashFolder)
{
   var it = trashFolder.getFiles();
   for (var file = it.first(); file; file = it.next())
   {
       if (file.isDeletedFile())
          util.out("ok");
       else
          util.out("Error: Found undeleted file in trash folder!");
   }
}
```

***

### isNewFile()

> **isNewFile**(): `boolean`

**Gather information whether the current file is a new file.**

#### Returns

`boolean`

`true` if new file, `false` if not

#### Since

ELC 3.50l01 / otrisPORTAL 5.0l01

#### Example

```ts
var docFile = context.file;
util.out(docFile.isNewFile());
```

***

### isSealed()

> **isSealed**(): `boolean`

**Checks, if the file is sealed.**

#### Returns

`boolean`

`true` if sealed, otherwise `false`

#### Since

DOCUMENTS 5.0i

#### See

[seal](#seal)

#### Example

```ts
var file = context.file;
util.out(file.isSealed())
```

***

### pdo()

> **pdo**(`filetype?`): `PDObject`

**`Internal`**

**Function returns the PDObject of the file or the file type.**  

This function is for internal use only!

#### Parameters

##### filetype?

`boolean`

**Default:** `false`.  
boolean parameter that indicates that the PDObject of the file type is requested

#### Returns

`PDObject`

#### Since

DOCUMENTS 5.0f HF1

***

### reactivate()

> **reactivate**(): `boolean`

**Reactivate an archive file to a file of the corresponding filetype.**

#### Returns

`boolean`

`true` if successful, `false` if not - get error message with getLastError()

#### Since

ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Example

```ts
var key = "Unit=Default/Instance=Default/Pool=DEMO/Pool=RECHNUNGEN/Document=RECHNUNGEN.41D3694E2B1E11DD8A9A000C29FACDC2@eex1"
var docFile = context.getArchiveFile(key);
if (!docFile)
   throw "archive file does not exist: " + key;
if (!docFile.reactivate())
   throw "Reactivation failed: " + docFile.getLastError();
docFile.startWorkflow....
```

***

### readEASLifeCycle()

> **readEASLifeCycle**(): `string`

**Read the life cycle timestamp and action of an EAS-archived DocFile.**

#### Returns

`string`

JSON String with the elements 'timestamp' and 'action' or `null` if there are not any lifecycle info at the EAS file; in case of an error an exception will be thrown

#### Since

DOCUMENTS 5.0h

#### See

[writeEASLifeCycle](#writeeaslifecycle)

#### Example

```ts
// Somehow gain access to a EAS DocFile docFile
try {
   const json = docFile.readEASLifeCycle();
   if (!json)
       throw "There is no life cycle info at the EAS file";
   // e.g. json = " { timestamp : "2021-10-06T14:08:01.988Z", action : "delete" } "
   const lifeCycleInfos = JSON.parse(json);
   if (lifeCycleInfos.timestamp != "")
   {
       const dateObj = new Date(lifeCycleInfos.timestamp);
       util.out("Timestamp: " + dateObj);
   }
   util.out("Action: " + lifeCycleInfos.action);
} catch (err) {
   util.out("Error: ") + err;
}
```

***

### readEASRecordAnnotations()

> **readEASRecordAnnotations**(`typeName`): `string`

**Read record-annotations of an EAS-archived DocFile.**  

Load and return annotation data of an EAS record. If the actual DocFile is not a representation of an EAS record, 
the function throws an exception. It also throws one, if the archive is inaccessible (technically or by rights management).  

 **Note:** The structure of the returned JSON is an array of objects with string-properties "type" and "value". 
Multiple annotations of the same type may exist. This operation only accesses annotations at the DocFile level 
("record" in EAS terminology). It cannot access annotations at the Document ("attachment") level. Unlike fields, 
annotations in the archive are not sealed for auditing purposes. Modifications occur without versioning.

#### Parameters

##### typeName

`string`

An optional string with the technical name of an annotation-type for filtering purposes. 
A script can omit the parameter or pass an empty string or pass "*" to read all annotations.

#### Returns

`string`

JSON string with annotation data.

#### Since

DOCUMENTS 5.0h

#### See

[writeEASRecordAnnotations](#writeeasrecordannotations)

#### Example

```ts
// Somehow gain access to a DocFile, which is
// a DOCUMENTS image of an EAS archive record
// (This example uses a search request.)
const searchsource="Typentest@EDA2"; // Resource pattern: "file_type@archive_server"
const keyfield = "F1_String";
const keyvalue = "RecordAnno1 Scripting";
var filter = keyfield + "|~" + util.getQuoted(keyvalue);
var hrs = new HitResultset(searchsource, filter, "");
if(hrs.getLastErrorCode() != 0 || hrs.size() <= 0)
    throw new Error("Test record not found.");
var df = hrs.first().getArchiveFile();
hrs.dispose(); // hrs is no longer needed.
if(df === null)
    throw new Error("Failed to create DOCUMENTS image of the test record.");
// Read and log the standard text annotations, which come
// from thw webclient's "Actions / add note" feature.
var textAnnos = df.readEASRecordAnnotations("3X");
util.out("\"3X\" annotations: " + textAnnos);
```

***

### restore()

> **restore**(): `boolean`

**Invalidates the Javascript-Docile Object cache and reads the data from the database again.**

#### Returns

`boolean`

`true`

#### Since

DOCUMENTS 5.0i

#### See

[restore](#restore)

***

### seal()

> **seal**(`value`): `boolean`

**Seal or unseal the file.**  

After sealing the file, it is not possible to modify it anymore.  

**Note:** Important: To use this method the user has to be switched to SuperMode (s. context.setSuperMode()). 
Sealing of a file is only possible, if it is not already sealed - otherwise an exception will be thrown. 
Unsealing of a file is only possible, if it is sealed - otherwise an exception will be thrown.

#### Parameters

##### value

`boolean`

boolean to seal / unseal the file.

#### Returns

`boolean`

`true` if successful or in case of an error an exception will be thrown

#### Since

DOCUMENTS 5.0i

#### See

[isSealed](#issealed)

#### Example

```ts
var file = context.file;
// sealing
try {
   if (!file.isSealed()) {
      context.setSuperMode(true); 
      file.seal(true);
   }
} catch (err) {
   util.out("Error: ") + err;
} finally {
   // Important: switch off the SuperMode!
   if (context.getSuperMode())
      context.setSuperMode(false);
}
// unsealing
try {
   if (file.isSealed()) {
      context.setSuperMode(true);
      file.seal(false);
   }
} catch (err) {
   util.out("Error: ") + err;
} finally {
   // Important: switch off the SuperMode!
   if (context.getSuperMode())
      context.setSuperMode(false);
}
```

***

### sendFileAdHoc()

> **sendFileAdHoc**(`receivers`, `sendMode`, `task`, `backWhenFinished`): `boolean`

**Send the DocFile directly.**

#### Parameters

##### receivers

`any`[]

Array with the names of the users or groups to which to send the DocFile. You need to specify at least one recipient.

##### sendMode

`string`

String containing the send type. The following values are available: 
 
+ `sequential` - one after the other 
+ `parallel_info` - concurrently for information

##### task

`string`

String specifying the task for the recipients of the DocFile

##### backWhenFinished

`boolean`

boolean indicating whether the DocFile should be returned to the own user account after the cycle.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0

#### Example

```ts
var docFile = context.createFile("Filetype1");
var success = docFile.sendFileAdHoc(["user2", "user3"], "parallel_info", "test task", true);
if (!success)
  util.out(docFile.getLastError());
```

***

### sendMail()

> **sendMail**(`from`, `templateName`, `to`, `cc?`, `addDocs?`, `bcc?`): `boolean`

**Send the file as email to somebody.**  

You must define an email template in the Windows Portal Client at the filetype of your DocFile object. 
This template may contain autotexts that can be parsed and replaced with their appropriate field values.  
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files   
**Since:** DOCUMENTS 4.0d new parameter bcc

#### Parameters

##### from

`string`

String value containing the sender's email address

##### templateName

`string`

String value containing the technical name of the email template. This must be defined on the email templates tab of the filetype.

##### to

`string`

String value containing the email address of the recipient

##### cc?

`string`

Optional String value for an additional recipient ("cc" means "carbon copy")

##### addDocs?

`boolean`

**Default:** `false`.  
optional boolean value whether to include the documents of the file

##### bcc?

`string`

Optional String value for the email addresses of blind carbon-copy recipients (remaining invisible to other recipients).

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50b / otrisPORTAL 5.0b

#### Example

```ts
var docFile = context.file;
docFile.sendMail("schreiber@toastup.de", "MyMailTemplate",
   "oppen@toastup.de", "", true
);
```

***

### setAttribute()

> **setAttribute**(`attribute`, `value`): `boolean`

**Set the String value of an attribute of the file to the desired value.**  
 
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

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

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
var myFile = context.file;
myFile.setAttribute("hasInvoicePlugin", "true");
```

***

### setFieldAttribute()

> **setFieldAttribute**(`fieldName`, `attrName`, `value`): `boolean`

**Set the value of an attribute of the desired file field.**  
 
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Parameters

##### fieldName

`string`

String containing the technical name of the desired field

##### attrName

`string`

String containing the name of the desired attribute

##### value

`string`

String value containing the desired field attribute value

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
var myFile = context.file;
myFile.setFieldAttribute("Samplefield", "Value", "1");
```

***

### setFieldValue()

> **setFieldValue**(`fieldName`, `value`): `boolean`

**Set the value of the desired file field.**  
 
**Since:** DOCUMENTS 4.0c HF2 available for multi-instance fields of an EE.i/EE.x archive file   
**Since:** DOCUMENTS 5.0c HF2 String array as value for a double select list field

#### Parameters

##### fieldName

`string`

String containing the technical field name can be followed by the desired instance number 
in form techFieldName[i] for multi-instance fields of an EE.i/EE.x archive file.   

**Note:** The index `i` is zero-based. The specification of field instance is only available for an EE.i/EE.x archive file, 
it will be ignored for other files. If the parameter contains no instance information, the first field instance is used. 
The field instance order is determined by the field order in the file.

##### value

`any`

The desired field value of the proper type according to the field type, e.g. a Date object as value of 
a field of type 'Timestamp'. In case of the value being `null` the field will be emptied. 

**Note:** The keys of the enumeration values for a double select list field may be passed either as an Array of strings 
or as an ordinary string with one key per line of text (see [Field Access Methods](../fieldmethods.html)).

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 4.0c

#### See

 - [DocFile.getFieldValue](#getfieldvalue)
 - [Field Access Methods](../fieldmethods.html)

#### Example

```ts
var myFile = context.file;
myFile.setFieldValue("NumericField", 3.14);
myFile.setFieldValue("TimestampField", new Date());
myFile.setFieldValue("BoolField", true);
myFile.setFieldValue("StringField", "Hello");
myFile.setFieldValue("DoubleListField1", "key1\nkey2";
myFile.setFieldValue("DoubleListField2", ["key1", "key2"]; // Since DOCUMENTS 5.0e HF2
myFile.sync();
// Since DOCUMENTS 4.0c HF2
var key = "Unit=Default/Instance=Default/Pool=FeldZ/Document=Feldzahlen.86C94C30438011E2B925080027B22D11@eex1";
var eexFile = context.getArchiveFile(key);
eexFile.startEdit();
eexFile.setFieldValue("multiInstanceField[2]", "Hello");
eexFile.commit();
```

***

### setFileOwner()

> **setFileOwner**(`owner`): `boolean`

**Set the file owner of the file to the desired user.**

#### Parameters

##### owner

[`SystemUser`](SystemUser.md)

SystemUser object representing the desired new file owner

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.51d / otrisPORTAL 5.1d

#### Example

```ts
var docFile = context.file;
var su = context.getSystemUser();
docFile.setFileOwner(su);
```

***

### setFollowUpDate()

> **setFollowUpDate**(`pUser`, `followUpDate`, `comment?`): `boolean`

**Set a followup date for a desired user.**

#### Parameters

##### pUser

[`SystemUser`](SystemUser.md)

SystemUser object of the desired user

##### followUpDate

`Date`

Date object representing the desired followup date

##### comment?

`string`

optional String value containing a comment that is displayed as a task as soon as the followup is triggered

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.51b / otrisPORTAL 5.1b

#### See

[DocFile.clearFollowUpDate](#clearfollowupdate)

#### Example

```ts
var docFile = context.file;
var su = context.getSystemUser();
var followup = util.convertStringToDate("31.12.2008", "dd.mm.yyyy");
docFile.setFollowUpDate(su, followup, "Silvester");
```

***

### setOrAddCustomProperty()

> **setOrAddCustomProperty**(`name`, `type`, `value`): [`CustomProperty`](CustomProperty.md)

**Creates a new [CustomProperty](CustomProperty.md) or modifies a [CustomProperty](CustomProperty.md) according the name and type for an acitve file.**  

This method creates or modifies a unique CustomProperty for the file. The combination of the name and the type make the CustomProperty unique for the file.

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

DOCUMENTS 6.1.0

#### See

[DocFile.getCustomProperties](#getcustomproperties)  
[DocFile.addCustomProperty](#addcustomproperty)

#### Example

```ts
var docFile = context.file;
var custProp = docFile.setOrAddCustomProperty("favorites", "string", "peachit");
if (!custProp)
  util.out(docFile.getLastError());
```

***

### setReferenceFile()

> **setReferenceFile**(`fieldName`, `referenceFile`): `boolean`

**set the referred file of the desired reference field in the current file.**  
 
  
**Since:** DOCUMENTS 5.0f (Option referenceFile = `null` for deselecting the referred file)

#### Parameters

##### fieldName

`string`

String value containing the technical name of the reference field

##### referenceFile

`DocFile`

DocFile object representing the referred file or `null` to indicate deselecting the referred file. 
If the property 'ReferenceFileClearDefaultValuesOnDeselect' is set to 1, the default values (of the other fields) 
from the referred file are deleted by deselecting the referred file.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
var docFile = context.file;
var refFile = context.createFile("refFileType");
if (!docFile.setReferenceFile("crmCompany", refFile))
  util.out(docFile.getLastError());
// Deselect the referred file
if (!docFile.setReferenceFile("crmCompany", null))
  util.out(docFile.getLastError());
```

***

### setUserRead()

> **setUserRead**(`login`, `fileRead`): `boolean`

**Mark the file as read or unread for the desired user.**  

**Note:** This function requires a full workflow engine license, it does not work with pure distribution lists.

#### Parameters

##### login

`string`

String containing the login name of the desired user

##### fileRead

`boolean`

boolean whether the file should be markes as read (`true`) or unread (`false`)

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50b / otrisPORTAL 5.0b

#### Example

```ts
var docFile = context.file;
docFile.setUserRead("schreiber", true);
```

***

### setUserStatus()

> **setUserStatus**(`login`, `status`): `boolean`

**Set the status of the file for a desired user to a desired value.**  

The file icon in the list view and file view depends on this status.  
  
**Since:** DOCUMENTS 4.0c (status values extended)

#### Parameters

##### login

`string`

String containing the login name of the desired user

##### status

`string`

String value containing the desired status  
Allowed values: 
 
+ `standard`
+ `new`
+ `fromFollowup`
+ `toForward`
+ `forInfo`
+ `task`
+ `workflowCanceled`
+ `backFromDistribution`
+ `consultation`

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50b / otrisPORTAL 5.0b

#### See

[DocFile.getUserStatus](#getuserstatus)

#### Example

```ts
var docFile = context.file;
docFile.setUserStatus("schreiber", "new");
```

***

### startEdit()

> **startEdit**(): `boolean`

**Switch a DocFile to edit mode.**  

Switching a file to edit mode with this function has the same effect as the "Edit" button in the web surface of DOCUMENTS. 
This means, a scratch copy of the file is created, and any changes you apply to the file are temporarily stored 
in the scratch copy - until you `commit()` your changes back to the original file. There are a few scripting event hooks 
which disallow the use of this function at all costs: 
 
+ `onEdit` hook - the system has already created the scratch copy. 
+ `onCreate` hook - a newly created file is always automatically in edit mode.
 
You should avoid using this function in scripts that are executed inside a workflow (signal exits, decisions etc.).

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### See

[DocFile.abort](#abort)

#### Example

```ts
var myFile = context.file;
if (!myFile) {
  throw new Error('This file doesn´t exist');
}
if (!myFile.startEdit()) {
  throw new Error(myFile.getLastError());
}
myFile.Field = "value";
if (!myFile.commit()) {
   errorMsg = myFile.getLastError();
   if (!myFile.abort()) { 
      errorMsg += '\n' + myFile.getLastError(); 
   }
   throw new Error(errorMsg); 
}
```

***

### startWorkflow()

> **startWorkflow**(`workflowName`): `boolean`

**Start a workflow for the DocFile object.**

#### Parameters

##### workflowName

`string`

String containing the technical name and optional the version number of the workflow. 
The format of the workflowName is `technicalName`[-version]. If you don't specify the version of the workflow, 
the workflow with the highest workflow version number will be used. If you want to start a specific version 
you have to use technicalName-version e.g. (Invoice-2) as workflowName.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
var myFile = context.file;
myFile.startWorkflow("Invoice");  // starts the latest version of the workflow "Invoice"
myFile.startWorkflow("Invoice-2"); // starts the version 2 of the workflow "Invoice"
```

***

### sync()

> **sync**(`checkHistoryFields?`, `notifyHitlistChange?`, `updateRefFields?`, `updateModifiedDate?`, `fieldPermissionCheckFlags?`, `checkLifeCyleScript?`): `boolean`

**Synchronize any changes to the DocFile object back to the real file.**  

If you want to apply changes to file fields through a script that is executed as a signal exit inside a workflow, 
you should rather prefer sync() than the `startEdit() / commit()` instruction pair.  

**Note:** If there's a scratch copy of the file in the system (e.g. by some user through the web surface), 
committing the changes in the scratch copy results in the effect that your synced changes are lost. 
So be careful with the usage of this operation.  

**Note:** In case of an error, the function stops immediately, regardless of how many values were already written 
to the database. So if sync() finishes due to an error, the file will probably contain some but not all new values. 
f you change field values using setFieldValue(), you can get the errors before you call sync().  
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i (checkHistoryFields parameter since)  
**Since:** DOCUMENTS 5.0a (new parameter updateRefFields)   
**Since:** DOCUMENTS 5.0a HF2 (new parameter updateModifiedDate)   
**Since:** DOCUMENTS 5.0h HF2 (new parameter fieldPermissionCheckFlags)   
**Since:** DOCUMENTS 5.0i (new parameter checkLifeCyleScript)

#### Parameters

##### checkHistoryFields?

`boolean`

optional boolean parameter has to be set to true, if the file contains history fields, that are modified  
**Default:** `false`

##### notifyHitlistChange?

`boolean`

optional boolean parameter indicates the web client to refresh the current hitlist  
**Default:** `true`

##### updateRefFields?

`boolean`

optional boolean parameter indicates to update reference fields if using the property AutoUpdateByRefFields  
**Default:** `false`

##### updateModifiedDate?

`boolean`

optional boolean parameter indicates to update the modification date of the file  
**Default:** `false`

##### fieldPermissionCheckFlags?

`number`

optional int parameter to specify which field rights should be checked (bit-mask of the following values) 

+ `0x001` : rights from filetype 
+ `0x002` : rights from workflow 
+ `0x004` : check mandatory field
+ the default value is `0x007`

**Default:** `7`

##### checkLifeCyleScript?

`boolean`

optional boolean parameter that triggers a possible global otrLifeCycle_OnMasterExit-Script
**Default:** `false`

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### See

[DocFile.startEdit](#startedit)  
[DocFile.commit](#commit)  
[DocFile.setFieldValue](#setfieldvalue)

#### Example

```ts
var myFile = context.file;
myFile.Field = "value";
if(!myFile.sync()){
 throw myFile.getLastError();
}
```

***

### undeleteFile()

> **undeleteFile**(): `boolean`

**Relive a deleted file.**  

Sets the status active to a file and redraws it from the trash folder. Deleted files are not searchable by a `FileResultSet`. 
You can only retrieve deleted files by iterating throw the trash-folder of the users

#### Returns

`boolean`

`true` if successful, `false` if not

#### Since

ELC 3.60e / otrisPORTAL 6.0e

#### Example

```ts
...
var trashFolder = user.getPrivateFolder("trash");
if (trashFolder)
{
   var it = trashFolder.getFiles();
   for (var file = it.first(); file; file = it.next())
   {
if (file.isDeletedFile())
      {
    file.undeleteFile();
         // now e.g. search a private folder and add the file...
      }
   }
}
```

***

### writeEASLifeCycle()

> **writeEASLifeCycle**(`jsonString`): `boolean`

**Write the life cycle timestamp and action of an EAS-archived DocFile.**

#### Parameters

##### jsonString

`string`

String in JSON-Format with an object, that contains the elements 'timestamp' and 'action'.

#### Returns

`boolean`

`true` if successful or in case of an error an exception will be thrown

#### Since

DOCUMENTS 5.0h

#### See

[readEASLifeCycle](#readeaslifecycle)

#### Example

```ts
// Somehow gain access to a EAS DocFile docFile
try {
   var lifeCycle = new Object();
   lifeCycle.timestamp = new Date(31,11, 2030);
   lifeCycle.action = "delete";
   docFile.writeEASLifeCycle(JSON.stringify(lifeCycle));
} catch (err) {
   util.out("Error: ") + err;
}
```

***

### writeEASRecordAnnotations()

> **writeEASRecordAnnotations**(`annoJSON`, `annoType`, `mergeForeignTypes`): `any`

**Write record-annotations of an EAS-archived DocFile.**  

Write (and replace) annotation data of an EAS record. If the actual DocFile is not a representation of an EAS record, 
the function throws an exception. It usually also throws one, if the archive server is inaccessible 
(technically or by rights management), or due to a JSON syntax error.  

**Note:** The basic structure of the annoJSON data is an array of objects with "type" and "value" string-properties. 
In case of an inconsistency between an object's type and the annoType parameter the function may react differently for each product version. 
The archive may silently ignore one of the conflicting values, or it may report an error. Depending on the parameters, 
the function can operate in different modes. 

+ For calls with an individual annoType the archive will replace the entire set of annotations of the given type with the new content. 
  Existing annotations of other types remain unaffected. 
+ If annoType is empty or "*" and mergeForeignTypes is `false`, annoJSON must define the record's entire new annotation content. 
  The archive will drop all old annotations.
+ If annoType is empty or "*" and mergeForeignTypes is `true`, the function will read the existing annotations at first. 
  Each old annotation of a type, which does not occur in the annoJSON data, will be copied into the new content buffer. 
  Finally the merge of copied and passed annotations will be written.
 
In the merge mode the function may take twice the time it takes in other modes. As a special case the merge mode accepts also objects without 
a value property within annoJSON. This capability allows (for instance) deleting the annotations of two types without side-effects to other types.   
 
This operation only accesses annotations at the DocFile level ("record" in EAS terminology). It cannot access annotations at the Document ("attachment") level.   
Unlike fields, annotations in the archive are not sealed for auditing purposes. Modifications occur without versioning. Multiple annotations of the same type are allowed.

#### Parameters

##### annoJSON

`string`

A JSON string with the annotation data to be written. The underlying structure is the same as in return values of readEASRecordAnnotations().

##### annoType

`string`

A string, which names an annotation-type, if the operation is intended to modify only annotations of one type. 
The parameter can be either an empty string or "*" in order to write/replace all types of annotations at once.

##### mergeForeignTypes

`boolean`

This boolean parameter enables a client-side merge of foreign existing annotations with the data passed in annoJSON. 
For calls with a given annoType this parameter is meaningless and optional. Otherwise it is mandatory.

#### Returns

`any`

No return value.

#### Since

DOCUMENTS 5.0h

#### See

[readEASRecordAnnotations](#readeasrecordannotations)

#### Example

```ts
// Somehow gain access to a DocFile, which is
// a DOCUMENTS image of an EAS archive record
// (This example uses a search request.)
const searchsource="Typentest@EDA2"; // Resource pattern: "file_type@archive_server"
const keyfield = "F1_String";
const keyvalue = "RecordAnno1 Scripting";
var filter = keyfield + "|~" + util.getQuoted(keyvalue);
var hrs = new HitResultset(searchsource, filter, "");
if(hrs.getLastErrorCode() != 0 || hrs.size() <= 0)
    throw new Error("Test record not found.");
var df = hrs.first().getArchiveFile();
hrs.dispose(); // hrs is no longer needed.
if(df === null)
    throw new Error("Failed to create DOCUMENTS image of the test record.");
// As next define a few demo annotations.
var testAnnotations = [
    { type : "testExample", value : "first demo annotation" },
    { type : "testExample", value : "second demo annotation" },
    { type : "test2Example", value : "another type of demo annotation" },
];
// Write these annotations into the archive record.
// We use the merge mode to protect foreign annotations
// (for instance the standard "3X" annotations) from being deleted.
// Old annotations of the types used above will disappear,
// because they have not been read and copied.
df.writeEASRecordAnnotations(JSON.stringify(testAnnotations), "", false);
```
