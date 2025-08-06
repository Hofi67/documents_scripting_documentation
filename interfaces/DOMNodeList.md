[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / DOMNodeList

# Interface: DOMNodeList

**A dynamic, ordered list of DOMNodes.**  

These lists always reflect the actual state of the DOM tree, which can differ from that state, when the list has been created. 
Getting the nodes from the list works with an integer index in square brackets, as if the list object would be an Array. DOMNodeLists 
cannot be created directly. Some methods or properties of DOMNode and its subclasses can create them.

**Remarks about W3C conformity**  
The class covers the NodeList interface of DOM level 2.

## Since

DOCUMENTS 4.0c

## Properties

### length

> **length**: `number`

**The actual number of nodes in the list.**

#### Since

DOCUMENTS 4.0c

## Methods

### item()

> **item**(`index`): [`DOMNode`](DOMNode.md)

**Returns the element at a certain position.**  

This is just the same as using the square brackets on the object.

#### Parameters

##### index

`number`

The zero-based position of the requested element

#### Returns

[`DOMNode`](DOMNode.md)

The DOMNode at the requested index. In the case of an invalid index the return value is `null`.

#### Since

DOCUMENTS 4.0c
