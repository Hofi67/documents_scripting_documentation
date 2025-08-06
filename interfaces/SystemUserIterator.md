[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / SystemUserIterator

# Interface: SystemUserIterator

**The SystemUserIterator class has been added to the DOCUMENTS PortalScripting API to gain full access to the DOCUMENTS users by scripting means.**  

The objects of this class represent lists of Systemuser objects and allow to loop through such a list of users.

## Since

ELC 3.50b / otrisPORTAL 5.0b

## Methods

### first()

> **first**(): [`SystemUser`](SystemUser.md)

**Retrieve the first [SystemUser](SystemUser.md) object in the SystemUserIterator.**

#### Returns

[`SystemUser`](SystemUser.md)

SystemUser or `null` in case of an empty SystemUserIterator

#### Since

ELC 3.50b / otrisPORTAL 5.0b

***

### getLastError()

> **getLastError**(): `string`

**Function to get the description of the last error that occurred.**

#### Returns

`string`

Text of the last error as String

#### Since

ELC 3.50b / otrisPORTAL 5.0b

#### See

[DocFile.getLastError](DocFile.md#getlasterror)

***

### next()

> **next**(): [`SystemUser`](SystemUser.md)

**Retrieve the next [SystemUser](SystemUser.md) object in the SystemUserIterator.**

#### Returns

[`SystemUser`](SystemUser.md)

SystemUser or `null` if end of SystemUserIterator is reached.

#### Since

ELC 3.50b / otrisPORTAL 5.0b

***

### size()

> **size**(): `number`

**Get the amount of [SystemUser](SystemUser.md) objects in the SystemUserIterator.**

#### Returns

`number`

integer value with the amount of SystemUser objects in the SystemUserIterator

#### Since

ELC 3.50b / otrisPORTAL 5.0b
