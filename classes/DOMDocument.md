[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / DOMDocument

# Class: DOMDocument

The DOMDocument is the root of a DOM tree.  

The constructor of this class always creates an empty document structure. Use the class DOMParser to obtain the structure of an existing XML. 
To create any new child nodes, a script must call the appropriate create method of the DOMDocument. It is not possible to create child nodes standalone.

After a DOMDocument has been deleted by the scripting engine's garbage collector, accessing any nodes and lists of that document may issue an error. 
You should avoid code like the following.

```js
function buildSomeElement()
{
  var domDoc = new DOMDocument("root");
  var someElement = domDoc.createElement("Test");
  // This is an error: Some operations on the DOMElement may no
  // longer work, when the owning DOMDocument has already died.
  return someElement;
}
```

**Remarks about W3C conformity**  

The class covers most of the Document interface of DOM level 2, but the following properties and functions have not been implemented.
<ul>
<li>DOMImplementation implementation</li>
</ul>  

**Since:** DOCUMENTS 5.0f (DOM level 2 core support)

## Properties

### doctype

> **doctype**: [`DOMDocumentType`](DOMDocumentType.md)

**The Document Type Declaration (see DOMDocumentType) associated with this document.**  

For documents without a document type declaration the value is `null`. This property is readonly.  

**Note:** The DOM Level 2 does not support editing the Document Type Declaration. doctype cannot be altered in any way, 
including through the use of methods inherited from the DOMNode interface.

#### Since

DOCUMENTS 5.0f

***

### documentElement

> **documentElement**: [`DOMElement`](../interfaces/DOMElement.md)

**The node, which represents the outermost structure element of the document.**  

This property is readonly.  

**Note:** Unlike written in older versions of this document, the documentElement is not necessarily the first child of the DOMDocument. 
A DocumentType node, for example, may precede it in the list of direct children.

#### Since

DOCUMENTS 4.0d

## Methods

### createAttribute()

> **createAttribute**(`name`): [`DOMAttr`](../interfaces/DOMAttr.md)

**Create a new atttribute within this document.**

#### Parameters

##### name

`string`

The name of the attribute.

#### Returns

[`DOMAttr`](../interfaces/DOMAttr.md)

A new DOMAttr object, which may initially appear anywhere or nowhere in the DOM tree.

#### Since

DOCUMENTS 4.0c

#### Throws

#### See

[DOMElement.setAttributeNode()](../interfaces/DOMElement.md#setattributenode) to place the node within the tree.

***

### createAttributeNS()

> **createAttributeNS**(`namespaceURI`, `qualifiedName`): [`DOMElement`](../interfaces/DOMElement.md)

**Creates a DOMAttr of the given qualified name and namespace URI.**  

**Note:** The new object is initialized with the following attributes.

| Attribute            | Value                                                                  |
|----------------------|------------------------------------------------------------------------|
| DOMNode.nodeName     | qualifiedName                                                          |
| DOMNode.namespaceURI | namespaceURI                                                           |
| DOMNode.prefix       | prefix, extracted from qualifiedName, or `null` if there is no prefix  |
| DOMNode.localName    | local name, extracted from qualifiedName                               |
| DOMAttr.name         | qualifiedName                                                          |
| DOMNode.nodeValue    | the empty string                                                       |

#### Parameters

##### namespaceURI

`string`

The namespace URI (String) of the attribute to create

##### qualifiedName

`string`

The qualified name (String) of the attribute to instantiate.

#### Returns

[`DOMElement`](../interfaces/DOMElement.md)

A new DOMAttr object.

#### Since

DOCUMENTS 5.0f

#### Throws

***

### createCDATASection()

> **createCDATASection**(`data`): [`DOMCharacterData`](../interfaces/DOMCharacterData.md)

**Create a new CDATA section within this document.**  

**Remarks about W3C conformity**  
The W3C specifies the return type as "CDATASection". Considering code size the actual API omits a class CDATASection 
and presents the only additional member (splitText(), inherited from "Text") directly in the second level base class. 
Scripts can examine [DOMNode.nodeType](../interfaces/DOMNode.md#nodetype) to distinguish different types of character data, if necessary.

#### Parameters

##### data

`string`

The data for the node

#### Returns

[`DOMCharacterData`](../interfaces/DOMCharacterData.md)

A new DOMCharacterData object, which may initially appear anywhere or nowhere in the DOM tree.

#### Since

DOCUMENTS 4.0c

#### Throws

#### See

[DOMNode.appendChild](../interfaces/DOMNode.md#appendchild) and [DOMNode.insertBefore](../interfaces/DOMNode.md#insertbefore) to place the node within the tree.

***

### createComment()

> **createComment**(`data`): [`DOMCharacterData`](../interfaces/DOMCharacterData.md)

**Create a new comment node within this document.**  

**Remarks about W3C conformity**  
The W3C specifies the return type as "Comment". Considering code size the actual API omits a class DOMComment, 
which would not get any more members apart from the inherited ones. Scripts can examine [DOMNode.nodeType](../interfaces/DOMNode.md#nodetype) to 
distinguish different types of character data, if necessary.

#### Parameters

##### data

`string`

The data for the node

#### Returns

[`DOMCharacterData`](../interfaces/DOMCharacterData.md)

A new DOMCharacterData object, which may initially appear anywhere or nowhere in the DOM tree.

#### Since

DOCUMENTS 4.0c

#### See

[DOMNode.appendChild](../interfaces/DOMNode.md#appendchild) and [DOMNode.insertBefore](../interfaces/DOMNode.md#insertbefore) to place the node within the tree.

***

### createDocumentFragment()

> **createDocumentFragment**(): [`DOMNode`](../interfaces/DOMNode.md)

**Creates an empty DocumentFragment object.**  

**Remarks about W3C conformity**  
The interface "DocumentFragment" in the "W3C DOM level 2 core" is virtually the same as "Node". This API omits 
a separate class "DOMDocumentFragment" to avoid code duplication. If a script needs to distinguish document fragments 
from other nodes, it can compare [DOMNode.nodeType](../interfaces/DOMNode.md#nodetype) with the constant [DOMNode.DOCUMENT\_FRAGMENT\_NODE](../interfaces/DOMNode.md#document_fragment_node).

#### Returns

[`DOMNode`](../interfaces/DOMNode.md)

A DOMNode object, representing the new DocumentFragment

#### Since

DOCUMENTS 5.0f

***

### createElement()

> **createElement**(`tagName`): [`DOMElement`](../interfaces/DOMElement.md)

**Create a new DOMElement within this document.**

#### Parameters

##### tagName

`string`

The name of the element.

#### Returns

[`DOMElement`](../interfaces/DOMElement.md)

A new DOMElement, which may initially appear anywhere or nowhere in the DOM tree.

#### Since

DOCUMENTS 4.0c

#### Throws

#### See

[DOMNode.appendChild](../interfaces/DOMNode.md#appendchild) and [DOMNode.insertBefore](../interfaces/DOMNode.md#insertbefore) to place the node within the tree.

***

### createElementNS()

> **createElementNS**(`namespaceURI`, `qualifiedName`): [`DOMElement`](../interfaces/DOMElement.md)

**Creates an element of the given qualified name and namespace URI.**  

**Note:** The new element is initialized with the following attributes.

| Attribute            | Value                                                                  |
|----------------------|------------------------------------------------------------------------|
| DOMNode.nodeName     | qualifiedName                                                          |
| DOMNode.namespaceURI | namespaceURI                                                           |
| DOMNode.prefix       | prefix, extracted from qualifiedName, or `null` if there is no prefix  |
| DOMNode.localName    | local name, extracted from qualifiedName                               |
| DOMElement.tagName   | qualifiedName                                                          |

#### Parameters

##### namespaceURI

`string`

The namespace URI (String) of the element to create

##### qualifiedName

`string`

The qualified name (String) of the element to instantiate.

#### Returns

[`DOMElement`](../interfaces/DOMElement.md)

A new DOMElement object.

#### Since

DOCUMENTS 5.0f

#### Throws

***

### createEntityReference()

> **createEntityReference**(`name`): [`DOMNode`](../interfaces/DOMNode.md)

**Creates an EntityReference object.**  

In addition, if the referenced entity is known, the child list of the EntityReference node is made the same as that of the corresponding Entity node.  

**Note:** If any descendant of the Entity node has an unbound namespace prefix, the corresponding descendant of the created EntityReference node is 
also unbound (its namespaceURI is null). The DOM Level 2 does not support any mechanism to resolve namespace prefixes.**Remarks about W3C conformity**  

The interface "EntityReference" in the "W3C DOM level 2 core" is virtually the same as "Node". This API omits a separate class "DOMEntityReference" 
to avoid code duplication. If a script needs to distinguish entity references from other nodes, it can compare [DOMNode.nodeType](../interfaces/DOMNode.md#nodetype) 
with the constant [DOMNode.ENTITY\_REFERENCE\_NODE](../interfaces/DOMNode.md#entity_reference_node).

#### Parameters

##### name

`string`

The name of the entity to reference.

#### Returns

[`DOMNode`](../interfaces/DOMNode.md)

A DOMNode object representing the new EntityReference

#### Since

DOCUMENTS 5.0f

#### Throws

***

### createProcessingInstruction()

> **createProcessingInstruction**(`target`, `data`): [`DOMProcessingInstruction`](../interfaces/DOMProcessingInstruction.md)

**Creates a DOMProcessingInstruction node given the specified name and data strings.**

#### Parameters

##### target

`string`

The target part of the processing instruction.

##### data

`string`

The data for the node.

#### Returns

[`DOMProcessingInstruction`](../interfaces/DOMProcessingInstruction.md)

DOMProcessingInstruction The new object

#### Since

DOCUMENTS 5.0f

#### Throws

***

### createTextNode()

> **createTextNode**(`data`): [`DOMCharacterData`](../interfaces/DOMCharacterData.md)

**Create a new text node within this document.**  

**Remarks about W3C conformity**  
The W3C specifies the return type as "Text". Considering code size the actual API omits a class DOMText 
and presents the only additional member (splitText()) directly in the base class. Scripts can examine 
[DOMNode.nodeType](../interfaces/DOMNode.md#nodetype) to distinguish different types of character data, if necessary.

#### Parameters

##### data

`string`

The data for the node

#### Returns

[`DOMCharacterData`](../interfaces/DOMCharacterData.md)

A new DOMCharacterData object, which may initially appear anywhere or nowhere in the DOM tree.

#### Since

DOCUMENTS 4.0c

#### See

[DOMNode.appendChild](../interfaces/DOMNode.md#appendchild) and [DOMNode.insertBefore](../interfaces/DOMNode.md#insertbefore) to place the node within the tree.

***

### getElementById()

> **getElementById**(`elementId`): [`DOMElement`](../interfaces/DOMElement.md)

**Returns the DOMElement whose ID is given by elementId.**  

Returns `null` if no such element exists. Behavior is not defined if more than one element has this ID.  

**Note:** The DOM implementation must have information that says which attributes are of type ID. 
Attributes with the name "ID" are not of type ID unless so defined. Implementations that do not know 
whether attributes are of type ID or not are expected to return `null`.

#### Parameters

##### elementId

`string`

The unique id value for an element.

#### Returns

[`DOMElement`](../interfaces/DOMElement.md)

The matching element.

#### Since

DOCUMENTS 5.0f

***

### getElementsByTagName()

> **getElementsByTagName**(`tagName`): [`DOMNodeList`](../interfaces/DOMNodeList.md)

**List all DOMElements in the document with a certain tag name.**  

The order of the elements in the returned list corresponds to a preorder traversal of the DOM tree.

#### Parameters

##### tagName

`string`

The name to match on. The special value "*" matches all tags.

#### Returns

[`DOMNodeList`](../interfaces/DOMNodeList.md)

A dynamic list of the found elements.

#### Since

DOCUMENTS 4.0c

#### See

[DOMNodeList](../interfaces/DOMNodeList.md)

***

### getElementsByTagNameNS()

> **getElementsByTagNameNS**(`namespaceURI`, `localName`): [`DOMNodeList`](../interfaces/DOMNodeList.md)

**List all DOMElements in the document with a given local name and namespace URI.**  

The order of the elements in the returned list corresponds to a preorder traversal of the DOM tree.

#### Parameters

##### namespaceURI

`string`

The namespace URI of the elements to match on. The special value "*" matches all namespaces.

##### localName

`string`

The local name of the elements to match on. The special value "*" matches all local names.

#### Returns

[`DOMNodeList`](../interfaces/DOMNodeList.md)

A new DOMNodeList object containing all the matched DOMElements.

#### Since

DOCUMENTS 5.0f

***

### importNode()

> **importNode**(`source`, `deep`): [`DOMNode`](../interfaces/DOMNode.md)

**Import a node from another document to this document.**  

The returned node has no parent. Its parentNode is `null`. The source node is not altered or removed from the original document. 
This method creates a new copy of the source node. Additional information is copied as appropriate to the nodeType.  

**Note:** Some node types cannot be imported (a whole DOMDocument for example). Copying child nodes may be restricted or mandatory 
for a specific node type. Further Reading: http://www.w3.org/TR/DOM-Level-2-Core/core.html#Core-Document-importNode

#### Parameters

##### source

[`DOMNode`](../interfaces/DOMNode.md)

The node to copy.

##### deep

`boolean`

Boolean value to request a deep copy with child nodes, if desired.

#### Returns

[`DOMNode`](../interfaces/DOMNode.md)

The imported node that belongs to this document.

#### Since

DOCUMENTS 5.0f

#### Throws

## Constructors

### Constructor

> **new DOMDocument**(`rootElementName`, `namespaceURI`, `doctype`): `DOMDocument`

**Create a new empty XML document structure.**  

**Note:** The namespaceURI parameter is mandatory, if rootElementName includes a namespace prefix. Otherwise it is optional. 
The optional doctype parameter can be used to place a Document Type Declaration in the new document, which may refererence an external DTD. 
The constructor fails, if doctype is already owned by another document. Otherwise the new document takes exclusive ownership of the passed 
object and doctype.ownerDocument is set to the new document.  
  
**Since:** DOCUMENTS 4.0c (restricted DOM level 1 support)  
**Since:** DOCUMENTS 5.0f (parameters namespaceURI and doctype)

#### Parameters

##### rootElementName

`string`

The (qualified) name for the document element.

##### namespaceURI

`string`

The namespace URI of the document element to create. Can be `null` for documents without namespaces.

##### doctype

[`DOMDocumentType`](DOMDocumentType.md)

An optional DOMDocumentType object. See remarks

#### Returns

`DOMDocument`

#### Since

DOCUMENTS 4.0c
