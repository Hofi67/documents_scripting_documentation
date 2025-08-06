[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / DOMEntity

# Interface: DOMEntity

**Objects of this class represent either an entity in an XML document or a notation in a DTD.**  

If the inherited attribute [DOMNode.nodeType](DOMNode.md#nodetype) equals [DOMNode.ENTITY\_NODE](DOMNode.md#entity_node) the object represents an entity, either parsed or unparsed, in an XML document. 
This models the entity itself not the entity declaration.   
The [DOMNode.nodeName](DOMNode.md#nodename) attribute contains the name of the entity. If the inherited attribute DOMNode.nodeType equals DOMNode.NOTATION_NODE the object represents 
a notation declared in the DTD. A notation either declares, by name, the format of an unparsed entity (according to section 4.7 of the XML 1.0 specification), 
or is used for formal declaration of processing instruction targets (according to section 2.6 of the XML 1.0 specification). The DOMNode.nodeName attribute is 
set to the declared name of the notation.  

**Note:** If an entity contains an unbound namespace prefix, the namespaceURI of the corresponding node in the Entity node subtree is `null`. 
The same is true for EntityReference nodes that refer to this entity, when they are created using 
the [DOMDocument.createEntityReference()](../classes/DOMDocument.md#createentityreference) method. The DOM Level 2 does not support any mechanism to resolve namespace prefixes.  

**Note:** An XML processor may choose to completely expand entities before the structure model is passed to the DOM. In this case there will 
be no EntityReference nodes in the document tree. XML does not mandate that a non-validating XML processor read and process entity declarations 
made in the external subset or declared in external parameter entities. This means that parsed entities declared in the external subset need not 
be expanded by some classes of applications, and that the replacement value of the entity may not be available. When the replacement value is available, 
the corresponding Entity node's child list represents the structure of that replacement text. Otherwise, the child list is empty. The DOM Level 2 does 
not support editing Entity nodes; if a user wants to make changes to the contents of an Entity, every related EntityReference node has to be replaced 
in the structure model by a clone of the Entity's contents, and then the desired changes must be made to each of those clones instead. Entity nodes and 
all their descendants are readonly. Entity nodes and notation nodes do not have any parent.**Remarks about W3C conformity**  

This API omits a separate class "DOMNotation" to avoid code duplication. Differing from the W3C standard the DOMEntity class is also used for notation nodes. 
To distinguish notation nodes from other nodes scripts can compare the attribute DOMNode.nodeType with the constant DOMNode.NOTATION_NODE.

## Since

DOCUMENTS 5.0f

## Properties

### notationName

> **notationName**: `string`

**For unparsed entities, the name of the notation for the entity.**  

For parsed entities this is `null`. For notation nodes the value is `undefined`.   
This property is readonly.

***

### publicId

> **publicId**: `string`

**The public identifier associated with the (entity or notation) node, if specified.**  

If the public identifier was not specified, this is `null`. This property is readonly.

***

### systemId

> **systemId**: `string`

**The system identifier associated with the (entity or notation) node, if specified.**  

If the system identifier was not specified, this is `null`. This property is readonly.
