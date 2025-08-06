[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / PropertyCache

# Interface: PropertyCache

**The PropertyCache class is a util class that allows it to store / cache data over the end of the run time of a script.**  

There is exactly one global implicit object of the class `PropertyCache` which is named `propCache`. At the SystemUser and
the AccessProfile are also PropertyCache objects (`SystemUser.propCache`, `AccessProfile.propCache`).

+ You can define named members (properties) at this object to store the data: `propCache.Name1 = one_value;` `propCache.Name2 = another_value;`
+ The stored data can be integer, boolean, string or array values 
+ There is no limit (except the memory of the OS) in the amount of properties or in the length of an array.
+ Every principal has it's own propCache object.

**Note:**  
It is not possible to create objects of the class `PropertyCache`, since the propCache object is always available.

## Example

```ts
// If you have an enumeration field at a filetype and the enumeration
// values (enumval) are defined by a PortalScript, then every time a
// file of that filetype will be displayed, the PortalScript has to be
// excecuted. If now in the PortalScript the enum values are the result
// of a query on a filetype or an external DB (DBResultset), then this
// is a very "expensive" resource. It is recommanded to cache this data.
if (!propCache.hasProperty("Contacts"))
{
   util.out("Creating cache");
   propCache.Contacts = getEmployees();
}
util.out("Using cache");
// copy values to enumval "manually" - concat etc. not possible
// with the global object enumval
copyArray(propCache.Contacts, enumval);
return;
function getEmployees()
{
   var myList = new Array();
   var sort = "hrLastName+,hrFirstName+";
   var it = new FileResultset("ftEmployee", "", sort);
   for (var empl=it.first(); empl; empl=it.next())
      myList.push(empl.hrLastName + ", " + empl.hrFirstName);
   return myList;
}
function copyArray(srcList, trgList)
{
   for (var cnt=0; cnt<srcList.length; cnt++)
      trgList.push(srcList[cnt]);
}
```

## Methods

### hasProperty()

> **hasProperty**(`name`): `boolean`

**Function to check if a named property exists in the PropertyCache.**

#### Parameters

##### name

`string`

#### Returns

`boolean`

`true` if the property exists, `false` if not

#### Since

DOCUMENTS 4.0

***

### listProperties()

> **listProperties**(): `string`[]

**Function to list all properties in the PropertyCache.**

#### Returns

`string`[]

Array with the names of the properties in the PropertyCache.

#### Since

DOCUMENTS 5.0c

***

### removeProperty()

> **removeProperty**(`name`): `boolean`

**Function to delete a named property exists in the PropertyCache.**

#### Parameters

##### name

`string`

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 4.0
