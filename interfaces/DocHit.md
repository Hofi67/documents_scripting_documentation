[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / DocHit

# Interface: DocHit

**The DocHit class presents the hit object collected by a HitResultset.**  

Objects of this class cannot be created directly. You may access a single DocHit by creating a HitResultset, 
which provides functions to retrieve its hit entries.

## Since

DOCUMENTS 4.0b

## See

[HitResultset.first](../classes/HitResultset.md#first)   
[HitResultset.getAt](../classes/HitResultset.md#getat)

## Example

```ts
var searchResource = "Standard";
var filter = "";
var sortOrder = "";
var myFile;
var myHRS = new HitResultset(searchResource, filter, sortOrder);
for (var myHit = myHRS.first(); myHit; myHit = myHRS.next())
{
    if (myHit.isArchiveHit())
        myFile = myHit.getArchiveFile();
    else
        myFile = myHit.getFile();
    if (myFile)
        util.out(myFile.getAutoText("title"));
    else
        util.out(myHit.getLastError());
}
```

## Properties

### columnName

> **columnName**: `any`

**Field value, addressed by a known column name.**  

Each field in a DocHit is mapped to an according property. You can read the value on the basis of the column name.  

**Note:** Overwriting values in a DocHit is not allowed. Each attempt will raise an exception. 
To read dates and numbers in DOCUMENTS' storage format, see getTechValueByName().

#### Since

DOCUMENTS 5.0HF2

#### Example

```ts
function logValue(label, value)
{
  util.out(label +" [" +  typeof(value) + "] "  + value);
}
var HRS = new HitResultset("ftOrder", "", "", "HL2");
var hitline = HRS.first();
if(hitline)
{
  // We assume, "ftOrder" has got a string field "company", a
  // date field "orderDate" and a numeric field "netPrice".
  var checkVal = hitline.company;
  logValue("company: ", checkVal);
  checkVal = hitline.orderDate;
  logValue("orderDate: ", checkVal);
  // The next example shows a different way to read "hitline.netPrice".
  // This style is necessary, if the name of a column contains
  // critical characters, or if the name equals a reserved JavaScript keyword.
  checkVal = hitline["netPrice"];
  logValue("orderDate: ", checkVal);
  // Columns can also be addressed by number (0..n-1)
  checkVal = hitline[0];
  logValue("first column: ", checkVal);
}
```

***

### RELOAD\_MISMATCH

> `readonly` **RELOAD\_MISMATCH**: `number`

This constant defines one of the possible return values of DocHit.reload().
 These constants are equally available in each instance of DocHit and in the constructor object.
 `RELOAD_MISMATCH` means the DocHit has been updated, but a new HitResultset with the same parameters 
 would not contain this hit, either because the hit does no longer match the filter expression
 or due to modified dynamic permissions (ACL, GACL or classic file class protection).
 `RELOAD_MISMATCH` can only occur, if the retestFilters parameter has been `true`.

***

### RELOAD\_NO\_FILE

> `readonly` **RELOAD\_NO\_FILE**: `number`

This constant defines one of the possible return values of DocHit.reload().
 These constants are equally available in each instance of DocHit and in the constructor object.
 `RELOAD_NO_FILE` indicates a failed update. The DocFile behind the DocHit is no longer available.
 reload() may return this value also when a server shutdown has begun.

***

### RELOAD\_OK

> `readonly` **RELOAD\_OK**: `number`

This constant defines one of the possible return values of DocHit.reload().
 These constants are equally available in each instance of DocHit and in the constructor object.
 `RELOAD_OK` indicates a successful update of the DocHit or an empty operation
 in the case of an archive hit.

## Methods

### asJSON()

> **asJSON**(): `string`

**`Internal`**

**Create a JSON representation of the contained fields.**  

This function is for internal use only!

#### Returns

`string`

#### Since

DOCUMENTS 5.0HF2

***

### getArchiveFile()

> **getArchiveFile**(): [`DocFile`](DocFile.md)

**Get a file from the archive associated to the archive hit.**  

You need the necessary access rights on the archive side.  

**Note:** This function creates a complete DOCUMENTS image of the archived file, except for the content of attachments. 
This is a time-consuming workstep. If a script calls this function for each hit in the set, it will not run any faster than a script, 
which uses a conventional ArchiveFileResultset instead of this class.

#### Returns

[`DocFile`](DocFile.md)

`DocFile` or `null`, if failed.

#### Since

DOCUMENTS 4.0b

#### See

[getFile](#getfile)

***

### getArchiveKey()

> **getArchiveKey**(`withServer?`): `string`

**Retrieve the key of the associated archive file object.**

#### Parameters

##### withServer?

`boolean`

optional boolean value to indicate, if the key should include an "@archiveServerName" appendix  
**Default:** `true`

#### Returns

`string`

The archive file's key as a String, but an empty String, if the hit does not refer to an archive file.

#### Since

DOCUMENTS 4.0b

#### See

[getFileId](#getfileid)

***

### getBlobInfo()

> **getBlobInfo**(): `string`

**Function to get the blob info of the hit as xml.**

#### Returns

`string`

String with xml content

#### Since

DOCUMENTS 5.0c

***

### getFile()

> **getFile**(): [`DocFile`](DocFile.md)

**Get the file associated to the hit.**  

If the file does not exist or the user in whose context the script is executed is not allowed to access the file, then the return value will be `null`.

#### Returns

[`DocFile`](DocFile.md)

`DocFile` or `null`, if failed.

#### Since

DOCUMENTS 4.0b

#### See

[getArchiveFile](#getarchivefile)

***

### getFileId()

> **getFileId**(): `string`

**Get the file id of the associated file object.**

#### Returns

`string`

The file id as String, if the associated file is an active file, but an empty String otherwise.

#### Since

DOCUMENTS 4.0b

#### See

[getArchiveKey](#getarchivekey)

***

### getLastError()

> **getLastError**(): `string`

**Function to get the description of the last error that occurred.**

#### Returns

`string`

Text of the last error as String

#### Since

DOCUMENTS 4.0b

***

### getLocalValue()

> **getLocalValue**(`colIndex`): `string`

**Get the local value of an available column.**

#### Parameters

##### colIndex

`number`

The zero-based index of the column.

#### Returns

`string`

The local value of the given column as String.

#### Since

DOCUMENTS 4.0b

#### See

[getLocalValueByName](#getlocalvaluebyname)

***

### getLocalValueByName()

> **getLocalValueByName**(`colName`): `string`

**Get the local value of an available column.**  

**Note:** Accesing a column by its index is a bit faster than by its name.

#### Parameters

##### colName

`string`

The name of the column.

#### Returns

`string`

The local value of the given column as String.

#### Since

DOCUMENTS 4.0b

#### See

[getLocalValue](#getlocalvalue)

***

### getSchema()

> **getSchema**(): `string`

**Get a schema identifier of the archive hit.**  

**Note:** For EE.i, the value is an archive identifier in the XML-Server's notation. For EDA it is just the name of a filetype.
 All values come with an "@Servername" appendix.

#### Returns

`string`

The schema identifier as a String.

#### Since

DOCUMENTS 4.0b

***

### getTechValue()

> **getTechValue**(`colIndex`): `string`

**Get the technical value of an available column.**  

**Note:** The function returns dates, timestamps and numbers in DOCUMENTS' storage format. 
(In the DOCUMENTS Manager see menu 'Documents/Settings', dialog page 'Locale/format', group 'Format settings'.) 
If you prefer JavaScript numbers and dates, simply use the object like an array: myDocHit[colIndex].

#### Parameters

##### colIndex

`number`

The zero-based index of the column.

#### Returns

`string`

The technical value of the given column as a String.

#### Since

DOCUMENTS 4.0b

#### See

[getTechValueByName](#gettechvaluebyname)

***

### getTechValueByName()

> **getTechValueByName**(`colName`): `string`

**Get the technical value of an available column.**  

**Note:** Accessing a column by its index is a bit faster than by its name.  

**Note:** The function returns dates, timestamps and numbers in DOCUMENTS' storage format. 
(In the DOCUMENTS Manager see menu 'Documents/Settings', dialog page 'Locale/format', group 'Format settings'.) 
If you prefer JavaScript numbers and dates, you can simply read the columns as a property [DocHit.columnName](#columnname).

#### Parameters

##### colName

`string`

The name of the column.

#### Returns

`string`

The technical value of the given column as String.

#### Since

DOCUMENTS 4.0b

#### See

[getTechValue](#gettechvalue)  
[DocHit.columnName](#columnname)

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

### isArchiveHit()

> **isArchiveHit**(): `boolean`

**Function to test whether the associated file is an archive file.**

#### Returns

`boolean`

`true`, if the associated file is an archive file, `false` otherwise.

#### Since

DOCUMENTS 4.0b

***

### reload()

> **reload**(`retestFilters`): `number`

**Load updated values into the DocHit.**
The values in a DocHit usually refer to the time at which the
HitResultset was created, or at which the current page of hits
was loaded. If the DocHit is not an archive hit, this function loads
the actual values of the DocFile into this DocHit.

#### Parameters

##### retestFilters

`boolean`

Indicator, whether the function shall verify the
validity of the DocHit with respect to the HitResultset's filter and dynamic permissions
such as GACLs.

#### Returns

`number`

One of the `RELOAD_` integer constants, which are equally defined on the constructor
and the prototype of this class.

#### Since

DOCUMENTS 6.1.0

#### Note

The retestFilters option can cost an extra database access, but it is the best
way to detect outdated hits, which should no longer be presented to a user.
A return value of `RELOAD_MISMATCH` instead of `RELOAD_OK` marks such hits.

For archive hits this function does nothing and returns always `RELOAD_OK`.

#### See

[DocHit.RELOAD\_OK](#reload_ok), [DocHit.RELOAD\_NO\_FILE](#reload_no_file), [DocHit.RELOAD\_MISMATCH](#reload_mismatch)
