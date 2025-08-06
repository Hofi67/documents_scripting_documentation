[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / PortalTestOperation

# Interface: PortalTestOperation

**`Internal`**

**JS_PortalTestOperation class.**  

This interface is for internal use only!

## Since

ELC 3.60e / otrisPORTAL 6.0e

## Methods

### getActualOutOids()

> **getActualOutOids**(): `number`[]

**`Internal`**

This function is for internal use only!

#### Returns

`number`[]

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### getActualOutParams()

> **getActualOutParams**(): `number`[]

**`Internal`**

This function is for internal use only!

#### Returns

`number`[]

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### getActualReturnValue()

> **getActualReturnValue**(): `number`

**`Internal`**

This function is for internal use only!

#### Returns

`number`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### getLastError()

> **getLastError**(): `string`

**`Internal`**

**Function to get the description of the last error that occurred.**  

This function is for internal use only!

#### Returns

`string`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### runTest()

> **runTest**(`checkIgnoreParams?`): `boolean`

**`Internal`**

**Start test.**  

This function is for internal use only!

#### Parameters

##### checkIgnoreParams?

`boolean`

**Default:** `true`

#### Returns

`boolean`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### setIngoreOids()

> **setIngoreOids**(`ingoreOids`): `boolean`

**`Internal`**

**Set the ingoreOids for an operation.**  

This function is for internal use only!

#### Parameters

##### ingoreOids

`number`[]

Array with ignore oids out

#### Returns

`boolean`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### setIngoreParams()

> **setIngoreParams**(`ignoreParams`): `boolean`

**`Internal`**

**Set the ignoreParams for an operation.**  

This function is for internal use only!

#### Parameters

##### ignoreParams

`number`[]

Array with ignore params out

#### Returns

`boolean`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### setInOids()

> **setInOids**(`inOids`): `boolean`

**`Internal`**

**Set the inOids for an operation.**  

This function is for internal use only!

#### Parameters

##### inOids

`number`[]

Array with the inOids

#### Returns

`boolean`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### setInParam()

> **setInParam**(`inParams`): `boolean`

**`Internal`**

**Set the inParams for an operation.**  

This function is for internal use only!

#### Parameters

##### inParams

`number`[]

Array with the inParams

#### Returns

`boolean`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### setMustOutOids()

> **setMustOutOids**(`outOids`): `boolean`

**`Internal`**

**Set the must outOids for an operation.**  

This function is for internal use only!

#### Parameters

##### outOids

`number`[]

Array with the must outOids

#### Returns

`boolean`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### setMustOutParams()

> **setMustOutParams**(`outParams`): `boolean`

**`Internal`**

**Set the must outParams for an operation.**  

This function is for internal use only!

#### Parameters

##### outParams

`number`[]

Array with the must outParams

#### Returns

`boolean`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### setMustReturnValue()

> **setMustReturnValue**(`value`): `boolean`

**`Internal`**

**Set the must return value for an operation.**  

This function is for internal use only!

#### Parameters

##### value

`number`

Must value

#### Returns

`boolean`

#### Since

ELC 3.60e / otrisPORTAL 6.0e
