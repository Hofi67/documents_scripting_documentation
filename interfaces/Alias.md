[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / Alias

# Interface: Alias

**The Alias class has been added to the DOCUMENTS Portalscript API to gain full access to the DOCUMENTS alias by scripting means.**  

An Alias object isn't created directly. You can get it using the [Context.createAlias](Context.md#createalias) function.

## Since

DOCUMENTS 5.0i HF6

## Properties

### label

> `readonly` **label**: `string`

**The label of the alias.**

#### Since

DOCUMENTS 5.0i HF7

***

### name

> `readonly` **name**: `string`

**The technical name of the alias.**

#### Since

DOCUMENTS 5.0i HF6

***

### systemUser

> `readonly` **systemUser**: [`SystemUser`](SystemUser.md)

**Returns the [SystemUser](SystemUser.md) currently assigned to this alias.**

#### Since

DOCUMENTS 5.0i HF6

## Methods

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

DOCUMENTS 5.0i HF6

***

### setLabel()

> **setLabel**(`label`): `boolean`

**Set the label of the alias.**

#### Parameters

##### label

`string`

The new label of the alias.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0i HF7

***

### setName()

> **setName**(`name`): `boolean`

**Set the name of the alias.**  

The alias will be renamed to the given name.

#### Parameters

##### name

`string`

The new name of the alias.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0i HF6

***

### setSystemUser()

> **setSystemUser**(`login?`): `boolean`

**Set a [SystemUser](SystemUser.md) to the alias.**  

The old `SystemUser` will be disconnected.

#### Parameters

##### login?

`string`

The login name of the `SystemUser` to be assigned to this alias.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0i HF6

#### Example

```ts
if (!testAlias.setSystemUser("schreiber"))
   throw testAlias.getLastError();
```
