[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / DOMNode

# Interface: DOMNode

**DOMNode is the base class of all tree elements in a DOMDocument.**  

DOMNodes cannot be created with `new`. Different create methods of DOMDocument can be used to create different types of nodes. 
As an exception the subclasses DOMDocument and DOMDocumentType have a constructor.  

**Note:** Accessing any node may generate a JavaScript error, when the owning document has been deleted or "garbage collected". See the negative example at class DOMDocument.

**Remarks about W3C conformity**  

The class widely conforms to the Node interface of DOM level 2. Only the function isSupported() does not work as expected. It should not be used.   
The above-mentioned constructors of DOMDocument and DOMDocumentType are non-standard. They are a simplifying substitute of the unsupported standard interface `DOMImplementation`.  
  
**Since:** DOCUMENTS 5.0f (DOM level 2)

## Since

DOCUMENTS 4.0c (DOM level 1)

## Properties

### attributes

> **attributes**: [`DOMNamedNodeMap`](DOMNamedNodeMap.md)

**A map of DOM attributes. If this node is not a [DOMElement](DOMElement.md), the value is `null`. The property is readonly.**

***

### childNodes

> **childNodes**: `DOMNode`[]

**A list of all children of this node. The property is readonly.**

***

### firstChild

> **firstChild**: `DOMNode`

**The first child node, otherwise `null`. The property is readonly.**

***

### lastChild

> **lastChild**: `DOMNode`

**The last child node, otherwise `null`. The property is readonly.**

***

### localName

> **localName**: `string`

**The local part of the qualified name of this node.**  

This property is readonly.  

**Note:** For nodes of any type other than ELEMENT_NODE and ATTRIBUTE_NODE and nodes created with a DOM Level 1 method, 
such as [DOMDocument.createElement()](../classes/DOMDocument.md#createelement), this is always `null`.

#### Since

DOCUMENTS 5.0f

***

### namespaceURI

> **namespaceURI**: `string`

**The namespace URI of this node, or `null` if it is unspecified.**  

This property is readonly.  

**Note:** This is not a computed value that is the result of a namespace lookup based on an examination of the namespace declarations in scope. 
It is merely the namespace URI given at creation time. Per the "Namespaces in XML" Specification an attribute does not inherit its namespace 
from the element it is attached to. If an attribute is not explicitly given a namespace, it simply has no namespace.  

**Note:** For nodes of any type other than ELEMENT_NODE and ATTRIBUTE_NODE and nodes created with a DOM Level 1 method, 
such as [DOMDocument.createElement()](../classes/DOMDocument.md#createelement), this is always `null`.

#### Since

DOCUMENTS 5.0f

***

### nextSibling

> **nextSibling**: `DOMNode`

**The next sibling node, otherwise `null`. The property is readonly.**

***

### nodeName

> **nodeName**: `string`

**The name of this node. The property is readonly.**

***

### nodeType

> **nodeType**: `number`

**The type or subclass of a this node, encoded as an integer. The property is readonly.**

***

### nodeValue

> **nodeValue**: `string`

**The value of the node, which depends on the type.**  

For several node types, the value is constantly an empty string. 
See also the [W3C documentation in the internet](http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113/core.html).

***

### ownerDocument

> **ownerDocument**: [`DOMDocument`](../classes/DOMDocument.md)

**The document, which owns this node. The property is readonly.**

***

### parentNode

> **parentNode**: `DOMNode`

**The parent node or `null`. The property is readonly.**

***

### prefix

> **prefix**: `string`

**The namespace prefix of this node, or `null` if it is unspecified.**  

**Note:** Note that setting this attribute, when permitted, changes the [nodeName](#nodename) attribute, which holds the qualified name, 
as well as the [DOMElement.tagName](DOMElement.md#tagname) and [DOMAttr.name](DOMAttr.md#name) attributes, when applicable. Note also that changing the prefix of an attribute 
that is known to have a default value, does not make a new attribute with the default value and the original prefix appear, 
since the namespaceURI and localName do not change.  

**Note:** For nodes of any type other than ELEMENT_NODE and ATTRIBUTE_NODE and nodes created with a DOM Level 1 method, 
such as[DOMDocument.createElement()](../classes/DOMDocument.md#createelement), this is always `null`.

#### Since

DOCUMENTS 5.0f

***

### previousSibling

> **previousSibling**: `DOMNode`

**The previous sibling node, otherwise `null`. The property is readonly.**

## Methods

### appendChild()

> **appendChild**(`newChild`): `DOMNode`

**Append a new node to the list of child nodes.**

#### Parameters

##### newChild

`DOMNode`

The DOMNode to append.

#### Returns

`DOMNode`

The node added.

#### Since

DOCUMENTS 4.0c

#### Throws

***

### cloneNode()

> **cloneNode**(`deep`): `DOMNode`

**Create a duplicate of this node.**  

**Note:** The returned node initially has not got a parent.

#### Parameters

##### deep

`boolean`

`true` to clone also the whole subtree, `false` to clone only the node (including the attributes, if it is a DOMElement).

#### Returns

`DOMNode`

The copy. The actual type equals the type of `this`.

#### Since

DOCUMENTS 4.0c

#### See

[DOMDocument.importNode(DOMNode source, boolean deep)](../classes/DOMDocument.md#importnode) to copy nodes from another document.

***

### hasAttributes()

> **hasAttributes**(): `boolean`

**Test, whether a node has got any associated attributes.**

#### Returns

`boolean`

#### Since

DOCUMENTS 4.0c

***

### hasChildNodes()

> **hasChildNodes**(): `boolean`

**Test, whether a node has got any associated child nodes.**

#### Returns

`boolean`

#### Since

DOCUMENTS 4.0c

***

### insertBefore()

> **insertBefore**(`newChild`, `refChild`): `DOMNode`

**Insert a new node into the list of child nodes.**

#### Parameters

##### newChild

`DOMNode`

The DOMNode to insert.

##### refChild

`DOMNode`

An existing DOMNode, which already is a child of `this`, and which shall become the next sibling of `newChild`.

#### Returns

`DOMNode`

The node inserted.

#### Since

DOCUMENTS 4.0c

#### Throws

***

### isSupported()

> **isSupported**(`feature`, `version`): `boolean`

**`Internal`**

* ***  
Internal: Tests whether the DOM implementation implements a specific feature and that feature is supported by this node.

#### Parameters

##### feature

`string`

The name of the feature to test.

##### version

`string`

String with the the version number of the feature to test. In Level 2, version 1, this is "2.0". If the version is not specified, 
supporting any version of the feature will cause the method to return `true`.

#### Returns

`boolean`

***

### normalize()

> **normalize**(): `void`

**Normalize the node ans its subtree.**  

This method restructures a DOMDocument (or a subtree of it) as if the document was written to a string and reparsed from it. 
Subsequent "Text" nodes without any interjacent markup are combined into one node, for example.

#### Returns

`void`

#### Since

DOCUMENTS 4.0c

***

### removeChild()

> **removeChild**(`oldChild`): `DOMNode`

**Remove a node from the list of child nodes.**

#### Parameters

##### oldChild

`DOMNode`

The child DOMNode being removed.

#### Returns

`DOMNode`

The node removed.

#### Since

DOCUMENTS 4.0c

#### Throws

***

### replaceChild()

> **replaceChild**(`newChild`, `oldChild`): `DOMNode`

**Replace a node in the list of child nodes.**

#### Parameters

##### newChild

`DOMNode`

The DOMNode to insert.

##### oldChild

`DOMNode`

The child DOMNode being replaced.

#### Returns

`DOMNode`

The node replaced.

#### Since

DOCUMENTS 4.0c

#### Throws

## Node Type Constants

These constants build an enumeration of the possible values of the property nodeType. The constants are also properties of the constructor, 
so it is possible to read them in the style `DOMNode.ELEMENT_NODE`.

### ATTRIBUTE\_NODE

> **ATTRIBUTE\_NODE**: `number`

Constant for the nodeType "Attr". The actual subclass is [DOMAttr](DOMAttr.md).

***

### CDATA\_SECTION\_NODE

> **CDATA\_SECTION\_NODE**: `number`

Constant for the nodeType "CDATASection". The actual subclass is [DOMCharacterData](DOMCharacterData.md), differing from the standard.

***

### COMMENT\_NODE

> **COMMENT\_NODE**: `number`

Constant for the nodeType "Comment". The actual subclass is [DOMCharacterData](DOMCharacterData.md), differing from the standard.

***

### DOCUMENT\_FRAGMENT\_NODE

> **DOCUMENT\_FRAGMENT\_NODE**: `number`

Constant for the nodeType "DocumentFragment". The actual implementation does not provide a subclass for this type.

***

### DOCUMENT\_NODE

> **DOCUMENT\_NODE**: `number`

Constant for the nodeType "Document". The actual subclass is [DOMDocument](../classes/DOMDocument.md).

***

### DOCUMENT\_TYPE\_NODE

> **DOCUMENT\_TYPE\_NODE**: `number`

Constant for the nodeType "DocumentType". The actual subclass is [DOMDocumentType](../classes/DOMDocumentType.md).

***

### ELEMENT\_NODE

> **ELEMENT\_NODE**: `number`

Constant for the nodeType "Element". The actual subclass is [DOMElement](DOMElement.md).

***

### ENTITY\_NODE

> **ENTITY\_NODE**: `number`

Constant for the nodeType "Entity".  The actual subclass is [DOMEntity](DOMEntity.md).

***

### ENTITY\_REFERENCE\_NODE

> **ENTITY\_REFERENCE\_NODE**: `number`

Constant for the nodeType "EntityReference". The actual implementation does not provide a subclass for this type.

***

### NOTATION\_NODE

> **NOTATION\_NODE**: `number`

Constant for the nodeType "Notation". The actual subclass is [DOMEntity](DOMEntity.md), differing from the standard.

***

### PROCESSING\_INSTRUCTION\_NODE

> **PROCESSING\_INSTRUCTION\_NODE**: `number`

Constant for the nodeType "ProcessingInstruction". The actual subclass is [DOMProcessingInstruction](DOMProcessingInstruction.md).

***

### TEXT\_NODE

> **TEXT\_NODE**: `number`

Constant for the nodeType "Text". The actual subclass is [DOMCharacterData](DOMCharacterData.md), differing from the standard.
