[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / WorkflowStepIterator

# Interface: WorkflowStepIterator

**The WorkflowStepIterator class has been added to the DOCUMENTS PortalScripting API to gain full control over a file's workflow by scripting means.**  

You may access WorkflowStepIterator objects by the getAllLockingWorkflowSteps() method described in the [DocFile](DocFile.md) chapter.  

**Note:** This class and all of its methods and attributes require a full workflow engine license, it does not work with pure distribution lists.

## Since

ELC 3.51e / otrisPORTAL 5.1e

## Methods

### first()

> **first**(): [`WorkflowStep`](WorkflowStep.md)

**Retrieve the first [WorkflowStep](WorkflowStep.md) object in the WorkflowStepIterator.**

#### Returns

[`WorkflowStep`](WorkflowStep.md)

WorkflowStep or `null` in case of an empty WorkflowStepIterator

#### Since

ELC 3.51e / otrisPORTAL 5.1e

***

### next()

> **next**(): [`WorkflowStep`](WorkflowStep.md)

**Retrieve the next [WorkflowStep](WorkflowStep.md) object in the WorkflowStepIterator.**

#### Returns

[`WorkflowStep`](WorkflowStep.md)

WorkflowStep or `null` if end of WorkflowStepIterator is reached.

#### Since

ELC 3.51e / otrisPORTAL 5.1e

***

### size()

> **size**(): `number`

**Get the amount of [WorkflowStep](WorkflowStep.md) objects in the WorkflowStepIterator.**

#### Returns

`number`

integer value with the amount of WorkflowStep objects in the WorkflowStepIterator

#### Since

ELC 3.51e / otrisPORTAL 5.1e
