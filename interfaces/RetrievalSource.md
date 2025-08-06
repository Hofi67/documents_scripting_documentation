[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / RetrievalSource

# Interface: RetrievalSource

**This class describes a searchable resource in the DOCUMENTS retrieval system.**

## Since

DOCUMENTS 4.0c HF2

## Properties

### resId

> **resId**: `string`

**A identifier of the resource.**  

For conventional file type resources the identifier equals the technical name of the file type. Archive related identifiers consist of 
a software dependent key or name plus an "@serverName" appendix.  

**Note:** Modifications of this property won't be forwarded to the retrieval system.

#### Since

DOCUMENTS 4.0c

***

### server

> **server**: `string`

**For archive resources: the technical name of the archive server. Otherwise empty.**  

**Note:** Modifications of this property won't be forwarded to the retrieval system.

#### Since

DOCUMENTS 4.0c

***

### type

> **type**: `number`

**The resource type encoded as an integer. See the enumeration constants in this class.**  

**Note:** Modifications of this property won't be forwarded to the retrieval system.

#### Since

DOCUMENTS 4.0c

## Searchable Resource

These constants are equally available in each instance of RetrievalSource and in the constructor object. Resource macroes can only 
occur in the "FillSearchMask" exit. Within an "OnSearch" exit they have already been replaced by their single components.

### MST\_EAS\_ONLY

> `readonly` **MST\_EAS\_ONLY**: `number`

Integer code of the macro source type "EAS only" (Remove standard file type sources after MST_EAS_SERVER macro expansion)  

**Note:** A "FillSearchMask" script can usually find a source of this type, when the user has deselected the "actual processes" checkbox. 
This source has not got any parameters. If there are user accounts in the system, for which the checkbox does not show up, the script code 
should not interpret this source type at all.

***

### MST\_EAS\_SERVER

> `readonly` **MST\_EAS\_SERVER**: `number`

Integer code of the macro source type "EAS server" (Apply selected file types also to the identified EDA-store)

***

### ST\_DLC\_FILETYPE

> `readonly` **ST\_DLC\_FILETYPE**: `number`

Integer code of the source type "DOCUMENTS file type"

***

### ST\_EAS\_FILETYPE

> `readonly` **ST\_EAS\_FILETYPE**: `number`

Integer code of the source type "DOCUMENTS file type within an EAS/EDA store"

***

### ST\_EEI\_ARCHIVE

> `readonly` **ST\_EEI\_ARCHIVE**: `number`

Integer code of the source type "EASY ENTERPRISE.i archive"

***

### ST\_EEX\_USERVIEW

> `readonly` **ST\_EEX\_USERVIEW**: `number`

Integer code of the source type "EASY ENTERPRISE.x user specific view"

***

### ST\_EEX\_VIEW

> `readonly` **ST\_EEX\_VIEW**: `number`

Integer code of the source type "EASY ENTERPRISE.x view"
