[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / PortalTest

# Interface: PortalTest

**`Internal`**

**The PortalTest class provides functionality for recording the webservers actions against the PortalServer and to replay them 
for automatic testing purposes. The calls of the webserver will be stored in xml-files.**  

This interface is for internal use only!

## Example

```ts
// Recording actions of a remote Portal
try {
   var portalTest = new PortalTest("dbtest", 11000, "peachit");
   portalTest.setRecordingPath("c:\\log");
   portalTest.startRecording();
   PDTools.sleep(60000):  // sleeping 60sec and doing something in the web client
   portalTest.stopRecording();
} catch (exp)
  util.out(exp);
...
try {
   // Replaying recorded actions from the xml-files of a directory
   var xmlDir = "c:\\log";
   var portalTest = new PortalTest("dbtest", 11000, "peachit");
   ...
```

## Methods

### addOperation()

> **addOperation**(`operationName`): `boolean`

**`Internal`**

**Add a opertion to the test.**  

This function is for internal use only!

#### Parameters

##### operationName

`string`

Name of the operation, that should be executed

#### Returns

`boolean`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### createIgnoreParams()

> **createIgnoreParams**(): `boolean`

**`Internal`**

**creates the ignore param lists **  

This function is for internal use only!

#### Returns

`boolean`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### getDiffs()

> **getDiffs**(): `string`

**`Internal`**

**Retrieve the differences after the test run.**  

This function is for internal use only!

#### Returns

`string`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### getLastError()

> **getLastError**(): `string`

**`Internal`**

**Function to get the description of the last error that occurred.**  

This function is for internal use only!

#### Returns

`string`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### isOk()

> **isOk**(): `string`

**`Internal`**

**Function to get the state, if the PortalTest object creation succeeded.**  

This function is for internal use only!

#### Returns

`string`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### runTest()

> **runTest**(`checkIgnoreParams?`): `boolean`

**`Internal`**

**Run the test.**  

This function is for internal use only!

#### Parameters

##### checkIgnoreParams?

`boolean`

**Default:** `true`

#### Returns

`boolean`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### saveDiffs()

> **saveDiffs**(`filePath`): `boolean`

**`Internal`**

**Save the differences after test run in a text file.**  

This function is for internal use only!

#### Parameters

##### filePath

`string`

Filepath for storing the diffs

#### Returns

`boolean`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### setRecordingPath()

> **setRecordingPath**(`path`): `boolean`

**`Internal`**

**Set the path to the directory where the recorded operations should be stored.**  

This function is for internal use only!

#### Parameters

##### path

`string`

Path to the directory

#### Returns

`boolean`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### setRecordXML()

> **setRecordXML**(`filePath`): `boolean`

**`Internal`**

**Set the path to the recorded xml, that should be replayed.**  

This function is for internal use only!

#### Parameters

##### filePath

`string`

Path to the xml-file

#### Returns

`boolean`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### startRecording()

> **startRecording**(`host`, `port`, `principal`, `user`, `passwd`): `boolean`

**`Internal`**

**Start recording operations at the in PortalTest.new() specified server.**  

This function is for internal use only!

#### Parameters

##### host

`string`

Host of local machine (optional)

##### port

`number`

Port of local machine (optional)

##### principal

`string`

Principal of local machine (optional)

##### user

`string`

User of local machine (optional)

##### passwd

`string`

Passwd of local machine (optional)

#### Returns

`boolean`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### stopRecording()

> **stopRecording**(): `boolean`

**`Internal`**

**Stop recording.**  

This function is for internal use only!

#### Returns

`boolean`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### writeJS()

> **writeJS**(`filePath`, `withIgnoreFlags?`): `boolean`

**`Internal`**

**creates a PortalScript / Javascript from the test **  

This function is for internal use only!

#### Parameters

##### filePath

`string`

Filepath for storing the js.

##### withIgnoreFlags?

`boolean`

Should the xml contains the ignore lists  

**Default:** `false`

#### Returns

`boolean`

#### Since

ELC 3.60e / otrisPORTAL 6.0e

***

### writeXML()

> **writeXML**(`filePath`, `withIgnoreFlags?`): `boolean`

**`Internal`**

**Writes the operation xml.**  

This function is for internal use only!

#### Parameters

##### filePath

`string`

Filepath for storing the xml

##### withIgnoreFlags?

`boolean`

Shoud the xml contains the ignore lists  

**Default:** `false`

#### Returns

`boolean`

#### Since

ELC 3.60e / otrisPORTAL 6.0e
