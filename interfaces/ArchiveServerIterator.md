[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / ArchiveServerIterator

# Interface: ArchiveServerIterator

**The ArchiveServerIterator class has been added to the DOCUMENTS PortalScripting API to gain full access to the DOCUMENTS ArchiveSerevr by scripting means.**

## Since

DOCUMENTS 5.0a

## Methods

### first()

> **first**(): [`ArchiveServer`](ArchiveServer.md)

**Retrieve the first [ArchiveServer](ArchiveServer.md) object in the ArchiveServerIterator.**

#### Returns

[`ArchiveServer`](ArchiveServer.md)

ArchiveServer or `null` in case of an empty ArchiveServerIterator

#### Since

DOCUMENTS 5.0a

***

### getLastError()

> **getLastError**(): `string`

**Function to get the description of the last error that occurred.**

#### Returns

`string`

Text of the last error as String

#### Since

DOCUMENTS 5.0a

***

### next()

> **next**(): [`ArchiveServer`](ArchiveServer.md)

**Retrieve the next [ArchiveServer](ArchiveServer.md) object in the ArchiveServerIterator.**

#### Returns

[`ArchiveServer`](ArchiveServer.md)

ArchiveServer or `null` if end of ArchiveServerIterator is reached.

#### Since

DOCUMENTS 5.0a

***

### size()

> **size**(): `number`

**Get the amount of [ArchiveServer](ArchiveServer.md) objects in the ArchiveServerIterator.**

#### Returns

`number`

integer value with the amount of ArchiveServer objects in the ArchiveServerIterator

#### Since

DOCUMENTS 5.0a
