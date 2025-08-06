[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / GlobalEnumeration

# Interface: GlobalEnumeration

**The GlobalEnumeration class has been added to the DOCUMENTS Portalscript API to gain full access to the DOCUMENTS global enumerations by scripting means.**  

A GlobalEnumeration object isn't created directly. You can get it using the [Context.createGlobalEnumeration(name)](Context.md#createglobalenumeration) function.

## Since

DOCUMENTS 6.0.2

## Properties

### description

> **description**: `string`

**The description of the GlobalEnumeration.**

#### Since

DOCUMENTS 6.0.2

***

### name

> **name**: `string`

**The technical name of the GlobalEnumeration.**

#### Since

DOCUMENTS 6.0.2

## Methods

### createGlobalEnumerationItem()

> **createGlobalEnumerationItem**(`name`): [`GlobalEnumerationItem`](GlobalEnumerationItem.md)

**Create a new [GlobalEnumerationItem](GlobalEnumerationItem.md) for the GlobalEnumeration.**

#### Parameters

##### name

`string`

The name of the GlobalEnumerationItem.

#### Returns

[`GlobalEnumerationItem`](GlobalEnumerationItem.md)

The new created GlobalEnumerationItem object or `null` if failed.

#### Since

DOCUMENTS 6.0.2

#### See

[GlobalEnumeration.deleteGlobalEnumerationItem](#deleteglobalenumerationitem)

#### Example

```ts
var testEnum = context.createGlobalEnumeration("testEnum");
var name = "testItem1";
var success = testEnum.createGlobalEnumerationItem(name);
if (success)
{
   util.out("Successfully created GlobalEnumerationItem " + name);
}
```

***

### deleteGlobalEnumerationItem()

> **deleteGlobalEnumerationItem**(`name`): `boolean`

**Remove a [GlobalEnumerationItem](GlobalEnumerationItem.md) from the GlobalEnumeration.**

#### Parameters

##### name

`string`

The name of the GlobalEnumerationItem to be removed.

#### Returns

`boolean`

`true` if the deletion was successful, `false` in case of any error

#### Since

DOCUMENTS 6.0.2

#### See

[GlobalEnumeration.createGlobalEnumerationItem](#createglobalenumerationitem)

#### Example

```ts
var name = "testItem1";
var success = testEnum.deleteGlobalEnumerationItem(name);
if (success)
{
   util.out("Successfully deleted GlobalEnumerationItem " + name);
}
```

***

### getGlobalEnumerationItems()

> **getGlobalEnumerationItems**(): [`GlobalEnumerationItemIterator`](GlobalEnumerationItemIterator.md)

**Get a [GlobalEnumerationItemIterator](GlobalEnumerationItemIterator.md) with all items of the GlobalEnumeration.**

#### Returns

[`GlobalEnumerationItemIterator`](GlobalEnumerationItemIterator.md)

GlobalEnumerationItemIterator

#### Since

DOCUMENTS 6.0.2

#### Example

```ts
var it = testEnum.getGlobalEnumerationItems();
for (var item of it)
{
   // do something
}
```

***

### getLastError()

> **getLastError**(`shortMessage?`): `string`

**Function to get the description of the last error that occurred.**

#### Parameters

##### shortMessage?

`boolean`

Flag indicating whether to remove "Error in function: class.method(): " from the message.  
**Default:** `false`

#### Returns

`string`

Text of the last error as String

#### Since

DOCUMENTS 6.0.2
