[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / RegisterIterator

# Interface: RegisterIterator

**The RegisterIterator class has been added to the DOCUMENTS PortalScripting API to gain full access to the registers of a DOCUMENTS file by scripting means.**  

**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

## Since

ELC 3.50n / otrisPORTAL 5.0n

## Example

```ts
var docFile = context.file;
if (docFile)
{
   var docregs = docFile.getRegisters("documents");
   if (docregs && docregs.size() > 0)
   {
      for (var d = docregs.first(); d; d = docregs.next())
      {
         util.out(d.Name + ", " + d.Label);
      }
   }
}
```

## Methods

### first()

> **first**(): [`Register`](Register.md)

**Retrieve the first Register object in the RegisterIterator.**  
 
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Returns

[`Register`](Register.md)

Register or `null` in case of an empty RegisterIterator

#### Since

ELC 3.50n / otrisPORTAL 5.0n

***

### getLastError()

> **getLastError**(): `string`

**Function to get the description of the last error that occurred.**  
 
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Returns

`string`

Text of the last error as String

#### Since

ELC 3.50n / otrisPORTAL 5.0n

#### See

[DocFile.getLastError](DocFile.md#getlasterror)

***

### next()

> **next**(): [`Register`](Register.md)

**Retrieve the next Register object in the RegisterIterator.**  
 
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Returns

[`Register`](Register.md)

Register or `null` if end of RegisterIterator is reached.

#### Since

ELC 3.50n / otrisPORTAL 5.0n

***

### size()

> **size**(): `number`

**Get the amount of Register objects in the RegisterIterator.**  
 
  
**Since:** ELC 3.60i / otrisPORTAL 6.0i available for archive files

#### Returns

`number`

integer value with the amount of Register objects in the RegisterIterator

#### Since

ELC 3.50n / otrisPORTAL 5.0n
