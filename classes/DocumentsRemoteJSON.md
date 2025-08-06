[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / DocumentsRemoteJSON

# Class: DocumentsRemoteJSON

This class allows the server as a gRPC client to access other (or its own) Documents Server via [gRPC API](../../../manuals/books/grpc/index.html).

## Properties

### locale

> **locale**: `string`

**locale of the gRPC client.**

#### Since

DOCUMENTS 5.0i

## Methods

### ArchiveFiles()

> **ArchiveFiles**(`json`): `string`

**Archive files.**  

**Note:** Invoked gRPC operation: DocFile.ArchiveFiles, see doc_file.proto for more information.

#### Parameters

##### json

`string`

JSON string containing the request of the corresponding gRPC call.

#### Returns

`string`

JSON string containing the response of the corresponding gRPC call.

#### Since

DOCUMENTS 6.0.1

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var reqJson = {};
  reqJson.file_ids = ["peachitreg_fi20230000000036", "peachitreg_fi20230000000037"];
  reqJson.delete_files = true;
  var res = dr.ArchiveFiles(JSON.stringify(reqJson));
  util.out("Response: " + res);
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### CancelWorkflow()

> **CancelWorkflow**(`json`): `boolean`

**Cancel the workflow of a file.**  

**Note:** Invoked gRPC operation: Workflow.CancelWorkflow, see workflow.proto for more information.

#### Parameters

##### json

`string`

JSON string containing the request of the corresponding gRPC call.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var reqJson = {};
  reqJson.file_id = "relations_fi20200000001335";
  dr.CancelWorkflow(JSON.stringify(reqJson));
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### CloseSession()

> **CloseSession**(): `boolean`

**Close the session.**  

**Note:** Invoked gRPC operation: Session.CloseSession, see sessions.proto for more information.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0i

***

### CreateFile()

> **CreateFile**(`json`): `string`

**Create a file.**  

**Note:** Invoked gRPC operation: DocFile.CreateFile, see doc_file.proto for more information.

#### Parameters

##### json

`string`

JSON string containing the request of the corresponding gRPC call.

#### Returns

`string`

JSON string containing the response of the corresponding gRPC call.

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var inJson = {};
  inJson.file_path = "c:\\tmp\\easy.pdf";
  inJson.file_ext = "pdf";
  var res = dr.SpoolDocument(JSON.stringify(inJson));
  var spoolId = JSON.parse(res).spool_id;
  var reqJson = {};
  reqJson.file = {};
  reqJson.file.type = "crmNote";
  reqJson.file.field_updates = [];
  reqJson.file.document_updates = [];
  var field1 = {};
  field1.name = "crmSubject";
  field1.str = "Test CreateFile";
  reqJson.file.field_updates.push(field1);
  var doc1 = {};
  doc1.spool_id = spoolId;
  doc1.name = "easy.pdf";
  doc1.register_name = "crmAttachments";
  reqJson.file.document_updates.push(doc1);
  res = dr.CreateFile(JSON.stringify(reqJson));
  util.out("Response: " + res);
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### DeleteFiles()

> **DeleteFiles**(`json`): `string`

**Delete files.**  

**Note:** Invoked gRPC operation: DocFile.DeleteFiles, see doc_file.proto for more information.

#### Parameters

##### json

`string`

JSON string containing the request of the corresponding gRPC call.

#### Returns

`string`

JSON string containing the response of the corresponding gRPC call.

#### Since

DOCUMENTS 5.0i HF3

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var reqJson = {};
  reqJson.file_ids = ["peachitreg_fi20230000000036", "peachitreg_fi20230000000037", "d9c5275d-4a4f-4940-bef0-2d4e4c50cae8|Filetype1@eas1"];
  reqJson.all_versions = true;
  var res = dr.DeleteFiles(JSON.stringify(reqJson));
  util.out("Response: " + res);
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### DownloadDocument()

> **DownloadDocument**(`json`): `string`

**Download a document from a file.**  

**Note:** Invoked gRPC operation: DocFile.DownloadDocument, see doc_file.proto for more information.

#### Parameters

##### json

`string`

JSON string containing the request of the corresponding gRPC call.

#### Returns

`string`

JSON string containing the file path and file name of the downloaded document.

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var reqJson = {};
  reqJson.file_id = "relations_fi20200000001335";
  reqJson.doc_id = "relationsdc0000000000000490";
  var res = dr.DownloadDocument(JSON.stringify(reqJson));
  util.out("Response: " + res);
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### FollowUp()

> **FollowUp**(`json`): `boolean`

**Move a file from the user's inbox to the resubmission folder.**  

**Note:** Invoked gRPC operation: DocFile.FollowUp, see doc_file.proto for more information.

#### Parameters

##### json

`string`

JSON string containing the request of the corresponding gRPC call.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 6.0.1

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var reqJson = {};
  reqJson.file_id = "relations_fi20200000001335";
  reqJson.comment = "Test for FollowUp";
  reqJson.absolute_time = context.addTimeInterval(new Date(), 2, "days", false);
  dr.FollowUp(JSON.stringify(reqJson));
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### ForwardFile()

> **ForwardFile**(`json`): `boolean`

**Forward the file to its next workflow step.**  

**Note:** Invoked gRPC operation: Workflow.ForwardFile, see workflow.proto for more information.

#### Parameters

##### json

`string`

JSON string containing the request of the corresponding gRPC call.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var reqJson = {};
  reqJson.file_id = "relations_fi20200000001335";
  reqJson.action_id = "{684E5F7B-D2E6-4307-8911-FC7260EF02BE}";
  dr.ForwardFile(JSON.stringify(reqJson));
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### GetAutoText()

> **GetAutoText**(`json`): `string`

**Determine auto-texts.**  

**Note:** Invoked gRPC operation: DocFile.GetAutoText, see doc_file.proto for more information.

#### Parameters

##### json

`string`

JSON string containing the request of the corresponding gRPC call.

#### Returns

`string`

JSON string containing the response of the corresponding gRPC call.

#### Since

DOCUMENTS 6.0.1

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var reqJson = {};
  reqJson.file_id = "peachitreg_fi20230000000036";
  reqJson.auto_text_names = ["fileOwner", "createdAt"];
  var res = dr.GetAutoText(JSON.stringify(reqJson));
  util.out("Response: " + res);
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### GetFileInfo()

> **GetFileInfo**(`json`): `string`

**Get the information of a file.**  

**Note:** Invoked gRPC operation: DocFile.GetFileInfo, see doc_file.proto for more information.

#### Parameters

##### json

`string`

JSON string containing the request of the corresponding gRPC call.

#### Returns

`string`

JSON string containing the response of the corresponding gRPC call.

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var reqJson = {};
  reqJson.file_id = "relations_fi20200000001335";
  reqJson.options = {};
  reqJson.options.add_fields = true;
  reqJson.options.add_documents = true;
  reqJson.options.add_field_display_value = true;
  reqJson.options.add_field_label = true;
  reqJson.options.add_field_reference_file_id = true;
  reqJson.options.add_registers = true;
  var res = dr.GetFileInfo(JSON.stringify(reqJson));
  util.out("Response: " + res);
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### GetFiles()

> **GetFiles**(`json`): `string`

**Get the information of files in a folder.**  

**Note:** Invoked gRPC operation: Folder.GetFiles, see folder.proto for more information.

#### Parameters

##### json

`string`

JSON string containing the request of the corresponding gRPC call.

#### Returns

`string`

JSON string containing the response of the corresponding gRPC call.

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var reqJson = {};
  reqJson.name = "testFolder"
  reqJson.start_index = 0;
  reqJson.count = -2;
  reqJson.preview = true;
  var res = dr.GetFiles(JSON.stringify(reqJson));
  util.out("Response: " + res);
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### GetFileTypes()

> **GetFileTypes**(`json?`): `string`

**Get the information of desired file types.**  

**Note:** Invoked gRPC operation: DocFile.GetFileTypes, see doc_file.proto for more information.

#### Parameters

##### json?

`string`

JSON string containing the request of the corresponding gRPC call.  
**Default:** "{}"

#### Returns

`string`

JSON string containing the response of the corresponding gRPC call.

#### Since

DOCUMENTS 6.0.2

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var reqJson = {};
  reqJson.name_pattern = "TestFileType*";
  reqJson.options = {};
  reqJson.options.add_fields = true;
  reqJson.options.add_registers = true;
  var res = dr.GetFileTypes(JSON.stringify(reqJson));
  util.out("Response: " + res);
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### getLastError()

> **getLastError**(): `string`

**Returns only the status message for the last error.**  

**Note:** You can use this after catching an error to get only the message string for this error

#### Returns

`string`

Status message

#### Since

DOCUMENTS 6.0

***

### getLastErrorCode()

> **getLastErrorCode**(): `number`

**Returns only the status code for the last error.**  

**Note:** You can use this after catching an error to get only the code number for this error

#### Returns

`number`

Status code

#### Since

DOCUMENTS 6.0

***

### GetPossibleActions()

> **GetPossibleActions**(`json`): `string`

**Determine the currently possible workflow steps of a file.**  

**Note:** Invoked gRPC operation: Workflow.GetPossibleActions, see workflow.proto for more information.

#### Parameters

##### json

`string`

JSON string containing the request of the corresponding gRPC call.

#### Returns

`string`

JSON string containing the response of the corresponding gRPC call.

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var reqJson = {};
  reqJson.file_id = "relations_fi20200000001335";
  var res = dr.GetPossibleActions(JSON.stringify(reqJson));
  util.out("Response: " + res);
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### GetPrivateFolder()

> **GetPrivateFolder**(`json`): `string`

**List the information of the files in a private folder.**  

**Note:** Invoked gRPC operation: Folder.GetPrivateFolder, see folder.proto for more information. 
This function is only available for the following folder types: Inbox and Sent.

#### Parameters

##### json

`string`

JSON string containing the request of the corresponding gRPC call.

#### Returns

`string`

JSON string containing the response of the corresponding gRPC call.

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var reqJson = {};
  reqJson.type_str = "Inbox"; // or reqJson.type = 1
  var res = dr.GetPrivateFolder(JSON.stringify(reqJson));
  util.out("Response: " + res);
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### GetPublicFolders()

> **GetPublicFolders**(): `string`

**Get the public folders.**  

**Note:** Invoked gRPC operation: Folder.GetPublicFolders, see folder.proto for more information.

#### Returns

`string`

JSON string containing the response of the corresponding gRPC call.

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var res = dr.GetPublicFolders();
  util.out("Response: " + res);
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### GetUserInfo()

> **GetUserInfo**(`json?`): `string`

**Get the information of the user.**  

**Note:** Invoked gRPC operation: User.GetUserInfo, see users.proto for more information.

#### Parameters

##### json?

`string`

JSON string containing the request of the corresponding gRPC call.  
**Default:** "{}"

#### Returns

`string`

JSON string containing the response of the corresponding gRPC call.

#### Since

DOCUMENTS 6.0.2

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var reqJson = {};
  reqJson.options = {};
  reqJson.options.add_particulars = true;
  var res = dr.GetUserInfo(JSON.stringify(reqJson));
  util.out("Response: " + res);
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### GetWorkflowPattern()

> **GetWorkflowPattern**(): `string`

**Get the workflows im Documents.**  

**Note:** Invoked gRPC operation: Workflow.GetWorkflowPattern, see workflow.proto for more information.

#### Returns

`string`

JSON string containing the response of the corresponding gRPC call.

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var res = dr.GetWorkflowPattern();
  util.out("Response: " + res);
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### Query()

> **Query**(`json`): `string`

**Search for files of one or more file types in one or more archives.**  

**Note:** Invoked gRPC operation: Search.Query, see search.proto for more information.

#### Parameters

##### json

`string`

JSON string containing the request of the corresponding gRPC call.

#### Returns

`string`

JSON string containing the response of the corresponding gRPC call.

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var reqJson = {};
  reqJson.filetypes = ["crmNote", "crmProduct"];
  reqJson.filter = "SETMETHOD(2)crmSubject ~ Test*";
  reqJson.sort = "crmDescription-";
  reqJson.field_names = ["crmDescription", "crmId", "crmSubject"];
  var res = dr.Query(JSON.stringify(reqJson));
  util.out("Response: " + res);
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### RunScript()

> **RunScript**(`json`): `string`

**Run a script.**  

**Note:** Invoked gRPC operation: Scripting.RunScript, see scripting.proto for more information.

#### Parameters

##### json

`string`

JSON string containing the request of the corresponding gRPC call.

#### Returns

`string`

JSON string containing the response of the corresponding gRPC call.

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var reqJson = {};
  reqJson.file_id = "relations_fi20200000001335";
  reqJson.script_name = "remoteScriptCall";
  reqJson.parameters = {};
  reqJson.parameters["param1"] = "value1";
  reqJson.parameters["param2"] = "value2";
  var res = dr.RunScript(JSON.stringify(reqJson));
  util.out("Response: " + res);
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### SpoolDocument()

> **SpoolDocument**(`json`): `string`

**Spool a document.**  

**Note:** Invoked gRPC operation: DocumentSpooler.Spool, see spooler.proto for more information.

#### Parameters

##### json

`string`

JSON string containing the request of the corresponding gRPC call.

#### Returns

`string`

JSON string containing the response of the corresponding gRPC call.

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var reqJson = {};
  reqJson.file_path = "c:\\tmp\\easy.pdf";
  reqJson.file_ext = "pdf";
  var res = dr.SpoolDocument(JSON.stringify(reqJson));
  util.out("Response: " + res);
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### StartWorkflow()

> **StartWorkflow**(`json`): `boolean`

**Start a workflow for a file.**  

**Note:** Invoked gRPC operation: Workflow.StartWorkflow, see workflow.proto for more information.

#### Parameters

##### json

`string`

JSON string containing the request of the corresponding gRPC call.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var reqJson = {};
  reqJson.file_id = "relations_fi20200000001335";
  reqJson.workflow_pattern_id = "352:8172";
  dr.StartWorkflow(JSON.stringify(reqJson));
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

***

### TestSession()

> **TestSession**(): `boolean`

**Check whether a valid session exists for the client.**  

**Note:** Invoked gRPC operation: Session.TestSession, see sessions.proto for more information.

#### Returns

`boolean`

`true` if successful, `false` in case of any error.

#### Since

DOCUMENTS 6.0.1

***

### UpdateFile()

> **UpdateFile**(`json`): `string`

**Update a file.**  

**Note:** Invoked gRPC operation: DocFile.UpdateFile, see doc_file.proto for more information.

#### Parameters

##### json

`string`

JSON string containing the request of the corresponding gRPC call.

#### Returns

`string`

JSON string containing the response of the corresponding gRPC call.

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
  var reqJson = {};
  reqJson..file_id = "relations_fi20200000001335";
  reqJson.file = {};
  reqJson.file.type = "crmNote";
  reqJson.file.field_updates = [];
  reqJson.file.document_updates = [];
  var field1 = {};
  field1.name = "crmSubject";
  field1.str = "Test UpdateFile";
  reqJson.file.field_updates.push(field1);
  var doc1 = {};
  doc1.name = "easy_renamed.pdf";
  doc1.document_id = "relationsdc0000000000000490";
  doc1.action = "UPDATE_DOCUMENT";
  doc1.register_name = "crmAttachments";
  reqJson.file.document_updates.push(doc1);
  var res = dr.UpdateFile(JSON.stringify(reqJson));
  util.out("Response: " + res);
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```

## Constructors

### Constructor

> **new DocumentsRemoteJSON**(`json`): `DocumentsRemoteJSON`

**Create a new DocumentsRemoteJSON object.**  

**Note:** Invoked gRPC operation: Session.CreateSession, see sessions.proto for more information.  
  
**Since:** DOCUMENTS 5.0i

#### Parameters

##### json

`string`

JSON string containing the settings for the options `host, principal, user, locale, tls, caCert, clientCert`, `clientKey` and `timeout` in ms (default 30000).

#### Returns

`DocumentsRemoteJSON`

#### Since

DOCUMENTS 5.0i

#### Example

```ts
const certPath = "c:\\mycerts\\";
var json = {    
              host : "localhost:50050",
              principal : "relations",
              user : "schreiber",
              locale : "de",
              tls : true,
              caCert: certPath + "ca_cert.pem",
              clientCert : certPath + "client_cert.pem",
              clientKey: certPath + "client_key.pem",
              timeout : 30000
            };
var dr = null;
try {
  dr = new DocumentsRemoteJSON(JSON.stringify(json));
   // do something
} catch (err) {
   util.out(err);
} finally {
  if (dr)
    dr.CloseSession();
}
```
