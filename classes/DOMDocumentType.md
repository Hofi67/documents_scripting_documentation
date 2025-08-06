[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / DOMDocumentType

# Class: DOMDocumentType

This class describes a Document Type Declaration associated with a DOMDocument.  

Each DOMDocument has a doctype attribute whose value is either `null` or a DOMDocumentType object. The DOMDocumentType class provides 
an interface to the list of entities that are defined for the document, and little else. The DOM Level 2 doesn't support editing DocumentType nodes.

**Remarks about W3C conformity**  

DOCUMENTS allows creating DOMDocumentType objects directly with `new`. The constructor function replaces the W3C recommended function 
`DOMImplementation.createDocumentType()`. Nodes listed in the notations property reuse the prototype of DOMEntity. Otherwise this class 
conforms to the DocumentType interface in the W3C DOM level 2 specification.

## Properties

### entities

> **entities**: [`DOMNamedNodeMap`](../interfaces/DOMNamedNodeMap.md)

**A DOMNamedNodeMap containing the general entities, both external and internal, declared in the DTD.**  

Parameter entities are not contained. This property is readonly.  

**Note:** Duplicates are discarded. For example in: 
` <!DOCTYPE ex SYSTEM "ex.dtd" [ <!ENTITY foo "foo"> <!ENTITY bar "bar"> <!ENTITY bar "bar2"> <!ENTITY % baz "baz"> ]> <ex/> 
` the interface provides access to foo and the first declaration of bar but not the second declaration of bar or baz. Every 
node in this map also is an instance of DOMEntity. The DOM Level 2 does not support editing entities, therefore entities cannot be altered in any way.

***

### internalSubset

> **internalSubset**: `string`

**The internal subset as a string.**  

This property is readonly.  

**Note:** The actual content returned depends on how much information is available to the implementation. 
This may vary depending on various parameters, including the XML processor used to build the document.

***

### name

> **name**: `string`

**The name of DTD; i.e., the name immediately following the DOCTYPE keyword.**  

This property is readonly.

***

### notations

> **notations**: [`DOMNamedNodeMap`](../interfaces/DOMNamedNodeMap.md)

**A DOMNamedNodeMap containing the notations declared in the DTD.**  

This property is readonly.  

**Note:** Duplicates are discarded. Every node in this map also implements the Notation interface. 
The DOM Level 2 does not support editing notations, therefore notations cannot be altered in any way.**Remarks about W3C conformity**  

This API omits a separate class "DOMNotation" to avoid code duplication. Differing from the W3C standard the nodes in the returned map 
are DOMEntity instances, having the attribute DOMEntity.notationName set to `undefined`.   
To distinguish notation nodes from other nodes scripts can compare the attribute DOMNode.nodeType with the constant DOMNode.NOTATION_NODE.

***

### publicId

> **publicId**: `string`

**The public identifier of the external subset.**  

This property is readonly.

***

### systemId

> **systemId**: `string`

**The system identifier of the external subset.**  

This property is readonly.

## Constructors

### Constructor

> **new DOMDocumentType**(`qualifiedName`, `publicId`, `systemId`): `DOMDocumentType`

**Creates an empty DocumentType node.**  

Entity declarations and notations are not made available. Entity reference expansions and default attribute additions do not occur. 
It is expected that a future version of the DOM will provide a way for populating a DocumentType.  

**Note:** The returned object can be forwarded to the DOMDocument constructor to create a document with a reference to an external DTD. 
Otherwise there is actually no benefit of creating nodes of this type directly.  
  
**Since:** DOCUMENTS 5.0f

#### Parameters

##### qualifiedName

`string`

String with the qualified name of the document type to be created.

##### publicId

`string`

String with the external subset public identifier.

##### systemId

`string`

String with the external subset system identifier.

#### Returns

`DOMDocumentType`

#### Since

DOCUMENTS 5.0f
