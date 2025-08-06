[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / DBResultSet

# Interface: DBResultSet

**The DBResultSet class contains a list of resultset rows.**  

You need an active [DBConnection](../classes/DBConnection.md) object to execute an SQL query which is used to create a DBResultSet.  

**Important:** Please consider the restrictions according the order of reading of the columns of the
DBResultSet. Read the example! The following data types for database columns will be supported:

| **SQL data type** | **access method**                                                                                                             |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------|
| SQL_INTEGER       | [getInt()](#getint), [getString()](#getstring)                                            |
| SQL_SMALLINT      | [getInt()](#getint), [getString()](#getstring)                                            |
| SQL_BIGINT        | [getInt()](#getint), [getString()](#getstring)                                            |
| SQL_FLOAT         | [getFloat()](#getfloat), [getInt()](#getint), [getString()](#getstring) |
| SQL_DECIMAL       | [getFloat()](#getfloat), [getInt()](#getint), [getString()](#getstring) |
| SQL_NUMERIC       | [getFloat()](#getfloat), [getInt()](#getint), [getString()](#getstring) |
| SQL_BIT           | [getBool()](#getbool), [getString()](#getstring)                                          |
| SQL_TIMESTAMP     | [getTimestamp()](#gettimestamp), [getString()](#getstring)                                |
| SQL_DATE          | [getDate()](#getdate), [getString()](#getstring)                                          |
| SQL_GUID          | [getString()](#getstring)                                                                                   |
| SQL_VARCHAR       | [getString()](#getstring)                                                                                   |
| SQL_CHAR          | [getString()](#getstring)                                                                                   |
| all other types   | [getString()](#getstring)                                                                                   |
  
**Since:** DOCUMENTS 5.0c HF1 (support for SQL_GUID)

## Since

ELC 3.50 / otrisPORTAL 5.0

## See

[DBConnection](../classes/DBConnection.md)

## Example

```ts
// create DB-Connection to ODBC-64 Datasource "Nordwind"
var myDB = new DBConnection("odbc", "Nordwind");
if (myDB && myDB.getLastError() == null)
{
   var myRS = myDB.executeQuery("SELECT Nachname, Vorname FROM Personal");
   if (myRS)
   {
      // read all persons from the result set
      while (myRS.next())
      {
         var fullName = myRS.getString(0) + ", " + myRS.getString(1);
         // var fullName = myRS.getString(1) + ", " + myRS.getString(0);  // Fails, because you must read the columns in the correct order!
         // var fullName = myRS.getString(0) + ", " + myRS.getString(0);  // Fails, because it is not allowed to read a value twice!
         util.out(fullName);
      }
     // Important: free resource!
     myRS.close()
   }
   else
      util.out("Error in SELECT statement: " + myDB.getLastError());
   // Important: free resource!
   myDB.close();
}
else
   util.out("Error connection the database: " + myDB.getLastError())
```

## Methods

### close()

> **close**(): `boolean`

**Close the DBResultSet and free the server ressources.**  

**Note:** It is strongly recommanded to close each DBResultSet object you have created, since
database connections and resultsets are so-called expensive ressources and should be used carefully.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### See

[DBConnection.close](../classes/DBConnection.md#close)

***

### getBool()

> **getBool**(`colNo`): `boolean`

**Read the indicated column of the current row of the DBResultSet as a boolean value.**

#### Parameters

##### colNo

`number`

integer value (zero based) indicating the desired column of the current row of the DBResultSet

#### Returns

`boolean`

boolean value representing the indicated column of the current row

#### Since

ELC 3.50 / otrisPORTAL 5.0

***

### getColName()

> **getColName**(`colNo`): `string`

**Function returns the name of a column.**

#### Parameters

##### colNo

`number`

integer value (zero based) indicating the desired column

#### Returns

`string`

Column name as String

#### Since

DOCUMENTS 5.0

***

### getDate()

> **getDate**(`colNo`): `Date`

**Read the indicated column of the current row of the DBResultSet as a Date object.**  

**Note:** The return value will be `null` if the content of the indicated column cannot be converted to a Date object.  
**Note:** every value of a DBResultSet can only be read one time and in the correct order!

#### Parameters

##### colNo

`number`

integer value (zero based) indicating the desired column of the current row of the DBResultSet

#### Returns

`Date`

Date object representing the indicated column of the current row or `null` if is null-value

#### Since

ELC 3.50 / otrisPORTAL 5.0

***

### getFloat()

> **getFloat**(`colNo`): `number`

**Read the indicated column of the current row of the DBResultSet as a float value.**  

**Note:** The return value will be NaN if the content of the indicated column cannot be converted to a float value.  
**Note:** every value of a DBResultSet can only be read one time and in the correct order!

#### Parameters

##### colNo

`number`

integer value (zero based) indicating the desired column of the current row of the DBResultSet

#### Returns

`number`

float value representing the indicated column of the current row or `null` if is null-value

#### Since

ELC 3.50 / otrisPORTAL 5.0

***

### getInt()

> **getInt**(`colNo`): `number`

**Read the indicated column of the current row of the DBResultSet as an integer value.**  

**Note:** The return value will be NaN if the content of the indicated column cannot be converted to an integer value.  
**Note:** every value of a DBResultSet can only be read one time and in the correct order!

#### Parameters

##### colNo

`number`

integer value (zero based) indicating the desired column of the current row of the DBResultSet

#### Returns

`number`

integer value representing the indicated column of the current row or `null` if is null-value

#### Since

ELC 3.50 / otrisPORTAL 5.0

***

### getLastError()

> **getLastError**(): `string`

**Function to get the description of the last error that occurred.**

#### Returns

`string`

Text of the last error as String

#### Since

ELC 3.50 / otrisPORTAL 5.0

#### See

[DocFile.getLastError](DocFile.md#getlasterror)

***

### getNumCols()

> **getNumCols**(): `number`

**Function returns the amount of columns of the DBResultSet.**

#### Returns

`number`

Column count as int

#### Since

DOCUMENTS 5.0

***

### getString()

> **getString**(`colNo`): `string`

**Read the indicated column of the current row of the DBResultSet as a String.**  

**Note:** x64/UTF-8 DOCUMENTS version: since DOCUMENTS 4.0a HF2 the method transcode the fetched data to UTF-8  
**Note:** every value of a DBResultSet can only be read one time and in the correct order!

#### Parameters

##### colNo

`number`

integer value (zero based) indicating the desired column of the current row of the DBResultSet

#### Returns

`string`

String representing the indicated column of the current row or `null` if is null-value

#### Since

ELC 3.50 / otrisPORTAL 5.0

***

### getTimestamp()

> **getTimestamp**(`colNo`): `Date`

**Read the indicated column of the current row of the DBResultSet as a Date object including the time.**  

**Note:** The return value will be `null` if the content of the indicated column cannot be converted to a Date object.  
**Note:** every value of a DBResultSet can only be read one time and in the correct order!

#### Parameters

##### colNo

`number`

integer value (zero based) indicating the desired column of the current row of the DBResultSet

#### Returns

`Date`

Date object (including time) representing the indicated column of the current row or `null` if is null-value

#### Since

ELC 3.50 / otrisPORTAL 5.0

***

### ~~getUCString()~~

> **getUCString**(`colNo`): `string`

**Read the indicated column of the current row of the DBResultSet on a x64/UTF-8 DOCUMENTS as a String.**  

**Note:** every value of a DBResultSet can only be read one time and in the correct order!

#### Parameters

##### colNo

`number`

integer value (zero based) indicating the desired column of the current row of the DBResultSet

#### Returns

`string`

String representing the indicated column of the current row or `null` if is null-value

#### Since

DOCUMENTS 4.0

#### Deprecated

since DOCUMENTS 4.0a HF2 use [DBResultSet.getString()](#getstring) instead

***

### next()

> **next**(): `boolean`

**Move the resultset pointer to the next row of the DBResultSet.**  

The method must be called at least once after retrieving a DBResultSet, because the newly created object does not point to the first result row but to BOF (beginning of file).  
**Note:** every value of a DBResultSet can only be read one time and in the correct order!

#### Returns

`boolean`

`true` if the DBResultSet now points to the next row, `false` if there is no further result row

#### Since

ELC 3.50 / otrisPORTAL 5.0
