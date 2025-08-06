[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / HitResultset

# Class: HitResultset

The HitResultset class allows comprehensive search operations in Documents and in connected archives.  

While the constructor of this class launches a search operation, the created object stores the results
and exposes them as a list of DocHit objects. Compared with the classes `FileResultset` and `ArchiveFileResultset`
this class has got the following characteristics.

+ Several filetypes and archives can be searched at one time.
+ Extracting archive hits from a HitResultset does not make DOCUMENTS create a temporary DocFile for each hit.
  This can save a lot of time.
+ Objects of this class may allocate large amounts of memory, because they sustain a complete hit list instead
  of a lean id-list. To save memory, scripts should prefer hit lists with as few columns as possible.
+ Search-related errors and warnings do not trigger exceptions. Instead, they are stored inside the object.
  You can access them with `getLastErrorCode()` and `getLastError()` respectively. Advantage: The caller gets
  the freedom to process the results also after a warning. In this case the hit list maybe incomplete or unsorted.

## Properties

### beginningOfLeanView

> **beginningOfLeanView**: `number`

**`Internal`**

* ***

#### Since

DOCUMENTS 5.0i

***

### searchability

> `readonly` **searchability**: `number`

**Searchability indicator for folder-based or register-based HitResultsets.**  

For objects created by `Folder.getHitResultset()` or `Register.getHitResultset()` without a fulltextFilter parameter this property provides a hint, 
if the same operation can succeed with a non-empty fulltext filter. For other HitResultsets it is not meaningful.   
Possible values: 
<ul> 
<li> 0 = The folder/register is not capable of fulltext searching.</li> 
<li> 1 = The folder/register technically supports fulltext searching. User interfaces, however, 
     should hide or disable corresponding input fields due to the actual DOCUMENTS-settings.</li> 
<li>3 = The folder/register is ready for fulltext searching.</li> 
</ul>

**Note:** The value can be interpreted as a bitmask, where Bit 0 indicates technical searchability and Bit 1 indicates UI-driven searchability.

#### Since

DOCUMENTS 5.0f

#### See

[Folder.getHitResultset](../interfaces/Folder.md#gethitresultset)

## Methods

### dispose()

> **dispose**(): `any`

**Free most of the memory of the HitResultset.**  

This function explicitly frees the memory used by the object. The Resultset itself becomes empty. All extracted DocHit objects become 
invalid and must no longer be used. Long-running scripts should use this function instead of waiting for the garbage collector to clean up.

#### Returns

`any`

The function does not return a value.

#### Since

DOCUMENTS 4.0b

***

### fetchedSize()

> **fetchedSize**(): `number`

**Get the number of already loaded hits in the set.**  

**Note:** If the object has been created with a non-zero page size, this value is often smaller than the total amount of hits.

#### Returns

`number`

integer value with the number of hits, which can actually be read from the resultset.

#### Since

DOCUMENTS 4.0b

#### See

[size](#size)

***

### fetchNextPage()

> **fetchNextPage**(): `boolean`

**Load the next page of hits into the Resultset.**  

If the object has been created with a non-zero page size, each call of this function appends another page of hits to the resultset until all hits are loaded.

#### Returns

`boolean`

The value indicates, if any more hits have been loaded.

#### Since

DOCUMENTS 4.0b

***

### first()

> **first**(): [`DocHit`](../interfaces/DocHit.md)

**Retrieve the first DocHit in the HitResultset.**

#### Returns

[`DocHit`](../interfaces/DocHit.md)

DocHit object, `null` in case of an empty HitResultset

#### Since

DOCUMENTS 4.0b

#### See

[next](#next)

***

### getAt()

> **getAt**(`pos`): [`DocHit`](../interfaces/DocHit.md)

**Retrieve the DocHit object at a given position in the HitResultset.**  

**Note:** Valid positions range from 0 to fetchedSize()-1.

#### Parameters

##### pos

`number`

Integer position of the hit, beginning with 0

#### Returns

[`DocHit`](../interfaces/DocHit.md)

DocHit object or `null` if the position is out of bounds.

#### Since

DOCUMENTS 4.0b

***

### getColumnCount()

> **getColumnCount**(): `number`

**Get the number of available columns in the set of hits.**

#### Returns

`number`

The number of columns as an Integer.

#### Since

DOCUMENTS 4.0b

***

### getColumnIndex()

> **getColumnIndex**(`colName`): `number`

**Find the index of a column with a defined name.**  

**Note:** The function tests for a technical column name prior to a localized name.

#### Parameters

##### colName

`string`

The name of the column.

#### Returns

`number`

The zero-based index of the column or a -1, which indicates an unknown column name.

#### Since

DOCUMENTS 4.0b

***

### getColumnNames()

> **getColumnNames**(`local?`): `any`[]

**List the names of all columns in the set of hits.**  

**Note:** If the resultset is bases on an EE.i hitlist, the function usually returns field numbers instead of technical names, 
because column descriptions of an EE.i hitlist only consist of the field number and a label. The label would not be a reliable 
identifier of the column. Columns, which correspond to a DocFile attribute may be given a special constant name instead of 
the name in an archive's scheme. "TITLE" on EE.x and "110" on EE.i may be presented as "DlcFile_Title", for example.

#### Parameters

##### local?

`boolean`

A boolean option to read the localized names instead of the technical names.  

**Default:** `false`

#### Returns

`any`[]

Array of strings with the column names.

#### Since

DOCUMENTS 4.0b

***

### getHitIds()

> **getHitIds**(`withServer?`): `string`[]

**Returns an array with all Hit-Ids (file ids or archive file keys) of the HitResultset.**

#### Parameters

##### withServer?

`boolean`

optional boolean value to indicate, if the archive file keys should include an "@archiveServerName" appendix.  

**Default:** `true`

#### Returns

`string`[]

Array of String with file ids and archive file keys of the HitResultset.

#### Since

DOCUMENTS 5.0d

#### See

[FileResultset.getIds](FileResultset.md#getids)

#### Example

```ts
var searchResources = ["Filetype1@myeas", "Filetype1"];
var myHRS = new HitResultset(searchResources, "", "");
util.out(myHRS.getHitIds());
```

***

### getLastError()

> **getLastError**(): `string`

**Function to get the description of the last error (or warning) that occurred.**

#### Returns

`string`

Text of the last error as String

#### Since

DOCUMENTS 4.0b

#### See

[getLastErrorCode](#getlasterrorcode)

***

### getLastErrorCode()

> **getLastErrorCode**(): `number`

**Function to get a numeric code of the last error, that occurred.**  

**Note:** The value 0 means "no error". Positive values indicate warnings or minor errors, while negative values indicate serious errors. 
After a serious error no hits should be processed. After a minor error, the resultset may be unsorted or truncated, but the contained data is still valid.

#### Returns

`number`

Integer error code.

#### Since

DOCUMENTS 4.0b

#### See

[getLastError](#getlasterror)

***

### next()

> **next**(): [`DocHit`](../interfaces/DocHit.md)

**Retrieve the next DocHit in the HitResultset.**  

**Note:** Calls of getAt() do not affect the internal cursor of next().

#### Returns

[`DocHit`](../interfaces/DocHit.md)

DocHit object, `null` if either the end of the resultset or the end of the loaded pages is reached.

#### Since

DOCUMENTS 4.0b

#### See

[first](#first)

***

### putAside()

> **putAside**(`lifetime`, `id`): `string`

**Put a HitResultset aside, for reuse in a later script execution.**  

This member function moves the HitResultset into a side buffer, which is located outside the scripting environment. A successful call 
invalidates the object and its descendant [DocHit](../interfaces/DocHit.md) objects. Later access to these objects by the caller would trigger an exception.   
The buffered version of the HitResultset, however, can outlive the actual script runtime. It can be reintegrated into script memory 
by a call of [HitResultset.reintegrate(String id)](#reintegrate).  

**Note:** By default the function assigns a unique id to the buffered object and returns it. The caller may pass a preferred id, 
which the function will replace or modify only, if it collides with an existing object in the buffer. The caller may instead pass 
a mandatory id, which is distinguished from preferred ids by an exclamation mark ('!') as the first character. If such an id is 
already assigned, the function will fail, returning an empty string. Invalid values in the lifetime parameter cause an exception. 
Please read also the tutorial [Moving HitResultsets across script boundaries](../HitResultsetSideBuffer.html)

#### Parameters

##### lifetime

`number`

Lifetime of the buffer object in seconds. Only Integer values in the rande 1 to 7200 are valid.

##### id

`string`

Optional string with a preferred id or a mandatory id. See remarks.

#### Returns

`string`

Usually a string with the actual id of the buffered object; an empty string, if a passed mandatory id is already assigned.

#### Since

DOCUMENTS 6.0

***

### reintegrate()

> `static` **reintegrate**(`id`): `HitResultset`

**Reintegrate a HitResultset from the side buffer.**  

This function does the opposite of [HitResultset.putAside(number lifetime, string id)](#putaside). 
It removes and extracts a HitResultset from the side buffer and reintegrates it into the actual scripting environment. 
The function can only reintegrate objects of the actual DOCUMENTS principal. The actual user account must also match, 
except if the script runs in supermode.  

**Note:** Please read also the tutorial [Moving HitResultsets across script boundaries](../HitResultsetSideBuffer.html) !

#### Parameters

##### id

`string`

The string which was formerly returned by the putAside() member function.

#### Returns

`HitResultset`

The reintegrated HitResultset on success, otherwise `null`.

#### Since

DOCUMENTS 6.0

***

### size()

> **size**(): `number`

**Get the total amount of hits in the set.**  

**Note:** If the object has been created with a non-zero page size, this value is often greater than the amount of already accessible hits.

#### Returns

`number`

integer value with the total amount of hits. The value -1 may be returned to indicate, that the search continues in the background, and the final number is not yet known.

#### Since

DOCUMENTS 4.0b

#### See

[fetchedSize](#fetchedsize)

## Constructors

### Constructor

> **new HitResultset**(`searchResources`, `filter`, `sortOrder`, `hitlist`, `pageSize?`, `unlimitedHits?`, `fullColumnLength?`, `withBlobInfo?`): `HitResultset`

**Perform a search and create a new HitResultset object.**  

**Note:**  
On a failed search request the constructor does not throw errors. To detect this kind of errors scripts should 
test the object's error state with [getLastErrorCode()](#getlasterrorcode) or [getLastError()](#getlasterror).

**Resource identifiers**  
  
A "resource identifier" can be one of the following: [ examples in brackets ]
+ a filetype name [ ftOrder ]
+ a filetype name for use with an EDA store [ ftOrder@peachitStore1 ]
+ a filetype name for use with all EDA stores [ ftOrder@ALLEAS ]
+ a EE.x view key [ Unit=Default/Instance=Default/View=Orders@MyEEX ]
+ a EE.i archive key [ $(#STANDARD)\\ORDERS@STDARC\_360 ]
Archive resource identifiers should always get a "@Servername" appendix, though Documents recognizes 
EE.x and EE.i resources of the primary archive server without that appendix.
  
**Resource ordering and hitlist specification**  
  
The resource, which owns a specified hitlist, has to be passed in the first position of the list. 
Search requests in EE.i/EE.x-archives do not work with a filetype's hitlist. These archives require 
a hitlist of their own. For this reason, a list of resources of different types must be ordered 
in the following way: EE.x before EE.i before anything else. Requests, which involve more than 
one Easy Enterprise server can work only, if a hitlist of the given name exists in each resource of these servers.  
  
**Automatic hitlist selection**  
   
If the parameter "hitlist" is an empty string, Documents scans the search resources for a named hitlist. 
If no named hitlist exists, Documents initializes an old-fashioned anonymous hitlist, which is based 
on the "Display in hit list" option of fields in the Documents Manager and on corresponding options 
for particular DocFile attributes (title, created, owner, last modified, last editor). An anonymous hitlist 
does actually not work with EE.x. It partially works with EE.i. In this case, Documents externally uses 
the setting "CommonDefaultHitlist" of the configuration file "ArchiveXML.ini" and transfers matching columns 
into the internal hitlist. As long as named hitlists become imported with the archive structure, it does not matter.  

Search requests, which involve more than one Easy Enterprise server cannot rely on the automatic selection feature. 
Scripts should always pass an appropriate hitlist name for these requests.  
  
**Since:** DOCUMENTS 4.0b   
**Since:** DOCUMENTS 4.0d HF1 new parameter `fullColumnLength`   
**Since:** DOCUMENTS 5.0 (New option for hitlist parameter: an array of field names instead of a hitlist name)

#### Parameters

##### searchResources

`any`

The list of resources to search through. The resource identifiers may be passed either as an array of strings 
or as an ordinary string with one identifier per line of text. Please read the remarks section about restrictions.

##### filter

`string`

A filter expression. Pass an empty string, if no filter ist required.

##### sortOrder

`string`

A sort expression. Pass an empty string, if no sorting is required.

##### hitlist

`any`

The technical name of a hitlist or an array of field names, which specifies the available columns in the resultset. 
If the parameter is left empty, Documents tries to choose a hitlist automatically. Details follow in the remarks section.   

**Note:** If this parameter is an array of field names, a search in EE.i or EE.x is not allowed and the field names must not contain commas (,).

##### pageSize?

`number`

This is a memory-saving and performance-tuning option. If the parameter is zero, Documents will load all available hits at once. If the parameter 
is a positive value, Documents will initially load only the requested number of hits as a first page. In order to access each further page, a call to 
[fetchNextPage()](#fetchnextpage) is necessary. A negative pageSize value will be replaced by the current user's "hits per page" preference setting.  

**Default:** `0`.

##### unlimitedHits?

`boolean`

A boolean that indicates, if the general hit limitations on filetypes and archives must be ignored. A wasteful use of this option 
may cause issues with the system performance or situations with low free memory.  

**Default:** `false`

##### fullColumnLength?

`boolean`

A boolean that indicates, if the general hit column length limitations must be ignored. The default column length is 50 characters 
(if not a different value is defined by the property Documents-Settings: `MaxHitfieldLength`). If a field value exceeds this size, 
the first 50 characters will be displayed followed by '...'. If the parameter `fullColumnLength` is set to `true`, no truncation will be done.  

**Default:** `false`

##### withBlobInfo?

`boolean`

A boolean that indicates, if the HitResultset should contain blob-information that can be fetched with [DocHit.getBlobInfo()](../interfaces/DocHit.md#getblobinfo)  

**Default:** `false`

#### Returns

`HitResultset`

#### Since

DOCUMENTS 4.0b

#### Examples

```ts
var searchResources = "Filetype1  Filetype2";
var filter = "";
var sortOrder = "";
var myFile;
var myHRS = new HitResultset(searchResources, filter, sortOrder);
if (myHRS.getLastErrorCode() < 0)
{
    util.out(myHRS.getLastError());
}
else
{
    for (var myHit = myHRS.first(); myHit; myHit = myHRS.next())
    {
        myFile = myHit.getFile();
        if (myFile)
            util.out(myFile.getAutoText("id"));
        else
            util.out(myHit.getLastError());
    }
}
```

```ts
var searchResources = ["$(#STANDARD)\\REGTEST@myeei", "Filetype1@myeas", "Filetype1"];
var filter = "";
var sortOrder = "";
var hitlist = ["feld1", "feld2", "feld3"];
var pageSize = 3;
var pos = 6;
var unlimitedHits = true;
var fullColumnLength = true;
var myHRS = new HitResultset(searchResources, filter, sortOrder, hitlist, pageSize, unlimitedHits, fullColumnLength);
if (myHRS.getLastErrorCode() < 0)
    throw new Error(myHRS.getLastError());
if (myHRS.size() > pos)
{
    while (pos >= myHRS.fetchedSize())
        myHRS.fetchNextPage();
    var myHit = myHRS.getAt(pos);
    if (myHit)
    {
        if (myHit.isArchiveHit())
            util.out(myHit.getArchiveKey());
        else
            util.out(myHit.getFileId());
    }
}
```

```ts
var searchResources = "Unit=Default/Instance=Default/View=REGTEST@myeex";
var filter = "";
var sortOrder = "myField+";
var hitlist = ["feld1", "feld2", "feld3"];
var pageSize = 10;
var myFile;
var myHRS = new HitResultset(searchResources, filter, sortOrder, hitlist, pageSize);
if (myHRS.getLastErrorCode() < 0)
    throw new Error(myHRS.getLastError());
// Iterate only the hit entries on the first page.
for (var myHit = myHRS.first(); myHit; myHit = myHRS.next())
{
    myFile = myHit.getArchiveFile();
    if (myFile)
        util.out(myFile.getAttribute("Key"));
    else
        util.out(myHit.getLastError());
}
```

#### See

[Filter Expressions](../filter.html)  
[Filter Expression Examples](../filter-examples.html)
