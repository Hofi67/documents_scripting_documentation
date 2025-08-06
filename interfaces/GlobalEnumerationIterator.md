[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / GlobalEnumerationIterator

# Interface: GlobalEnumerationIterator

**The EnumerationIterator class has been added to the DOCUMENTS Portalscript API to gain full access to the DOCUMENTS global enumerations by scripting means.**  

The objects of this class represent lists of [GlobalEnumeration](GlobalEnumeration.md) objects and allow to loop through such a list of global enumerations. 
The following method returns a GlobalEnumerationIterator: [context.getGlobalEnumerations](Context.md#getglobalenumerations)

## Since

DOCUMENTS 6.0.2

## See

[context.getGlobalEnumerations](Context.md#getglobalenumerations)

## Example

```ts
var itEnum = context.getGlobalEnumerations();
for (var gEnum = itEnum.first(); gEnum; gEnum = itEnum.next())
{
   // do something
}
```

## Methods

### first()

> **first**(): [`GlobalEnumeration`](GlobalEnumeration.md)

**Retrieve the first [GlobalEnumeration](GlobalEnumeration.md) object in the GlobalEnumerationIterator.**

#### Returns

[`GlobalEnumeration`](GlobalEnumeration.md)

GlobalEnumeration or `null` in case of an empty GlobalEnumerationIterator

#### Since

DOCUMENTS 6.0.2

***

### next()

> **next**(): [`GlobalEnumeration`](GlobalEnumeration.md)

**Retrieve the next [GlobalEnumeration](GlobalEnumeration.md) object in the GlobalEnumerationIterator.**

#### Returns

[`GlobalEnumeration`](GlobalEnumeration.md)

GlobalEnumeration or `null` if end of GlobalEnumerationIterator is reached.

#### Since

DOCUMENTS 6.0.2

***

### size()

> **size**(): `number`

**Get the amount of [GlobalEnumeration](GlobalEnumeration.md) objects in the GlobalEnumerationIterator.**

#### Returns

`number`

Integer value with the amount of GlobalEnumeration objects in the GlobalEnumerationIterator

#### Since

DOCUMENTS 6.0.2
