[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / Util

# Interface: Util

**The Util class supports some functions that do not need any user or file context.**  

These functions allow customizable Date/String conversions and other useful stuff.
There is exactly ONE implicit object of the class \`Util\` which is named [\`util\`](../variables/util.md).

**Note:**  
It is not possible to create objects of the class Util. There are no properties
in this class, it supports only the help functions as documented below.

## Properties

### buildNo

> **buildNo**: `number`

**Build version number of the PortalServer.**  

This property allows to retrieve the build version number of the PortalServer to customize your PortalScripts in dependence of the used PortalServer.

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
if (util.buildNo > 1826)
{
   // do update
}
```

***

### DB

> **DB**: `string`

**Database using by the PortalServer.**  

The following databases are supported by the PortalServer: 

+ `oracle`
+ `mysql`
+ `mssql`

#### Since

DOCUMENTS 4.0

***

### memoryModel

> **memoryModel**: `string`

**Memory model of the PortalServer.**  

There are two possible memory models available : x64 or x86.

#### Since

DOCUMENTS 4.0

***

### version

> **version**: `number`

**Main version number of the PortalServer.**  

This property allows to retrieve the version number of the PortalServer to customize your PortalScripts in dependence of the used PortalServer. 
For example: 
<ul> 
<li>otrisPORTAL 5.1 / ELC 3.51 returns 5100 </li> 
<li>otrisPORTAL 6.0 / ELC 3.60 returns 6000 </li> 
<li>DOCUMENTS 4.0 returns 7000</li> 
</ul>

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
if (util.version < 6000)
{
   // do update
}
```

## Methods

### base64Decode()

> **base64Decode**(`value`, `returnArray?`): `any`

**Decodes a base64 string and returns a string or byte-array.**

#### Parameters

##### value

`string`

String to decode

##### returnArray?

`boolean`

boolean as an optional parameter to define if the return value must be a byte-array or string (default)  

**Default:** `false`

#### Returns

`any`

decoded string or byte-array

#### Since

DOCUMENTS 4.0c HF1

#### Example

```ts
var b64Str = util.base64Encode("Hello World");
util.out(b64Str);   // SGVsbG8gV29ybGQ=
var str = util.base64Decode(b64Str);
util.out(str);      // Hello World
var byteArr = util.base64Decode(b64Str, true);
util.out(byteArr);  // 72,101,108,108,111,32,87,111,114,108,100
b64Str = util.base64Encode(byteArr);
util.out(b64Str);   // SGVsbG8gV29ybGQ=
```

***

### base64Encode()

> **base64Encode**(`value`, `urlStyle?`): `string`

**Encodes a byte-array or string to base64 and returns the base 64 string.**  

**Note:** The URL style uses the characters '-' and '_' in place of '+' and '/', and it does not allow padding characters ('='). 
[base64Decode()](#base64decode) does actually not support this style.

**Since:** 5.0d HF2 urlStyle

#### Parameters

##### value

`any`

String or byte-array to encode

##### urlStyle?

`boolean`

optional boolean flag to request Base64URL encoding instead of standard Base64 encoding  

**Default:** `false`

#### Returns

`string`

base64 encoded string

#### Since

DOCUMENTS 4.0c HF1

#### Example

```ts
var b64Str = util.base64Encode("Hello World");
util.out(b64Str);   // SGVsbG8gV29ybGQ=
var str = util.base64Decode(b64Str);
util.out(str);      // Hello World
var byteArr = util.base64Decode(b64Str, true);
util.out(byteArr);  // 72,101,108,108,111,32,87,111,114,108,100
b64Str = util.base64Encode(byteArr);
util.out(b64Str);   // SGVsbG8gV29ybGQ=
```

***

### beep()

> **beep**(`frequency`, `duration`): `void`

**Plays a beep sound at the PortalServer's system.**  

For testing purposes a beep sound can be played at the server

#### Parameters

##### frequency

`number`

int with the frequency in hertz

##### duration

`number`

int with the length of the sound in milliseconds (ms)

#### Returns

`void`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

#### Example

```ts
util.beep(1250, 3000);
```

***

### byteLength()

> **byteLength**(`input`, `encoding?`): `number`

Calculates the size in bytes of the given input in a specified encoding.

#### Parameters

##### input

The input whose byte length is to be calculated. Can be a string, array, or various typed arrays.

`string` | `ArrayBuffer` | `Int8Array`\<`ArrayBuffer`\> | `Uint8Array`\<`ArrayBuffer`\> | `Uint8ClampedArray`\<`ArrayBuffer`\> | `Int16Array`\<`ArrayBuffer`\> | `Uint16Array`\<`ArrayBuffer`\> | `Int32Array`\<`ArrayBuffer`\> | `Uint32Array`\<`ArrayBuffer`\> | `Float32Array`\<`ArrayBuffer`\> | `Float64Array`\<`ArrayBuffer`\> | `number`[]

##### encoding?

`string`

The encoding to use for string inputs. The following encodings are supported: 
 
+ `Local`: The standard system encoding for Windows systems is `Windows-1252` and for Linux systems `ISO-8859-1` or `UTF-8`.
+ `UTF-8`: Unicode-characterset as ASCII-compatible 8-Bit-coding. 
+ `ISO-8859-1`: West-European characterset without Euro-Symbol. 
+ `ISO-8859-15`: West-European characterset with Euro-Symbol.
+ `Windows-1252`
+ `Windows-1250`

**Default:** `UTF-8`

#### Returns

`number`

Number of bytes

#### Throws

Invalid values for the arguments

#### Since

DOCUMENTS 6.2.0

#### Examples

```ts
// Calculate byte length of a string
const str = "Hello, world!";
const byteLength = util.byteLength(str); // => 13 bytes
util.out("Byte length of string: " + byteLength);
```

```ts
// Calculate byte length of a number array
const numberArray = [1, 2, 3, 4, 5];
const byteLength = util.byteLength(numberArray); // => 40 bytes
util.out("Byte length of number array: " + byteLength);
```

```ts
// Calculate byte length of a Uint8Array
const uint8Array = new Uint8Array([1, 2, 3, 4, 5]);
const byteLength = util.byteLength(uint8Array); // => 5 bytes
util.out("Byte length of Uint8Array: " + byteLength);
```

```ts
// Calculate byte length of an ArrayBuffer
const arrayBuffer = new ArrayBuffer(10);
const byteLength = util.byteLength(arrayBuffer); // => 10 bytes
util.out("Byte length of ArrayBuffer: " + byteLength);
```

```ts
// Calculate byte length of a string with specific encoding
const str = "Köln"; 
const byteLength = util.byteLength(str, 'utf-8'); // => 5 bytes
util.out("Byte length of string in UTF-8: " + byteLength);
```

***

### concatPDF()

> **concatPDF**(`pdfFilePaths`, `deleteSinglePdfs?`): `string`

**Concatenate the given PDFs together into one PDF.**

#### Parameters

##### pdfFilePaths

`any`[]

Array containing the file paths of PDFs to be concatenated.

##### deleteSinglePdfs?

`boolean`

Optional boolean value to decide whether to delete the single PDFs on the server's filesystem after concatenating.  

**Default:** `false`

#### Returns

`string`

String with file path of the PDF, an empty string in case of any error.

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var arr = ["C:\\temp\\number1.pdf", "C:\\temp\\number2.pdf"];
var filePath = util.concatPDF(arr, false);
util.out("PDF file path: " + filePath);
```

***

### convertBlobToPDF()

> **convertBlobToPDF**(`sourceFilePath`): `string`

**Convert a file to a PDF file and return the path in the file system.**  

The different file types require the appropriate PDF filter programs to be installed and configured in DOCUMENTS.

#### Parameters

##### sourceFilePath

`string`

String containing the path of the file to be converted.

#### Returns

`string`

`String` with file path of the PDF, an empty string in case of any error.

#### Since

DOCUMENTS 4.0d HF3

#### Example

```ts
var pathPdfFile = util.convertBlobToPDF("C:\\tmp\\testFile.doc");
util.out(pathPdfFile);
```

***

### convertDateToExcelDate()

> **convertDateToExcelDate**(`timeStamp`): `number`

**Convert a Date object to an Excel numeric date format.**  

Excel stores timestamp as a double value. This value exists by two parts. The pre-decimal position is the amount of days since 01.01.1900. 
The fractional part is the percential time in day. 
<ul> 
<li>e.g. 10.01.1900 12:00 => 10.5</li> 
<li>e.g. 19.10.2018 14:30: => 43392.6042</li> 
</ul> 
A date before 01.03.1900 can not be converted. The method will return -1.0.

#### Parameters

##### timeStamp

`Date`

Date object representing the desired date

#### Returns

`number`

double as excel date representation

#### Since

DOCUMENTS 5.0e

#### Example

```ts
var now = new Date();
var excelDate = util.convertDateToExcelDate(now);
if (excelDate < 0.0)
   util.out("I can only convert dates that are after 01.03.1900")
else
   util.out(excelDate + " is now a numeric value");
```

***

### convertDateToString()

> **convertDateToString**(`timeStamp`, `format`): `string`

**Convert a Date object representing a date into a String.**  

The output String may have any format you like. The second parameter defines the format to configure which part of the date String should match the according properties of the Date object.  
  
**Since:** DOCUMENTS 5.0a (new: Special formats `"@date"` and `"@timestamp"`)

#### Parameters

##### timeStamp

`Date`

Date object representing the desired date

##### format

`string`

String defining the date format of the output String, e.g. "dd.mm.yyyy".  

The possible format parts are:
+ `dd` = two digit day
+ `mm` = two digit month
+ `yy` = two digit year
+ `yyyy` = four digit year
+ `HH` = two digit hour (24 hour format)
+ `MM` = two digit minute
+ `SS` = two digit second

Special formats:
+ `@date` = `@yyyymmdd` (locale independant format for filter in a [FileResultset](../classes/FileResultset.md), [HitResultset](../classes/HitResultset.md))
+ `@timestamp` = `@yyyymmddHHMMSS` (locale independant format for filter in a [FileResultset](../classes/FileResultset.md), [HitResultset](../classes/HitResultset.md))

#### Returns

`string`

String representing the desired date

#### Since

ELC 3.50e / otrisPORTAL 5.0e

#### See

[util.convertStringToDate](#convertstringtodate)  
[context.convertDateToString](Context.md#convertdatetostring)

#### Example

```ts
var format = "dd.mm.yyyy HH:MM";
var now = new Date();
util.out(util.convertDateToString(now, format));
```

***

### convertStringToDate()

> **convertStringToDate**(`dateOrTimeStamp`, `format`): `Date`

**Convert a String representing a date into a Date object.**  

The String may contain a date or timestamp in any date format you like. The second parameter defines the format to configure which part of 
the date String should match the according properties of the Date object.  
  
**Since:** DOCUMENTS 5.0a (new: Special formats `"@date"` and `"@timestamp"`)

#### Parameters

##### dateOrTimeStamp

`string`

String representing a date, e.g. "19.09.1974"

##### format

`string`

String defining the date format of the input String, e.g. "dd.mm.yyyy".

The possible format parts are:
+ `dd` = two digit day
+ `mm` = two digit month
+ `yy` = two digit year
+ `yyyy` = four digit year
+ `HH` = two digit hour (24 hour format)
+ `MM` = two digit minute
+ `SS` = two digit second

Special formats:
+ `@date` = `@yyyymmdd` (locale independant format for filter in a [FileResultset](../classes/FileResultset.md), [HitResultset](../classes/HitResultset.md))
+ `@timestamp` = `@yyyymmddHHMMSS` (locale independant format for filter in a [FileResultset](../classes/FileResultset.md), [HitResultset](../classes/HitResultset.md))

#### Returns

`Date`

Date object representing the desired date

#### Since

ELC 3.50e / otrisPORTAL 5.0e

#### See

[util.convertDateToString](#convertdatetostring)

#### Example

```ts
var format = "dd.mm.yyyy HH:MM";
var dateString = "19.09.1974";
var birthDay = util.convertStringToDate(dateString, format);
```

***

### cryptPassword()

> **cryptPassword**(`pwPlain`): `string`

**Encrypt a plain password into an MD5 hash.**

#### Parameters

##### pwPlain

`string`

String containing the plain password

#### Returns

`string`

String containing the encrypted password

#### Since

ELC 3.50o / otrisPORTAL 5.0o

#### Example

```ts
var cryptPW = util.cryptPassword("Hello World");
util.out(cryptPW);
```

***

### decodeURIComponent()

> **decodeURIComponent**(`uriComponent`): `string`

**Returns the decoded URI String.**

#### Parameters

##### uriComponent

`string`

String with the encoded URI component

#### Returns

`string`

String with decoded content

#### Since

DOCUMENTS 5.0h

#### See

[util.encodeURIComponent](#encodeuricomponent)

#### Example

```ts
const text = "I live in München";
const encText = util.encodeURIComponent(text);   // I%20live%20in%20M%C3%BCnchen
const url = "https://api.deepl.com/v2/translate/?auth_key=123&target_lang=DE&text=" + encText;
const decodedText = util.decodeURIComponent(encText);
```

***

### decodeUrlCompatible()

> **decodeUrlCompatible**(`encodedParam`): `string`

**Decode URL parameter from DOCUMENTS Urls.**

#### Parameters

##### encodedParam

`string`

String containing the encoded URL param

#### Returns

`string`

`String` with decoded URL param.

#### Since

DOCUMENTS 5.0a

#### See

[util.encodeUrlCompatible](#encodeurlcompatible)

#### Example

```ts
// URL with an archive key
var encUrl = "http://localhost:8080/documents/UserLoginSuccessAction.act;cnvid=n0RIshUTRnOH3qAn?
              pri=easyhr&lang=de#fi_96:3020/
              id_{ehrmEmployeeDocument$EAstore2$HMUnit$DNDefault$CPInstance$DNDefault$CPPool$DNAdaptive
              $CPPool$DNAdaptive02$CPDocument$DNADAPTIVE$CO060C8A9C3A1811E6B75A000C29E0A93B}
              /ri_FileCover/di_easyhrdc0000000000000497";
var decUrl = util.decodeUrlCompatible(encUrl);
decUrl == "http://localhost:8080/documents/UserLoginSuccessAction.act;cnvid=n0RIshUTRnOH3qAn
           ?pri=easyhr&lang=de#fi_96:3020/
           id_{ehrmEmployeeDocument@store2|Unit=Default/Instance=Default/Pool=Adaptive/Pool=
           Adaptive02/Document=ADAPTIVE.060C8A9C3A1811E6B75A000C29E0A93B}
           /ri_FileCover/di_easyhrdc0000000000000497";
```

***

### decryptString()

> **decryptString**(`input`): `string`

**Decrypts a String value hat was encrypted with the method [Util.encryptString(String input)](#encryptstring)**

#### Parameters

##### input

`string`

The string that will be decrypted

#### Returns

`string`

String decrypted value

#### Since

DOCUMENTS 5.0b

#### See

[util.encryptString](#encryptstring)

#### Example

```ts
var text = "I'm a secret password";
var encryptedText = util.encryptString(text);
util.out(encryptedText);  // NABPIGCGBHEBBOMECMJHDBHIIHOCDNOMODEILCABDKOLJBMFBKDDOFDABNAMCLJC
var decryptedText = util.decryptString(encryptedText);
util.out(decryptedText);  // I'm a secret password
```

***

### deleteDirectory()

> **deleteDirectory**(`dirPath`): `string`

**Deletes a directory including all its subdirectories and files.**

#### Parameters

##### dirPath

`string`

String with the path to the directory to be deleted on the server.

#### Returns

`string`

empty String if successful, the error message in case of any error

#### Since

DOCUMENTS 5.0h

#### Example

```ts
var errMsg = util.deleteDirectory("c:\\tmp\\test");
if (errMsg.length > 0)
    util.out(errMsg);
else
    util.out("Ok.");
```

***

### deleteFile()

> **deleteFile**(`filePath`): `string`

**Delete a file (file system object) at the PortalServer's system.**  

This functions provides a simple delete method for files on the server's file system.

#### Parameters

##### filePath

`string`

String with the file path

#### Returns

`string`

empty String if successful, the error message in case of any error

#### Since

ELC 3.60e / otrisPORTAL 6.0e

#### Example

```ts
var errMsg = util.deleteFile("c:\\Test.log");
if (errMsg.length > 0)
    util.out(errMsg);
else
    util.out("Ok.");
```

***

### doOCR()

> **doOCR**(`filePath`, `options?`): `string`

**Execute OCR for the document and create a searchable pdf-document.**  

The doOCR method will create a searchable pdf-document and returns the path to the document.  

**Note:** OCR license is necessary

#### Parameters

##### filePath

`string`

String with the path to binary (jpg, png, tif, pdf)

##### options?

`string`

String containing an optional value; currently supported "-f 2 -l 3" => create a new searchable pdf containing the pages 2-3

#### Returns

`string`

filePath of the searchable pdf-documents

#### Since

DOCUMENTS 5.0i HF3

***

### encodeURIComponent()

> **encodeURIComponent**(`uriComponent`): `string`

**Returns the URI encoded String.**

#### Parameters

##### uriComponent

`string`

String with the URI component

#### Returns

`string`

String with encoded content

#### Since

DOCUMENTS 5.0g

#### See

[util.decodeURIComponent](#decodeuricomponent)

#### Example

```ts
const text = "I live in München";
const encText = util.encodeURIComponent(text);   // I%20live%20in%20M%C3%BCnchen
const url = "https://api.deepl.com/v2/translate/?auth_key=123&target_lang=DE&text=" + encText;
```

***

### encodeUrlCompatible()

> **encodeUrlCompatible**(`param`): `string`

**Encode URL parameter for DOCUMENTS Urls.**  

Some parameters in DOCUMENTS urls must be encoded. E.g. the archive keys can contain invalid characters like / etc.

#### Parameters

##### param

`string`

String containing the value to encode

#### Returns

`string`

`String` with encoded value.

#### Since

DOCUMENTS 5.0a

#### See

[util.decodeUrlCompatible](#decodeurlcompatible)

#### Example

```ts
// URL with an archive key
var url = "http://localhost:8080/documents/UserLoginSuccessAction.act;cnvid=n0RIshUTRnOH3qAn?
           pri=easyhr&lang=de#fi_96:3020/
           id_{ehrmEmployeeDocument@store2|Unit=Default/Instance=Default/Pool=Adaptive/Pool=
           Adaptive02/Document=ADAPTIVE.060C8A9C3A1811E6B75A000C29E0A93B}
           /ri_FileCover/di_easyhrdc0000000000000497";
// The archive key is the value between  id_{   }
// "ehrmEmployeeDocument@store2|Unit=Default/Instance=Default/Pool=
//  Adaptive/Pool=Adaptive02/Document=ADAPTIVE.060C8A9C3A1811E6B75A000C29E0A93B"
// this key must be encoded
var encUrl = encodeURL(url);
encUrl == "http://localhost:8080/documents/UserLoginSuccessAction.act;cnvid=n0RIshUTRnOH3qAn?
           pri=easyhr&lang=de#fi_96:3020/
           id_{ehrmEmployeeDocument$EAstore2$HMUnit$DNDefault$CPInstance$DNDefault$CPPool$DNAdaptive
           $CPPool$DNAdaptive02$CPDocument$DNADAPTIVE$CO060C8A9C3A1811E6B75A000C29E0A93B}
           /ri_FileCover/di_easyhrdc0000000000000497";
function encodeURL(url)
{
   // RegEx to split the url in it's parts
   var reg = /(.*id_{)(.*)(}.*)/
   if (!url.match(reg))
      throw "unable to encode";
   var part1 = RegExp.$1;
   var partKey = RegExp.$2;
   var part3 = RegExp.$3;
   return encoded = part1 + util.encodeUrlCompatible(partKey) + part3;
}
```

***

### encryptString()

> **encryptString**(`input`): `string`

**Encrypts a String value with the AES 256 CBC algorithm for symmetric encryption/decryption.**  

The length of the input String is limited to 1024 bytes. The encrypted value depends on the principal name. Usage is e.g. storing of passwords 
in the database for authorization against 3rd party web services.  
  
**Since:** DOCUMENTS 5.0i HF1 max length 4096 bytes

#### Parameters

##### input

`string`

The string that will be encrypted

#### Returns

`string`

String encrypted value

#### Since

DOCUMENTS 5.0b

#### See

[util.decryptString](#decryptstring)

#### Example

```ts
var text = "I'm a secret password";
var encryptedText = util.encryptString(text);
util.out(encryptedText);  // NABPIGCGBHEBBOMECMJHDBHIIHOCDNOMODEILCABDKOLJBMFBKDDOFDABNAMCLJC
var decryptedText = util.decryptString(encryptedText);
util.out(decryptedText);  // I'm a secret password
```

***

### extractText()

> **extractText**(`filePath`, `textFormat?`, `options?`): `string`

**Extracts the text content of a document (e.g. docx) or returns the OCR content of binary (e.g. tif, pdf).**  

This method has two modes. Mode 1 is the OCR Mode. If you call the method with at minimum
two parameters (`filePath` and `textFormat`), then an OCR of the document (e.g. tif, pdf) will
be done and the content will be returned in the desired textFormat (**Note:** OCR license is necessary)

Mode 2 is the extraction mode. If you call the method with exatct one parameter (`filePath`)
the text of the document (e.g. docx) will be extracted if an 
appropriate extract program is defined in the `documents.ini: $extracttext.docx`.
If no extract program is defined for the document, then an OCR with default values will be done.
  
**Since:** DOCUMENTS 5.0i HF3: Parameter options

**Since:** DOCUMENTS 6.0.1: Mode for text extraction

#### Parameters

##### filePath

`string`

String with the path to binary (jpg, png, tif, pdf)

##### textFormat?

`string`

String "txt" or "alto"

##### options?

`string`

String containing an optional value; currently supported "-f 2 -l 3" => only extract from pages 2-3

#### Returns

`string`

String with text content

#### Since

DOCUMENTS 5.0f HF2

***

### fileCopy()

> **fileCopy**(`sourceFilePath`, `targetFilePath`): `string`

**Copy a file (file system object) at the PortalServer's system.**  

This functions provides a simple copy method for files on the server's file system.

#### Parameters

##### sourceFilePath

`string`

String with the source file path

##### targetFilePath

`string`

String with the target file path

#### Returns

`string`

empty String if successful, the error message in case of any error

#### Since

ELC 3.60e / otrisPORTAL 6.0e

#### See

[util.fileMove](#filemove)

#### Example

```ts
var errMsg = util.fileCopy("c:\\Test.log", "d:\\Test.log");
if (errMsg.length > 0)
    util.out(errMsg);
else
    util.out("Ok.");
```

***

### fileMove()

> **fileMove**(`sourceFilePath`, `targetFilePath`): `string`

**Move a file (file system object) at the PortalServer's system from a source file path to the target file path.**  

This functions provides a simple move method for files on the server's file system.

#### Parameters

##### sourceFilePath

`string`

String with the source file path

##### targetFilePath

`string`

String with the target file path

#### Returns

`string`

empty String if successful, the error message in case of any error

#### Since

ELC 3.60e / otrisPORTAL 6.0e

#### See

[util.fileCopy](#filecopy)

#### Example

```ts
var errMsg = util.fileMove("c:\\Test.log", "d:\\Test.log");
if (errMsg.length > 0)
    util.out(errMsg);
else
    util.out("Ok.");
```

***

### fileSize()

> **fileSize**(`filePath`): `number`

**Retrieve the filesize of a file (file system object) at the PortalServer's system.**  

This functions returns the filesize of a file.

#### Parameters

##### filePath

`string`

String with the file path

#### Returns

`number`

Int with file size if successful, the value -1 in case of any error

#### Since

ELC 3.60e / otrisPORTAL 6.0e

#### Example

```ts
var size = util.fileSize("c:\\Test.log");
if (size < 0)
    util.out("File does not exist.");
else
    util.out(size);
```

***

### generateChecksum()

> **generateChecksum**(`input`): `string`

**Creates a MD5 checksum for the String value.**

#### Parameters

##### input

`string`

The string for that the checksum will be generated

#### Returns

`string`

String with the checksum

#### Since

DOCUMENTS 4.0c

#### Example

```ts
var text = "I'm some type of text";
var md5 = util.generateChecksum(text);
if (md5 != "a77c16d60b9939295c0af4c7242b6c02")
   util.out("wrong md5!");
```

***

### generateRandomString()

> **generateRandomString**(`length`, `encoding?`): `string`

**Generates a random String with Chars based on the encoding.**  

If parameters are out of bounds or the generation of chars fails, the function throws an exception.

#### Parameters

##### length

`number`

The length of the wanted string. Maximum of 32 is supported

##### encoding?

`number`

The following encodings are supported:

 + `0`: Possible chars: A-Z 2-7
 + `1`: Possible chars: A-Z a-z 2-9
 + `2`: Possible chars: 0-9

**Default:** `0`

#### Returns

`string`

String containing random chars based on the Encoding

#### Since

DOCUMENTS 6.2.0

#### Example

```ts
let randomString = util.generateRandomString(32, 0);
util.out(randomString.length); // Prints "32"
util.out(randomString); // Prints the 'randomString' containing characters from A-Z | 2-7
```

***

### getBaseURL()

> **getBaseURL**(): `string`

**Returns the base url of the web application.**

#### Returns

`string`

`String` with the URL.

#### Since

DOCUMENTS 5.0i HF1

***

### getDir()

> **getDir**(`dirname`, `files`, `subDirs`): `string`

**Retrieving files and subdirectories of a specified directory.**  

This function retrieve the content (files, subdirectories) of a specified directory of the PortalServer's file system. It expected two empty Arrays, 
which the function fill with the filenames and subdirectory names. The names will not contain the full path, only the name itself. This function will not work recursively.

#### Parameters

##### dirname

`string`

String containing the name of the wanted directory

##### files

`any`[]

Empty array for the filenames

##### subDirs

`any`[]

Empty array for the subdirectory names

#### Returns

`string`

empty String if successful, the error message in case of any error

#### Since

ELC 3.60e / otrisPORTAL 6.0e

#### Example

```ts
var files = new Array();
var dirs = new Array();
util.getDir("c:\\Test", files, dirs);
var i=0;
for (i=0; i < files.length; i++)
   util.out(files[i])
for (i=0; i < dirs.length; i++)
   util.out(dirs[i])
```

***

### getDirSep()

> **getDirSep**(): `string`

**`Internal`**

**Returns the dir separator.**  

This function is for internal use only!

#### Returns

`string`

#### Since

DOCUMENTS 5.0e

***

### getEnvironment()

> **getEnvironment**(`variableName`): `string`

**Reads an environment variable of the PortalServer's system.**  

With this function an environment variable in the server's context can be read.

#### Parameters

##### variableName

`string`

String with the name of the variable

#### Returns

`string`

Environment value as String

#### Since

ELC 3.60e / otrisPORTAL 6.0e

#### Example

```ts
util.out(util.getEnvironment("HOME"));
```

***

### getFileContentAsString()

> **getFileContentAsString**(`filePath`): `string`

**Get the content of a file at the PortalServer's system as string in base64 format.**

#### Parameters

##### filePath

`string`

String with the file path.

#### Returns

`string`

String containing the file content in base64 format.

#### Since

DOCUMENTS 4.0c

***

### getIniNames()

> **getIniNames**(): `string`[]

**`Internal`**

Returns a list of the defined ini parameters.

#### Returns

`string`[]

`string[]` with the names of the ini parameters

#### Since

DOCUMENTS 6.0.1

#### See

[util.getIniValue](#getinivalue)

***

### getIniValue()

> **getIniValue**(`name`): `string`

**Returns the value of the desired ini parameter.**

#### Parameters

##### name

`string`

String containing the name of the ini parameter.

#### Returns

`string`

`String` with the value or empty string for an unknown parameter.

#### Since

DOCUMENTS 5.0i

#### Example

```ts
var dhs = util.getIniValue("$DefaultHostName");
util.out("DefaultHostName: " + dhs);
```

***

### getModelAttributes()

> **getModelAttributes**(`classname`, `flags`): `any`[]

**`Internal`**

**Returns an array with all attribute names for the class.**  

This function is for internal use only!

#### Parameters

##### classname

`string`

String containing the name of the class.

##### flags

`number`

Integer with internal flag, use 0.

#### Returns

`any`[]

#### Since

DOCUMENTS 5.0a

***

### getModelDatatype()

> **getModelDatatype**(`classname`, `attrname`): `string`

**`Internal`**

**Returns the datatype as string for an attribute of a class.**  

This function is for internal use only!

#### Parameters

##### classname

`string`

String containing the name of the class.

##### attrname

`string`

String containing the name of the attribute.

#### Returns

`string`

#### Since

DOCUMENTS 5.0a

***

### getModelErgname()

> **getModelErgname**(`classname`, `attrname`): `string`

**`Internal`**

**Returns the label for an attribute of a class.**  

This function is for internal use only!

#### Parameters

##### classname

`string`

String containing the name of the class.

##### attrname

`string`

String containing the name of the attribute.

#### Returns

`string`

#### Since

DOCUMENTS 5.0a

***

### getQuoted()

> **getQuoted**(`input`): `string`

**Returns the input string enclosed in either double or single quotation marks.**  

This function is designed to simplify the composition of filter expressions for a FileResultSet or an ArchiveFileResultSet. 
If the input string does not contain any double quotation mark ("), the function returns the input enclosed in double quotation marks. 
Otherwise the function tests if it can use single quotation marks (') instead. If both quotation styles are already used within the input, 
the function throws an exception.

#### Parameters

##### input

`string`

The string to be enclosed

#### Returns

`string`

String with quotation marks around.

#### Since

DOCUMENTS 4.0b

***

### getServerConfig()

#### Call Signature

> **getServerConfig**(`name`): `string` \| `false`

Returns the value of a general setting from the server
configuration, i.e. the Ini file.

##### Parameters

###### name

`string`

Name of the requested setting or empty string.

##### Returns

`string` \| `false`

Set config value or false, if the setting is not set
  or does not exist

##### Remarks

If an empty string is provided, a description of all settings
as an JSON string will be returned. But this depends on the
availabiliy of the iniSpec.janus.xml in server directory. If
this file is missing an empty description is returned.

If application-specific settings shall be read,
[util.getIniValue](#getinivalue) has to be used.

##### Throws

Invalid value for the argument or internal server error

##### Since

DOCUMENTS 6.1.0

##### See

 - [util.getIniValue](#getinivalue)
 - [util.getServerConfig(names)](./Util.html#getServerConfig.getServerConfig-2)

##### Example

```ts
context.returnValue = util.getServerConfig("");
// {"params": []}
// (in case of a missing iniSpec.janus.xml)
// 
context.returnValue = util.getServerConfig("Port");
// 11000
//
context.returnValue = util.getServerConfig("DoesNotExist");
// false
```

#### Call Signature

> **getServerConfig**(`names`): `false` \| `string`[]

Returns the values of general settings from the server
configuration, i.e. the Ini file.

##### Parameters

###### names

`string`[]

Names of the requested settings

##### Returns

`false` \| `string`[]

Config values in an array or false, if one of the
requested settings is not set or does not exist

##### Remarks

If application-specific settings shall be read,
[util.getIniValue](#getinivalue) has to be used.

##### Throws

Invalid value for the argument or internal server error

##### Since

DOCUMENTS 6.1.0

##### See

 - [util.getIniValue](#getinivalue)
 - [util.getServerConfig(name)](./Util.html#getServerConfig.getServerConfig-1)

##### Example

```ts
context.returnValue = JSON.stringify(util.getServerConfig([
  "Port",
  "JSMaxMemory"
]));
// ["11000","16384"]
//
context.returnValue = JSON.stringify(util.getServerConfig([
  "Port",
  "JSMaxMemory",
  "DoesNotExist"
]));
// false
```

***

### getServerOS()

> **getServerOS**(): `string`

**Returns the server OS.**

#### Returns

`string`

String with the server OS.

#### Since

DOCUMENTS 5.0e

***

### getServerPath()

> **getServerPath**(): `string`

**Returns the path where the documents server binary is located.**

#### Returns

`string`

String with the path to the documentsserver binary

#### Since

DOCUMENTS 5.0f

***

### getSourceLineInfo()

> **getSourceLineInfo**(): `string`

**Retrieve the scriptName with the current line no of this methed.**  

This functions returns the scriptName and line no for debugging or logging purposes

#### Returns

`string`

String with the scriptName and line no

#### Since

DOCUMENTS 5.0a

***

### getTmpPath()

> **getTmpPath**(): `string`

**Get the path to the temporary directory on the Portalserver.**

#### Returns

`string`

String containing the complete path to the temporary directory

#### Since

ELC 3.51 / otrisPORTAL 5.1

#### Example

```ts
util.out(util.getTmpPath());
```

***

### getUniqueId()

> **getUniqueId**(): `string`

**Get a unique id from the system.**  

The length of the id is 40 characters and the id contains only the characters 'a-z','-','0-9'. This unique id can e.g. be used for file names etc.

#### Returns

`string`

String containing the unique id

#### Since

ELC 3.60 / otrisPORTAL 6.0

#### Example

```ts
var uniqueId = util.getUniqueId();
util.out(uniqueId);
```

***

### getUsedPrivateBytes()

> **getUsedPrivateBytes**(): `number`

**Returns the current usage of private bytes memory of the documensserver process.**

#### Returns

`number`

integer value with the used memory in KBytes

#### Since

DOCUMENTS 5.0b

***

### hash()

> **hash**(`filePath`, `hashfunction`): `string`

**Generate the hash value for a file using the given hash function.**  

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

##### filePath

`string`

String containing the path of the file to be hashed.

##### hashfunction

`string`

String containing the name of the hash function.

#### Returns

`string`

String with the hash value of the file, an empty string in case of any error.

#### Since

DOCUMENTS 5.0e

#### See

[Document.hash](Document.md#hash)

#### Example

```ts
try
{
  var hashValue = util.hash("c:/tmp/dok1.pdf", "sha256");
  util.out(hashValue);
}
catch (ex)
{
  util.out(ex);
}
```

***

### hmac()

> **hmac**(`hashfunction`, `key`, `message`, `rawOutput?`): `string`

**Generates a hash-based message authentication code (hmac) of a message string using a secret key.**  

These hash functions are supported: 

+ `"sha1"`
+ `"sha224"`
+ `"sha256"`
+ `"sha384"` 
+ `"sha512"` 
+ `"md4"` 
+ `"md5"`

#### Parameters

##### hashfunction

`string`

Name of the hash function.

##### key

`string`

Secret key.

##### message

`string`

Message string to be hashed.

##### rawOutput?

`Boolean`

Optional flag:   
If set to `true`, the function outputs the raw binary representation of the hmac.   
If set to `false`, the function outputs the hexadecimal representation of the hmac.   

**Default:** `false`

#### Returns

`string`

String containing the hash-based message authentication code (hmac) of the message (see rawOutput for representation).

#### Since

DOCUMENTS 5.0a HF2

#### Example

```ts
var key = "MySecretKey";
var msg = "Hello world!";
var hmac = util.hmac("sha1", key, msg);
util.out(hmac);
```

***

### htmlToText()

> **htmlToText**(`value`): `string`

Removes the HTML tags from a string.

#### Parameters

##### value

`string`

HTML text to be converted.

#### Returns

`string`

Input with HTML tags removed or error message
  (starting with "ERROR:")

#### Remarks

Requires that the text browser links (`server/../addon/links` on windows OS) is available and can be
executed by the application. If it is not available in the
PATH environment variable, the direct path can be set with
[setLinksPath](#setlinkspath).

This function is <b>only</b> available on the server.

#### Throws

Invalid value for the argument

#### Since

DOCUMENTS 6.1.2

#### See

[setLinksPath](#setlinkspath)

#### Example

```ts
context.returnValue = util.htmlToText("<p>Hello world!</p>");
// Hello world!
```

***

### initializeAdminPassword()

> **initializeAdminPassword**(`password`, `force`): `boolean`

Sets the password for the admin user if it is empty.

#### Parameters

##### password

`string`

##### force

`false`

Set password even if it is already set

#### Returns

`boolean`

true if password initialised, false if password already set or error occurred

***

### isEncryptedBlob()

> **isEncryptedBlob**(`blobFilePath`): `boolean`

**Checks, if the current blob is encrypted (Repository encryption) or not.**

#### Parameters

##### blobFilePath

`string`

String containing the path of the file to be checked.

#### Returns

`boolean`

`true`, if the blob is encrypted.

#### Since

DOCUMENTS 4.0d HF3

***

### isWindowsOS()

> **isWindowsOS**(): `boolean`

**Returns true, if the OS is a windows system.**

#### Returns

`boolean`

`true`, if the server runs on windows, `false` if the server runs on linux

#### Since

DOCUMENTS 5.0f

***

### ~~length\_u()~~

> **length\_u**(`value`): `number`

**Returns the number of characters of a UTF-8 string.**  

You can use this function in a x64 / UTF-8 server to count the characters in a UTF-8 string.  

**Note:** for use in x64 / UTF-8 versions

#### Parameters

##### value

`string`

UTF-8 String of which the number of characters will be counted

#### Returns

`number`

Integer with the length in characters

#### Since

DOCUMENTS 4.0a HF1

#### Deprecated

since DOCUMENTS 6.0 - Use `String.length` instead

#### Example

```ts
var text = "Köln is a german city";
util.out(text.length);          // => 22 bytes in DOCUMENTS 5 or older
util.out(util.length_u(text));  // => 21 characters
```

***

### log()

> **log**(`output`): `any`

**Log a String to the DOCUMENTS server window.**  

Same as util.out() with additional debugging information (script name and line number) You may output whatever information you want. 
This function is useful especially for debugging purposes. Be aware that you should run the Portalserver as an application if you want 
to make use of the `out()` function, otherwise the output is stored in the Windows Eventlog instead.

#### Parameters

##### output

`string`

String you want to output to the Portalserver Window

#### Returns

`any`

#### Since

ELC 3.50e / otrisPORTAL 5.0e

#### Example

```ts
util.log("Hello World");
```

***

### makeFullDir()

> **makeFullDir**(`dirPath`): `string`

**Creates a directory with subdirectories at the PortalServer's file system.**  

This functions provides a simple method for directory creation on the file system.

#### Parameters

##### dirPath

`string`

String with the directory path

#### Returns

`string`

empty String if successful, the error message in case of any error

#### Since

ELC 3.60e / otrisPORTAL 6.0e

#### Example

```ts
var errMsg = util.makeFullDir("c:\\log\\ELC");
if (errMsg.length > 0)
    util.out(errMsg);
else
    util.out("Ok.");
```

***

### makeGACLValue()

> **makeGACLValue**(`val1`, `val2`, ...`restParams`): `string`

**Makes a valid GACL value from the parameters.**  

This method helps to create valid GACL values when set by PortalScripting. As separator for the single GACL values a `\r\n` (`%CRLF%`) will be used. 
The values will be trimed (leading and ending whitespaces) and multiple values will be removed. The method returns a String value 
in the format `\r\n` AP1 `\r\n` AP2 `\r\n` .... `\r\n` APx `\r\n`

#### Parameters

##### val1

`any`

String or Array

##### val2

`any`

String or Array

##### restParams

...`any`[]

#### Returns

`string`

String containing the GACL value.

#### Since

DOCUMENTS 5.0c HF2

#### Example

```ts
var sep = context.getAutoText("%CRLF%");    // \r\n
var val1 = ["AP1", "AP2"];
var val2 = "AP3" + sep + "AP4";
var val3 = " AP5";
var val4 = "AP3";
var gaclVal = util.makeGACLValue(val1, val2, val3, val4);
util.out(gaclVal);
=>
AP1
AP2
AP3
AP4
AP5
<=
```

***

### makeHTML()

> **makeHTML**(`val`, `isUTF8?`): `string`

**Masks all HTML-elements of a String.**  

This function masks the following characters for HTML output:

| `>`  | &gt;    |
|------|---------|
| `<`  | &lt;    |
| `\n` |         |
| `&`  | &amp;   |
| `"`  | &quot;  |

If the String is in UTF-8 Format, all UTF-8 characters will be replaced with the according HTML entities.

#### Parameters

##### val

`string`

String to be masked

##### isUTF8?

`boolean`

boolean flag, if the val is in UTF-8 format  

**Default:** `false`

#### Returns

`string`

HTML-String

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### out()

> **out**(`output`): `any`

**Output a String to the Portalserver window.**  

You may output whatever information you want. This function is useful especially for debugging purposes. Be aware that you should run the Portalserver 
as an application if you want to make use of the `out()` function, otherwise the output is stored in the Windows Eventlog instead.  
Since DOCUMENTS 6.2.0, the script user is output in the form `suid=<login>` if the "documents.ini" contains the setting `LogFmt true`.

#### Parameters

##### output

`string`

String you want to output to the Portalserver Window

#### Returns

`any`

#### Since

ELC 3.50e / otrisPORTAL 5.0e

#### Example

```ts
util.out("Hello World");
```

***

### prepareJSON()

> **prepareJSON**(`jsonString`): `string`

**Converts JSON-Strings with Source Code entities, e.g. \u00FA to UTF-8 Strings representation.**

#### Parameters

##### jsonString

`string`

String with the JSON content to be converted.

#### Returns

`string`

String with UTF-8 representation

#### Since

DOCUMENTS 5.0e HF2

***

### readBinaryFileAsBase64()

> **readBinaryFileAsBase64**(`path`): `string`

**Reads a binary file from the file system and returns it's data as a string in base64 format.**

#### Parameters

##### path

`string`

Path to the binary file in the file system

#### Returns

`string`

Base64 string with data of the binary file; empty string in case of errors

#### Since

DOCUMENTS 6.0.2

#### See

[util.writeBase64ToBinaryFile](#writebase64tobinaryfile)

***

### readTextFileAsString()

> **readTextFileAsString**(`pathToTextFile`, `encoding?`): `string`

**Reads a text file (e.g. html, json... ) from the file system and returns it's content as a string.**

#### Parameters

##### pathToTextFile

`string`

##### encoding?

`string`

The following encodings are supported: 

+ `UTF-8`: Unicode-characterset as ASCII-compatible 8-Bit-coding. 
+ `ISO-8859-1`: West-European characterset without Euro-Symbol. 
+ `ISO-8859-15`: West-European characterset with Euro-Symbol.
+ `Windows-1252`
+ `Windows-1250`

#### Returns

`string`

String with content of the text file; empty string in case of errors

#### Since

DOCUMENTS 5.0f

#### Since

DOCUMENTS 6.0.1 parameter encoding

#### See

[util.writeStringToTextFile](#writestringtotextfile)

***

### removeCtrlCharacters()

> **removeCtrlCharacters**(`inputString`): `string`

**Removes control characters in String.**
Following control characters are not removed:

+ `TAB`: Horizontal tab character
+ `CR`: Carriage return
+ `LF`: Line feed

#### Parameters

##### inputString

`string`

#### Returns

`string`

Input string without control characters.

#### Since

DOCUMENTS 5.0i HF10

***

### runPDFTool()

> **runPDFTool**(`command`, `inPdf`, `outPdf`, `jsonData`, `addParam1?`, `addParamN?`): `string`[]

**Executes the otrPdfTool.**  

Executes the pdf-Tool, that has to be definded in the documents.ini: $otrPdfTool

#### Parameters

##### command

`string`

String containing command for the tool

##### inPdf

`string`

String containing the path to source pdf to work with

##### outPdf

`string`

String containing the path for the target pdf

##### jsonData

`string`

String jsonString with additional data for the tool

##### addParam1?

`string`

String Additional param for the tool

##### addParamN?

`string`

String Additional param for the tool

#### Returns

`string`[]

a string array with the exit code and the content of the standard output

#### Since

DOCUMENTS 5.0h HF1

#### Example

```ts
const command = "pdfoverlay";
const sourcePdf = "c:\\tmp\\source.pdf";
const targetPdf = "c:\\tmp\\target.pdf";
var data = [{ type: "text", text: "Hello World", size: 16, x: 10, y: 10, invertY: true, page: 0 }];
var res = util.runPDFTool(command, sourcePdf, targetPdf, JSON.stringify(data));
var exitcode = res[0];
if (exitcode !== "0")
  throw "Executing the otrPdfTool failed: " + exitcode;
```

***

### searchInArray()

> **searchInArray**(`theArray`, `searchedString`, `occurence?`): `number`

**Search for a String in an Array.**  

This functions provides a simple search method for Arrays to find the position of a string in an array.

#### Parameters

##### theArray

`any`[]

Array in that the String will be searched

##### searchedString

`string`

String that will be searched

##### occurence?

`number`

Integer that define the wanted position at a multi-occurence of the String in the Array  

**Default:** `1`

#### Returns

`number`

Integer with the position of the String in the array, -1 in case of the String isn't found

#### Since

ELC 3.60e / otrisPORTAL 6.0e

#### Example

```ts
enumval[0] = "This";
enumval[1] = "is";
enumval[2] = "a";
enumval[3] = "sample";
var pos = util.searchInArray(enumval, "is");
util.out(pos);  // should be the value 1
```

***

### setLinksPath()

> **setLinksPath**(`value`): `void`

Sets the path to links browser used by [htmlToText](#htmltotext).

#### Parameters

##### value

`string`

Path to links or empty string to use links available
  in the PATH environment variable, which is the default.

#### Returns

`void`

#### Remarks

This function is <b>only</b> available on the server.

#### Throws

Invalid value for the argument

#### See

[htmlToText](#htmltotext)

#### Since

DOCUMENTS 6.1.2

#### Example

```ts
util.setLinksPath(util.getServerPath() + "/../addon/links");
context.returnValue = util.htmlToText("<p>Hello world!</p>");
```

***

### sha256()

> **sha256**(`message`): `string`

**Generates the SHA256 hash of any string.**

#### Parameters

##### message

`string`

Message string to be hashed.

#### Returns

`string`

SHA256 hash of the message.

#### Since

DOCUMENTS 5.0a HF2

***

### sign()

> **sign**(`algorithm`, `privateKeyPEM`, `pkPassword`, `payload`, `urlStyle?`): `string`

**Create a digital signature.**  

**Note:** Signing strings with characters, which are not in the 7-Bit ASCII-Charset, may require a transcoded string. 
This depends on how the string was created or received. See transcode(). The list of available hash algorithms depends 
on the linked OpenSSL libraries, not on DOCUMENTS itself. About Arraybuffers Passing a TypedArray (UInt8Array, Int16Array etc.) 
instead of an ArrayBuffer is possible, but not recommended. The actual implementation always sends the complete associated buffer. 
The result can be unexpected, if the TypedArray covers only a section of a bigger buffer. This behaviour might change in future releases.

#### Parameters

##### algorithm

`string`

string Short identification of used algorithms, for example "RSASHA256". The first three characters specify 
an encryption standard. Actually only "RSA" is supported. The other characters select a hash algorithm, for example SHA1, SHA256.

##### privateKeyPEM

`string`

string with a (usually encrypted) private key in PEM format.

##### pkPassword

`string`

string The password to decrypt the private key.

##### payload

`any`

The text or data to sign. Allowed data types are "String", "Array of Bytes (Integer 0..255)" and "ArrayBuffer".

##### urlStyle?

`boolean`

boolean to request the result Base64URL-encoded  

**Default:** `false`

#### Returns

`string`

Base64- or Base64URL-encoded string with signature data.

#### Since

DOCUMENTS 5.0d HF2

#### Example

```ts
// Load a private key in PEM-Format for digital signing.
// The file should look like this:
// -----BEGIN ENCRYPTED PRIVATE KEY-----
// <Base64-encoded binary data; usually 64 Characters per line>
// -----END ENCRYPTED PRIVATE KEY-----
//
// The openssl command-line tool, for instance, can be used in the
// following way to generate a private key-file for RSA enccryption.
// > openssl.exe genpkey -out testPK.pem -outform PEM -pass pass:myKeyPassword -des3 -algorithm RSA -pkeyopt rsa_keygen_bits:2048
// The next command extracts the public parts of the key and stores
// them in a separate PEM-file. A signature validator will require it.
// > openssl pkey -in testPK.pem -passin pass:myKeyPassword -out testPub.pem -pubout
function loadMyPrivateKey()
{
var f = new File("E:\\testPK.pem");
var text;
if(f.ok())
{
var text = f.read(10000);
f.close();
return text;
}
throw new Error("Keyfile not found");
}
function signMyData() {
var results = {};
var privateKey = loadMyPrivateKey();
var pkPassword = "myKeyPassword";
// 1) Sign a string.
var data = "This message needs to be signed.";
results.data1 = data;
results.signature1 = util.sign("RSASHA256", privateKey, pkPassword, data);
// 2) Sign a sequence of bytes, passed as a conventional array.
// Use the simpler SHA1 hash this time.
data = [65, 70, 70, 69, 0];
results.data2 = data;
results.signature2 = util.sign("RSASHA1", privateKey, pkPassword, data);
// 3) Sign a sequence of bytes, passes as an ArrayBuffer
data = new Uint8Array(4);
data[0] = 192;
data[1] = 168;
data[2] = 6;
data[3] = 101;
results.data3 = data;
results.signature3 = results.signature1 = util.sign("RSASHA256", privateKey, pkPassword, data.buffer);
return JSON.stringify(results);
}
return signMyData();
```

***

### sleep()

> **sleep**(`duration`): `void`

**Let the PortalScript sleep for a defined duration.**

#### Parameters

##### duration

`number`

Integer containing the duration in milliseconds

#### Returns

`void`

#### Since

DOCUMENTS 5.0a

***

### ~~substr\_u()~~

> **substr\_u**(`value`, `startIndex`, `length`): `string`

**Returns a substring of a UTF-8 string.**  

You can use this function in a x64 / UTF-8 server to get a substring of a UTF-8 string.  

**Note:** for use in x64 / UTF-8 versions

#### Parameters

##### value

`string`

UTF-8 String of which the substring is wanted

##### startIndex

`number`

int with the 0-based start index of the substring

##### length

`number`

int with the length in characters of the substring

#### Returns

`string`

UTF-8 String with the wanted substring

#### Since

DOCUMENTS 4.0a HF1

#### Deprecated

since DOCUMENTS 6.0 - Use `String.slice()` instead

#### Example

```ts
var text = "Köln is a german city";
util.out(util.substr_u(text, 0, 4));   // => Köln
util.out(util.substr_u(text, 5));      // => is a german city
// but
util.out(text.substr(0, 4));      // => Köl (in DOCUMENTS 5 or older)
```

***

### transcode()

> **transcode**(`nameSourceEncoding`, `text`, `nameTargetEncoding`): `string`

**Transcode a String from encoding a to encoding b.**  

This method performs an transcoding for a String from a source encoding to a target encoding. The following encodings are supported: 
 
+ `Local`: The standard system encoding for Windows systems is `Windows-1252` and for Linux systems `ISO-8859-1` or `UTF-8`.
+ `UTF-8`: Unicode-characterset as ASCII-compatible 8-Bit-coding. 
+ `ISO-8859-1`: West-European characterset without Euro-Symbol. 
+ `ISO-8859-15`: West-European characterset with Euro-Symbol.
+ `Windows-1252`
+ `Windows-1250`

#### Parameters

##### nameSourceEncoding

`string`

String containing the name of the source encoding

##### text

`string`

String containing the text to transcode

##### nameTargetEncoding

`string`

String containing the name of the target encoding

#### Returns

`string`

String containing the transcoded text

#### Since

ELC 3.60d / otrisPORTAL 6.0d

#### Example

```ts
var text = "Köln is a german city"
var utf8Text = util.transcode("windows-1252", text, "UTF-8");
util.out(utf8Text);
text = util.transcode("UTF-8", utf8Text, "windows-1252");
util.out(text);
```

***

### unlinkFile()

> **unlinkFile**(`filePath`): `boolean`

**Delete a physical file on the server's file system.**

#### Parameters

##### filePath

`string`

String containing the full path and filename to the desired physical file

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.51 / otrisPORTAL 5.1

#### Example

```ts
var success = util.unlinkFile("c:\\tmp\\tempfile.txt");
```

***

### verify()

> **verify**(`algorithm`, `publicKey`, `payload`, `signature`, `urlStyle?`): `boolean`

**Verify a digital signature.**
**Note:** The data in the publicKey parameter is assumed to be trustworthy.
No extra vallidation occurs, if the parameter contains (of includes) a certificate.

#### Parameters

##### algorithm

`string`

Short identification of used algorithms, for example "RSASHA256". The first three characters specify an encryption standard. 
Actually only "RSA" is supported. The other characters select a hash algorithm, for example SHA1, SHA256.

##### publicKey

`string`

The signer's public key or certificate, either in PEM format or in JWK format.

##### payload

`any`

The signed text or data. Allowed data types are "String", "Array of Bytes (Integer 0..255)" and "ArrayBuffer".

##### signature

`string`

The Base64- or Base64URL-encoded signature to verify

##### urlStyle?

`boolean`

Indicator, whether the passed signature is Base64URL-encoded.
**Default:** `false`

#### Returns

`boolean`

The return value indicates whether the passed signature matches the passed data and key.

#### Since

DOCUMENTS 6.0.1

***

### writeBase64ToBinaryFile()

> **writeBase64ToBinaryFile**(`path`, `base64String`): `boolean`

**Writes a base64 string to a binary file in the file system.**

#### Parameters

##### path

`string`

Path to the file

##### base64String

`string`

The base64 string to be written to the file

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 6.0.2

#### See

[util.readBinaryFileAsBase64](#readbinaryfileasbase64)

***

### writeStringToTextFile()

> **writeStringToTextFile**(`pathToTextFile`, `content`, `encoding?`): `boolean`

**Writes a string as a text file to file system.**

#### Parameters

##### pathToTextFile

`string`

##### content

`string`

##### encoding?

`string`

The following encodings are supported: 

+ `UTF-8`: Unicode-characterset as ASCII-compatible 8-Bit-coding.
+ `ISO-8859-1`: West-European characterset without Euro-Symbol.
+ `ISO-8859-15`: West-European characterset with Euro-Symbol. 
+ `Windows-1252` 
+ `Windows-1250`

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0f

#### Since

DOCUMENTS 6.0.1 parameter encoding

#### See

[util.readTextFileAsString](#readtextfileasstring)

## JSON-Mode Constants

These constants build an enumeration of the possible values for the [Docfile.asJSON()](DocFile.md#asjson) method.  
**Since** DOCUMENTS 5.0f

### JSON\_LABEL

> **JSON\_LABEL**: `number`

***

### JSON\_LOCALE

> **JSON\_LOCALE**: `number`

***

### JSON\_RAW

> **JSON\_RAW**: `number`
