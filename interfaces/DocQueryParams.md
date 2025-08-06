[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / DocQueryParams

# Interface: DocQueryParams

**This class encapsulates the basic parameters of a Documents search request.**  

Only the script-exits "OnSearch" and "FillSearchMask" provide access to such an object. See also [Context.getQueryParams()](Context.md#getqueryparams). 
Scripts can modify the parameters only in the following ways. 
<ol> 
<li>A project-related "OnSearch" script may detect in advance, if an individual query won't find any hits in a specified searchable resource. 
In this case, the script can call [removeSource()](#removesource) for each zero-hits resource to reduce the workload on the database and/or archive systems. 
However the very first listed resource cannot be removed, because it regularly owns the selected hit list. As a result, removeSource() 
is not suitable for implementing extraordinary permission restrictions. </li> 
<li>A "OnSearch" script can substitute the relational operator or the value in a search field. This practice is not recommended, 
because it may make the user find something competely different than he sought for. </li> 
<li>A "OnSearch" script may cancel some special search requests and submit a custom message. The type (or origin) of the search request determines, 
if and where this message will be displayed. </li> 
<li>A "FillSearchMask" script can place default values in the search fields. </li> 
</ol>

## Since

DOCUMENTS 4.0d

## Example

```ts
util.out("* *** *** **** onSearch start * *** *** *** ***");
var params = context.getQueryParams();
if(params)
{
    // First write the contents of the object to the server window
    util.out("got retrieval parameter object");
    var requestType = params.requestType;
    util.out("queryType =  " + requestType);
    // Print the list of searchable resources.
    var count = params.sourceCount;
    util.out("sourceCount =  " + count);
    var cnt;
    for(cnt = 0; cnt < count; ++cnt)
    {
        var source = params.getSource(cnt);
        if(source)
        {
            util.out("<Source " + (cnt+1) + ">");
            util.out("resId = " + source.resId);
            util.out("type = " + source.type);
            util.out("server = " + source.server);
        }
        else
            util.out("got a NULL source");
    }
    // Print the list of all search fields.
    // This dump may include many empty fields.
    count = params.searchFieldCount;
    util.out("\r\nsearch fields = " + count);
    for(cnt = 0; cnt < count; ++cnt)
    {
        var sfield = params.getSearchField(cnt);
        if(sfield)
        {
            util.out("<Searchfield " + (cnt+1) + ">");
            var filter = sfield.name + sfield.compOp + sfield.valueExpr;
            util.out("Condition: " + filter);
            util.out("fieldType = " + sfield.type);
            util.out("label = " + sfield.label);
        }
        else
            util.out("got a NULL field");
    }
    // Print the search fields again, but this time ignore all empty
    // fields.
    count = params.filledSearchFieldCount;
    util.out("\r\nfilled search fields = " + count);
    for(cnt = 0; cnt < count; ++cnt)
    {
        sfield = params.getSearchField(cnt, true);
        if(sfield)
        {
            util.out("<Searchfield " + (cnt+1) + ">");
            var filter = sfield.name + sfield.compOp + sfield.valueExpr;
            util.out("Condition: " + filter);
            util.out("fieldType = " + sfield.type);
            util.out("label = " + sfield.label);
        }
        else
            util.out("got a NULL field");
    }
    // The subsequent test code requires at least one filled in search field
    if(count > 0)
    {
        sfield = params.getSearchField(0, true);
        var testExpr = sfield.valueExpr;
        // Test 1:
        // Let's assume we have got a bunch of EDA stores. We know,
        // that the value "rarely" is frequently searched across many
        // stores, but it never can appear in a store named "Playground".
        // We can try to exclude this store from the search request to
        // reduce the workload.
        if(testExpr == "rarely")
        {
            // Note: Source #0 cannot not be removed.
            for(cnt = 1; cnt < params.sourceCount; ++cnt)
            {
                source = params.getSource(cnt);
                if(source.server == "Playground")
                {
                    params.removeSource(cnt--);
                    // About the "--": removeSource() has implicitly
                    // decreased the index number of all subsequent
                    // sources and also the "sourceCount" property.
                    // To skip nothing, the loop needs to run with
                    // the same index once again.
                }
            }
        }
        // Test 2:
        // If the OnSearchScript triggers a search request itself, it
        // ends up in a recursive call! This section does nothing serious.
        // It just demonstrates the effect with a few log messages.
        if(testExpr == "recurse")
        {
            if(requestType == DocQueryParams.API)
                util.out("OnSearchScript avoiding another recursion");
            else
            {
                util.out("OnSearchScript before recursion");
                var iter = new FileResultset("ftEmployee", "hrRemarks=recurse", "");
                var o = iter.first();
                util.out("OnSearchScript after recursion");
            }
        }
        // Test 3:
        // Generate an error for a specific search expression.
        if((requestType == DocQueryParams.DIRECT
            || requestType == DocQueryParams.EXTENDED)
           && testExpr == "want an error")
        {
            context.errorMessage = "Here is the error message you desired!";
            return -142;
        }
        // Test 4:
        // Substitute a search expression (not recommended; just a demo)
        if(requestType == DocQueryParams.EXTENDED && (testExpr == "U" ||testExpr == "u"))
            sfield.valueExpr = "X";
    }
}
else
    util.out("No retrieval parameters available.");
util.out("* *** *** **  onSearch end * *** *** *** ****");
```

## Properties

### API

> `readonly` **API**: `number`

(Archive-)FileResultsets, HitResultsets and the SOAP report functions belong to this category.   
This constant is member of constant group: Request Type Constants  
These constants are equally available in each instance of DocQueryParams and in the constructor object.

***

### DIRECT

> `readonly` **DIRECT**: `number`

This constant is member of constant group: Request Type Constants  
These constants are equally available in each instance of DocQueryParams and in the constructor object.

***

### EXTENDED

> `readonly` **EXTENDED**: `number`

This constant is member of constant group: Request Type Constants  
These constants are equally available in each instance of DocQueryParams and in the constructor object.

***

### FILING\_PLAN

> `readonly` **FILING\_PLAN**: `number`

This constant is member of constant group: Request Type Constants  
These constants are equally available in each instance of DocQueryParams and in the constructor object.

***

### filledSearchFieldCount

> **filledSearchFieldCount**: `number`

**The number of filled in search fields in the query (read-only).**  

This is in other words the number of conditions in the query.  

**Note:** Attaching a default value to a search field does not fill it in this context. 
Default values are being stored separately from concrete search values, for technical reasons.

#### Since

DOCUMENTS 4.0c

***

### FOLDER\_D

> `readonly` **FOLDER\_D**: `number`

Listing the contents of such a folder already triggers a search request.   
This constant is member of constant group: Request Type Constants  
These constants are equally available in each instance of DocQueryParams and in the constructor object.

***

### FOLDER\_S

> `readonly` **FOLDER\_S**: `number`

In the current release, this type can occur only, if the Documents setting "search field in folder" is enabled.   
This constant is member of constant group: Request Type Constants  
These constants are equally available in each instance of DocQueryParams and in the constructor object.

***

### QUICK\_VIEW

> `readonly` **QUICK\_VIEW**: `number`

**Note:** Quick view URLs with just an id-Parameter do not trigger a search.   
This constant is member of constant group: Request Type Constants  
These constants are equally available in each instance of DocQueryParams and in the constructor object.

***

### REFERENCE

> `readonly` **REFERENCE**: `number`

This request type originates from the web dialog, which opens, when a user is editing a file and presses a reference fields select button.   
This constant is member of constant group: Request Type Constants  
These constants are equally available in each instance of DocQueryParams and in the constructor object.

***

### REGISTER

> `readonly` **REGISTER**: `number`

This constant is member of constant group: Request Type Constants  
These constants are equally available in each instance of DocQueryParams and in the constructor object.

***

### requestType

> `readonly` **requestType**: `number`

**The type (or trigger) of the search request (read-only).**  

See the enumeration constants in this class. If Documents encounters a request, which it cannot categorize exactly, 
it will return the nearest match with respect to the server's internal interfaces.

#### Since

DOCUMENTS 4.0c

***

### SCRIPT\_TREE

> `readonly` **SCRIPT\_TREE**: `number`

This is a special feature, where a script in the web server process sends a seach request and immediately generates a hit tree from the results. 
The tabular list is not displayed in this case.   
This constant is member of constant group: Request Type Constants  
These constants are equally available in each instance of DocQueryParams and in the constructor object.

***

### searchFieldCount

> `readonly` **searchFieldCount**: `number`

**The number of declared search fields in the query (read-only).**  

This count may include fields from a search mask, which have not been filled in.

#### Since

DOCUMENTS 4.0c

***

### searchMaskName

> **searchMaskName**: `string`

**The (technical) name of the selected search mask, if available (read only).**  

**Note:** The value is an empty string, if the query has been prepared without a search mask or with an anonymous mask 
(controlled by "show in search mask" checkboxes). Search mask names are unique with regard to a single searchable resource. 
As soon as multiple resources are involved, the names are often ambiguous, because each resource may supply a search mask 
with the same name. To obtain a better identifier, the script may combine the mask's name and the resId of the first selected resource. 
However, even this identifier is not always unique. If a user has selected multiple EE.x views and the DOCUMENTS property "UseMainArchives" 
is undefined or zero, the query does not specify a main resource. DOCUMENTS then passes the RetrievalSource objects with random order. 
In this case the script cannot distinguish search masks with equal names.

#### Since

DOCUMENTS 4.0e

#### See

[getSource](#getsource)  
[sourceCount](#sourcecount)

***

### sourceCount

> `readonly` **sourceCount**: `number`

**The number of searchable resources involved in the query (read-only).**

#### Since

DOCUMENTS 4.0c undefined

## Methods

### getLastError()

> **getLastError**(): `string`

**Function to get the description of the last error that occurred.**

#### Returns

`string`

Text of the last error

#### Since

DOCUMENTS 4.0c

***

### getSearchField()

> **getSearchField**(`index`, `skipEmpty`): [`RetrievalField`](RetrievalField.md)

**Get a descriptive object of one of the search fields (conditions), which are declared in the query.**  

**Note:** If the request has been prepared with any kind of searck mask in the background, all available fields of 
that mask appear in the internal list, not only those, which the user has filled in. The skipEmpty flag provides 
a simple opportunity to examine only effective search conditions. Internally generated conditions (for example ACL-filters) 
cannot be returned by this function. Attaching a default value to a field does not modify its "empty" state in terms of this function.

#### Parameters

##### index

`number`

The index of the desired search field. The valid range is 0 to (filledSearchFieldCount - 1), if the flag `skipEmpty` is set. 
Otherwise the range is 0 to (searchFieldCount - 1).

##### skipEmpty

`boolean`

An optional boolean to treat all empty search fields as non-existing. By default all fields can be examined.

#### Returns

[`RetrievalField`](RetrievalField.md)

A RetrievalField object, which contains a search field name, an operator and (sometimes) a value expression.

#### Since

DOCUMENTS 4.0c

***

### getSource()

> **getSource**(`index`): [`RetrievalSource`](RetrievalSource.md)

**Get a descriptive object of one selected search resource.**

#### Parameters

##### index

`number`

The integer index of the resource in the internal list. Range: 0 to (sourceCount - 1)

#### Returns

[`RetrievalSource`](RetrievalSource.md)

A RetrievalSource object on success, otherwise `null`.

#### Since

DOCUMENTS 4.0c

***

### removeSource()

> **removeSource**(`refSource`): `boolean`

**Remove a search resource from the query.**  

**Note:** The access to this function is restricted. Only the "OnSearchScript" can effectively use it.  

**Note:** The id can be read from the property RetrievalSource.resId. Valid index values range from 1 to (sourceCount - 1). 
The resource at index 0 cannot be removed (see the class details). After a succesful call, the sourceCount and the index 
of each subsequent resource in the list are decreased by one. The method does not perform type-checking on the refSource parameter. 
It interprets a value like "12345" always as an index, even when this value has been passed as a string.

#### Parameters

##### refSource

`any`

Either the current integer index or the id of the resource.

#### Returns

`boolean`

A boolean value, which indicates a succesful call.

#### Since

DOCUMENTS 4.0c
