[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / ArchiveConnectionBlobIterator

# Interface: ArchiveConnectionBlobIterator

**The ArchiveConnectionBlobIterator class is an iterator that holds a list of objects of the class [ArchiveConnectionBlob](ArchiveConnectionBlob.md).**  

You may access ArchiveConnectionBlobIterator objects by the ArchiveConnection.downloadBlobs() method described in the ArchiceConnection chapter.

**Note:** Class is only available for an ArchiceConnection to a XML-Server

## Since

ELC 3.60h / otrisPORTAL 6.0h

## Methods

### first()

> **first**(): [`ArchiveConnectionBlob`](ArchiveConnectionBlob.md)

**Retrieve the first [ArchiveConnectionBlob](ArchiveConnectionBlob.md) object in the ArchiveConnectionBlobIterator.**

#### Returns

[`ArchiveConnectionBlob`](ArchiveConnectionBlob.md)

ArchiveConnectionBlob or `null` in case of an empty ArchiveConnectionBlobIterator

#### Since

ELC 3.60h / otrisPORTAL 6.0h

***

### next()

> **next**(): [`ArchiveConnectionBlob`](ArchiveConnectionBlob.md)

**Retrieve the next [ArchiveConnectionBlob](ArchiveConnectionBlob.md) object in the ArchiveConnectionBlobIterator.**

#### Returns

[`ArchiveConnectionBlob`](ArchiveConnectionBlob.md)

ArchiveConnectionBlob or `null` if end of ArchiveConnectionBlobIterator is reached

#### Since

ELC 3.60h / otrisPORTAL 6.0h

***

### size()

> **size**(): `number`

**Get the amount of [ArchiveConnectionBlob](ArchiveConnectionBlob.md) objects in the ArchiveConnectionBlobIterator.**

#### Returns

`number`

integer value with the amount of ArchiveConnectionBlob objects in the ArchiveConnectionBlobIterator

#### Since

ELC 3.60h / otrisPORTAL 6.0h
