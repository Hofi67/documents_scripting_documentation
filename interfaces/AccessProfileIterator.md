[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / AccessProfileIterator

# Interface: AccessProfileIterator

**This class gives access to the DOCUMENTS access profiles**  

The objects of this class represent lists of [AccessProfile](../classes/AccessProfile.md) objects and allow to loop through such a list of profiles. The following methods return an AccessProfileIterator: 
<ul> 
<li>[Context.getAccessProfiles](Context.md#getaccessprofiles)</li>
<li>[SystemUser.getAccessProfiles](SystemUser.md#getaccessprofiles)</li>
</ul>

## Since

ELC 3.50b / otrisPORTAL 5.0b

## Example

```ts
// take a certain Systemuser object (stored in user) and assign all availabe
// accessprofiles to this user
var itRoles = context.getAccessProfiles();
if (itRoles && itRoles.size() > 0)
{
   for (var ap = itRoles.first(); ap; ap = itRoles.next())
   {
      user.addToAccessProfile(ap); // add user to profile
   }
}
```

## Methods

### first()

> **first**(): [`AccessProfile`](../classes/AccessProfile.md)

**Retrieve the first [AccessProfile](../classes/AccessProfile.md) object in the AccessProfileIterator.**

#### Returns

[`AccessProfile`](../classes/AccessProfile.md)

AccessProfile or `null` in case of an empty AccessProfileIterator

#### Since

ELC 3.50b / otrisPORTAL 5.0b

***

### getLastError()

> **getLastError**(): `string`

**Function to get the description of the last error that occurred.**

#### Returns

`string`

Text of the last error as String

#### Since

ELC 3.50b / otrisPORTAL 5.0b

#### See

[DocFile.getLastError](DocFile.md#getlasterror)

***

### next()

> **next**(): [`AccessProfile`](../classes/AccessProfile.md)

**Retrieve the next [AccessProfile](../classes/AccessProfile.md) object in the AccessProfileIterator.**

#### Returns

[`AccessProfile`](../classes/AccessProfile.md)

AccessProfile or `null` if end of AccessProfileIterator is reached.

#### Since

ELC 3.50b / otrisPORTAL 5.0b

***

### size()

> **size**(): `number`

**Get the amount of [AccessProfile](../classes/AccessProfile.md) objects in the AccessProfileIterator.**

#### Returns

`number`

integer value with the amount of AccessProfile objects in the AccessProfileIterator

#### Since

ELC 3.50b / otrisPORTAL 5.0b
