[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / ArchiveConnection

# Interface: ArchiveConnection

**The ArchiveConnection class allows low level access to the EAS Interface, EBIS and the EASY ENTERPRISE XML-Server.**

## Methods

### downloadBlob()

> **downloadBlob**(`fileKey`, `docKey`): [`ArchiveConnectionBlob`](ArchiveConnectionBlob.md)

**Download an attachment from the XML-Server.**  

With this method you can download an attachment from the EASYWARE ENTERPRISE archive using the XML-Server. 
The method returns an object of the class [\`ArchiveConnectionBlob\`](ArchiveConnectionBlob.md). This object allows you to access the attachment. 
If the method fails the return value is `null`. You can retrieve the error message by executing `ArchiveConnection.getLastError()`.

**Note:** Method is only available for EE.x using XML-Server

#### Parameters

##### fileKey

`string`

String containing the key of the file

##### docKey

`string`

String containing the key of the attachment

#### Returns

[`ArchiveConnectionBlob`](ArchiveConnectionBlob.md)

`ArchiveConnectionBlob` or `null`, if failed

#### Since

ELC 3.60h / otrisPORTAL 6.0h

#### Example

```ts
var xmlserver = context.getArchiveConnection();
if (xmlserver)
{
   var fileKey = "Unit=Default/Instance=Default/Pool=DEMO/Pool=RECHNUNGEN/Document=RECHNUNGEN.41D3694E2B1E11DD8A9A000C29FACDC2"
   var docKey = "41D3695F2B1E11DD8A9A000C29FACDC2"
   var res = xmlserver.downloadBlob(fileKey, docKey);
   if (!res)
      util.out(xmlserver.getLastError());
   else
      util.out(res.localPath)
}
```

***

### downloadBlobs()

> **downloadBlobs**(`fileKey`, `docKey`): [`ArchiveConnectionBlobIterator`](ArchiveConnectionBlobIterator.md)

**Download multiple attachments from the XML-Server.**  

This method allows downloading multiple attachments from the EASYWARE ENTERPRISE archive using the XML-Server. 
The method returns an object of the class [\`ArchiveConnectionBlobIterator\`](ArchiveConnectionBlobIterator.md). This object allows you to access the attachments. 
If the method fails the return value is `null`. You can retrieve the error message by executing `ArchiveConnection.getLastError()`.

**Note:** Method is only available for EE.x using XML-Server

#### Parameters

##### fileKey

`string`

String Array containing the keys of the files

##### docKey

`string`

String Array containing the keys of the attachments

#### Returns

[`ArchiveConnectionBlobIterator`](ArchiveConnectionBlobIterator.md)

`ArchiveConnectionBlobIterator` or `null`, if failed

#### Since

ELC 3.60h / otrisPORTAL 6.0h

#### Example

```ts
var fileKeys = new Array();
var docKeys = new Array();
var fileKey1 = "Unit=Default/Instance=Defaul...";
var docKey1 = "41D3695F2B1E11DD8A9A000C29FACDC2";
var fileKey2 = "Unit=Default/Instance=Defaul...";
var docKey2 = "28CDB49ECE1B11DB9FC3000C29FACDC2";
fileKeys[0] = fileKey1;
docKeys[0] = docKey1;
fileKeys[1] = fileKey2;
docKeys[1] = docKey2;
var itArchDoc = xmlserver.downloadBlobs(fileKeys, docKeys);
if (!itArchDoc)
{
   util.out(xmlserver.getLastError())
   return -1;
}
for (var archDoc=itArchDoc.first(); archDoc; archDoc=itArchDoc.next())
{
   util.out(archDoc.name);
   util.out(archDoc.localPath);
}
```

***

### getLastError()

> **getLastError**(): `string`

**Function to get the description of the last error that occurred.**

#### Returns

`string`

Text of the last error as String

#### Since

ELC 3.60h / otrisPORTAL 6.0h

***

### putBlob()

> **putBlob**(`doc`, `blobreference`): `boolean`

**Upload an attachment to the XML-Server.**  

This method performs a "putblob" request to an installed EASY XML-Server.  

**Note:** You may use [util.getUniqueId()](Util.md#getuniqueid) to create a blobreference. However this may be not unique enough, 
if several portal servers are connected to the same XML-server in this way.  

**Note:** Method is only available for EE.x using XML-Server

#### Parameters

##### doc

[`Document`](Document.md)

The Document object, whose binary content is to be uploaded

##### blobreference

`string`

A unique string, which will identify the content in the XML-Server's blobcache.

#### Returns

`boolean`

A boolean value indicates, if the attachment has succeessfully been uploaded.

#### Since

ELC 3.60h / otrisPORTAL 6.0h

#### Example

```ts
var xmlserver = context.getArchiveConnection();
if (!xmlserver)
   throw "Error: no ArchiveConnection"
// Create a unique id as BlobReference for the upload
var blobRef = util.getUniqueId();
// take a Document object and upload it to the ArchiveConnection
if (!xmlserver.putBlob(doc, blobRef))
   throw "Upload failed";
// Now the blobRef can be used e.g. for an IMPORT request
```

***

### queryRawEEx()

> **queryRawEEx**(`eql`, `wantedHits?`, `maxHits?`): `string`

**Sends a query EQL to the EE.x XML-Server and returns the response XML.**  

With this method you can send a query EQL to the XML-Server of EASY ENTERPRISE.x If the method succeed the return value is the response-xml, 
otherwise it returns `null`. If the value is `null` you can retrieve the error message by executing `ArchiveConnection.getLastError()`.

**Note:** Method is only available for EE.x using XML-Server

#### Parameters

##### eql

`string`

String containing the EQL

##### wantedHits?

`number`

Number of currently wanted hits (optional)   
**Default:** `-1`

##### maxHits?

`number`

Max. number of hits, that the ArchiveConnection should respond (optional).  
**Default:** `-1`

#### Returns

`string`

String with the response (xml) or `null` in case of any error

#### Since

ELC 3.60h / otrisPORTAL 6.0h

#### Example

```ts
var xmlserver = context.getArchiveConnection();
if (xmlserver)
{
   var eql = "SELECT @Finance.Type FROM @Finance WHERE isnewestversion(FIBU) ORDER BY FIBU.BUCHUNGSTYP ASC";
   var res = xmlserver.queryRawEEx(eql);
   if (!res)
      util.out(xmlserver.getLastError());
   else
      util.out(res);
 }
```

***

### sendDARequest()

> **sendDARequest**(`resourceIdentifier`, `postData?`, `extraHeaders?`): `string`

**`Internal`**

**Sends a request to a DOUCMENTS archive server (EAS/EDA) and returns the response.**  

Internal: With this method you can send a GET or a POST request to an EDA store. If the request succeeds, 
the return value is the HTTP-content of the response. Otherwise the function returns an empty String. 
Call  subsequently to test for eventual errors. If the archive reports an error, it will be prefixed with "[EAS] ".

#### Parameters

##### resourceIdentifier

`string`

String containing the REST resource identifier (in other words: the back part of the URL).

##### postData?

`string`

A optional String with content data of a HTTP-POST request. If the parameter is missing or empty, the function generates a GET request.

##### extraHeaders?

`string`[]

A optional Array of Strings with an even number of elements. The first element of each pair must contain the name, 
the second one the value of an additional HTTP header element.  
**Default:** `[]`

#### Returns

`string`

#### Since

DOCUMENTS 4.0b

#### Example

```ts
var easInterface = context.getArchiveConnection("peachitStore1");
if (easInterface)
{
  var versionInfo = easInterface.sendDARequest("version");
  var eText = easInterface.getLastError();
  if(eText == "")
    util.out(versionInfo);
  else
    util.out(eText);
}
```

***

### sendEbisRequest()

> **sendEbisRequest**(`resourceIdentifier`, `postData?`, `extraHeaders?`): `string`

**Sends a request to the EBIS interface and returns the response.**  

With this method you can send a GET or a POST request to an EBIS interface. If the request succeeds, 
the return value is the HTTP-content of the response. Otherwise the function returns an empty String. 
Call `ArchiveConnection.getLastError()` subsequently to test for eventual errors. 
If the interface reports an error, it will be prefixed with "[EBIS] ".

**Note:** The function is unable to handle a response with binary data. The function does not check the parameters for 
illegal characters, such as linefeeds in the extraHeaders, for example.  

**Note:** Method is only available for EBIS

#### Parameters

##### resourceIdentifier

`string`

String containing the REST resource identifier (in other words: the back part of the URL).

##### postData?

`string`

A optional String with content data of a HTTP-POST request. If the parameter is missing or empty, the function generates a GET request.

##### extraHeaders?

`string`[]

A optional Array of Strings with an even number of elements. The first element of each pair must contain the name, 
the second one the value of an additional HTTP header element.  
**Default:** `[]`

#### Returns

`string`

A String with the response. This may be an XML or plain text. It depends on the request.

#### Since

DOCUMENTS 5.0a

#### Example

```ts
//
// Example for GET
//
var ebisConn = context.getArchiveConnection("ebisStore1");
if (ebisConn)
{
  var factoryInfo = ebisConn.sendEbisRequest("/factory");
  var eText = ebisConn.getLastError();
  if(eText == "")
    util.out(factoryInfo);
  else
    util.out(eText);
}
//
// Example for POST (do a query on EBIS with JSON)
//
var req = {};
req.maxHits = 250;
req.pageSize = 20;
req.unformattedResult = true;
req.includeTextmarkers = true;
// search sources
req.sources = ["Unit=Default/Instance=Default/View=Store01"];
// hitlist fields
req.fields = [];
req.fields.push({field: "TITLE", sort: "NONE"})
req.fields.push({field: "MODIFIED_DATE", sort: "NONE"})
req.fields.push({field: "_type", sort: "NONE"})
// search condition: all files of filetype "Simple"
req.conditions = {};
req.conditions.type = "set";
req.conditions.conditions = [{type : "compare", field : "_type", value : "Simple", or : true, not : false}];
var json = JSON.stringify(req);
var archiveServer = context.getArchiveServer("ebisStore1");
var ebisConn = archiveServer.getArchiveConnection();
var headers = ["Content-Type", "application/json", "Accept", "application/json"];
var res = ebisConn.sendEbisRequest("/search", json, headers);
util.out(res);
=> EBIS returns query id  { id : "8c31d9352240a1c507d8d5f163e49085", columns : [ ], infos : [ ], executed : false }
```

***

### sendRequest()

> **sendRequest**(`request`): `string`

**Sends a request to the ArchiveConnection and returns the response XML.**  

With this method you can send a request to the XML-Server of EASY ENTERPRISE. If the method succeeds the return value is the response-xml, 
otherwise it returns `null`. If the value is `null` you can retrieve the error message by executing `ArchiveConnection.getLastError()`.

**Note:** Method is only available for EE.x using XML-Server

#### Parameters

##### request

`string`

String containing the request

#### Returns

`string`

an String with the response (xml) or `null` in case of any error

#### Since

ELC 3.60h / otrisPORTAL 6.0h

#### Example

```ts
var xmlserver = context.getArchiveConnection();
if (xmlserver)
{
   var req = "<INFO REQUESTID=\"1\"/>";
   var res = xmlserver.sendRequest(req);
   if (!res)
      util.out(xmlserver.getLastError());
   else
      util.out(res);
 }
```
