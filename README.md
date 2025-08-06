**Portalscript API (internal)**

***

# Portalscript API / Documents Script API

## Introduction

The DOCUMENTS Server supports an embedded scripting language called PortalScript and is an extension to JavaScript.
Since DOCUMENTS 6 the Chrome JavaScript Engine V8 is embedded.

### Script Exits

The PortalScripting allows to widely customize the behaviour of your system.
For this purpose, PortalScripts (JavaScript files that use PortalScripting) can be
called at special points in the system. These points are called <b>Script Exits</b>.
To use this feature, you can simply create a PortalScript and attach it to one
of the Script Exits. You'll find the Script Exits in the DOCUMENTS Manager.

You can find the entire list and documentation in chapter <a href="scriptexits.md">Script Exits</a>.
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
* Realization of daily housekeeping jobs


The PortalScript runtime environment grants access to a couple of properties of files or fields.
You can also read out named constants (AutoTexts) like the current user or the name of the current workflow step.
Prerequisites to implement PortalScripts are at least basic skills in general JavaScript programming and knowledge of 
classes, objects and properties allocated by the DOCUMENTS scripting interface (PortalScripting API).

### Classes and Predefined Objects

In the following list you will find a small overview of all available classes and predefined objects.
Predefined objects are explained in a contextual usage (i.e. when editing a file, fill a dropdown list etc.).

Predefined objects:
* [Context](modules/context.md) (implicit object) - root object which refers to DOCUMENTS objects via PortalScript (i.e. file, folder).
* [Util](modules/util.md) (implicit object) - global object, providing several utility functions.
* [PropertyCache](interfaces/propertycache.md) - this class makes it possible to store / cache data over the end of the run time of a script.
* enumval (implicit array) - Definition of enumeration values using a script.

Some classes and interfaces:
* [AccessProfile](classes/AccessProfile.md) / [AccessProfileIterator](interfaces/AccessProfileIterator.md) - represents an access profile (group)
* [SystemUser](interfaces/SystemUser.md) / [SystemUserIterator](interfaces/SystemUserIterator.md) - represents DOCUMENTS Users
* [CustomProperty](interfaces/CustomProperty.md) / [CustomPropertyIterator](interfaces/CustomPropertyIterator.md) - represents a class for storing user specific properties

* [DocFile](interfaces/DocFile.md) - represents a certain file of a filetype
* [Register](interfaces/Register.md) / [RegisterIterator](interfaces/RegisterIterator.md) - represents a (public) folder of a file
* [Document](interfaces/Document.md) / [DocumentIterator](interfaces/DocumentIterator.md) - represents a certain document that is stored on a document register of a file
* [FileResultset](classes/FileResultset.md) - represents a list of DOCUMENTS files
* [ArchiveFileResultset](classes/ArchiveFileResultset.md) - represents a list of archive files
* [Folder](interfaces/Folder.md) / [FolderIterator](interfaces/FolderIterator.md) - this class grants access to all kinds of (public) folders
* [HitResultset](classes/HitResultset.md) / [DocHit](interfaces/DocHit.md) - classes allow comprehensive search operations in Documents and in connected archives.
* [ArchivingDescription](classes/ArchivingDescription.md) - class to specify archiving option for a [DocFile](interfaces/DocFile.md)

* [WorkflowStep](interfaces/WorkflowStep.md) / [WorkflowStepIterator](interfaces/WorkflowStepIterator.md) - represents a workflow step
* [ControlFlow](interfaces/ControlFlow.md) / [ControlFlowIterator](interfaces/ControlFlowIterator.md) - represents the controlflows in the workflow-engine

* [File](classes/File.md) - class granting access to the physical file system of the machine running the DOCUMENTS-Server
* [DBConnection](classes/DBConnection.md) / [DBResultSet](interfaces/DBResultSet.md) - These classes grant access to ODBC data sources and databases
* [XMLExport](classes/XMLExport.md) / [XMLExportDescription](classes/XMLExportDescription.md) - classes to specify XML-export options to Documents elements.
* [ScriptCall](classes/ScriptCall.md) - this class allows asynchronous calling a script from another script.
* [Email](classes/Email.md) - this class allows to create and send an email.
* [XMLHTTPRequest](classes/XMLHTTPRequest.md) - represents a HTTP request using XML in Windows.

* [XLSXWriter](classes/XLSXWriter.md) - allows creating files in the Excel 2007+ XLSX file format.
* [XLSXWorksheet](interfaces/XLSXWorksheet.md) - represents the Excel worksheet.
* [XLSXChartsheet](interfaces/XLSXChartsheet.md) - represents the Excel chartsheet.
* [XLSXFormat](interfaces/XLSXFormat.md) - allows formatting cells in Excel.
* [XLSXChart](interfaces/XLSXChart.md) - allows creating an Excel chart.
* [XLSXChartSeries](interfaces/XLSXChartSeries.md) - represents the Excel chart data series.
* [XLSXChartAxis](interfaces/XLSXChartAxis.md) - represents the Excel chart axis.

* [DOMParser](classes/DOMParser.md) - provides basic methods to parse or synthesize XML documents using the DOM.
* [DOMDocument](classes/DOMDocument.md) - represents the root of a DOM tree.
* [DOMNode](interfaces/DOMNode.md) - the base class of all tree elements in a DOMDocument.
* [DOMNodeList](interfaces/DOMNodeList.md) - a dynamic, ordered list of DOMNodes.
* [DOMNamedNodeMap](interfaces/DOMNamedNodeMap.md) - a kind of index for a set of DOMNodes, in which each node has got a unique name.
* [DOMElement](interfaces/DOMElement.md) - represents a HTML or XML element in the DOM.
* [DOMCharacterData](interfaces/DOMCharacterData.md) - represents text-like nodes in the DOM tree.
* [DOMAttr](interfaces/DOMAttr.md) - this class models a single attribute of a DOMElement.
* [DOMDocumentType](classes/DOMDocumentType.md) - a container for %Document Type Declaration (DTD) information associated with a DOMDocument.
* [DOMProcessingInstruction](interfaces/DOMProcessingInstruction.md) - represents a processing instruction node in the DOM tree.
* [DOMEntity](interfaces/DOMEntity.md) - represents either an entity in an XML document or a notation in a DTD.
* [DOMException](interfaces/DOMException.md) - represents DOMExceptions thrown by the DOM API functions.
