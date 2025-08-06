[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / FileResultset

# Class: FileResultset

The FileResultset class supports basic functions to loop through a list of DocFile objects.  

You can manually create a FileResultset as well as access the (selected) files of a (public) Folder.

## Methods

### first()

> **first**(): [`DocFile`](../interfaces/DocFile.md)

**Retrieve the first DocFile object in the FileResultset.**

#### Returns

[`DocFile`](../interfaces/DocFile.md)

DocFile or `null` in case of an empty FileResultset

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
var myFRS = new FileResultset("Standard", "", "");
var myFile = myFRS.first();
```

***

### fromIds()

> `static` **fromIds**(`idList`): `FileResultset`

**Recreate a FileResultset from a formerly extracted id-list.**

#### Parameters

##### idList

`string`[]

Array of String with file ids, as returned by FileResultset.getIds()

#### Returns

`FileResultset`

A new FileResultset, which will iterate over the DocFiles with the given ids

#### Since

DOCUMENTS 5.0f

#### Example

```ts
// * **
// * ** Main script * **
// * **
var myFRS = new FileResultset("ftEmployee", "", "");
var idListJson = JSON.stringify(myFRS.getIds());
var worker = new ScriptCall(context.currentUser, "AsyncFRSWorker", false);
// It is technically impossible to pass complex objects like a FileResultset as a script parameter.
// The above idListJson can be passed instead, provided it fits into memory.
worker.addParameter("idListJson", idListJson);
worker.launch();
// * ** End of main script * **
// * **
// * ** Background processing script "AsyncFRSWorker" * **
// * **
// Expects JSONified id list from employees-FileResultset in the script parameter "idListJson"
var idArray = JSON.parse(idListJson);
// +++ Now create a twin of the caller's FileResultset +++
var frs = FileResultset.fromIds(idArray);
var sumSalary = 0;
for(var df = frs.first(); df; df = frs.next())
{
  sumSalary += ensureInt(df.salary);
}
context.setOrAddCustomProperty("SumOfSalaries", "number", sumSalary);
function ensureInt(p)
{
  if(typeof(p) == "number") return Math.floor(p);
  var num = parseInt(p, 10);
  return isNaN(num) ? 0 : num;
}
// * ** End of background processing script * **
```

***

### fromIdsJSON()

> `static` **fromIdsJSON**(`idList`): `FileResultset`

**Recreate a FileResultset from a formerly extracted id-list in JSON format.**  

**Note:** The following expression produces the same result ` FileResultset.fromIds(JSON.parse(idList)); `

#### Parameters

##### idList

`string`

JSON string with file ids, as returned by FileResultset.getIdsJSON()

#### Returns

`FileResultset`

A new FileResultset, which will iterate over the DocFiles with the given ids

#### Since

DOCUMENTS 5.0f

#### See

[fromIds](#fromids)

***

### getIds()

> **getIds**(): `string`[]

**Returns an array with all file ids in the FileResultset.**

#### Returns

`string`[]

Array of String with file ids of the FileResultset

#### Since

DOCUMENTS 5.0c

#### Example

```ts
var myFRS = new FileResultset("Standard", "", "");
util.out(myFRS.getIds());
```

***

### getIdsJSON()

> **getIdsJSON**(): `string`

**Returns JSON string with all file ids in the FileResultset.**  

**Note:** Assuming "myFRS" is a FileResultset the following expression produces the same result. ` JSON.stringify(myFRS.getIds()); `

#### Returns

`string`

JSON string with file ids of the FileResultset

#### Since

DOCUMENTS 5.0f

#### See

[getIds](#getids)

***

### last()

> **last**(): [`DocFile`](../interfaces/DocFile.md)

**Retrieve the last DocFile object in the FileResultset.**

#### Returns

[`DocFile`](../interfaces/DocFile.md)

DocFile or `null` if end of FileResultset is reached.

#### Since

ELC 3.60j / otrisPORTAL 6.0j

***

### next()

> **next**(): [`DocFile`](../interfaces/DocFile.md)

**Retrieve the next DocFile object in the FileResultset.**

#### Returns

[`DocFile`](../interfaces/DocFile.md)

DocFile or `null` if end of FileResultset is reached.

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
var myFRS = new FileResultset("Standard", "", "");
for (var myFile = myFRS.first(); myFile; myFile = myFRS.next())
{
   // do something with each DocFile object
}
```

***

### size()

> **size**(): `number`

**Get the amount of DocFile objects in the FileResultset.**

#### Returns

`number`

integer value with the amount of DocFile objects in the FileResultset

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
var myFRS = new FileResultset("Standard", "", "");
util.out(myFRS.size());
```

## Constructors

### Constructor

> **new FileResultset**(`fileType`, `filter?`, `sortOrder?`): `FileResultset`

**Create a new FileResultset object.**  

Like in other programming languages you create a new object with the `new` operator (refer to example below).  

**Note:** Details for the filter expression you find in section [Filter Expressions ](../filter.html)  

**Note:** Further samples are in [Filter Expression Examples](../filter-examples.html)

#### Parameters

##### fileType

`string`

String containing the technical name of the desired filetype

##### filter?

`string`

String containing an optional filter criterium; use empty String ('') if you don't want to filter at all

##### sortOrder?

`string`

String containing an optional sort order; use empty String ('') if you don't want to sort at all

#### Returns

`FileResultset`

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### Example

```ts
var fileType = "Standard";
var filter = "";
var sortOrder = "";
var myFRS = new FileResultset(fileType, filter, sortOrder);
```
