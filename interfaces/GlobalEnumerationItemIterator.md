[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / GlobalEnumerationItemIterator

# Interface: GlobalEnumerationItemIterator

**The EnumerationItemIterator class has been added to the DOCUMENTS Portalscript API to gain full access to the items of the DOCUMENTS global enumerations by scripting means.**  

The objects of this class represent lists of [GlobalEnumerationItem](GlobalEnumerationItem.md) objects and allow to loop through such a list of global enumeration items. 
The following method returns a GlobalEnumerationItemIterator: [GlobalEnumeration.getGlobalEnumerationItems](GlobalEnumeration.md#getglobalenumerationitems)

## Since

DOCUMENTS 6.0.2

## See

[GlobalEnumeration.getGlobalEnumerationItems](GlobalEnumeration.md#getglobalenumerationitems)

## Example

```ts
var itItem = testEnum.getGlobalEnumerationItems();
for (var item = itItem.first(); item; item = itItem.next())
{
   // do something
}
```

## Methods

### first()

> **first**(): [`GlobalEnumerationItem`](GlobalEnumerationItem.md)

**Retrieve the first [GlobalEnumerationItem](GlobalEnumerationItem.md) object in the GlobalEnumerationItemIterator.**

#### Returns

[`GlobalEnumerationItem`](GlobalEnumerationItem.md)

GlobalEnumerationItem or `null` in case of an empty GlobalEnumerationItemIterator

#### Since

DOCUMENTS 6.0.2

***

### next()

> **next**(): [`GlobalEnumerationItem`](GlobalEnumerationItem.md)

**Retrieve the next [GlobalEnumerationItem](GlobalEnumerationItem.md) object in the GlobalEnumerationItemIterator.**

#### Returns

[`GlobalEnumerationItem`](GlobalEnumerationItem.md)

GlobalEnumerationItem or `null` if end of GlobalEnumerationItemIterator is reached.

#### Since

DOCUMENTS 6.0.2

***

### size()

> **size**(): `number`

**Get the amount of [GlobalEnumerationItem](GlobalEnumerationItem.md) objects in the GlobalEnumerationItemIterator.**

#### Returns

`number`

Integer value with the amount of GlobalEnumerationItem objects in the GlobalEnumerationItemIterator

#### Since

DOCUMENTS 6.0.2
