[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / CustomPropertyIterator

# Interface: CustomPropertyIterator

**The CustomPropertyIterator class is an iterator that holds a list of objects of the class CustomProperty.**

## Since

DOCUMENTS 4.0a

## Methods

### first()

> **first**(): [`CustomProperty`](CustomProperty.md)

**Retrieve the first CustomProperty object in the CustomPropertyIterator.**

#### Returns

[`CustomProperty`](CustomProperty.md)

CustomProperty or `null` in case of an empty CustomPropertyIterator

#### Since

DOCUMENTS 4.0a

***

### next()

> **next**(): [`CustomProperty`](CustomProperty.md)

**Retrieve the next CustomProperty object in the CustomPropertyIterator.**

#### Returns

[`CustomProperty`](CustomProperty.md)

CustomProperty or `null` if end of CustomPropertyIterator is reached

#### Since

DOCUMENTS 4.0a

***

### size()

> **size**(): `number`

**Get the amount of CustomProperty objects in the CustomPropertyIterator.**

#### Returns

`number`

integer value with the amount of CustomProperty objects in the CustomPropertyIterator

#### Since

DOCUMENTS 4.0a
