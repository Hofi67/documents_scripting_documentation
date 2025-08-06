[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / EmailIterator

# Interface: EmailIterator

**The EmailIterator class has been added to the DOCUMENTS PortalScripting API to gain full access to the DOCUMENTS emails by scripting means.**  

The objects of this class represent lists of Email objects and allow to loop through such a list of emails. 
The following method returns an EmailIterator: [context.getMails](Context.md#getmails).

## Since

DOCUMENTS 5.0i

## Example

```ts
var itMail = context.getMails();
if (itMail && itMail.size() > 0)
{
   for (var mail = itMail.first(); mail; mail = itMail.next())
   {
      // do something
   }
}
```

## Methods

### first()

> **first**(): [`Email`](../classes/Email.md)

**Retrieve the first Email object in the EmailIterator.**

#### Returns

[`Email`](../classes/Email.md)

Email or `null` in case of an empty EmailIterator

#### Since

DOCUMENTS 5.0i

***

### next()

> **next**(): [`Email`](../classes/Email.md)

**Retrieve the next Email object in the EmailIterator.**

#### Returns

[`Email`](../classes/Email.md)

Email or `null` if end of EmailIterator is reached.

#### Since

DOCUMENTS 5.0i

***

### size()

> **size**(): `number`

**Get the amount of Email objects in the EmailIterator.**

#### Returns

`number`

integer value with the amount of Email objects in the EmailIterator

#### Since

DOCUMENTS 5.0i
