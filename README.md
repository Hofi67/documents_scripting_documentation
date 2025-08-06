**Portalscript API (internal)**

***

# Portalscript API

## Introduction

The DOCUMENTS Server supports an embedded scripting language called PortalScript and is an extension to JavaScript.
 In DOCMENTS 5 the Mozilla JavaScript engine SpiderMonkey 24 is used and implements ECMAScript 5.1 and parts of ECMAScript 6.
Since DOCUMENTS 6 the Chrome JavaScript Engine V8 is embedded. DOCUMENTS 6 uses the same V8 engine as Nodes.js.
Currently is this Node.js v18.15.0 (LTS) / V8 10.2.

**Import**

*   There are some breaking changes in PortalScripting between Documents 5 and Documents 6. For details check our documentation portal [https://otris.software](https://otris.software)

**Notes**

* The PortalScripting API environment is only available in fully activated DOCUMENTS licenses, it cannot be used inside pure retrieval principals (EasyWEB principals).
* A history of the PortalScripting API can be found at the [Changelog](changelog.html)
* For Documents 5 see also [Firefox JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
* For Documents 6 see also [https://V8.dev](https://v8.dev)

### Script Exits

The PortalScripting allows to widely customize the behaviour of your system.
For this purpose, PortalScripts (JavaScript files that use PortalScripting) can be
called at special points in the system. These points are called <b>Script Exits</b>.
To use this feature, you can simply create a PortalScript and attach it to one
of the Script Exits. You'll find the Script Exits in the DOCUMENTS Manager.

You can find the entire list and documentation in chapter <a href="scriptexits.html">Script Exits</a>.
The following list just shows a small overview:

* Common file actions like
  * creating new files
  * activating the edit mode of a file
  * saving a file (both before and after)
  * archiving a file
  * deleting a file
* User defined actions attached to filetypes or folders
* As a signal exit shape within workflows
* Using actions to set field values in workflows
* Definitions of the enumeration values using an enumeration-type field
* Script-execution at user login

### Features

PortalScripts may also be used to implement special requirements in DOCUMENTS, such as:
* Dropdown lists which enumeration values depend on another field's value
* Access an external database to fill dropdown lists or field values
* Complex guard-conditions that can't be defined in a simple term
* Calculate data
* Create reports
* Access to xml-data with integrated DOMParser
  * **E4X is removed from DOCUMENTS since 5.0!**
  * [See example](xml-dom.html)
* Realization of daily housekeeping jobs
* Call [external DLLs](dlls.html) to trigger third-party systems

The PortalScript runtime environment grants access to a couple of properties of files or fields.
You can also read out named constants (AutoTexts) like the current user or the name of the current workflow step.
Prerequisites to implement PortalScripts are at least basic skills in general JavaScript programming and knowledge of 
classes, objects and properties allocated by the DOCUMENTS scripting interface (PortalScripting API).

### Classes and Predefined Objects

In the following list you will find a small overview of all available classes and predefined objects.
Predefined objects are explained in a contextual usage (i.e. when editing a file, fill a dropdown list etc.).

Predefined objects:
* [Context](modules/context.html) (implicit object) - root object which refers to DOCUMENTS objects via PortalScript (i.e. file, folder).
* [Util](modules/util.html) (implicit object) - global object, providing several utility functions.
* [PropertyCache](interfaces/propertycache.html) - this class makes it possible to store / cache data over the end of the run time of a script.
* enumval (implicit array) - Definition of enumeration values using a script.

Some classes and interfaces:
* [AccessProfile](classes/AccessProfile.html) / [AccessProfileIterator](interfaces/AccessProfileIterator.html) - represents an access profile (group)
* [SystemUser](interfaces/SystemUser.html) / [SystemUserIterator](interfaces/SystemUserIterator.html) - represents DOCUMENTS Users
* [CustomProperty](interfaces/CustomProperty.html) / [CustomPropertyIterator](interfaces/CustomPropertyIterator.html) - represents a class for storing user specific properties

* [FileResultset](classes/FileResultset.html) - represents a list of DOCUMENTS files
* [ArchiveFileResultset](classes/ArchiveFileResultset.html) - represents a list of archive files
* [Folder](interfaces/Folder.html) / [FolderIterator](interfaces/FolderIterator.html) - this class grants access to all kinds of (public) folders
* [HitResultset](classes/HitResultset.html) / [DocHit](interfaces/DocHit.html) - classes allow comprehensive search operations in Documents and in connected archives.

* [DocFile](interfaces/DocFile.html) - represents a certain file of a filetype
* [ArchivingDescription](classes/ArchivingDescription.html) - class to specify archiving option for a [DocFile](interfaces/DocFile.html)
* [Register](interfaces/Register.html) / [RegisterIterator](interfaces/RegisterIterator.html) - represents a (public) folder of a file
* [Document](interfaces/Document.html) / [DocumentIterator](interfaces/DocumentIterator.html) - represents a certain document that is stored on a document register of a file

* [WorkflowStep](interfaces/WorkflowStep.html) / [WorkflowStepIterator](interfaces/WorkflowStepIterator.html) - represents a workflow step
* [ControlFlow](interfaces/ControlFlow.html) / [ControlFlowIterator](interfaces/ControlFlowIterator.html) - represents the controlflows in the workflow-engine

* [DOMParser](classes/DOMParser.html) - provides basic methods to parse or synthesize XML documents using the DOM.
* [DOMDocument](classes/DOMDocument.html) - represents the root of a DOM tree.
* [DOMNode](interfaces/DOMNode.html) - the base class of all tree elements in a DOMDocument.
* [DOMNodeList](interfaces/DOMNodeList.html) - a dynamic, ordered list of DOMNodes.
* [DOMNamedNodeMap](interfaces/DOMNamedNodeMap.html) - a kind of index for a set of DOMNodes, in which each node has got a unique name.
* [DOMElement](interfaces/DOMElement.html) - represents a HTML or XML element in the DOM.
* [DOMCharacterData](interfaces/DOMCharacterData.html) - represents text-like nodes in the DOM tree.
* [DOMAttr](interfaces/DOMAttr.html) - this class models a single attribute of a DOMElement.
* [DOMDocumentType](classes/DOMDocumentType.html) - a container for %Document Type Declaration (DTD) information associated with a DOMDocument.
* [DOMProcessingInstruction](interfaces/DOMProcessingInstruction.html) - represents a processing instruction node in the DOM tree.
* [DOMEntity](interfaces/DOMEntity.html) - represents either an entity in an XML document or a notation in a DTD.
* [DOMException](interfaces/DOMException.html) - represents DOMExceptions thrown by the DOM API functions.

* [File](classes/File.html) - class granting access to the physical file system of the machine running the DOCUMENTS-Server
* [DBConnection](classes/DBConnection.html) / [DBResultSet](interfaces/DBResultSet.html) - These classes grant access to ODBC data sources and databases
* [XMLExport](classes/XMLExport.html) / [XMLExportDescription](classes/XMLExportDescription.html) - classes to specify XML-export options to Documents elements.
* [ScriptCall](classes/ScriptCall.html) - this class allows asynchronous calling a script from another script.
* [Email](classes/Email.html) - this class allows to create and send an email.
* [XMLHTTPRequest](classes/XMLHTTPRequest.html) - represents a HTTP request using XML in Windows.

* [XLSXWriter](classes/XLSXWriter.html) - allows creating files in the Excel 2007+ XLSX file format.
* [XLSXWorksheet](interfaces/XLSXWorksheet.html) - represents the Excel worksheet.
* [XLSXChartsheet](interfaces/XLSXChartsheet.html) - represents the Excel chartsheet.
* [XLSXFormat](interfaces/XLSXFormat.html) - allows formatting cells in Excel.
* [XLSXChart](interfaces/XLSXChart.html) - allows creating an Excel chart.
* [XLSXChartSeries](interfaces/XLSXChartSeries.html) - represents the Excel chart data series.
* [XLSXChartAxis](interfaces/XLSXChartAxis.html) - represents the Excel chart axis.
