[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / DOMNamedNodeMap

# Interface: DOMNamedNodeMap

**A DOMNamedNodeMap is a kind of index for a set of DOMNodes, in which each node has got a unique name.**  

The attributes of a DOMElement are organized in a DOMNamedNodeMap. See DOMElement.attributes. The attached nodes can 
be accessed either by the name or by an integer index. When using an index, the output order of the nodes is not determined. 
Objects of this class cannot be created directly.
**Remarks about W3C conformity**  
This class conforms to the NamedNodeMap interface of DOM level 2.  
  
**Since:** DOCUMENTS 5.0f (DOM level 2)

## Since

DOCUMENTS 4.0c (DOM level 1)

## Properties

### length

> **length**: `number`

**The number of nodes in the map.**  

This property is readonly.

#### Since

DOCUMENTS 4.0c

## Methods

### getNamedItem()

> **getNamedItem**(`name`): [`DOMNode`](DOMNode.md)

**Get a node from the map by its unique name.**

#### Parameters

##### name

`string`

The name.

#### Returns

[`DOMNode`](DOMNode.md)

The node, respectively `null`, if no node with the name is in the map.

#### Since

DOCUMENTS 4.0c

***

### getNamedItemNS()

> **getNamedItemNS**(`namespaceURI`, `localName`): [`DOMNode`](DOMNode.md)

**Retrieves a node specified by local name and namespace URI.**

#### Parameters

##### namespaceURI

`string`

The namespace URI of the node to retrieve.

##### localName

`string`

The local name of the node to retrieve.

#### Returns

[`DOMNode`](DOMNode.md)

A DOMNode (of any type) with the specified local name and namespace URI, or `null` if they do not identify any node in this map.

#### Since

DOCUMENTS 5.0f

***

### item()

> **item**(`index`): [`DOMNode`](DOMNode.md)

**Get the a node from the map at a certain position.**  

This is useful only to iterate over all nodes in the map.  

**Note:** It is also possible to access the nodes using square brackets, as if the object would be an array.

#### Parameters

##### index

`number`

the zero based index of the element.

#### Returns

[`DOMNode`](DOMNode.md)

The requested DOMNode Object. If the index is invalid, the method returns `null`.

#### Since

DOCUMENTS 4.0c

***

### removeNamedItem()

> **removeNamedItem**(`name`): [`DOMNode`](DOMNode.md)

**Remove a node from the map.**

#### Parameters

##### name

`string`

The unique node name.

#### Returns

[`DOMNode`](DOMNode.md)

The removed node.

#### Since

DOCUMENTS 4.0c

#### Throws

***

### removeNamedItemNS()

> **removeNamedItemNS**(`namespaceURI`, `localName`): [`DOMNode`](DOMNode.md)

**Removes a node specified by local name and namespace URI.**  

**Note:** A removed attribute may be known to have a default value when this map contains the attributes attached to an element, 
as returned by the DOMNode.attributes attribute. If so, an attribute immediately appears containing the default value as well as 
the corresponding namespace URI, local name, and prefix when applicable.

#### Parameters

##### namespaceURI

`string`

The namespace URI of the node to remove.

##### localName

`string`

The local name of the node to remove.

#### Returns

[`DOMNode`](DOMNode.md)

The node removed from this map, if a node with such a local name and namespace URI exists.

#### Since

DOCUMENTS 5.0f

#### Throws

***

### setNamedItem()

> **setNamedItem**(`arg`): [`DOMNode`](DOMNode.md)

**Add a node to the map or replace an existing one.**

#### Parameters

##### arg

[`DOMNode`](DOMNode.md)

The node to add. The name for indexing is the value of the attribute DOMNode.nodeName,

#### Returns

[`DOMNode`](DOMNode.md)

If a node with the same name has already been added, the method removes that node and returns it. Otherwise it returns `null`.

#### Since

DOCUMENTS 4.0c

#### Throws

***

### setNamedItemNS()

> **setNamedItemNS**(`arg`): [`DOMNode`](DOMNode.md)

**Adds a node using its namespaceURI and localName.**  
If a node with that namespace URI and that local name is already present in this map, it is replaced by the new one.

#### Parameters

##### arg

[`DOMNode`](DOMNode.md)

A node to store in this map. The node will later be accessible using the value of its namespaceURI and localName attributes.

#### Returns

[`DOMNode`](DOMNode.md)

If the new node replaces an existing node the replaced node is returned, otherwise `null` is returned.

#### Since

DOCUMENTS 5.0f

#### Throws
