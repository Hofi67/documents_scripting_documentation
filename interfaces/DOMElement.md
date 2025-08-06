[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / DOMElement

# Interface: DOMElement

**An object of this class represents a HTML or XML element in the DOM.**  

DOMElements cannot be created directly. This applies to almost all kinds of DOMNodes.
**Remarks about W3C conformity**  
The class conforms to the Element interface of DOM level 2.  

**Since:** DOCUMENTS 4.0c (DOM level 1)  
**Since:** DOCUMENTS 5.0f (DOM level 2)

## Since

DOCUMENTS 4.0c

## Properties

### tagName

> **tagName**: `string`

**The name of the element.**  

This property is readonly.

#### Since

DOCUMENTS 4.0c

## Methods

### getAttribute()

> **getAttribute**(`name`): `string`

**Get the string value of an attribute of this element.**

#### Parameters

##### name

`string`

The name of the attribute

#### Returns

`string`

The atrribute's value or the empty string, if the attribute is not specified and has not got a default value.

#### Since

DOCUMENTS 4.0c

***

### getAttributeNode()

> **getAttributeNode**(`name`): [`DOMAttr`](DOMAttr.md)

**Get an attribute of this element.**

#### Parameters

##### name

`string`

The attribute's name

#### Returns

[`DOMAttr`](DOMAttr.md)

The object, which represents the attribute in the DOM. If no attribute of the given name exists, the value is `null`.

***

### getAttributeNodeNS()

> **getAttributeNodeNS**(`namespaceURI`, `localName`): [`DOMAttr`](DOMAttr.md)

**Retrieves a DOMAttr node by local name and namespace URI.**

#### Parameters

##### namespaceURI

`string`

The namespace URI of the attribute to retrieve.

##### localName

`string`

The local name of the attribute to retrieve.

#### Returns

[`DOMAttr`](DOMAttr.md)

The DOMAttr node with the specified local name and namespace URI or `null` if there is no such attribute.

#### Since

DOCUMENTS 5.0f

***

### getAttributeNS()

> **getAttributeNS**(`namespaceURI`, `localName`): `string`

**Retrieves an attribute value by local name and namespace URI.**

#### Parameters

##### namespaceURI

`string`

The namespace URI of the attribute to retrieve.

##### localName

`string`

The local name of the attribute to retrieve.

#### Returns

`string`

The attribute's value as a string, or the empty string if that attribute does not have a specified or default value.

#### Since

DOCUMENTS 5.0f

***

### getElementsByTagName()

> **getElementsByTagName**(`tagName`): [`DOMNodeList`](DOMNodeList.md)

**List all DOMElements in the subtree with a certain tag name.**  

The order of the elements in the returned list corresponds to a preorder traversal of the DOM tree.

#### Parameters

##### tagName

`string`

The name to match on. The special value "*" matches all tags.

#### Returns

[`DOMNodeList`](DOMNodeList.md)

A dynamic list of the found elements.

#### Since

DOCUMENTS 4.0c

#### See

[DOMNodeList](DOMNodeList.md)

***

### getElementsByTagNameNS()

> **getElementsByTagNameNS**(`namespaceURI`, `localName`): [`DOMNodeList`](DOMNodeList.md)

**Returns a DOMNodeList of all the descendant DOMElements with a given local name and namespace URI.**  

The elements are listed in the order in which they are encountered in a preorder traversal of this element tree.

#### Parameters

##### namespaceURI

`string`

The namespace URI of the elements to match on. The special value "*" matches all namespaces.

##### localName

`string`

The local name of the elements to match on. The special value "*" matches all local names.

#### Returns

[`DOMNodeList`](DOMNodeList.md)

A new DOMNodeList object containing all the matched DOMElements.

#### Since

DOCUMENTS 5.0f

***

### hasAttribute()

> **hasAttribute**(`name`): `boolean`

**Test whether an attribute with the given name is specified on this element or has a default value.**

#### Parameters

##### name

`string`

The name of the attribute to look for.

#### Returns

`boolean`

`true` if an attribute with the given name is specified on this element or has a default value, `false` otherwise.

#### Since

DOCUMENTS 5.0f

***

### hasAttributeNS()

> **hasAttributeNS**(`namespaceURI`, `localName`): `boolean`

**Test whether an attribute with the given local name and namespace URI is specified on this element or has a default value.**

#### Parameters

##### namespaceURI

`string`

The namespace URI of the attribute to look for.

##### localName

`string`

The local name of the attribute to look for.

#### Returns

`boolean`

`true` if an attribute with given parameters is specified on this element or has a default value, `false` otherwise.

#### Since

DOCUMENTS 5.0f

***

### removeAttribute()

> **removeAttribute**(`name`): `void`

**Remove an attribute from this element by name.**

#### Parameters

##### name

`string`

The attribute's name

#### Returns

`void`

#### Since

DOCUMENTS 4.0c

#### Throws

***

### removeAttributeNode()

> **removeAttributeNode**(`oldAttr`): [`DOMAttr`](DOMAttr.md)

**Remove an attribute node from this element.**

#### Parameters

##### oldAttr

[`DOMAttr`](DOMAttr.md)

The attribute object to remove

#### Returns

[`DOMAttr`](DOMAttr.md)

The removed attribute node.

#### Since

DOCUMENTS 4.0c

#### Throws

***

### removeAttributeNS()

> **removeAttributeNS**(`namespaceURI`, `localName`): `any`

**Removes an attribute by local name and namespace URI.**  

If the removed attribute has a default value it is immediately replaced. The replacing attribute has the same namespace URI and local name, as well as the original prefix.

#### Parameters

##### namespaceURI

`string`

The namespace URI of the attribute to remove.

##### localName

`string`

The local name of the attribute to remove.

#### Returns

`any`

No return value.

#### Since

DOCUMENTS 5.0f

#### Throws

***

### setAttribute()

> **setAttribute**(`name`, `value`): `void`

**Set an attribute of this element by string.**  

If an attribute of the given name exists, the method only updates its value. Otherwise it creates the attribute.

#### Parameters

##### name

`string`

The attribute's name

##### value

`string`

The new value of the attribute

#### Returns

`void`

#### Since

DOCUMENTS 4.0c

#### Throws

***

### setAttributeNode()

> **setAttributeNode**(`newAttr`): [`DOMAttr`](DOMAttr.md)

**Attach an attribute node to this element.**

#### Parameters

##### newAttr

[`DOMAttr`](DOMAttr.md)

The DOMAttr object, which defines the attribute to add or replace.

#### Returns

[`DOMAttr`](DOMAttr.md)

The formerly attached DOMAttr, if the call has replaced an attribute with the same name. Otherwise the method returns `null`.

#### Since

DOCUMENTS 4.0c

#### Throws

***

### setAttributeNodeNS()

> **setAttributeNodeNS**(`newAttr`): [`DOMAttr`](DOMAttr.md)

**Adds a new attribute.**  

If an attribute with that local name and that namespace URI is already present in the element, it is replaced by the new one.

#### Parameters

##### newAttr

[`DOMAttr`](DOMAttr.md)

The DOMAttr node to add to the attribute list.

#### Returns

[`DOMAttr`](DOMAttr.md)

If the newAttr replaces an existing attribute with the same local name and namespace URI, the replaced DOMAttr node is returned, otherwise `null` is returned.

#### Since

DOCUMENTS 5.0f

#### Throws

***

### setAttributeNS()

> **setAttributeNS**(`namespaceURI`, `qualifiedName`, `value`): `any`

**Adds a new attribute or overwrites it.**  

If an attribute with the same local name and namespace URI is already present on the element, its prefix is changed to be the prefix part of the qualifiedName, 
and its value is changed to be the value parameter.  

**Note:** The assigned value is a simple string; it is not parsed as it is being set. So any markup (such as syntax to be recognized as an entity reference) 
is treated as literal text. In order to assign an attribute value that contains entity references, the user must create a [DOMAttr](DOMAttr.md) node plus any Text and 
EntityReference nodes, build the appropriate subtree, and use [setAttributeNodeNS()](#setattributenodens) or [setAttributeNode()](#setattributenode) 
to assign it as the value of an attribute.

#### Parameters

##### namespaceURI

`string`

The namespace URI of the attribute to create or alter.

##### qualifiedName

`string`

The qualified name of the attribute to create or alter.

##### value

`string`

The value to set in string form.

#### Returns

`any`

No return value.

#### Since

DOCUMENTS 5.0f

#### Throws
