[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / ArchivingDescription

# Class: ArchivingDescription

The ArchivingDescription class has been added to the DOCUMENTS PortalScripting API to improve the archiving process of DOCUMENTS files by scripting means.  

For instance this allows to use different target archives for each file as well as to influence the archiving process by the file's contents itself. 
The ArchivingDescription object can only be used as parameter for the method [DocFile.archive(ArchivingDescription)](../interfaces/DocFile.html#archive.archive-3) 

**Note:** By default, archiving with an ArchivingDescription does not include any attachments. To archive some attachments, the script needs to call 
[\`addRegister()\`](#addregister) on this object.  

**Since:** EE.x: ELC 3.60a / otrisPORTAL 6.0a  
**Since:** EAS: ELC 4.0 / otrisPORTAL 7

## Properties

### archiveMonitor

> **archiveMonitor**: `boolean`

**boolean value whether to archive the monitor of the file.**  

Like on the filetype in the Portal Client you may decide whether you want to archive the monitor of the file along with the file. 
If so, the file's monitor will be transformed to a HTML file named monitor.html, and it will be part of the archived file in the desired target archive.  

**Since:** ELC 3.51c / otrisPORTAL 5.1c EE.i  
**Since:** ELC 3.60a / otrisPORTAL 6.0a EE.x  
**Since:** ELC 4.0 / otrisPORTAL 7.0 EAS

#### Since

ELC 3.51c / otrisPORTAL 5.1c

#### Example

```ts
var ad = new ArchivingDescription();
ad.archiveMonitor = true; // archive monitor of file as HTML page as well
```

***

### archiveServer

> **archiveServer**: `string`

**String containing the name of the archive server in a multi archive server environment.**  

You need to define the archive server if you want to archive in an archive server that is different from the main archives server. 
If you want to archive into the main archive you can leave this value empty.  

**Note:** This value has only to be set if you habe multiple archive servers

#### Since

ELC 4.0 / otrisPORTAL 7.0 (EE.i, EE.x, EAS)

#### Example

```ts
var ad = new ArchivingDescription();
ad.archiveServer = "myeei"";
```

***

### archiveStatus

> **archiveStatus**: `boolean`

**boolean value whether to archive the status of the file.**  

Like on the filetype in the Portal Client you may decide whether you want to archive the status of the file along with the file. 
If so, the file's status will be transformed to a HTML file named status.html, and it will be part of the archived file in the desired target archive.  
  
**Since:** EE.i: ELC 3.51c / otrisPORTAL 5.1c  
**Since:** EE.x: ELC 3.60a / otrisPORTAL 6.0a   
**Since:** EAS: ELC 4.0 / otrisPORTAL 7

#### Since

ELC 3.51c / otrisPORTAL 5.1c

#### Example

```ts
var ad = new ArchivingDescription();
ad.archiveStatus = true; // archive status of file as HTML page as well
```

***

### targetArchive

> **targetArchive**: `string`

**String containing the complete address of the target archive for archiving to EE.i.**  

You need to define the target archive including the "Storageplace".  

**Note:** This value has only to be set if you want to archive to EE.i. If you want to archive to EE.x, you have to set targetView and targetSchema. 
It is important to know that the target archive String must use the socalled XML-Server syntax. It is as well neccessary to use a double backslash (\\) 
if you define your target archive as an PortalScript String value, because a single backslash is a special character.

**Since:** EE.i: ELC 3.51c / otrisPORTAL 5.1c

#### Since

ELC 3.51c / otrisPORTAL 5.1c

#### Example

```ts
var ad = new ArchivingDescription();
ad.targetArchive = "$(#DEMO)\\BELEGE";  // archiving to "DEMO\BELEGE"
```

***

### targetSchema

> **targetSchema**: `string`

**String containing the complete address of the target schema used for archiving to EE.x.**  

You need to define the target schema you want to archive into.  

**Note:** This value has only to be set if you want to archive to EE.x.

#### Since

ELC 3.60a / otrisPORTAL 6.0a

#### Example

```ts
var ad = new ArchivingDescription();
ad.targetView = "Unit=Default/Instance=Default/DocumentSchema=LIEFERSCHEINE";
```

***

### targetView

> **targetView**: `string`

**String containing the complete address of the target view used for archiving to EE.x.**  

You need to define the target view (write pool) you want to archive into.  

**Note:** This value has only to be set if you want to archive to EE.x.

#### Since

ELC 3.60a / otrisPORTAL 6.0a

#### Example

```ts
var ad = new ArchivingDescription();
ad.targetView = "Unit=Default/Instance=Default/View=DeliveryNotes";
```

***

### versioning

> **versioning**: `boolean`

**boolean value whether to use the versioning technique in the archive.**  

If the DocFile has already been archived and if you define this attribute to be true, a new version of the archive file 
will be created otherwise a independent new file in the archive will be created.  

**Since:**  EE.i: ELC 3.51c / otrisPORTAL 5.1c  
**Since:** EE.x: ELC 3.60a / otrisPORTAL 6.0a   
**Since:** EAS: ELC 4.0 / otrisPORTAL 7

#### Since

ELC 3.51c / otrisPORTAL 5.1c

#### Example

```ts
var ad = new ArchivingDescription();
ad.versioning = true; // use versioning for archived file
```

## Methods

### addRegister()

> **addRegister**(`registerName`): `void`

**flag an additional (document) register to be archived with the file.**  

You may add the technical names of different document registers to an internal list of your ArchivingDescription object. 
This allows for example to archive only part of your documents of your DocFile.  
  
**Since:** EE.i: ELC 3.51c / otrisPORTAL 5.1c  
**Since:** EE.x: ELC 3.60a / otrisPORTAL 6.0a   
**Since:** EAS: ELC 4.0 / otrisPORTAL 7

#### Parameters

##### registerName

`string`

String containing the technical name of the register to be archived. Pass "all_docs" to archive all attachments of your DocFile.

#### Returns

`void`

#### Since

ELC 3.51c / otrisPORTAL 5.1c

#### Example

```ts
var docFile = context.file;
var ad = new ArchivingDescription();
ad.targetArchive = "$(#DEMO)\\BELEGE";
ad.addRegister("Documents");
ad.addRegister("InternalDocuments");
docFile.archive(ad);
```

## Constructors

### Constructor

> **new ArchivingDescription**(): `ArchivingDescription`

**Create a new ArchivingDescription object.**  

Like in other programming languages you create a new object with the `new` operator (refer to example below).  
  
**Since:** EE.i: ELC 3.51c / otrisPORTAL 5.1c   
**Since:** EE.x: ELC 3.60a / otrisPORTAL 6.0a   
**Since:** EAS: ELC 4.0 / otrisPORTAL 7

#### Returns

`ArchivingDescription`

#### Since

ELC 3.51c / otrisPORTAL 5.1c

#### See

[DocFile.archive(ArchivingDescription)](../interfaces/DocFile.html#archive.archive-3)

#### Examples

```ts
// Example for EE.i:
var docFile = context.file;
if (!docFile)
{
   // error handling
}
var ad = new ArchivingDescription();
ad.targetArchive = "$(#DEMO)\\BELEGE";
ad.archiveServer = "myeei";  // since Documents 4.0 using multi archive server
// Note: This example does not archive any attachments
var success = docFile.archive(ad);
if (!success)
{
   util.out(docFile.getLastError());
}
```

```ts
// Example for EE.x:
var docFile = context.file;
if (!docFile)
{
   // error handling
}
var ad = new ArchivingDescription();
ad.targetView = "Unit=Default/Instance=Default/View=DeliveryNotes";
ad.targetSchema = "Unit=Default/Instance=Default/DocumentSchema=LIEFERSCHEINE";
ad.archiveServer = "myeex";  // since Documents 4.0 using multi archive server
ad.archiveMonitor = true;
// Note: This example does not archive any attachments
var success = docFile.archive(ad);
if (!success)
{
   util.out(docFile.getLastError());
}
```

```ts
// Example for EAS:
var docFile = context.file;
if (!docFile)
{
   // error handling
}
var ad = new ArchivingDescription();
ad.archiveServer = "myeas";
ad.archiveMonitor = true;
// Note: This example does not archive any attachments
var success = docFile.archive(ad);
if (success)
   util.out(docFile.getArchiveKey());
else
   util.out(docFile.getLastError());
```
