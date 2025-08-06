[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / DocumentIterator

# Interface: DocumentIterator

**The DocumentIterator class has been added to the DOCUMENTS PortalScripting API to gain full access to the documents stored on registers of a DOCUMENTS file by scripting means.**  

**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

## Since

ELC 3.50n / otrisPORTAL 5.0n

## Example

```ts
var docFile = context.file;
if (docFile)
{
   var docreg = docFile.getRegisterByName("Documents");
   if (docreg)
   {
      var docs = docreg.getDocuments();
      if (docs && docs.size() > 0)
      {
         for (var d = docs.first(); d; d = docs.next())
         {
            util.out(d.fullname);
         }
      }
   }
}
```

## Methods

### first()

> **first**(): [`Document`](Document.md)

**Retrieve the first Document object in the DocumentIterator.**  
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Returns

[`Document`](Document.md)

Document or `null` in case of an empty DocumentIterator

#### Since

ELC 3.50n / otrisPORTAL 5.0n

***

### getLastError()

> **getLastError**(): `string`

**Function to get the description of the last error that occurred.**

#### Returns

`string`

Text of the last error as String

#### Since

ELC 3.50n / otrisPORTAL 5.0n

#### See

[DocFile.getLastError](DocFile.md#getlasterror)

***

### next()

> **next**(): [`Document`](Document.md)

**Retrieve the next Document object in the DocumentIterator.**  
 
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Returns

[`Document`](Document.md)

Document or `null` if end of DocumentIterator is reached.

#### Since

ELC 3.50n / otrisPORTAL 5.0n

***

### size()

> **size**(): `number`

**Get the amount of Document objects in the DocumentIterator.**  
 
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Returns

`number`

integer value with the amount of Document objects in the DocumentIterator

#### Since

ELC 3.50n / otrisPORTAL 5.0n
