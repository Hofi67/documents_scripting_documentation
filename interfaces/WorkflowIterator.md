[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / WorkflowIterator

# Interface: WorkflowIterator

**An Iterator over a list of [Workflow](Workflow.md) objects.**  

You may create Workflowterator objects by the method getAllWorklows() described in the [Context](Context.md) chapter.  

**Note:** This class is designed for usage with a a full workflow engine license. Pure distribution lists can also be enumerated by a WorkflowIterator, 
but such Workflow objects have got very limited capabilities. For the most part they only contain a name.

## Since

DOCUMENTS 6.0

## Example

```ts
// Log the names of all worklows and all distribution lists.
let it = context.getAllWorkflows(3);
for (let wfobj of it)
{
  let wfname = wfobj.name;
  let ver = wfobj.version;
  if(ver !== "")
    wfname += " (Version: " + ver + ")";
   util.out(wfname);
}
```

## Methods

### first()

> **first**(): [`Workflow`](Workflow.md)

**Retrieve the first [Workflow](Workflow.md) object in the WorkflowIterator.**  

**Note:** The function silently skips Worklows, which have been deleted since the iterator's creation time. So the result can occasionally 
be null even if size() returns a value greater than 0.

#### Returns

[`Workflow`](Workflow.md)

Workflow or `null` in case of an empty WorkflowIterator

#### Since

DOCUMENTS 6.0

***

### next()

> **next**(): [`Workflow`](Workflow.md)

**Retrieve the next [Workflow](Workflow.md) object in the WorkflowIterator.**  

**Note:** The function silently skips Worklows, which have been deleted since the iterator's creation time. So the total count of objects returned 
by first() and next() can occasionally be less than the retunr value of size()

#### Returns

[`Workflow`](Workflow.md)

Workflow or `null` if end of the iterator is reached.

#### Since

DOCUMENTS 6.0

***

### size()

> **size**(): `number`

**Get the amount of [Workflow](Workflow.md) objects in the WorkflowIterator.**

#### Returns

`number`

integer value with the amount of Workflow objects in the WorkflowIterator

#### Since

DOCUMENTS 6.0
