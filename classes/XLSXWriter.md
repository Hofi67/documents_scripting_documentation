[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / XLSXWriter

# Class: XLSXWriter

The XLSXWriter class allows creating files in the Excel 2007+ XLSX file format by use of the library Libxlsxwriter.  

An XLSXWriter object represents an entire Excel document. It can be used to write text, numbers, formulas and hyperlinks to multiple worksheets. 
It supports features such as:
<ul>
<li>100% compatible Excel XLSX files </li>
<li>Excel formatting </li>
<li>Merged cells </li>
<li>Autofilters </li>
<li>Charts </li>
<li>Worksheet PNG/JPEG images </li>
</ul>

**Note:** However, the XLSXWriter can only create new files. It **CANNOT READ OR MODIFY** existing files.

## Properties

### version

> **version**: `string`

**String value containing the version number of the used library Libxlsxwriter.**

#### Since

DOCUMENTS 5.0e

## Methods

### activateChartsheet()

> **activateChartsheet**(`chartsheet`): `boolean`

**Make a chartsheet the active, i.e., visible chartsheet.**  

This function is used to specify which chartsheet is initially visible in a multi-sheet Excel document.  

**Note:** More than one chartsheet can be selected via the [XLSXWriter.selectChartsheet(chartsheet)](#selectchartsheet) function, 
however only one chartsheet can be active.

#### Parameters

##### chartsheet

`any`

The chartsheet to be updated can be specified as follows: 
<ul> 
<li>String containing the chartsheet name. </li> 
<li>XLSXChartsheet object representing the chartsheet. </li> 
</ul>

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### See

[XLSXWriter.activateWorksheet](#activateworksheet)

#### Example

```ts
writer.activateChartsheet(chartsheet2);
```

***

### activateWorksheet()

> **activateWorksheet**(`worksheet`): `boolean`

**Make a worksheet the active, i.e., visible worksheet.**  

This function is used to specify which worksheet is initially visible in a multi-sheet Excel document.  

**Note:** More than one worksheet can be selected via the [XLSXWriter.selectWorksheet(worksheet)](#selectworksheet) function, however only 
one worksheet can be active. The default active worksheet is the first worksheet.

#### Parameters

##### worksheet

`any`

The worksheet to be updated can be specified as follows: 
<ul> 
<li>String containing the worksheet name. </li> 
<li>XLSXWorksheet object representing the worksheet. </li> 
</ul>

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### See

[XLSXWriter.activateChartsheet](#activatechartsheet)

#### Example

```ts
writer.activateWorksheet(worksheet2);
```

***

### addChart()

> **addChart**(`type`): [`XLSXChart`](../interfaces/XLSXChart.md)

**Create a new chart to be added to a worksheet/chartsheet.**

#### Parameters

##### type

`number`

The type (from constant group [\`Chart types\`](#chart_area)) of chart to be created.

#### Returns

[`XLSXChart`](../interfaces/XLSXChart.md)

An XLSXChart object if successful, `null` in case of any error.

#### Since

DOCUMENTS 5.0e

#### Example

```ts
// Create a chart object.
var chart = writer.addChart(writer.CHART_COLUMN);
// Add data series to the chart.
chart.addSeries(NULL, "Worksheet2!$A$1:$A$5");
chart.addSeries(NULL, "Worksheet2!$B$1:$B$5");
chart.addSeries(NULL, "Worksheet2!$C$1:$C$5");
// Insert the chart into the worksheet
worksheet2.insertChart(6, 1, chart);
```

***

### addChartsheet()

> **addChartsheet**(`name?`): [`XLSXChartsheet`](../interfaces/XLSXChartsheet.md)

**Add a new chartsheet to the current Excel document.**  

**Note:** At least one worksheet should be added to a new Excel file when creating a chartsheet in order to provide data for the chart.

#### Parameters

##### name?

`string`

Optional chartsheet name. If it is empty the default Excel convention will be followed, i.e. Chart1, Chart2, etc. 
The chartsheet name must be a valid Excel chartsheet name, i.e. it must be less than 32 character and it cannot contain any of the characters: `/ \ [ ] : * ?`  
In addition, you cannot use the same, case insensitive, `sheetname` for more than one worksheet, or chartsheet.

#### Returns

[`XLSXChartsheet`](../interfaces/XLSXChartsheet.md)

An XLSXChartsheet object if successful, `null` in case of any error.

#### Since

DOCUMENTS 5.0e

#### Example

```ts
var worksheet1 = writer.addWorksheet("Worksheet1");
var chartsheet1 = writer.addChartsheet("Chartsheet1");
```

***

### addFormat()

> **addFormat**(`name`): [`XLSXWorksheet`](../interfaces/XLSXWorksheet.md)

**Create a new format object to format cells in worksheets.**

#### Parameters

##### name

`string`

Unique format name.

#### Returns

[`XLSXWorksheet`](../interfaces/XLSXWorksheet.md)

An XLSXFormat object if successful, `null` in case of any error.

#### Since

DOCUMENTS 5.0e

#### Example

```ts
// Create the Format.
var format1 = writer.addFormat("format1");
// Set some of the format properties.
format1.setFontStyle("bold");
format1.setFontColor(writer.COLOR_RED); // see Predefined values for common colors
// Use the format to change the text format in a cell.
worksheet1.writeCell("string", 0, 0, "Hello", format1);
```

***

### addWorksheet()

> **addWorksheet**(`name?`): [`XLSXWorksheet`](../interfaces/XLSXWorksheet.md)

**Add a new worksheet to the current Excel document.**  

**Note:** At least one worksheet should be added to a new Excel file.

#### Parameters

##### name?

`string`

Optional worksheet name. If it is empty the default Excel convention will be followed, i.e. Sheet1, Sheet2, etc. 
The worksheet name must be a valid Excel worksheet name, i.e. it must be less than 32 character and it cannot contain any of the characters: `/ \ [ ] : * ?`  
In addition, you cannot use the same, case insensitive, `sheetname` for more than one worksheet, or chartsheet.

#### Returns

[`XLSXWorksheet`](../interfaces/XLSXWorksheet.md)

An XLSXWorksheet object if successful, `null` in case of any error.

#### Since

DOCUMENTS 5.0e

#### Example

```ts
var worksheet1 = writer.addWorksheet("Worksheet1");
```

***

### getChartsheetByName()

> **getChartsheetByName**(`name`): [`XLSXChartsheet`](../interfaces/XLSXChartsheet.md)

**Get a chartsheet object from its name.**

#### Parameters

##### name

`string`

Chartsheet name.

#### Returns

[`XLSXChartsheet`](../interfaces/XLSXChartsheet.md)

An XLSXChartsheet object if successful, `null` in case of any error.

#### Since

DOCUMENTS 5.0e

#### Example

```ts
var chartsheet1 = writer.getChartsheetByName("Chartsheet1");
```

***

### getFilePath()

> **getFilePath**(): `string`

**Get the file path of the created Excel file.**

#### Returns

`string`

The file path as String.

#### Since

DOCUMENTS 5.0e

#### Example

```ts
util.out(writer.getFilePath());
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

### getWorksheetByName()

> **getWorksheetByName**(`name`): [`XLSXWorksheet`](../interfaces/XLSXWorksheet.md)

**Get a worksheet object from its name.**

#### Parameters

##### name

`string`

Worksheet name.

#### Returns

[`XLSXWorksheet`](../interfaces/XLSXWorksheet.md)

An XLSXWorksheet object if successful, `null` in case of any error.

#### Since

DOCUMENTS 5.0e

#### Example

```ts
var worksheet1 = writer.getWorksheetByName("Worksheet1");
```

***

### hideChartsheet()

> **hideChartsheet**(`chartsheet`): `boolean`

**Hide the given chartsheet.**  

**Note:** A hidden chartsheet can not be activated or selected so this function is mutually exclusive with the 
[XLSXWriter.activateChartsheet(chartsheet)](#activatechartsheet) and 
[XLSXWriter.selectChartsheet(chartsheet)](#selectchartsheet) functions.

#### Parameters

##### chartsheet

`any`

The chartsheet to be updated can be specified as follows: 
<ul> 
<li>String containing the chartsheet name. </li> 
<li>XLSXChartsheet object representing the chartsheet. </li> 
</ul>

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### See

[XLSXWriter.hideWorksheet](#hideworksheet)

#### Example

```ts
writer.activateChartsheet(chartsheet2);
writer.hideChartsheet(chartsheet1);
```

***

### hideWorksheet()

> **hideWorksheet**(`worksheet`): `boolean`

**Hide the given worksheet.**  

**Note:** A hidden worksheet can not be activated or selected so this function is mutually exclusive with the 
[XLSXWriter.activateWorksheet(worksheet)](#activateworksheet) and 
[XLSXWriter.selectWorksheet(worksheet)](#selectworksheet) functions. In addition, 
since the first worksheet will default to being the active worksheet, you cannot hide the first worksheet without activating another sheet.

#### Parameters

##### worksheet

`any`

The worksheet to be updated can be specified as follows: 
<ul> 
<li>String containing the worksheet name. </li> 
<li>XLSXWorksheet object representing the worksheet. </li> 
</ul>

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### See

[XLSXWriter.hideChartsheet](#hidechartsheet)

#### Example

```ts
writer.hideWorksheet(worksheet2);
```

***

### save()

> **save**(): `boolean`

**Write the Excel file to disk and free any memory allocated internally to the Excel file.**  

**Note:** After calling this function only both functions [XLSXWriter.getFilePath()](#getfilepath) and 
[XLSXWriter.getLastError()](#getlasterror) are available for the XLSXWriter object.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
if (!writer.save())
  util.out(writer.getLastError());
```

***

### selectChartsheet()

> **selectChartsheet**(`chartsheet`): `boolean`

**Set a chartsheet tab as selected.**  

This function is used to indicate that a chartsheet is selected in a multi-sheet Excel document.  

**Note:** A selected chartsheet has its tab highlighted. Selecting chartsheets is a way of grouping them together so that, 
for example, several chartsheets could be printed in one go. A chartsheet that has been activated via the 
[XLSXWriter.activateChartsheet(chartsheet)](#activatechartsheet) function will also appear as selected.

#### Parameters

##### chartsheet

`any`

The chartsheet to be updated can be specified as follows: 
<ul> 
<li>String containing the chartsheet name. </li> 
<li>XLSXChartsheet object representing the chartsheet. </li> 
</ul>

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### See

[XLSXWriter.selectWorksheet](#selectworksheet)

#### Example

```ts
writer.selectChartsheet("Chartsheet2");
```

***

### selectWorksheet()

> **selectWorksheet**(`worksheet`): `boolean`

**Set a worksheet tab as selected.**  

This function is used to indicate that a worksheet is selected in a multi-sheet Excel document.  

**Note:** A selected worksheet has its tab highlighted. Selecting worksheets is a way of grouping them together so that, 
for example, several worksheets could be printed in one go. A worksheet that has been activated via the 
[XLSXWriter.activateWorksheet(worksheet)](#activateworksheet) function will also appear as selected.

#### Parameters

##### worksheet

`any`

The worksheet to be updated can be specified as follows: 
<ul> 
<li>String containing the worksheet name. </li> 
<li>XLSXWorksheet object representing the worksheet. </li> 
</ul>

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### See

[XLSXWriter.selectChartsheet](#selectchartsheet)

#### Example

```ts
writer.selectWorksheet(worksheet2);
```

***

### setProperties()

> **setProperties**(`title`, `subject`, `author`, `manager`, `company`, `category`, `keywords`, `comments`, `status`, `hyperlinkBase`): `boolean`

**Set the document properties.**  

This function can be used to set the document properties of the current Excel document. These properties are visible in Excel 
(e.g. under `File -> Information -> Properties` in Excel 2013) and are also available to external applications that read or index windows files.

#### Parameters

##### title

`string`

Title of the Excel document.

##### subject

`string`

Optional subject of the Excel document.

##### author

`string`

Optional author of the Excel document.

##### manager

`string`

Optional manager field of the Excel document.

##### company

`string`

Optional company field of the Excel document.

##### category

`string`

Optional category of the Excel document.

##### keywords

`string`

Optional keywords of the Excel document.

##### comments

`string`

Optional comment of the Excel document.

##### status

`string`

Optional status of the Excel document.

##### hyperlinkBase

`string`

Optional hyperlink base url of the Excel document.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
writer.setProperties("This is an example spreadsheet");
```

## Background Patterns

These constants build an enumeration of the available fill patterns for the background of a cell.  
**Since** DOCUMENTS 5.0e  
**See** [XLSXFormat.setBackgroundPattern(pattern)](../interfaces/XLSXFormat.md#setbackgroundpattern)

### PATTERN\_DARK\_DOWN

> **PATTERN\_DARK\_DOWN**: `number`

Dark diagonal stripe pattern

***

### PATTERN\_DARK\_GRAY

> **PATTERN\_DARK\_GRAY**: `number`

Dark gray pattern

***

### PATTERN\_DARK\_GRID

> **PATTERN\_DARK\_GRID**: `number`

Dark grid pattern

***

### PATTERN\_DARK\_HORIZONTAL

> **PATTERN\_DARK\_HORIZONTAL**: `number`

Dark horizontal line pattern

***

### PATTERN\_DARK\_TRELLIS

> **PATTERN\_DARK\_TRELLIS**: `number`

Dark trellis pattern

***

### PATTERN\_DARK\_UP

> **PATTERN\_DARK\_UP**: `number`

Reverse dark diagonal stripe pattern

***

### PATTERN\_DARK\_VERTICAL

> **PATTERN\_DARK\_VERTICAL**: `number`

Dark vertical line pattern

***

### PATTERN\_GRAY\_0625

> **PATTERN\_GRAY\_0625**: `number`

6.25% gray pattern

***

### PATTERN\_GRAY\_125

> **PATTERN\_GRAY\_125**: `number`

12.5% gray pattern

***

### PATTERN\_LIGHT\_DOWN

> **PATTERN\_LIGHT\_DOWN**: `number`

Light diagonal stripe pattern

***

### PATTERN\_LIGHT\_GRAY

> **PATTERN\_LIGHT\_GRAY**: `number`

Light gray pattern

***

### PATTERN\_LIGHT\_GRID

> **PATTERN\_LIGHT\_GRID**: `number`

Light grid pattern

***

### PATTERN\_LIGHT\_HORIZONTAL

> **PATTERN\_LIGHT\_HORIZONTAL**: `number`

Light horizontal Line pattern

***

### PATTERN\_LIGHT\_TRELLIS

> **PATTERN\_LIGHT\_TRELLIS**: `number`

Light trellis pattern

***

### PATTERN\_LIGHT\_UP

> **PATTERN\_LIGHT\_UP**: `number`

Reverse light diagonal stripe pattern

***

### PATTERN\_LIGHT\_VERTICAL

> **PATTERN\_LIGHT\_VERTICAL**: `number`

Light vertical line pattern

***

### PATTERN\_MEDIUM\_GRAY

> **PATTERN\_MEDIUM\_GRAY**: `number`

Medium gray pattern

***

### PATTERN\_NONE

> **PATTERN\_NONE**: `number`

Empty pattern

***

### PATTERN\_SOLID

> **PATTERN\_SOLID**: `number`

Solid pattern

## Cell border styles

The constants build an enumeration of the available values for cell border styles.  
**Since** DOCUMENTS 5.0e  
**See** [XLSXFormat.setBorderStyle(border, style)](../interfaces/XLSXFormat.md#setborderstyle)

### BORDER\_DASH\_DOT

> **BORDER\_DASH\_DOT**: `number`

Dash-dot border style

***

### BORDER\_DASH\_DOT\_DOT

> **BORDER\_DASH\_DOT\_DOT**: `number`

Dash-dot-dot border style

***

### BORDER\_DASHED

> **BORDER\_DASHED**: `number`

Dashed border style

***

### BORDER\_DOTTED

> **BORDER\_DOTTED**: `number`

Dotted border style

***

### BORDER\_DOUBLE

> **BORDER\_DOUBLE**: `number`

Double border style

***

### BORDER\_HAIR

> **BORDER\_HAIR**: `number`

Hair border style

***

### BORDER\_MEDIUM

> **BORDER\_MEDIUM**: `number`

Medium border style

***

### BORDER\_MEDIUM\_DASH\_DOT

> **BORDER\_MEDIUM\_DASH\_DOT**: `number`

Medium dash-dot border style

***

### BORDER\_MEDIUM\_DASH\_DOT\_DOT

> **BORDER\_MEDIUM\_DASH\_DOT\_DOT**: `number`

Medium dash-dot-dot border style

***

### BORDER\_MEDIUM\_DASHED

> **BORDER\_MEDIUM\_DASHED**: `number`

Medium dashed border style

***

### BORDER\_NONE

> **BORDER\_NONE**: `number`

No border

***

### BORDER\_SLANT\_DASH\_DOT

> **BORDER\_SLANT\_DASH\_DOT**: `number`

Slant dash-dot border style

***

### BORDER\_THICK

> **BORDER\_THICK**: `number`

hick border style

***

### BORDER\_THIN

> **BORDER\_THIN**: `number`

Thin border style

## Chart types

These constants build an enumeration of the available chart types.  
**Since** DOCUMENTS 5.0e  
**See** [XLSXWriter.addChart(type)](#addchart)

### CHART\_AREA

> **CHART\_AREA**: `number`

Area chart

***

### CHART\_AREA\_STACKED

> **CHART\_AREA\_STACKED**: `number`

Area chart - stacked

***

### CHART\_AREA\_STACKED\_PERCENT

> **CHART\_AREA\_STACKED\_PERCENT**: `number`

Area chart - percentage stacked

***

### CHART\_BAR

> **CHART\_BAR**: `number`

Bar chart

***

### CHART\_BAR\_STACKED

> **CHART\_BAR\_STACKED**: `number`

Bar chart - stacked

***

### CHART\_BAR\_STACKED\_PERCENT

> **CHART\_BAR\_STACKED\_PERCENT**: `number`

Bar chart - percentage stacked

***

### CHART\_COLUMN

> **CHART\_COLUMN**: `number`

Column chart

***

### CHART\_COLUMN\_STACKED

> **CHART\_COLUMN\_STACKED**: `number`

Column chart - stacked

***

### CHART\_COLUMN\_STACKED\_PERCENT

> **CHART\_COLUMN\_STACKED\_PERCENT**: `number`

Column chart - percentage stacked

***

### CHART\_DOUGHNUT

> **CHART\_DOUGHNUT**: `number`

Doughnut chart

***

### CHART\_LINE

> **CHART\_LINE**: `number`

Line chart

***

### CHART\_PIE

> **CHART\_PIE**: `number`

Pie chart

***

### CHART\_RADAR

> **CHART\_RADAR**: `number`

Radar chart

***

### CHART\_RADAR\_FILLED

> **CHART\_RADAR\_FILLED**: `number`

Radar chart - filled

***

### CHART\_RADAR\_WITH\_MARKERS

> **CHART\_RADAR\_WITH\_MARKERS**: `number`

Radar chart - with markers

***

### CHART\_SCATTER

> **CHART\_SCATTER**: `number`

Scatter chart

***

### CHART\_SCATTER\_SMOOTH

> **CHART\_SCATTER\_SMOOTH**: `number`

Scatter chart - smooth

***

### CHART\_SCATTER\_SMOOTH\_WITH\_MARKERS

> **CHART\_SCATTER\_SMOOTH\_WITH\_MARKERS**: `number`

Scatter chart - smooth with markers

***

### CHART\_SCATTER\_STRAIGHT

> **CHART\_SCATTER\_STRAIGHT**: `number`

Scatter chart - straight

***

### CHART\_SCATTER\_STRAIGHT\_WITH\_MARKERS

> **CHART\_SCATTER\_STRAIGHT\_WITH\_MARKERS**: `number`

Scatter chart - straight with markers

## Constructors

### Constructor

> **new XLSXWriter**(`filename`): `XLSXWriter`

**Create a new XLSXWriter object with a given filename.**  

**Note:** When specifying a filename it is recommended that you use an .xlsx extension or Excel will generate a warning when opening the file.  
  
**Since:** DOCUMENTS 5.0e

#### Parameters

##### filename

`string`

The name of the new Excel file to create.

#### Returns

`XLSXWriter`

#### Since

DOCUMENTS 5.0e

#### Example

```ts
var writer = new XLSXWriter("c:\\tmp\\writer.xlsx");
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
// Add an other worksheet with a user defined sheet name.
var worksheet2 = writer.addWorksheet("Worksheet2");
// Write some data to the worksheet.
writeWorksheetData(worksheet2);
// Create a chart object.
var chart = writer.addChart(writer.CHART_COLUMN);
// Configure the chart. In simplest case we just add some value data
// series. The empty categories will default to 1 to 5 like in Excel.
var series1 = chart.addSeries("", "=Worksheet2!$A$1:$A$5");
var series2 = chart.addSeries("", "=Worksheet2!$B$1:$B$5");
var series3 = chart.addSeries("", "=Worksheet2!$C$1:$C$5");
// Insert the chart into the worksheet
worksheet2.insertChart(6, 1, chart);
// Save the file.
if (!writer.save())
    throw writer.getLastError();
  
function writeWorksheetData(worksheet)
{
    var data = [
        // Three columns of data.
        [1,   2,   3],
        [2,   4,   6],
        [3,   6,   9],
        [4,   8,  12],
        [5,  10,  15]
    ];
    var row, col;
    for (row = 0; row < 5; row++)
        for (col = 0; col < 3; col++)
            worksheet.writeCell("number", row, col, data[row][col]);
}
```

## Predefined values for common colors

The colors are specified using a HTML style RGB integer value. For convenience a limited number of common colors are predefined as follows.  
 
**Note:** Black in HTML is actually `0x000000` but [\`XLSXWriter.COLOR\_BLACK\`](#color_black) is defined as `0x1000000` 
to avoid confusion with an undefined or Zero color value. It is converted to the correct HTML code internally.  
 
**Since** DOCUMENTS 5.0e  
  
**See**    
[XLSXWorksheet.setTabColor(color)](../interfaces/XLSXWorksheet.md#settabcolor)  
[XLSXChartsheet.setTabColor(color)](../interfaces/XLSXChartsheet.md#settabcolor)  
[XLSXFormat.setFontColor(color)](../interfaces/XLSXFormat.md#setfontcolor)  
[XLSXFormat.setBorderColor(border, color)](../interfaces/XLSXFormat.md#setbordercolor)  
[XLSXFormat.setForegroundColor(color)](../interfaces/XLSXFormat.md#setforegroundcolor)  
[XLSXFormat.setBackgroundColor(color)](../interfaces/XLSXFormat.md#setbackgroundcolor)

### COLOR\_BLACK

> **COLOR\_BLACK**: `number`

Black defined as `0x1000000`

***

### COLOR\_BLUE

> **COLOR\_BLUE**: `number`

Blue defined as `0x0000FF`

***

### COLOR\_BROWN

> **COLOR\_BROWN**: `number`

Brown defined as `0x800000`

***

### COLOR\_CYAN

> **COLOR\_CYAN**: `number`

Cyan defined as `0x00FFFF`

***

### COLOR\_GRAY

> **COLOR\_GRAY**: `number`

Gray defined as `0x808080`

***

### COLOR\_GREEN

> **COLOR\_GREEN**: `number`

Green defined as `0x008000`

***

### COLOR\_LIME

> **COLOR\_LIME**: `number`

Lime defined as `0x00FF00`

***

### COLOR\_MAGENTA

> **COLOR\_MAGENTA**: `number`

Magenta defined as `0xFF00FF`

***

### COLOR\_NAVY

> **COLOR\_NAVY**: `number`

Navy defined as `0x000080`

***

### COLOR\_ORANGE

> **COLOR\_ORANGE**: `number`

Orange defined as `0xFF6600`

***

### COLOR\_PINK

> **COLOR\_PINK**: `number`

Pink defined as `0xFF00FF`

***

### COLOR\_PURPLE

> **COLOR\_PURPLE**: `number`

Purple defined as `0x800080`

***

### COLOR\_RED

> **COLOR\_RED**: `number`

Red defined as `0xFF0000`

***

### COLOR\_SILVER

> **COLOR\_SILVER**: `number`

Silver defined as `0xC0C0C0`

***

### COLOR\_WHITE

> **COLOR\_WHITE**: `number`

White defined as `0xFFFFFF`

***

### COLOR\_YELLOW

> **COLOR\_YELLOW**: `number`

Yellow defined as `0xFFFF00`

## Text alignments

These constants build an enumeration of the available values for the horizontal and vertical text alignment within a cell.  
**Since** DOCUMENTS 5.0e   
**See** [XLSXFormat.setAlign(alignment)](../interfaces/XLSXFormat.md#setalign)

### ALIGN\_CENTER

> **ALIGN\_CENTER**: `number`

Center horizontal alignment

***

### ALIGN\_CENTER\_ACROSS

> **ALIGN\_CENTER\_ACROSS**: `number`

Center Across horizontal alignment

***

### ALIGN\_DISTRIBUTED

> **ALIGN\_DISTRIBUTED**: `number`

Distributed horizontal alignment

***

### ALIGN\_FILL

> **ALIGN\_FILL**: `number`

Cell fill horizontal alignment

***

### ALIGN\_JUSTIFY

> **ALIGN\_JUSTIFY**: `number`

Justify horizontal alignment

***

### ALIGN\_LEFT

> **ALIGN\_LEFT**: `number`

Left horizontal alignment

***

### ALIGN\_NONE

> **ALIGN\_NONE**: `number`

No alignment. Cell will use Excel's default for the data type

***

### ALIGN\_RIGHT

> **ALIGN\_RIGHT**: `number`

Right horizontal alignment

***

### ALIGN\_VERTICAL\_BOTTOM

> **ALIGN\_VERTICAL\_BOTTOM**: `number`

Bottom vertical alignment

***

### ALIGN\_VERTICAL\_CENTER

> **ALIGN\_VERTICAL\_CENTER**: `number`

Center vertical alignment

***

### ALIGN\_VERTICAL\_DISTRIBUTED

> **ALIGN\_VERTICAL\_DISTRIBUTED**: `number`

Distributed vertical alignment

***

### ALIGN\_VERTICAL\_JUSTIFY

> **ALIGN\_VERTICAL\_JUSTIFY**: `number`

Justify vertical alignment

***

### ALIGN\_VERTICAL\_TOP

> **ALIGN\_VERTICAL\_TOP**: `number`

Top vertical alignment
