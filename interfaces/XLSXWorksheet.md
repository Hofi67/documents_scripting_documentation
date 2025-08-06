[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / XLSXWorksheet

# Interface: XLSXWorksheet

**The XLSXWorksheet class represents the Excel worksheet.**  

An XLSXWorksheet object isn't created directly. Instead an XLSXWorksheet is created by calling the [XLSXWriter.addWorksheet(name)](../classes/XLSXWriter.md#addworksheet) 
function from an [XLSXWriter](../classes/XLSXWriter.md) object. It handles operations such as writing data to cells or formatting worksheet layout.

## Since

DOCUMENTS 5.0e

## Example

```ts
var writer = new XLSXWriter("c:\\tmp\\worksheet.xlsx");
// Add a worksheet with a user defined sheet name.
var worksheet1 = writer.addWorksheet("Worksheet1");
// Add a cell format.
var format1 = writer.addFormat("format1");
// Set the bold property for the format.
format1.setFontStyle("bold");
// Set the alignment for the format
format1.setAlign(writer.ALIGN_CENTER);
// Write formatted data. 
worksheet1.writeCell("string", 0, 0, "Hello Excel", format1);
// Change the row height
worksheet1.setRow(0, 20);
// Change the column width
worksheet1.setColumn(0, 0, 15);
// Save the file.
if (!writer.save())
    throw writer.getLastError();
```

## Methods

### addAutofilter()

> **addAutofilter**(`firstRow`, `firstCol`, `lastRow`, `lastCol`): `boolean`

**Add an autofilter area to the current worksheet.**  

An autofilter is a way of adding drop down lists to the headers of a 2D range of worksheet data. This allows users to filter the data based 
on simple criteria so that some data is shown and some is hidden.  

**Note:** It isn't currently possible to apply filter conditions to the autofilter.

#### Parameters

##### firstRow

`number`

The first row of the range. (All zero indexed.)

##### firstCol

`number`

The first column of the range.

##### lastRow

`number`

The last row of the range.

##### lastCol

`number`

The last column of the range.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
if (!worksheet1.addAutofilter(0, 0, 50, 3))
  throw worksheet1.getLastError();
```

***

### freezePanes()

> **freezePanes**(`row`, `col`): `boolean`

**Split and freeze the current worksheet into panes.**  

This function can be used to divide a worksheet into horizontal or vertical regions known as panes and to "freeze" these panes 
so that the splitter bars are not visible. The parameters `row` and `col` are used to specify the location of the split. 
It should be noted that the split is specified at the top or left of a cell and that the function uses zero based indexing. 
Therefore to freeze the first row of a worksheet it is necessary to specify the split at row 2 (which is 1 as the zero-based index). 
You can set one of the `row` and `col` parameters as zero if you do not want either a vertical or horizontal split.

#### Parameters

##### row

`number`

The cell row (zero indexed).

##### col

`number`

The cell column (zero indexed).

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
worksheet1.freezePanes(1, 0); // Freeze the first row.
worksheet2.freezePanes(0, 1); // Freeze the first column.
worksheet3.freezePanes(1, 1); // Freeze first row/column.
```

***

### getLastError()

> **getLastError**(): `string`

**Function to get the description of the last error that occurred.**

#### Returns

`string`

Text of the last error as String

#### Since

DOCUMENTS 5.0e

***

### importFromJSON()

> **importFromJSON**(`jsonString`, `row?`, `col?`): `boolean`

**Import data from a JSON-String to the current worksheet.**  

**Specification of the JSON-String / object-structure**  

The JSON-String represents a table and has the following structure:
```json
{
   "formats" : [Format-Defintion1, Format-Defintion2, ...],
   "table" : {
      "columns" : [Column-Defintion1, Column-Defintion2, Column-Defintion3, ...],
      "body" : {
         "rows" : [
            [val_11, val_12, val_13, ...],
            [val_21, val_22, val_23, ...],
            ....
         ]
      }
   }
}
```

+ `formats:` array of format-definitions, that can be used for the columns-header and body (how shall a cell look like)
+ `table:` contains columns definition and the table-data (body)
+ `columns:` array of columns-definitions with specification of column-label and column style
+ `rows:` array of arrays - each array specify one line in the table

**Format-Definition**  

```json
{
    "name"       : formatName,
    "bgcolor"    : colorName,      // optional
    "pattern"    : patternName,    // optional
    "fontcolor"  : colorName,      // optional
    "fontstyle"  : styleName,      // optional
    "fontsize"   : int-value,      // optional
    "cellborder" : int-value,      // optional
    "align"      : alignStyle,     // optional
    "textwrap"   : 1,              // optional
    "numformat"  : "format-string" // optional

    // colorName = 0xaabbcc , "black", "blue", "brown", "cyan", "gray", "green", "lime", "magenta", "navy", "orange", "pink", "purple", "red", "silver", "white", "yellow"
    // patternName = "solid", "mediumgrey", "lightgrey"
    // styleName = "bold", "italic"
    // alignStyle = "left", "center", "right"
}
```
 
**Column-Definition**  

```json
{
    "label"      : "Column-Label",                                           // optional
    "header"     : "Name of Format-Definition for the column in the 1. row", // optional
    "body"       : "Name of Format-Definition for the column in the 2+. row",// optional
    "width"      : int-value,                                                // optional
    "type"       : "string"     forces to convert values to string           // optional
}
```

#### Parameters

##### jsonString

`string`

Containing the data to be imported.

##### row?

`number`

**Default:** `0`.  
Optional the zero indexed row number of the first cell of the area the data to be written to.

##### col?

`number`

**Default:** `0`.  
Optional the zero indexed column number of the first cell of the area the data to be written to.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### See

[XLSXWorksheet.importFromJSONFile](#importfromjsonfile)

#### Example

```ts
// Definition of the data object
var impobj = {}
// first some format definitions, that will be used as header and body defs
impobj.formats = [];
impobj.formats[0] = {};
impobj.formats[0].name = "header";
impobj.formats[0].fontsize = 11;
impobj.formats[0].bgcolor = "gray";
impobj.formats[1] = {};
impobj.formats[1].name = "headerRight";
impobj.formats[1].fontsize = 11;
impobj.formats[1].bgcolor = 0x00FF00;
impobj.formats[1].align = "right";
impobj.formats[2] = {};
impobj.formats[2].name = "headerBold";
impobj.formats[2].fontsize = 11;
impobj.formats[2].bgcolor = "silver";
impobj.formats[2].fontstyle = "bold";
impobj.formats[3] = {};
impobj.formats[3].name = "bodyString";
impobj.formats[3].cellborder = 1;
impobj.formats[4] = {};
impobj.formats[4].name = "bodyNum";
impobj.formats[4].cellborder = 1;
impobj.formats[4].numformat = "#,##0.00";
impobj.formats[5] = {};
impobj.formats[5].name = "bodyDate";
impobj.formats[5].numformat = "yyyy-mm-dd"; 
// Data table
impobj.table = {};
impobj.table.columns = [];
// Definition of the columns
impobj.table.columns[0] = {};
impobj.table.columns[0].label = "String Label";
impobj.table.columns[0].width = 100;
impobj.table.columns[0].header = "headerBold";
impobj.table.columns[0].body = "bodyString";
impobj.table.columns[1] = {};
impobj.table.columns[1].label = "Number Label";
impobj.table.columns[1].width = 20;
impobj.table.columns[1].header = "headerRight";
impobj.table.columns[1].body = "bodyNum";
impobj.table.columns[2] = {};
impobj.table.columns[2].label = "Date Label";
impobj.table.columns[2].width = 30;
impobj.table.columns[2].header = "header";
impobj.table.columns[2].body = "bodyDate";
// Now add 3 rows with data
impobj.table.body = {};
impobj.table.body.rows = [];
impobj.table.body.rows.push( ["Hello", 2117.99, util.convertDateToExcelDate(new Date())] );
impobj.table.body.rows.push( ["World", 42, util.convertDateToExcelDate(new Date(2018, 11, 31))] );
impobj.table.body.rows.push( ["again", -42.30, new Date()] );
// Data object is now complete
// Create the JSON String..
var jsonString = JSON.stringify(impobj, null, 2);
var writer = new XLSXWriter("c:\\tmp\\importJson.xlsx")
var sheet = writer.addWorksheet("Sheet1");
if (!sheet.importFromJSON(jsonString))
    throw sheet.getLastError();
if (!writer.save())
    throw writer.getLastError();
```

***

### importFromJSONFile()

> **importFromJSONFile**(`jsonFilePath`, `row?`, `col?`): `boolean`

**Import data from a file containing a JSON-String to the current worksheet.**

#### Parameters

##### jsonFilePath

`string`

The JSON-file path.

##### row?

`number`

**Default:** `0`.  
Optional the zero indexed row number of the first cell of the area the data to be written to.

##### col?

`number`

**Default:** `0`.  
Optional the zero indexed column number of the first cell of the area the data to be written to.

#### Returns

`boolean`

#### Since

DOCUMENTS 5.0e

#### See

[XLSXWorksheet.importFromJSON](#importfromjson)

#### Example

```ts
if (!worksheet1.importFromJSONFile("c:\\tmp\\json.txt"))
  throw worksheet1.getLastError();
```

***

### insertChart()

> **insertChart**(`row`, `col`, `chart`, `xOffset?`, `yOffset?`, `xScale?`, `yScale?`): `boolean`

**Insert a chart into the current worksheet.**  

This function can be used to insert an [XLSXChart](XLSXChart.md) object into a worksheet. It takes additional optional parameters to position 
and scale the image of the chart. The XLSXChart object must be created first using the [XLSXWriter.addChart(type)](../classes/XLSXWriter.md#addchart) function 
and configured using the functions from the class XLSXChart.  

**Note:** A chart may only be inserted once into a chartsheet or a worksheet. If several similar charts are required then each one 
must be created separately with [XLSXWriter.addChart(type)](../classes/XLSXWriter.md#addchart).

#### Parameters

##### row

`number`

The zero indexed row number.

##### col

`number`

The zero indexed column number.

##### chart

[`XLSXChart`](XLSXChart.md)

An XLSXChart object created via XLSXWriter.addChart(number type).

##### xOffset?

`number`

**Default:** `0`.  
Optional integer offset from the left of the cell in pixels.

##### yOffset?

`number`

**Default:** `0`.  
Optional integer offset from the top of the cell in pixels.

##### xScale?

`number`

**Default:** `1`.  
Optional X scale of the image as a decimal.

##### yScale?

`number`

**Default:** `1`.  
Optional Y scale of the image as a decimal.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### See

[XLSXChartsheet.insertChart](XLSXChartsheet.md#insertchart)

#### Example

```ts
// Create a chart object.
var chart = writer.addChart(writer.CHART_COLUMN);
// Add some data series to the chart.
var series1 = chart.addSeries("", "Worksheet1!$A$1:$A$5");
var series2 = chart.addSeries("", "Worksheet1!$B$1:$B$5");
var series3 = chart.addSeries("", "Worksheet1!$C$1:$C$5");
// Insert the chart into the worksheet.
if (!worksheet1.insertChart(6, 1, chart, 30, 10, 0.5, 0.75))
  throw worksheet1.getLastError();
```

***

### insertImage()

> **insertImage**(`row`, `col`, `filename`, `xOffset?`, `yOffset?`, `xScale?`, `yScale?`): `boolean`

**Insert an image in a worksheet cell specified by row and column.**  

This function can be used to insert an image (in PNG or JPEG format) into a worksheet. It takes additional optional parameters to position and scale the image.  

**Note:** The scaling of an image may be affected if it crosses a row that has its default height changed due to a font that is larger than the default font 
size or that has text wrapping turned on. To avoid this you should explicitly set the height of the row using [XLSXWorksheet.setRow()](#setrow) 
if it crosses an inserted image.

#### Parameters

##### row

`number`

The zero indexed row number.

##### col

`number`

The zero indexed column number.

##### filename

`string`

The image filename, with path if required.

##### xOffset?

`number`

**Default:** `0`.  
Optional integer offset from the left of the cell in pixels.

##### yOffset?

`number`

**Default:** `0`.  
Optional integer offset from the top of the cell in pixels.

##### xScale?

`number`

**Default:** `1`.  
Optional X scale of the image as a decimal.

##### yScale?

`number`

**Default:** `1`.  
Optional Y scale of the image as a decimal.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
if (!worksheet1.insertImage(12, 4, "C:\\temp\\logo.jpg", 15, 10, 0.2, 0.2))
    throw worksheet1.getLastError();
```

***

### mergeRange()

> **mergeRange**(`firstRow`, `firstCol`, `lastRow`, `lastCol`, `value`, `format?`): `boolean`

**Merge a range of cells.**  

This function allows cells to be merged together so that they act as a single area. Excel generally merges and centers cells at same time. 
To get similar behavior you need to apply a format object with the appropriate alignment: 

```js 
var mergeFormat = writer.addFormat("mergeFormat"); 
mergeFormat.setAlign(writer.ALIGN_CENTER); 

worksheet1.mergeRange(1, 1, 1, 3, "Merged Range", mergeFormat); 
```  

**Note:** This function writes a string value to the merged range. In order to write other data types, such as a number or a formula, 
you can overwrite the first cell with a call to the function [XLSXWorksheet.writeCell(type, row, col, value, format)](#writecell) 
with the appropriate value type. The same format should be used as was used in the merged range. 

```js 
// First write a range with a blank string. 
worksheet1.mergeRange(1, 1, 1, 3, "", format); 

// Then overwrite the first cell with a number. 
worksheet1.writeCell("number", 1, 1, 123, format); 
```

#### Parameters

##### firstRow

`number`

The first row of the range. (All zero indexed.)

##### firstCol

`number`

The first column of the range.

##### lastRow

`number`

The last row of the range.

##### lastCol

`number`

The last col of the range.

##### value

`string`

String value to write to the merged range.

##### format?

[`XLSXFormat`](XLSXFormat.md)

**Default:** `null`.  
Optional XLSXFormat object used to apply formatting to the merged cells. The default value is `null` to indicate no formatting.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

***

### setColumn()

> **setColumn**(`firstCol`, `lastCol`, `width?`, `format?`, `hidden?`, `level?`, `collapsed?`): `boolean`

**Set the properties for one or more columns of cells.**  

This function can be used to change the default properties of a single column or a range of columns. If it is applied to a single column 
the value of `firstCol` and `lastCol` should be the same. It can also be used to create Outlines and Grouping of columns with 
the optional parameters `hidden`, `level` and `collapsed`. Adjacent columns with the same outline level are grouped together into a single outline. 
Columns can be collapsed by setting the parameter `hidden` for the hidden columns and setting the parameter `collapsed` for a column that has the collapsed '+' symbol.

#### Parameters

##### firstCol

`number`

The zero indexed first column.

##### lastCol

`number`

The zero indexed last column.

##### width?

`number`

**Default:** `8.43`.  
Optional width of the column(s). The default column width is `8.43`. The `width` parameter sets the column width in the same units used 
by Excel which is: the number of characters in the default font. The default width is `8.43` in the default font of Calibri 11. 
The actual relationship between a string width and a column width in Excel is complex. See the 
[following explanation of column widths](https://support.microsoft.com/en-us/kb/214123) from the Microsoft support documentation for more details.   

**Note:** There is no way to specify "AutoFit" for a column in the Excel file format. This feature is only available at runtime from within Excel. 
It is possible to simulate "AutoFit" in your application by tracking the maximum width of the data in the column as your write it 
and then adjusting the column width at the end.

##### format?

[`XLSXFormat`](XLSXFormat.md)

**Default:** `null`.  
Optional XLSXFormat object used to apply formatting to any cells in the column that don't have a format. 
As in Excel a row format takes precedence over a default column format.

##### hidden?

`boolean`

**Default:** `false`.  
Optional flag used to hide the column(s).

##### level?

`number`

**Default:** `0`.  
Optional integer outline level of the column(s) used to create Outlines and Grouping. Excel allows up to 7 outline levels. 
Therefore the level parameter should be in the range `0 <= level <= 7`.

##### collapsed?

`boolean`

**Default:** `false`.  
Optional flag used to create Outlines and Grouping and indicating whether to collapse a column that has the collapsed '+' symbol.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### See

[setRow](#setrow)

#### Example

```ts
if (!worksheet1.setColumn(1, 6, 5, null, false, 1, false))
   throw worksheet1.getLastError();
```

***

### setFirstSheet()

> **setFirstSheet**(): `boolean`

**Set current worksheet as the first visible sheet tab.**  

The [XLSXWriter.activateWorksheet(worksheet)](../classes/XLSXWriter.md#activateworksheet) function determines which worksheet is initially selected. 
However, if there are a large number of worksheets the selected worksheet may not appear on the screen. To avoid this you can select the leftmost 
visible worksheet tab using this function.  
The default value is the first worksheet.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
worksheet19.setFirstSheet(); // worksheet19: First visible worksheet tab.
writer.activateWorksheet(worksheet20); // worksheet20: First visible worksheet.
```

***

### setFooter()

> **setFooter**(`footer`, `margin?`): `boolean`

**Set the printed page footer caption.**  

Footers are generated using a string which is a combination of plain text and control characters (see [Generating header/footer](../xlsxwriter.html) for more details).

#### Parameters

##### footer

`string`

The footer string.

##### margin?

`number`

**Default:** `0.3`.  
Optional footer margin in inches. Excel default is 0.3.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
if (!worksheet1.setFooter("some text", 0.2))
  throw worksheet1.getLastError();
```

***

### setGridlines()

> **setGridlines**(`option`): `boolean`

**Set the option to display or hide gridlines on the screen and the printed page.**  

There are two options 

+ `hideAll`: Hide gridlines on the screen and the printed page.
+ `showPrint`: Display gridlines on the screen and the printed page.

**Note:** The Excel default is that the screen gridlines are on and the printed worksheet is off.

#### Parameters

##### option

`string`

string Gridline option. Possible values are `hideAll` and `showPrint`. See description for details.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
worksheet1.setGridlines("showPrint");
```

***

### setHeader()

> **setHeader**(`header`, `margin?`): `boolean`

**Set the printed page header caption.**  

Headers are generated using a string which is a combination of plain text and control characters (see [Generating header/footer](../xlsxwriter.html) for more details).

#### Parameters

##### header

`string`

The header string.

##### margin?

`number`

**Default:** `0.3`.  
Optional header margin in inches. Excel default is 0.3.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
if (!worksheet1.setHeader("some text", 0.2))
  throw worksheet1.getLastError();
```

***

### setHorizontalPagebreaks()

> **setHorizontalPagebreaks**(`breaks`): `boolean`

**Set the horizontal page breaks on the current worksheet.**  

This function adds horizontal page breaks to the worksheet. A page break causes all the data that follows it to be printed on the next page. 
Horizontal page breaks act between rows.  

**Note:** There is an Excel limitation of 1023 horizontal page breaks per worksheet.

#### Parameters

##### breaks

`number`[]

Integer array of page breaks.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
// To create a page break between rows 20 and 21 you must specify the break at
// row 21. However in zero index notation this is actually row 20:
if (!worksheet1.setHorizontalPagebreaks([20]))
  throw worksheet1.getLastError();
```

***

### setLandscape()

> **setLandscape**(): `boolean`

**Set the page orientation as landscape.**  

This function is used to set the orientation of the worksheet's printed page to landscape.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

***

### setMargins()

> **setMargins**(`left?`, `right?`, `top?`, `bottom?`): `boolean`

**Set the worksheet margins for the printed page.**  

This function is used to set the margins of the worksheet when it is printed. The units are in inches. 
Specifying -1 for any parameter will give the default Excel value as shown below.

#### Parameters

##### left?

`number`

**Default:** `-1`.  
Optional left margin in inches. Excel default is 0.7.

##### right?

`number`

**Default:** `-1`.  
Optional right margin in inches. Excel default is 0.7.

##### top?

`number`

**Default:** `-1`.  
Optional top margin in inches. Excel default is 0.75.

##### bottom?

`number`

**Default:** `-1`.  
Optional bottom margin in inches. Excel default is 0.75.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
worksheet1.setMargins(1.3, 1.2, -1, -1);
```

***

### setPageView()

> **setPageView**(): `boolean`

**Set the page layout to page view mode.**  

This function is used to display the worksheet in "Page View/Layout" mode.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

***

### setPaperType()

> **setPaperType**(`type?`): `boolean`

**Set the paper format for the printed output of the current worksheet.**  

The following paper styles are available:

| Index   | Paper format           | Paper size           |
|---------|------------------------|----------------------|
| 0       | Printer default        | Printer default      |
| 1       | Letter                 | 8 1/2 x 11 in        |
| 2       | Letter Small           | 8 1/2 x 11 in        |
| 3       | Tabloid                | 11 x 17 in           |
| 4       | Ledger                 | 17 x 11 in           |
| 5       | Legal                  | 8 1/2 x 14 in        |
| 6       | Statement              | 5 1/2 x 8 1/2 in     |
| 7       | Executive              | 7 1/4 x 10 1/2 in    |
| 8       | A3                     | 297 x 420 mm         |
| 9       | A4                     | 210 x 297 mm         |
| 10      | A4 Small               | 210 x 297 mm         |
| 11      | A5                     | 148 x 210 mm         |
| 12      | B4                     | 250 x 354 mm         |
| 13      | B5                     | 182 x 257 mm         |
| 14      | Folio                  | 8 1/2 x 13 in        |
| 15      | Quarto                 | 215 x 275 mm         |
| 16      | undefined              | 10x14 in             |
| 17      | undefined              | 11x17 in             |
| 18      | Note                   | 8 1/2 x 11 in        |
| 19      | Envelope 9             | 3 7/8 x 8 7/8        |
| 20      | Envelope 10            | 4 1/8 x 9 1/2        |
| 21      | Envelope 11            | 4 1/2 x 10 3/8       |
| 22      | Envelope 12            | 4 3/4 x 11           |
| 23      | Envelope 14            | 5 x 11 1/2           |
| 24      | C size sheet           | undefined            |
| 25      | D size sheet           | undefined            |
| 26      | E size sheet           | undefined            |
| 27      | Envelope DL            | 110 x 220 mm         |
| 28      | Envelope C3            | 324 x 458 mm         |
| 29      | Envelope C4            | 229 x 324 mm         |
| 30      | Envelope C5            | 162 x 229 mm         |
| 31      | Envelope C6            | 114 x 162 mm         |
| 32      | Envelope C65           | 114 x 229 mm         |
| 33      | Envelope B4            | 250 x 353 mm         |
| 34      | Envelope B5            | 176 x 250 mm         |
| 35      | Envelope B6            | 176 x 125 mm         |
| 36      | Envelope               | 110 x 230 mm         |
| 37      | Monarch                | 3.875 x 7.5 in       |
| 38      | Envelope               | 3 5/8 x 6 1/2 in     |
| 39      | Fanfold                | 14 7/8 x 11 in       |
| 40      | German Std Fanfold     | 8 1/2 x 12 in        |
| 41      | German Legal Fanfold   | 8 1/2 x 13 in        |

**Note:** It is likely that not all of these paper types will be available to the end user since it will depend on the paper formats 
that the user's printer supports. Therefore, it is best to stick to standard paper types. If you do not specify a paper type the worksheet 
will print using the printer's default paper style.

#### Parameters

##### type?

`number`

**Default:** `0`.  
Optional integer paper format type (see table of paper styles).

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
worksheet1.setPaperType(1);  // US Letter
worksheet2.setPaperType(9);  // A4
```

***

### setPortrait()

> **setPortrait**(): `boolean`

**Set the page orientation as portrait.**  

This function is used to set the orientation of the worksheet's printed page to portrait. 
The default worksheet orientation is portrait, so this function isn't generally required.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

***

### setRow()

> **setRow**(`row`, `height?`, `format?`, `hidden?`, `level?`, `collapsed?`): `boolean`

**Set the properties for a row of cells.**  

The function is used to change the default properties of a row. The most common use for this function is to change the height of a row. 
It can also be used to create Outlines and Grouping of rows with the optional parameters `hidden`, `level` and `collapsed`. 
Adjacent rows with the same outline level are grouped together into a single outline. Rows can be collapsed by setting the parameter `hidden` 
for the hidden rows and setting the parameter `collapsed` for a row that has the collapsed '+' symbol.

#### Parameters

##### row

`number`

The zero indexed row number.

##### height?

`number`

**Default:** `15`.  
Optional row height. The default row height is 15.

##### format?

[`XLSXFormat`](XLSXFormat.md)

**Default:** `null`.  
Optional XLSXFormat object used to apply formatting to any cells in the row that don't have a format. 
As with Excel the row format is overridden by an explicit cell format.

##### hidden?

`boolean`

**Default:** `false`.  
Optional flag used to hide the row.

##### level?

`number`

**Default:** `0`.  
Optional integer outline level of the row used to create Outlines and Grouping. Excel allows up to 7 outline levels. 
Therefore the level parameter should be in the range `0 <= level <= 7`.

##### collapsed?

`boolean`

**Default:** `false`.  
Optional flag used to create Outlines and Grouping and indicating whether to collapse a row that has the collapsed '+' symbol.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### See

[setColumn](#setcolumn)

#### Example

```ts
// Set the row options with the outline level.
worksheet1.setRow(1, 15, null, false, 2, false);
worksheet1.setRow(2, 15, null, false, 2, false);
worksheet1.setRow(3, 15, null, false, 2, false);
worksheet1.setRow(4, 15, null, false, 2, false);
worksheet1.setRow(5, 15, null, false, 1, false);
worksheet1.setRow(6, 15, null, false, 2, false);
worksheet1.setRow(7, 15, null, false, 2, false);
worksheet1.setRow(8, 15, null, false, 2, false);
worksheet1.setRow(9, 15, null, false, 2, false);
worksheet1.setRow(10, 15, null, false, 1, false);
```

***

### setTabColor()

> **setTabColor**(`color`): `boolean`

**Set the color of the current worksheet tab.**

#### Parameters

##### color

`number`

The desired tab color specified using a HTML style RGB integer value.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
worksheet1.setTabColor(0xFF9900); // Orange
worksheet1.setTabColor(writer.COLOR_RED); // from Predefined values for common colors
```

***

### setVerticalPagebreaks()

> **setVerticalPagebreaks**(`breaks`): `boolean`

**Set the vertical page breaks on the current worksheet.**  

This function adds vertical page breaks to the worksheet. A page break causes all the data that follows it to be printed on the next page. 
Vertical page breaks act between columns.  

**Note:** There is an Excel limitation of 1023 vertical page breaks per worksheet.

#### Parameters

##### breaks

`number`[]

Integer array of page breaks.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
// To create a page break between columns 20 and 21 you must specify the break
// at column 21. However in zero index notation this is actually column 20:
if (!worksheet1.setVerticalPagebreaks([20]))
  throw worksheet1.getLastError();
```

***

### setZoom()

> **setZoom**(`scale?`): `boolean`

**Set the worksheet zoom factor.**  

The default zoom factor is 100.  

**Note:** This function does not affect the scale of the printed page.

#### Parameters

##### scale?

`number`

**Default:** `100`.  
Optional integer worksheet zoom factor in the range `10 <= zoom <= 400`.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
worksheet1.setZoom(50);
```

***

### splitPanes()

> **splitPanes**(`vertical`, `horizontal`): `boolean`

**Split the current worksheet into panes.**  

This function can be used to divide a worksheet into horizontal or vertical regions known as panes. 
This function is different from the function [XLSXWorksheet.freezePanes(row, col)](#freezepanes) 
in that the splits between the panes will be visible to the user and each pane will have its own scroll bars. 
The parameters `vertical` and `horizontal` are used to specify the vertical and horizontal position of the split. 
The units for `vertical` and `horizontal` are the same as those used by Excel to specify row height and column width. 
However, the vertical and horizontal units are different from each other. Therefore you must specify the `vertical` 
and `horizontal` parameters in terms of the row heights and column widths that you have set or the default values 
which are 15 for a row and 8.43 for a column.

#### Parameters

##### vertical

`number`

The position for the vertical split.

##### horizontal

`number`

The position for the horizontal split.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
worksheet1.splitPanes(15, 0);    // First row.
worksheet2.splitPanes(0, 8.43);  // First column.
worksheet3.splitPanes(15, 8.43); // First row and column.
```

***

### writeBlank()

> **writeBlank**(`row`, `col`, `format?`): `boolean`

**Write a blank cell specified by row and column.**  

This function is used to add formatting to a cell which doesn't contain a string or number value. Excel differentiates 
between an "Empty" cell and a "Blank" cell. An Empty cell is a cell which doesn't contain data or formatting whilst a Blank cell 
doesn't contain data but does contain formatting. Excel stores Blank cells but ignores Empty cells. As such, if you write 
an empty cell without formatting it is ignored.

#### Parameters

##### row

`number`

The zero indexed row number.

##### col

`number`

The zero indexed column number.

##### format?

[`XLSXFormat`](XLSXFormat.md)

**Default:** `null`.  
Optional XLSXFormat object used to apply formatting to the cell. The default value is `null` to indicate no formatting.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
format1.setBackgroundColor(writer.COLOR_RED);
worksheet1.writeBlank(0, 0, format1);
```

***

### writeBoolean()

> **writeBoolean**(`row`, `col`, `value`, `format?`): `boolean`

**Write an Excel boolean to a worksheet cell specified by row and column.**  

This function is an alternative to using [XLSXWorksheet.writeCell(type, row, col, value, format)](#writecell) 
with `type = "boolean"`.

#### Parameters

##### row

`number`

The zero indexed row number.

##### col

`number`

The zero indexed column number.

##### value

`boolean`

The boolean value to write to the cell.

##### format?

[`XLSXFormat`](XLSXFormat.md)

**Default:** `null`.  
Optional XLSXFormat object used to apply formatting to the cell. The default value is `null` to indicate no formatting.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
if (!worksheet1.writeBoolean(1,5, false))
  throw worksheet1.getLastError();
```

***

### writeCell()

> **writeCell**(`type`, `row`, `col`, `value`, `format?`): `boolean`

**Write a value to a worksheet cell.**  

This function writes a value according to the type (see below) to a worksheet cell specified by `row` and `column`.  
  
**Available value types:** 

+ **`string`**  
  A value of this type is a string. Unicode strings are supported in UTF-8 encoding. This generally requires 
  that your source file is UTF-8 encoded or that the data has been read from a UTF-8 source.
+ **`number`**  
  A value of this type is a number. The native data type for all numbers in Excel is an IEEE-754 64-bit 
  double-precision floating point, which is also the default type used by this function. According to 
  the used number format, a number can be displayed as an integer, a floating point number, a date, a currency value 
  or some other user defined format. See [XLSXFormat.setNumberFormat(numFormat)](XLSXFormat.md#setnumberformat) for more details.   

  **Note:** Excel doesn't support `NaN`, `Inf` or `-Inf` as a number value. If you are writing data that contains 
  these values then your application should convert them to a string or handle them in some other way.

   **Note:** Since DOCUMENTS 6.1.1, an empty field will be generated for an empty string or `NaN`.   
+ **`boolean`**  
  A value of this type is a boolean value.
+ **`formula`**  
  A value of this type is a string containing a formula. Formulas must be written with the US style separator/range operator 
  which is a comma (not semi-colon). Therefore a formula with multiple values should be written e.g. as follows: `"=SUM(1, 2, 3)"`.
+ **`link`**   
  A value of this type is a string containing a URL/hyperlink. The usual web style URI's are supported: `http://`, `https://`, `ftp://` and `mailto:`. 
  An Excel hyperlink is comprised of two elements: the displayed string and the non-displayed link. By default the displayed string is the same 
  as the link. However, it is possible to overwrite it with any other value type. The most common case is to overwrite the displayed link text 
  with another string:

  ```js 
  // The typical worksheet format for a hyperlink is a blue underline: 
  var urlFormat = writer.addFormat("urlFormat"); urlFormat.setFontStyle("underline"); 
  urlFormat.setFontColor(writer.COLOR_BLUE); 
  
  // Write a hyperlink but overwrite the displayed string. 
  worksheet1.writeCell("link", 2, 0, "http://libxlsxwriter.github.io", urlFormat); 
  worksheet1.writeCell("string", 2, 0, "Read the documentation.", urlFormat); 
  ```

  Two local URIs are supported: `internal:` and `external:`. These are used for hyperlinks to internal worksheet references 
  or external Excel file and worksheet references. Worksheet references are typically of the form `Worksheet1!A1`. You can also 
  link to a worksheet range using the standard Excel notation: `Worksheet1!A1:B2`.In external links the Excel file and worksheet 
  name must be separated by the `#` character: 
  ```js
  worksheet1.writeCell("link", 0, 0, "external:c:\\foo.xlsx#Worksheet2!A1", urlFormat);
  ```
  Excel requires that worksheet names containing spaces or non alphanumeric characters are single quoted as follows: 
  ```js
  worksheet1.writeCell("link", 0, 0, "internal:'Sales Data'!A1", urlFormat);
  ```
  Links to network files are also supported. 
  Network files normally begin with two back slashes as follows `\\NETWORK\etc`. 

  ```js
  worksheet1.writeCell("link", 0, 0, "external:c:/temp/foo.xlsx",     urlFormat); 
  worksheet1.writeCell("link", 1, 0, "external://NET/share/foo.xlsx", urlFormat); 
  ```

  **Note:** This function will escape the following characters in URLs as required by Excel: `\s " < > \ [ ] ^ { }` unless 
  the URL already contains `%xx` style escapes. In which case it is assumed that the URL was escaped correctly by the user 
  and will by passed directly to Excel. 
+ **`datetime`**  
  A value of this type is a Date object. Dates and times in Excel are represented by real numbers. For example a date that 
  is displayed in Excel as `"Feb 28 2013 12:00 PM"` is stored as the number `41333.5`. The integer part of the number stores 
  the number of days since the epoch, which is generally 1900, and the fractional part stores the percentage of the day. 
  A date or time in Excel is just like any other number. To display the number as a date you must apply an Excel number format to it. 

  ```js
  // Write the number without formatting. 
  worksheet1.writeCell("number", 0, 0, 41333.5);  // 41333.5 

  // Write the date without formatting. 
  worksheet1.writeCell("datetime", 0, 1, new Date(2013, 1, 28, 12)); // 41333.5 

  // Add a format with date formatting. 
  var dtFormat = writer.addFormat("dtFormat"); 
  dtFormat.setNumberFormat("mmm d yyyy hh:mm AM/PM"); 

  // Write the number with formatting. 
  worksheet1.writeCell("number", 1, 0, 41333.5, dtFormat); // Feb 28 2013 12:00 PM 

  // Write the date with formatting. 
  worksheet1.writeCell("datetime", 1, 1, new Date(2013, 1, 28, 12), dtFormat); // Feb 28 2013 12:00 PM 

  // Widen the columns to make the text clearer. 
  worksheet1.setColumn(0, 1, 20);
  ```

  Dates in Excel do not support timezones and the maximum resolution of times is milliseconds. Dates can be formatted using any of the date formats 
  supported by Excel. See [XLSXFormat.setNumberFormat(numFormat)](XLSXFormat.md#setnumberformat) for more details.
+ **`richString`**  
  This type is used to write strings with multiple formats. A value of this type is a JSON-String containing an array of objects with the property pair 
  `format` and `string`. Each object represents a fragment of the rich multi-format string with an [XLSXFormat](XLSXFormat.md) (specified with the format name or `null`) 
  to define the format for the string part. If the string fragment is unformatted then `null` can be used for the format.  

  **Note:** An empty string fragment is not allowed in a rich string.

#### Parameters

##### type

`string`

The type (see below) of the value to write to the cell.

##### row

`number`

The zero indexed row number.

##### col

`number`

The zero indexed column number.

##### value

`any`

The value to write to the cell can be specified as follows: 
 
+ String for the value types `string`, `formula`, `link` and `richString`.
+ Number for the value type `number`. 
+ Boolean for the value type `boolean`.
+ Date object for the value type `datetime`.

##### format?

[`XLSXFormat`](XLSXFormat.md)

**Default:** `null`.  
Optional [XLSXFormat](XLSXFormat.md) object used to apply formatting to the cell. The default value is `null` to indicate no formatting.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### See

[XLSXWorksheet.writeString](#writestring)  
[XLSXWorksheet.writeNumber](#writenumber)  
[XLSXWorksheet.writeBoolean](#writeboolean)  
[XLSXWorksheet.writeFormula](#writeformula)  
[XLSXWorksheet.writeLink](#writelink)  
[XLSXWorksheet.writeDatetime](#writedatetime)  
[XLSXWorksheet.writeRichString](#writerichstring)

#### Example

```ts
var writer = new XLSXWriter("c:\\tmp\\exWriteCell.xlsx");
var worksheet1 = writer.addWorksheet("Worksheet1");
var format1 = writer.addFormat("format1");
format1.setFontStyle("bold");
format1.setFontColor(writer.COLOR_RED);
format1.setNumberFormat("$#,##0.00");
var format2 = writer.addFormat("format2");
format2.setNumberFormat("d-mm-yy");
// Value type : string
if (!worksheet1.writeCell("string", 1,2,"Hello World", format1))
  throw worksheet1.getLastError();
// Value type : formula
if (!worksheet1.writeCell("formula", 1,3, "=DATEVALUE(\"1-Jan-2013\")", format2))
  throw worksheet1.getLastError();
// Value type : number
if (!worksheet1.writeCell("number", 1,4, 100, format1))
  throw worksheet1.getLastError();
// Value type : boolean
if (!worksheet1.writeCell("boolean", 1,5, false))
  throw worksheet1.getLastError();
// Value type : datetime
// Without a date format the datetime will appear as a number only.
if (!worksheet1.writeCell("datetime", 1,6, new Date(2014, 1, 14), format2))
  throw worksheet1.getLastError();
// Value type : link
if (!worksheet1.writeCell("link", 1,7, "http://libxlsxwriter.github.io"))
  throw worksheet1.getLastError();
var richString = [];
richString[0] = {};
richString[0].format = "format1";
richString[0].string = "Rich";
richString[1] = {};
richString[1].format = null;
richString[1].string = " string"; 
var jsonString = JSON.stringify(richString);
// Value type : richString
if (!worksheet1.writeCell("richString", 1, 8, jsonString))
  throw worksheet1.getLastError()
// Change the column width
worksheet1.setColumn(2, 8, 12);
worksheet1.setColumn(7, 7, 25);
if (!writer.save())
  throw writer.getLastError();
```

***

### writeDatetime()

> **writeDatetime**(`row`, `col`, `value`, `format?`): `boolean`

**Write a date or time to a worksheet cell specified by row and column.**  

This function is an alternative to using [XLSXWorksheet.writeCell(type, row, col, value, format)](#writecell) 
with `type = "datetime"`. See the value type **`datetime`** in the documentation of `XLSXWorksheet.writeCell()` for more details.

#### Parameters

##### row

`number`

The zero indexed row number.

##### col

`number`

The zero indexed column number.

##### value

`Date`

The datetime to write to the cell.

##### format?

[`XLSXFormat`](XLSXFormat.md)

**Default:** `null`.  
Optional XLSXFormat object used to apply formatting to the cell. The default value is `null` to indicate no formatting.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
if (!worksheet1.writeDatetime(1,6, new Date(2014, 1, 14), format2))
  throw worksheet1.getLastError();
```

***

### writeFormula()

> **writeFormula**(`row`, `col`, `value`, `format?`): `boolean`

**Write a formula or function to a worksheet cell specified by row and column.**  

This function is an alternative to using 
[XLSXWorksheet.writeCell(type, row, col, value, format)](#writecell) with `type = "formula"`.

#### Parameters

##### row

`number`

The zero indexed row number.

##### col

`number`

The zero indexed column number.

##### value

`string`

Formula string to write to cell. See the value type **`formula`** in the documentation of `XLSXWorksheet.writeCell()` for more details.

##### format?

[`XLSXFormat`](XLSXFormat.md)

**Default:** `null`.  
Optional XLSXFormat object used to apply formatting to the cell. The default value is `null` to indicate no formatting.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
if (!worksheet1.writeFormula(1,3, "=DATEVALUE(\"1-Jan-2013\")", format2))
  throw worksheet1.getLastError();
```

***

### writeLink()

> **writeLink**(`row`, `col`, `value`, `format?`): `boolean`

**Write a URL/hyperlink to a worksheet cell specified by row and column.**  

This function is an alternative to using [XLSXWorksheet.writeCell(type, row, col, value, format)](#writecell) 
with `type = "link"`. See the value type **`link`** in the documentation of `XLSXWorksheet.writeCell()` for more details.

#### Parameters

##### row

`number`

The zero indexed row number.

##### col

`number`

The zero indexed column number.

##### value

`string`

The URL/hyperlink to write to the cell.

##### format?

[`XLSXFormat`](XLSXFormat.md)

**Default:** `null`.  
Optional XLSXFormat object used to apply formatting to the cell. The default value is `null` to indicate no formatting.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
if (!worksheet1.writeLink(1,7, "http://libxlsxwriter.github.io"))
  throw worksheet1.getLastError();
```

***

### writeNumber()

> **writeNumber**(`row`, `col`, `value`, `format?`): `boolean`

**Write a numeric value to a worksheet cell specified by row and column.**  

This function is an alternative to using 
[XLSXWorksheet.writeCell(type, row, col, value, format)](#writecell) with `type = "number"`.

#### Parameters

##### row

`number`

The zero indexed row number.

##### col

`number`

The zero indexed column number.

##### value

`number`

The number to write to the cell. See the value type **`number`** in the documentation of `XLSXWorksheet.writeCell()` for more details.

##### format?

[`XLSXFormat`](XLSXFormat.md)

**Default:** `null`.  
Optional XLSXFormat object used to apply formatting to the cell. The default value is `null` to indicate no formatting.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
if (!worksheet1.writeNumber(1,4, 100, format1))
  throw worksheet1.getLastError();
```

***

### writeRichString()

> **writeRichString**(`row`, `col`, `value`, `format?`): `boolean`

**Write strings with multiple formats to a worksheet cell specified by row and column.**  

This function is an alternative to using 
[XLSXWorksheet.writeCell(type, row, col, value, format)](#writecell) with `type = "richString"`.

#### Parameters

##### row

`number`

The zero indexed row number.

##### col

`number`

The zero indexed column number.

##### value

`string`

A JSON-String containing an array of objects with the property pair `format` and `string`. See the value type **`richString`** 
in the documentation of `XLSXWorksheet.writeCell()` for more details.

##### format?

[`XLSXFormat`](XLSXFormat.md)

**Default:** `null`.  
Optional XLSXFormat object used to apply formatting to the cell. The default value is `null` to indicate no formatting.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
var writer = new XLSXWriter("c:\\tmp\\exWriteRichString.xlsx");
var worksheet1 = writer.addWorksheet("Worksheet1");
var format1 = writer.addFormat("format1");
format1.setFontStyle("bold");
format1.setFontColor(writer.COLOR_RED);
format1.setNumberFormat("$#,##0.00");
var format2 = writer.addFormat("format2");
format2.setFontStyle("italic");
format2.setFontColor(writer.COLOR_ORANGE);
// Array of objects with format/string pairs
var richString = [];
richString[0] = {};
richString[0].format = "format1";
richString[0].string = "Rich";
richString[1] = {};
richString[1].format = null;
richString[1].string = " string"; 
richString[2] = {};
richString[2].format = "format2";
richString[2].string = " example"; 
var jsonString = JSON.stringify(richString);
if (!worksheet1.writeRichString(0, 0, jsonString))
  throw worksheet1.getLastError()
// Change the column width
worksheet1.setColumn(0, 0, 20);
if (!writer.save())
  throw writer.getLastError();
```

***

### writeString()

> **writeString**(`row`, `col`, `value`, `format?`): `boolean`

**Write a string to a worksheet cell specified by row and column.**  

This function is an alternative to using 
[XLSXWorksheet.writeCell(type, row, col, value, format)](#writecell) with `type = "string"`.

#### Parameters

##### row

`number`

The zero indexed row number.

##### col

`number`

The zero indexed column number.

##### value

`string`

String to write to cell. See the value type **`string`** in the documentation of `XLSXWorksheet.writeCell()` for more details.

##### format?

[`XLSXFormat`](XLSXFormat.md)

**Default:** `null`.  
Optional XLSXFormat object used to apply formatting to the cell. The default value is `null` to indicate no formatting.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
if (!worksheet1.writeString(1,2,"Hello World", format1))
  throw worksheet1.getLastError();
```
