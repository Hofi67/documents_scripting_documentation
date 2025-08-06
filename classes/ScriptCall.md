[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / ScriptCall

# Class: ScriptCall

This class allows asynchronously calling a script from another script.  

You should deliberate whether a script call can be waitable or not. Only waitable script calls can be managed, 
e.g. waiting for a script call to finish or checking whether a call is still running.  

**Note:** In the called script, which implements an asynchronous task, nested waitable calls should occur rarely. 
Special caution is necessary with regard to the following scenarios.

All of these scenarios carry the risk of a possible deadlock of the server! Since version 5.0i the server tries 
to repel known deadlock conditions by returning or throwing errors.

1. A script runs within a DOCUMENTS search operation. It launches a waitable call. The called script uses a method 
like [Folder.getFiles()](../interfaces/Folder.md#getfiles), which initiates another search operation on behalf of the same user. 
(* Example: a search operation may call an enumeration script to allow translation of technical values into localized values.)

2. Recursive usage: A script launches a waitable call of the same script.

3. Indirect recursive usage: A script launches a waitable call of another script, which recalls the first script. 
The recall is either synchronous or waitable. The recall may also be hidden (in a third script, which is called by an API method, for example).

4. Waitable script calls are used at a high nesting level. The risk of deadlock increases with each level.

5. A script launches 30 or more waitable calls at once, without awaiting previous results. It does not matter 
whether different scripts are called or always the same script. Every called script (or script-instance) subsequently 
launches only one other waitable script call.

6. A script "A" calls a script "B" asynchronously (maybe waitable or not). "B" launches any waitable call. Many instances of 
script "A" are expected to run concurrently, for example when many users perform the same action at once.

The first scenario is a classic example of a deadlock. The calling script already holds the user's search mutex and 
waits for the called script to finish. The called script, however, cannot make progress while the search mutex is locked.

If the caller does not need to access the state or the return value of the called script, the simple solution is 
a detached (not waitable) script call. Otherwise you can avoid this problem by using modules and normal function calls instead of separate scripts.

The only search operations, which can safely be used in the first scenario, are the constructors of the classes [FileResultset](FileResultset.md) 
and [HitResultset](HitResultset.md). They operate isolated from the normal user session.

In the other scenarios the problem can occur, because every waitable call may block a worker thread and the number of worker threads in the server is limited.

In detail: After a successful [launch()](#launch) every waitable call requires a later synchronization, even if the script does not utilize 
the [waitForFinish()](#waitforfinish) method. At the latest when the script run ends, the server will await the end of unfinished waitable 
calls in order to safely free the associated shared memory.

This synchronization often blocks the thread on which the script runs. If the calling script itself was started by a ScriptCall, it runs on 
a worker thread from a limited pool (usually upto 32 threads).

In the worst case the thread pool has already reached its capacity limit and all the threads are blocked. There exists at least one other waitable 
call in the queue, but no thread is ready to process it. The consequence is an infinite wait state.

The scenarios #5 and #6 are critical though the nesting level of waitable calls looks harmless. In these cases the top-level script calls can occupy 
all worker threads before a second-level call gets a chance to run, but all threads will wait for the inner calls. Again: the consequence is an infinite wait state.

## Methods

### addParameter()

> **addParameter**(`name`, `value`): `boolean`

**Add a parameter to the called script.**

#### Parameters

##### name

`string`

String value containing the parameter name.

##### value

`string`

String value containing the parameter value.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0

#### See

[addParameterWithType](#addparameterwithtype)

#### Example

```ts
var call = new ScriptCall("schreiber", "testScript", false);
call.addParameter("testParam", "testValue");
```

***

### addParameterWithType()

> **addParameterWithType**(`name`, `value`, `datatype?`): `boolean`

**Add a parameter to the called script.**

#### Parameters

##### name

`string`

String value containing the parameter name.

##### value

The desired parameter value of the specified data type, e.g. a Date object as value of data type 'Timestamp'.

`string` | `number` | `boolean` | `Date`

##### datatype?

`string`

Optional string specified the data type of the parameter value. If no data type is specified, the data type will 
be determined based on the given value. The following data types are available: 
<ul> 
<li>String </li> 
<li>Bool </li> 
<li>Numeric </li> 
<li>Date </li> 
<li>Timestamp </li> 
</ul>

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0i HF3

#### See

[addParameter](#addparameter)

#### Example

```ts
var call = new ScriptCall("schreiber", "testScript", true);
if (!call.addParameterWithType("testParam", 12, "Numeric"))
   util.out(call.getLastError());
```

***

### getEnumval()

> **getEnumval**(): `string`[]

**Get the return enumval value of the called script.**  

**Note:** This function is only available for a waitable ScriptCall.

#### Returns

`string`[]

The return value as an array if the waitable ScriptCall was successfully completed, otherwise the string "Undefined".

#### Since

DOCUMENTS 5.0 HF2

#### Example

```ts
var call = new ScriptCall("schreiber", "myEnumScript", true);
if (call.launch())
{
  if (call.waitForFinish())
      util.out(call.getEnumval());
}
```

***

### getLastError()

> **getLastError**(`shortMessage?`): `string`

**Get the description of the last error that occurred.**  
 
  
**Since:** DOCUMENTS 5.0g (new parameter shortMessage)

#### Parameters

##### shortMessage?

`boolean`

optional Boolean; removes "Error in function: class.method(): " from the message.  

**Default:** `false`

#### Returns

`string`

Text of the last error as String

#### Since

DOCUMENTS 5.0

#### Example

```ts
var call = new ScriptCall("schreiber", "testScript", true);
if (!call.launch())
  util.out(call.getLastError());
```

***

### getReturnValue()

> **getReturnValue**(): `string`

**Get the return value of the called script.**  

**Note:** This function is only available for a waitable ScriptCall.

#### Returns

`string`

The return value as String if the waitable ScriptCall was successfully completed, otherwise the string "Undefined".

#### Since

DOCUMENTS 5.0

#### Example

```ts
var call = new ScriptCall("schreiber", "testScript", true);
if (call.launch())
{
  if (call.waitForFinish())
      util.out(call.getReturnValue());
}
```

***

### isFinished()

> **isFinished**(): `boolean`

**Check whether the script call was finished.**  

**Note:** This function is only available for a waitable script call.

#### Returns

`boolean`

`true` if the script call is finished, otherwise `false`

#### Since

DOCUMENTS 5.0e HF2

#### See

[ScriptCall.isRunning](#isrunning)

#### Example

```ts
var call = new ScriptCall("schreiber", "testScript", true);
if (!call.launch())
   throw call.getLastError();
while (!call.isFinished())
{
   // do something different
}
// Call is finished and result is available
return call.getReturnValue();
```

***

### isRunning()

> **isRunning**(): `boolean`

**Check whether the script call is actually running.**  

Actually running means, that the script will be executed at this moment (other states are new or queued) 

**Note:** This function is only available for a waitable script call.

#### Returns

`boolean`

`true` if the script call is running, otherwise `false`

#### Since

DOCUMENTS 4.0d

#### See

[ScriptCall.isFinished](#isfinished)

#### Example

```ts
var call = new ScriptCall("schreiber", "testScript", true);
if (call.launch())
{
  if (call.isRunning())
  {
      // do something
  }
}
```

***

### launch()

> **launch**(): `boolean`

**Launch the script call.**  

In case of successful launch the script will be executed in an own context.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 4.0d

#### Example

```ts
var call = new ScriptCall("schreiber", "testScript", true);
if (!call.launch())
  util.out(call.getLastError());
```

***

### setDocFile()

> **setDocFile**(`docFile`): `boolean`

**Set the execution context file of the called script.**

#### Parameters

##### docFile

[`DocFile`](../interfaces/DocFile.md)

DocFile object representing the desired execution context file.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 4.0d

#### See

[context.file](../interfaces/Context.md#file)

#### Example

```ts
var user = context.findSystemUser("schreiber");
var call = new ScriptCall(user, "testScript", true);
var file = context.getFileById("peachit_fi20120000000016");
if (file)
  call.setDocFile(file);
```

***

### setDocument()

> **setDocument**(`doc`): `boolean`

**Set the execution context document of the called script.**

#### Parameters

##### doc

[`Document`](../interfaces/Document.md)

Document object representing the desired execution context document.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 4.0d

#### See

[context.document](../interfaces/Context.md#document)

#### Example

```ts
var call = new ScriptCall("schreiber", "testScript", false);
var file = context.getFileById("peachit_fi20120000000016");
if (file)
{
   var reg = file.getRegisterByName("Doc1");
  if (reg)
  {
      var it = reg.getDocuments();
      if (it.size() > 0)
          call.setDocument(it.first());
}
}
```

***

### setEnumval()

> **setEnumval**(`enumValues`): `boolean`

**Set the enumval value of the called script.**  

**Note:** This function is only available for a waitable enumval ScriptCall.

#### Parameters

##### enumValues

`string`[]

String array containing the desired enumval value.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 6.1.1

#### See

[ScriptCall.getEnumval](#getenumval)  
     [ScriptCall.setRunAsEnumScript](#setrunasenumscript)

#### Example

```ts
var call = new ScriptCall("schreiber", "testScript", true);
call.setRunAsEnumScript(true);
call.setEnumval(["field1", "field2", "field3"]);
```

***

### setEvent()

> **setEvent**(`scriptEvent`): `boolean`

**Set the execution context event of the called script.**

#### Parameters

##### scriptEvent

`string`

String value containing the desired script event of the execution context.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 4.0d

#### See

[context.event](../interfaces/Context.md#event)

#### Example

```ts
var call = new ScriptCall("schreiber", "testScript", false);
call.setEvent("onArchive");
```

***

### setFolder()

> **setFolder**(`folder`): `boolean`

**Set the execution context folder of the called script.**

#### Parameters

##### folder

[`Folder`](../interfaces/Folder.md)

Folder object representing the desired execution context folder.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0d

#### See

[context.folder](../interfaces/Context.md#folder)

#### Example

```ts
var call = new ScriptCall("schreiber", "testScript", false);
call.setFolder(context.folder);
```

***

### setRegister()

> **setRegister**(`register`): `boolean`

**Set the execution context register of the called script.**

#### Parameters

##### register

[`Register`](../interfaces/Register.md)

Register object representing the desired execution context register.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 4.0d

#### See

[context.register](../interfaces/Context.md#register)

#### Example

```ts
var call = new ScriptCall("schreiber", "testScript", false);
var file = context.getFileById("peachit_fi20120000000016");
if (file)
{
   var reg = file.getRegisterByName("Doc1");
   call.setRegister(reg);
}
```

***

### setRunAsEnumScript()

> **setRunAsEnumScript**(`runAsEnumScript`): `boolean`

**Let the called script run as an enumeration script.**  

The global parameter `enumval` is then available in the called script

#### Parameters

##### runAsEnumScript

`boolean`

boolean value.

#### Returns

`boolean`

#### Since

DOCUMENTS 5.0 HF2

#### See

[ScriptCall.getEnumval](#getenumval)

#### Example

```ts
var call = new ScriptCall(context.getSystemUser(), "myEnumScript", true);
call.setRunAsEnumScript(true);
if (!call.launch())
     throw call.getLastError();
call.waitForFinish();
util.out(call.getEnumval());
```

***

### waitForFinish()

> **waitForFinish**(): `boolean`

**Wait for the script call to finish.**  

**Note:** This function is only available for a waitable script call.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 4.0d

#### Example

```ts
var call = new ScriptCall("schreiber", "testScript", true);
if (call.launch())
{
  if (call.waitForFinish())
  {
      // do something
  }
  else
      util.out(call.getLastError());
}
```

## Constructors

### Constructor

> **new ScriptCall**(`systemUser`, `scriptName`, `waitable`): `ScriptCall`

**Create a new ScriptCall object.**  

The following properties of the execution context of the called script are carried over from the execution context of the script 
where this ScriptCall object is created: 
<ul> 
<li>file </li> 
<li>register </li> 
<li>document </li> 
<li>event </li> 
</ul> 
You can change these context properties with the available set-methods.  
  
**Since:** DOCUMENTS 4.0d

#### Parameters

##### systemUser

`any`

The system user who triggers execution of the called script and can be specified as follows: 
<ul> 
<li>String containing the login name of the system user. </li> 
<li>SystemUser object representing the system user. </li> 
</ul>

##### scriptName

`string`

String with the name of the called script.

##### waitable

`boolean`

boolean flag indicating whether this script call is waitable.

#### Returns

`ScriptCall`

#### Since

DOCUMENTS 4.0d
