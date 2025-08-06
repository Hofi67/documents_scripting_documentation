[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / Document

# Interface: Document

**The Document class has been added to the DOCUMENTS PortalScripting API to gain full access to the documents stored on registers of a DOCUMENTS file by scripting means.**  

**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

## Since

ELC 3.50n / otrisPORTAL 5.0n

## Properties

### bytes

> `readonly` **bytes**: `number`

**The file size of the Document object in bytes.**

#### Since

DOCUMENTS 4.0e

#### See

[Document.size](#size)

***

### comment

> `readonly` **comment**: `string`

**The comment of the Document object.**

#### Since

DOCUMENTS 5.0d HF1

***

### encrypted

> `readonly` **encrypted**: `boolean`

**Info, if the blob is encrypted in the repository.**

#### Since

DOCUMENTS 4.0d HF3

***

### extension

> `readonly` **extension**: `string`

**The extension of the Document object.**  
 
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Since

ELC 3.50n / otrisPORTAL 5.0n

***

### fullname

> `readonly` **fullname**: `string`

**The complete filename (name plus extension) of the Document object.**  
 
  
**Since:** ELC 3.50n / otrisPORTAL 5.0n

#### Since

ELC 3.60i / otrisPORTAL 6.0i available for archive files

***

### id

> `readonly` **id**: `string`

**The id of the Document object.**

#### Since

DOCUMENTS 5.0e

***

### name

> `readonly` **name**: `string`

**The name (without extension) of the Document object.**  
 
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Since

ELC 3.50n / otrisPORTAL 5.0n

***

### size

> `readonly` **size**: `string`

**The formatted file size (e.g. 3.91 KB) of the Document object.**  
 
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Since

ELC 3.50n / otrisPORTAL 5.0n

#### See

[Document.bytes](#bytes)

## Methods

### deleteDocument()

> **deleteDocument**(): `boolean`

**Delete the Document object.**  

With the necessary rights you can delete a document of the file. Do this only on scratch copies (startEdit, commit)  

**Note:** It is strictly forbidden to access the Document object after this function has been executed successfully; 
if you try to access it, your script will fail, because the Document does not exist any longer in DOCUMENTS.  
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.60b / otrisPORTAL 6.0b

#### Example

```ts
// Deletion of the first document of the register "docs"
var myFile = context.file;
if (!myFile)
{
   util.out("missing file");
   return -1;
}
if (!myFile.startEdit())
{
   util.out("Unable to create scratch copy: " + myFile.getLastError());
   return -1;
}
var myReg = myFile.getRegisterByName("docs");
if (!myReg)
{
   util.out("missing >docs< register");
   return -1;
}
var firstDoc = myReg.getDocuments().first();
if (!firstDoc)
{
   return 0; // Nothing to do
}
if (!firstDoc.deleteDocument())
{
   util.out(firstDoc.getLastError());
   myFile.abort();
   return -1;
}
if (!myFile.commit())
{
   util.out("commit failed: " + myFile.getLastError());
   myFile.abort();
  return -1;
}
return 0;
```

***

### doOCR()

> **doOCR**(`ocrOutputFormat?`, `ocrTextFormat?`, `ocrTextTarget?`, `background?`, `force?`): `string`

**Execute OCR for the current document.**  

The OCR is executed independently of the main OCR property. Meaning OCR will be executed even if the
OCR property is not set for that document. The OCR method will create a searchable pdf-document or a
docx-document (not supported by Tesseract). If the type of the current document is an image format
like tif, png etc, the created searchable-document will be uploaded into the same register. If the
type of the current document already is a pdf/docx, the OCR-pdf will be uploaded as a new version of
the current document.  

Additionally to the pdf/docx creation, you can get the text content of the
document by using the parameters ocrTextFormat and ocrTextTarget. (The properties OCRTextFormat and
OCRTextTarget will be ignored in this function. If you specify an ocrTextFormat ("txt" or "alto")
the method will return the extracted words in the specified format as a string. If you specify an
ocrTextTarget (Registername), then the ocrTextFormat is uploaded to the specified register. The
parameters ocrTextFormat and ocrTextTarget are supported for the OCR-Engines Tesseract and Abbyy.  

If the parameter background is set to `true` only the OCR flag is set. In that case OCR is
executed in the background. As default, background is set to `false` and OCR is executed
immediately.  

Usually the job checks, if the document contains text before executing OCR. If you
want OCR to be executed even though the document contains text, set the parameter `force`
to `true`. If the check is performed, the Property OCRMinWordCount will be taken into account.

#### Parameters

##### ocrOutputFormat?

`string`

`"pdf"` or `"docx"`, see main description  

**Default:** `"pdf"`

##### ocrTextFormat?

`string`

`"txt"` or `"alto"`, see main description

##### ocrTextTarget?

`string`

the registername, where the ocrText will be uploaded

##### background?

`boolean`

`false`: OCR will be executed immediately, `true`: OCR will be executed later in a background job  

**Default:** `false`

##### force?

`boolean`

`false`: OCR will be sipped, if document is text, `true`: OCR will be executed in any case  

**Default:** `false`

#### Returns

`string`

the recongized text or an empty string, in case of an error, an exception will be thrown

#### Since

DOCUMENTS 5.0f

#### See

[Document.extractText](#extracttext)

#### Example

```ts
var file = context.file;
var reg1 = file.getRegisterByName("RegisterA");
var offerDoc = reg1.getDocuments().first();
if (offerDoc)
{
  try
  {
      // e.g. offerDoc.fullname = "offer.tif"
    var ocrText = offerDoc.doOCR("pdf", "txt", "RegisterA", false, false);
    util.out(ocrText);  // text content of offer.tif after OCR
      // now there are 3 documents at RegisterA
      // 1. offer.tif
      // 2. offer-ocr.pdf
      // 3. offer.txt
  }
  catch (ex)
  {
    util.out(ex);
  }
}
```

***

### downloadDocument()

> **downloadDocument**(`filePath?`, `version?`): `string`

**Download the Document to the server's filesystem for further use.**  
 
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files   
**Since:** DOCUMENTS 4.0 (new parameter filePath)   
**Since:** DOCUMENTS 4.0d (new parameter version)

#### Parameters

##### filePath?

`string`

Optional string specifying where the downloaded Document to be stored.  
 
**Note:** A file path containing special characters can be modified due to the encoding problem. The modified file path will be returned.

##### version?

`string`

Optional string value specifying which version of this Document to be downloaded (e.g. "2.0"). The default value is the active version.   

**Note:** This parameter is ignored for an archive document.

#### Returns

`string`

String containing full path and file name of the downloaded Document, an empty string in case of any error.

#### Since

ELC 3.50n / otrisPORTAL 5.0n

#### Examples

```ts
// Example 1
var docFile = context.file;
var reg = docFile.getRegisterByName("Documents");
var docIter = reg.getDocuments();
if (docIter && docIter.size() > 0)
{
   var doc = docIter.first();
   var docPath = doc.downloadDocument();
   var txtFile = new File(docPath, "r+t");
   if (txtFile.ok())
   {
      var stringVar = txtFile.readLine(); // read the first line
      txtFile.close();
   }
}
```

```ts
// Example 2
var docFile = context.file;
var reg = docFile.getRegisterByName("Documents");
var docIter = reg.getDocuments();
if (docIter && docIter.size() > 0)
{
   var doc = docIter.first();
   var docPath = "C:\\tmp\\test.txt";
   docPath = doc.downloadDocument(docPath, "2.0"); // since DOCUMENTS 4.0d
   if (docPath == "")
    util.out(doc.getLastError());
}
```

***

### extractText()

> **extractText**(`version?`, `options?`): `string`

**Extracts the text content of a document (eg pdf) **  

A appropriate extract program has to be defined in the documents.ini: $extracttext.pdf

#### Parameters

##### version?

`string`

String containing the wanted version of the document e.g. "2.0", use an empty value for the actual version.

##### options?

`string`

String containing additional options that will passed to the extract program.

#### Returns

`string`

`String` with the extracted text, an exception in case of any error.

#### Since

DOCUMENTS 5.0f

#### Example

```ts
var docFile = context.file;
var reg = docFile.getRegisterByName("Doc1");
var docIt = reg.getDocuments();
for (doc = docIt.first(); doc; doc = docIt.next())
{
  var text = doc.extractText();
  if (text == "")
    util.out(doc.getLastError());
  else
      util.out(text);
}
```

***

### getAsPDF()

> **getAsPDF**(): `string`

**Create a PDF file containing the current Document's contents and return the path in the file system.**  

The different document types of your documents require the appropriate PDF filter programs to be installed and configured in DOCUMENTS.

#### Returns

`string`

`String` with file path of the PDF, an empty string in case of any error.

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var docFile = context.file;
var reg = docFile.getRegisterByName("Doc1");
var docIt = reg.getDocuments();
for (doc = docIt.first(); doc; doc = docIt.next())
{
  var pathPdfFile = doc.getAsPDF();
  if (pathPdfFile == "")
      util.out(doc.getLastError());
  else
   util.out("File path: " + pathPdfFile);
}
```

***

### getAttribute()

> **getAttribute**(`attribute`): `string`

**Get the String value of an attribute of the Document.**  
 
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Parameters

##### attribute

`string`

String containing the name of the desired attribute

#### Returns

`string`

String containing the value of the desired attribute

#### Since

ELC 3.50n / otrisPORTAL 5.0n

***

### getLastError()

> **getLastError**(`shortMessage?`): `string`

**Function to get the description of the last error that occurred.**  
 
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files   
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

ELC 3.50n / otrisPORTAL 5.0n

#### See

[DocFile.getLastError](DocFile.md#getlasterror)

***

### getOID()

> **getOID**(`oidLow?`): `string`

**Returns the object-id.**  
 
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files   
**Since:** DOCUMENTS 5.0 (new parameter oidLow)

#### Parameters

##### oidLow?

`boolean`

Optional flag:   
If `true` only the id of the Document object (`m_oid`) will be returned.   
If `false` the id of the Document object will be returned together with the id of the corresponding class in the form `class-id:m_oid`.   

**Default:** `false`

#### Returns

`string`

the object-id

#### Since

ELC 3.60c / otrisPORTAL 6.0c

***

### getRegister()

> **getRegister**(): [`Register`](Register.md)

**Returns the Register the Document belongs to.**

#### Returns

[`Register`](Register.md)

Register object or `null` if missing

#### Since

DOCUMENTS 5.0c HF1

#### Example

```ts
var file = context.file;
var reg1 = file.getRegisterByName("RegisterA");
var firstDoc = reg1.getDocuments().first();
if (firstDoc)
{
   var reg = firstDoc.getRegister();
   if (reg)
      util.out(reg.name);  // "RegisterA"
}
```

***

### hash()

> **hash**(`hashfunction`, `version?`): `string`

**Generate the hash value for the Document using the given hash function.**  

These hash functions are supported: 
 
+ `sha1` 
+ `sha224` 
+ `sha256` 
+ `sha384`
+ `sha512`
+ `md4` 
+ `md5` 
+ `whirlpool` 
+ `ripemd160`

#### Parameters

##### hashfunction

`string`

String containing the name of the hash function.

##### version?

`string`

Optional string value specifying which version of this Document to be hashed (e.g. "2.0"). The default value is the active version.   

**Note:** This parameter is ignored for an archive document.

#### Returns

`string`

String with the hash value of the Document, an empty string in case of any error.

#### Since

DOCUMENTS 5.0e

#### See

[util.hash](Util.md#hash)

#### Example

```ts
var file = context.file;
var reg1 = file.getRegisterByName("RegisterA");
var firstDoc = reg1.getDocuments().first();
if (firstDoc)
{
  try
  {
    var hashValue = firstDoc.hash("sha256", "2.0");
    if (hashValue == "")
        util.out(firstDoc.getLastError());
  }
  catch (ex)
  {
    util.out(ex);
  }
}
```

***

### hasOcrFlag()

> **hasOcrFlag**(): `boolean`

**Checks if the current document still has to processed by the OCR engine.**  

If the OCR flag is set, the document must be processed by the OCR engine. After finishing the OCR process the flag is set back.

#### Returns

`boolean`

`true` if flag is set, `false` if not

#### Since

DOCUMENTS 5.0f

***

### hasWords()

> **hasWords**(`minWords?`, `version?`): `boolean`

**Check, if the current document has at least the specified number of words.**

#### Parameters

##### minWords?

`number`

Number of words  

**Default:** `5`

##### version?

`string`

Optional string value specifying which version of this document to be read (e.g. "2.0").

#### Returns

`boolean`

***

### moveToDocFile()

> **moveToDocFile**(`targetFile`, `targetRegister`): `boolean`

**Move the document to a documents register of another file.**  

With the necessary rights you can move the document to a documents register of another file.  

**Note:** This operation is not available for a document located in an archive file.

#### Parameters

##### targetFile

[`DocFile`](DocFile.md)

The file this document will be moved to.

##### targetRegister

[`Register`](Register.md)

The register in the target file this document will be moved to.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 6.0

#### Example

```ts
var sourceFile = context.getFileById("peachitreg_fi20230000000241");
var targetFile = context.getFileById("peachitreg_fi20230000000240");
var sourceReg = sourceFile.getRegisterByName("Doc1");
var targetReg = targetFile.getRegisterByName("Doc1");
var docIt = sourceReg.getDocuments();
for (var doc = docIt.first(); doc; doc = docIt.next())
{
  if (!doc.moveToDocFile(targetFile, targetReg))
  {
      util.out(doc.getLastError());
      break;
  }
}
```

***

### moveToRegister()

> **moveToRegister**(`regObj`): `boolean`

**Move the Document to another document Register of the file.**  

With the necessary rights you can move the Document to another document Register of the file.  

**Note:** This operation is not available for a Document located in an archive file.

#### Parameters

##### regObj

[`Register`](Register.md)

The Register this Document will be moved to.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var file = context.file;
if (!file.isArchiveFile())
{
   var regDoc1 = file.getRegisterByName("Doc1");
   var regDoc2 = file.getRegisterByName("Doc2");
   var docIt = regDoc2.getDocuments();
   for (var doc = docIt.first(); doc; doc = docIt.next())
   {
      if (!doc.moveToRegister(regDoc1))
          util.out(doc.getLastError());
   }
}
```

***

### pdo()

> **pdo**(): `PDObject`

**`Internal`**

**Function returns the PDObject of the Document.**  

This function is for internal use only!

#### Returns

`PDObject`

PDObject, in case of an error an exception will be thrown

#### Since

DOCUMENTS 5.0f HF1

***

### readAsString()

> **readAsString**(`version?`): `string`

**Read the document and return its content as a string in case of the document being a text file.**

#### Parameters

##### version?

`string`

Optional string value specifying which version of this document to be read (e.g. "2.0"). The default version is the active version.   

**Note:** This parameter is ignored for an archive document.

#### Returns

`string`

String with content of the document; empty string in case of errors.

#### Since

DOCUMENTS 5.0f

***

### reindexBlob()

> **reindexBlob**(): `boolean`

**Reindex the blob located in an active file.**  

This method is only allowed if at the filetype the option `'automatic document indexing'` is enabled.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e HF2

***

### setAttribute()

> **setAttribute**(`attribute`, `value`): `boolean`

**Set the String value of an attribute of the Document to the desired value.**  
  
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

ELC 3.50n / otrisPORTAL 5.0n

***

### setDocumentName()

> **setDocumentName**(`nameWithExt`): `boolean`

**Set the name of the current document.**  

This method is only allowed for documents at a scratch copy (`startEdit`, `commit`).

#### Parameters

##### nameWithExt

`string`

String containing the document name with extension.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e HF2

#### Example

```ts
// Rename the first document of the register "docs"
var myFile = context.file;
if (!myFile)
{
   util.out("missing file");
   return -1;
}
if (!myFile.startEdit())
{
   util.out("Unable to create scratch copy: " + myFile.getLastError());
   return -1;
}
var myReg = myFile.getRegisterByName("docs");
if (!myReg)
{
   util.out("missing >docs< register");
   return -1;
}
var firstDoc = myReg.getDocuments().first();
if (!firstDoc)
{
   return 0; // Nothing to do
}
if (!firstDoc.setDocumentName("newName.txt"))
{
   util.out(firstDoc.getLastError());
   myFile.abort();
   return -1;
}
if (!myFile.commit())
{
   util.out("commit failed: " + myFile.getLastError());
   myFile.abort();
  return -1;
}
return 0;
```

***

### uploadDocument()

> **uploadDocument**(`sourceFilePath`, `versioning?`): `boolean`

**Upload a file stored on the server's filesystem for replacing or versioning this Document.**  

**Note:** After successful upload of the Document the source file on the server's directory structure is removed!

#### Parameters

##### sourceFilePath

`string`

String containing the path of the desired file to be uploaded.   

**Note:** Backslashes contained in the filepath must be quoted with a leading backslash, since the backslash is a special char in ECMAScript!

##### versioning?

`boolean`

Optional flag: `true` for versioning the Document and `false` for replacing it.  

**Default:** `true`

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 4.0d

#### Example

```ts
var docFile = context.file;
var reg = docFile.getRegisterByName("Documents");
var docIter = reg.getDocuments();
if (docIter && docIter.size() > 0)
{
   var doc = docIter.first();
   if (!doc.uploadDocument("c:\\tmp\\test.txt", true))
      util.out(doc.getLastError());
}
```
