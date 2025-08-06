[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / ArchiveFileResultset

# Class: ArchiveFileResultset

The ArchiveFileResultset class supports basic functions to loop through a list of ArchiveFile objects.

## Methods

### first()

> **first**(): [`DocFile`](../interfaces/DocFile.md)

**Retrieve the first [DocFile](../interfaces/DocFile.md) object in the ArchiveFileResultset.**

#### Returns

[`DocFile`](../interfaces/DocFile.md)

DocFile, `null` in case of an empty ArchiveFileResultset, throws an exception on error loading archive file.

#### Since

ELC 3.60i / otrisPORTAL 6.0i

***

### getLastError()

> **getLastError**(): `string`

**Function to get the description of the last error that occurred.**

#### Returns

`string`

Text of the last error as String

#### Since

ELC 3.60i / otrisPORTAL 6.0i

#### See

[DocFile.getLastError](../interfaces/DocFile.md#getlasterror)

***

### last()

> **last**(): [`DocFile`](../interfaces/DocFile.md)

**Retrieve the last [DocFile](../interfaces/DocFile.md) object in the ArchiveFileResultset.**

#### Returns

[`DocFile`](../interfaces/DocFile.md)

DocFile or `null` if end of ArchiveFileResultset is reached.

#### Since

ELC 3.60j / otrisPORTAL 6.0j

***

### next()

> **next**(): [`DocFile`](../interfaces/DocFile.md)

**Retrieve the next [DocFile](../interfaces/DocFile.md) object in the ArchiveFileResultset.**

#### Returns

[`DocFile`](../interfaces/DocFile.md)

DocFile, `null` if end of ArchiveFileResultset is reached, throws an exception on error loading archive file.

#### Since

ELC 3.60i / otrisPORTAL 6.0i

***

### size()

> **size**(): `number`

**Get the amount of [DocFile](../interfaces/DocFile.md) objects in the ArchiveFileResultset.**

#### Returns

`number`

integer value with the amount of DocFile objects in the ArchiveFileResultset

#### Since

ELC 3.60i / otrisPORTAL 6.0i

## Constructors

### Constructor

> **new ArchiveFileResultset**(`archiveKey`, `filter`, `sortOrder`, `hitlist`, `unlimitedHits?`): `ArchiveFileResultset`

**Create a new ArchiveFileResultset object.**  

Like in other programming languages you create a new object with the `new` operator (refer to example below).  

**Note:** Important: The resultset may contain less hits than really exist. For EE.i and EE.x the limit of 
returned hits is the value of the DOCUMENTS property "MaxArchiveHitsFolder". If the property is not set, 
the limit is the XML-Server's default hit count. For EAS, The limit is either the "MaxArchiveHitsFolder" 
value or the limit of free research hitlists. The method is the same for dynamic folders and link-registers.

#### Parameters

##### archiveKey

`string`

String containing the key of the desired view or archive

##### filter

`string`

String containing an filter criterium; use empty String ('') if you don't want to filter at all

##### sortOrder

`string`

String containing an sort order; use empty String ('') if you don't want to sort at all

##### hitlist

`string`

String containing the hitlist that you want to use (optional für EE.i / mandatory for EE.x

##### unlimitedHits?

`boolean`

boolean that indicates if the archive hit limit must be ignored  
**Default:** `false`

#### Returns

`ArchiveFileResultset`

#### Since

ELC 3.60i / otrisPORTAL 6.0i

#### Examples

```ts
// Example for EE.i:
var archiveKey = "$(#STANDARD)\\EINRECH";
archiveKey += "@myeei";            // since Documents 4.0 using multi archive server
var filter = "Kreditor='ALFKI'";
var sortOrder = "BelegNr+";
var hitlist = "STANDARD";
var myAFRS = new ArchiveFileResultset(archiveKey, filter, sortOrder, hitlist);
var archFile = null;
while (true)
{
   try
   {
      archFile = archFile ? myAFRS.next() : myAFRS.first();
      if (!archFile) // end of ArchiveFileResultset
         break;
      util.out(archFile.getArchiveKey());
   }
   catch (err)
   {
      util.out("Unable to load archFile: " + err);
   }
}
```

```ts
// Example for EE.x:
var archiveKey = "Unit=Default/Instance=Default/View=Scanners";
archiveKey += "@myeex";            // since Documents 4.0 using multi archive server
var filter = "Speed=10";
var sortOrder = "";
var hitlist = "Default";
var myAFRS = new ArchiveFileResultset(archiveKey, filter, sortOrder, hitlist);
```

```ts
// Example for EAS:
var archiveKey = "Order";
archiveKey += "@myeas";            // since Documents 4.0 using multi archive server
var filter = "company=A*";
var sortOrder = "company+";
var myAFRS = new ArchiveFileResultset(archiveKey, filter, sortOrder);
```
