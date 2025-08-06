[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / DOMParser

# Class: DOMParser

This class provides basic methods to parse or synthesize XML documents using the Document Object Model (DOM).

## See

[XML-DOM Example](../xml-dom.html)

## Since

DOCUMENTS 4.0c

## Properties

### loadExternalDTD

> **loadExternalDTD**: `boolean`

**Control flag to enable or disable DTD loading.**  

If an input document contains a doctype declaration which refers an external DTD, the parser by default attempts to load and parse the DTD 
(and possibly further files referenced from there). Setting this flag to `false` disables the parsing of external declarations.  

**Note:** In some cases this flag can prevent a deadlock. See the note at [parse()](#parse).

#### Since

DOCUMENTS 5.0f

## Methods

### getDocument()

> **getDocument**(): [`DOMDocument`](DOMDocument.md)

**This returns the root of the DOM tree after a successful call of [parse()](#parse), otherwise `null`.**

#### Returns

[`DOMDocument`](DOMDocument.md)

***

### getLastError()

> **getLastError**(): `string`

**This returns the text of the last occurred error.**

#### Returns

`string`

***

### parse()

> **parse**(`xml`, `fromFile`): `number`

**Parse an XML document, either from a String or from a local file.**  

**Note:** On success, call [getDocument()](#getdocument) to access the DOM tree. On error use [getLastError()](#getlasterror) to obtain an error text. 
The encapsulated native DOM library supports the following character encodings: ASCII, UTF-8, UTF-16, UCS4, EBCDIC code pages IBM037, 
IBM1047 and IBM1140, ISO-8859-1 (aka Latin1) and Windows-1252. (no guarantee)   

**Note:** When parsing a doctype declaration with an URL-style systemId such as "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd" 
the parser usually attempts to download the referenced definition file and all depedencies. Some public servers ignore these requests 
in a way, which makes parse() wait forever. Unfortunately there is no timeout option. There are two ways to solve this problem. 
<ul> 
<li>Prepare a file system folder with local copies of the needed DTD files. Pre-process the document externally to replace the standard URLs with local "file://..." URLs. </li> 
<li>Before calling parse(), disable the downloads with the loadExternalDTD property.</li> 
</ul>

#### Parameters

##### xml

`string`

Either the XML itself or the path and file name of a local file

##### fromFile

`boolean`

`true` to parse a local file, otherwise `false`.

#### Returns

`number`

An integer, which describes an error category. See [ErrCatNone](#errcatnone) and further constants.

#### Since

DOCUMENTS 4.0c

***

### write()

> **write**(`node`, `path`, `encoding`, `prettyPrint`): `any`

**Build an XML document from a DOM tree.**  

**Note:** Saving to a local file is not supported on all platforms. If a script tries it while the version of the native DOM library is too old, 
the method just throws a JavaScript error.  

**Note:** To obtain an error message use `getLastError()`. When the message is just "NULL pointer", the native DOM library may have failed to open 
the output file for writing. When the method writes to a string, the encoding is always the server application's internal encoding. 
The encapsulated native DOM library supports the following character encodings: ASCII, UTF-8, UTF-16, UCS4, EBCDIC code pages IBM037, IBM1047 and 
IBM1140, ISO-8859-1 (aka Latin1) and Windows-1252. (no guarantee)  
  
**Since:** Parameter prettyPrint since DOCUMENTS 5.0b HF3

#### Parameters

##### node

[`DOMNode`](../interfaces/DOMNode.md)

The root node to build the document from. Though the interface accepts any DOMNode, only a DOMDocument should be passed. 
Otherwise the output may be a fragment which is not a valid XML.

##### path

`string`

Optional path and filename to save the XML in the local file system.

##### encoding

`string`

Optional encoding specification for the file. Only used when <em>path</em> is also specified.

##### prettyPrint

`boolean`

Optional boolean value.

#### Returns

`any`

The return type depends on the parameters. After saving to a local file, the method returns a boolean value, 
which indicates the success of the operation. Otherwise the return value is a String with the XML itself, or an empty string after an error.

#### Since

DOCUMENTS 4.0c

## Constructors

### Constructor

> **new DOMParser**(): `DOMParser`

**The constructor actually takes no arguments.**

#### Returns

`DOMParser`

#### Since

DOCUMENTS 4.0c

## Error Constants

In contrast to many other methods of the DOM API, the [parse()](#parse) method does not forward exceptions of the native parser to the calling script. 
It rather stores the error text in a buffer, which the script can read with [getLastError()](#getlasterror). The return value signals the type of the exception, 
which equals one of these constants. The constants are also properties of the constructor, so it is possible to read them in the style 
`DOMParser.ErrCatDOM`.

### ErrCatDOM

> **ErrCatDOM**: `number`

This constant represents a caught exception of the type "DOMException".

***

### ErrCatEnv

> **ErrCatEnv**: `number`

This constant represents errors detected by interface code outside the native parser.

***

### ErrCatNone

> **ErrCatNone**: `number`

This constant with the value zero indicates "no error".

***

### ErrCatSAX

> **ErrCatSAX**: `number`

This constant represents a caught exception of the type "SAXException".

***

### ErrCatXML

> **ErrCatXML**: `number`

This constant represents a caught exception of the type "XMLException".
