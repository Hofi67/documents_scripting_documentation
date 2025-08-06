[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / FolderIterator

# Interface: FolderIterator

**The FolderIterator class has been added to the DOCUMENTS PortalScripting API to gain full access to the DOCUMENTS folders by scripting means.**

## Since

ELC 3.50l01 / otrisPORTAL 5.0l01

## Example

```ts
if (context.getFoldersByName(lstName, "public").size() == 0)
{
   var folderIter = context.getFoldersByName("TemplateFolder", "public");
   if (folderIter && folderIter.size() > 0)
   {
      var source = folderIter.first(); // fetch list folder
      var target = source.copyFolder(true, true, true);
      target.Name = lstName;
      target.Label = docFile.crmName;
      target.Type = "public";
   }
}
```

## Methods

### first()

> **first**(): [`Folder`](Folder.md)

**Retrieve the first Folder object in the FolderIterator.**

#### Returns

[`Folder`](Folder.md)

Folder or `null` in case of an empty FolderIterator

#### Since

ELC 3.50l01 / otrisPORTAL 5.0l01

***

### getLastError()

> **getLastError**(): `string`

**Function to get the description of the last error that occurred.**

#### Returns

`string`

Text of the last error as String

#### Since

ELC 3.50l01 / otrisPORTAL 5.0l01

#### See

[DocFile.getLastError](DocFile.md#getlasterror)

***

### next()

> **next**(): [`Folder`](Folder.md)

**Retrieve the next Folder object in the FolderIterator.**

#### Returns

[`Folder`](Folder.md)

Folder or `null` if end of FolderIterator is reached.

#### Since

ELC 3.50l01 / otrisPORTAL 5.0l01

***

### size()

> **size**(): `number`

**Get the amount of Folder objects in the FolderIterator.**

#### Returns

`number`

integer value with the amount of Folder objects in the FolderIterator

#### Since

ELC 3.50l01 / otrisPORTAL 5.0l01
