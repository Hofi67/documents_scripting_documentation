[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / AliasIterator

# Interface: AliasIterator

**The AliasIterator class has been added to the DOCUMENTS PortalScripting API to gain full access to the DOCUMENTS aliases by scripting means.**  

The objects of this class represent lists of [Alias](Alias.md) objects and allow to loop through such a list of aliases. The following method 
returns an AliasIterator: [context.getAllAliases](Context.md#getallaliases).

## Since

DOCUMENTS 5.0i HF7

## Example

```ts
var itAlias = context.getAllAliases();
for (var alias = itAlias.first(); alias; alias = itAlias.next())
{
   // do something
}
```

## Methods

### first()

> **first**(): [`Alias`](Alias.md)

**Retrieve the first [Alias](Alias.md) object in the AliasIterator.**

#### Returns

[`Alias`](Alias.md)

Alias or `null` in case of an empty AliasIterator

#### Since

DOCUMENTS 5.0i HF7

***

### next()

> **next**(): [`Alias`](Alias.md)

**Retrieve the next [Alias](Alias.md) object in the AliasIterator.**

#### Returns

[`Alias`](Alias.md)

Alias or `null` if end of AliasIterator is reached.

#### Since

DOCUMENTS 5.0i HF7

***

### size()

> **size**(): `number`

**Get the amount of [Alias](Alias.md) objects in the AliasIterator.**

#### Returns

`number`

integer value with the amount of Alias objects in the AliasIterator

#### Since

DOCUMENTS 5.0i HF7
