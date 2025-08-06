[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / XLSXChart

# Interface: XLSXChart

**The XLSXChart class allows creating an Excel chart.**  

An XLSXChart object represents an Excel chart. It provides functions for adding data series to the chart and for configuring the chart. 
An XLSXChart object isn't created directly. Instead it is created by calling the [XLSXWriter.addChart(number type)](../classes/XLSXWriter.md#addchart) 
function from an [XLSXWriter](../classes/XLSXWriter.md) object.  
   
The basic procedure for adding a chart to a worksheet is: 

+ Create the chart with `XLSXWriter.addChart()`.
+ Add one or more data series to the chart which refers to data in the Excel file using `XLSXChart.addSeries()`.
+ Configure the chart with the other available functions shown below. 
+ Insert the chart into a worksheet using `XLSXWorksheet.insertChart()`.

## Since

DOCUMENTS 5.0e

## See

[XLSXWriter.addChart](../classes/XLSXWriter.md#addchart)  
[XLSXChart.addSeries](#addseries)  
[XLSXWorksheet.insertChart](XLSXWorksheet.md#insertchart)  
[XLSXChartsheet.insertChart](XLSXChartsheet.md#insertchart)

## Example

```ts
var writer = new XLSXWriter("c:\\tmp\\chart.xlsx");
var worksheet1 = writer.addWorksheet("Worksheet1");
// Write some data to the worksheet.
writeWorksheetData(worksheet1);
// Create a chart object.
var chart = writer.addChart(writer.CHART_COLUMN);
// Configure the chart. In simplest case we just add some value data series. 
// The empty categories will default to 1 to 6 like in Excel.
var series1 = chart.addSeries("", "=Worksheet1!$A$1:$A$6");
var series2 = chart.addSeries("", "=Worksheet1!$B$1:$B$6");
var series3 = chart.addSeries("", "=Worksheet1!$C$1:$C$6");
chart.setTable(); // Turn on the data table
chart.setStyle(37);
chart.setTitle("Chart with Data Table");
// Insert the chart into the worksheet
worksheet1.insertChart(8, 1, chart);
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
        [5,  10,  15],
        [6,  12,  18]
    ];
    var row, col;
    for (row = 0; row < 6; row++)
        for (col = 0; col < 3; col++)
            worksheet.writeCell("number", row, col, data[row][col]);
}
```

## Methods

### addSeries()

> **addSeries**(`categories?`, `values?`): [`XLSXChartSeries`](XLSXChartSeries.md)

**Add a data series to the current chart.**  

The series numbering and order in the Excel chart will be the same as the order in which they are added with this function.

#### Parameters

##### categories?

`string`

Optional range of categories in the data series being a string formula like `"=Worksheet1!$A$1:$A$6"`. 
The category is more or less the same as the X axis. In most Excel chart types the `categories` property is optional and 
the chart will just assume a sequential series from `1..n`.

##### values?

`string`

Optional range of values in the data series being a string formula like `"=Worksheet1!$A$1:$A$6"`. 
This parameter links the chart with the worksheet data that it displays.

#### Returns

[`XLSXChartSeries`](XLSXChartSeries.md)

An XLSXChartSeries object if successful, `null` in case of any error.

#### Since

DOCUMENTS 5.0e

#### See

[XLSXChartSeries.setCategories](XLSXChartSeries.md#setcategories)  
[XLSXChartSeries.setValues](XLSXChartSeries.md#setvalues)

#### Example

```ts
// The empty categories will default to 1 to 6 like in Excel.
var series1 = chart1.addSeries("", "=Worksheet1!$A$1:$A$6");
var series2 = chart1.addSeries("", "=Worksheet1!$B$1:$B$6");
// It is also possible to specify non-contiguous ranges:
chart2.addSeries("=(Sheet1!$A$1:$A$9,Sheet1!$A$14:$A$25)", "=(Sheet1!$B$1:$B$9,Sheet1!$B$14:$B$25)");
```

***

### getAxis()

> **getAxis**(`axisType`): [`XLSXChartAxis`](XLSXChartAxis.md)

**Get an axis from the chart.**

#### Parameters

##### axisType

`string`

The axis type: `x` or `y`.

#### Returns

[`XLSXChartAxis`](XLSXChartAxis.md)

An XLSXChartAxis object if successful, `null` in case of any error.

#### Since

DOCUMENTS 5.0e

#### Example

```ts
var xAxis = chart.getAxis("x");
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

### setStyle()

> **setStyle**(`styleId?`): `boolean`

**Set the chart style type.**  

This function is used to set the style of the chart to one of the 48 built-in styles available on the "Design" tab in Excel 2007.  

**Note:** In Excel 2013 the Styles section of the "Design" tab in Excel shows what were referred to as "Layouts" in previous versions of Excel. 
These layouts are not defined in the file format. They are a collection of modifications to the base chart type. They can not be defined by this function.

#### Parameters

##### styleId?

`number`

Optional index representing the chart style, 1 - 48. The style index number is counted from 1 on the top left in the Excel dialog. The default style is 2.  

**Default:** `2`

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
chart.setStyle(37);
```

***

### setTable()

> **setTable**(): `boolean`

**Add a data table below the horizontal axis with the data used to plot the chart.**  

**Note:** The data table can only be shown with Bar, Column, Line and Area charts.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

***

### setTitle()

> **setTitle**(`title`): `boolean`

**Set the title of the chart.**

#### Parameters

##### title

`string`

The chart title displayed above the chart. This parameter can also be a formula such as `"=Worksheet1!$A$1"` to 
point to a cell in the Excel file that contains the title. The Excel default is to have no chart title.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### See

[XLSXChart.setTitleRange](#settitlerange)

#### Example

```ts
chart1.setTitle("Test Results");
chart2.setTitle("=Worksheet1!$B$1");
```

***

### setTitleRange()

> **setTitleRange**(`sheetname`, `row`, `col`): `boolean`

**Set a chart title formula using row and column values.**  

This function can be used to set a chart title range and is an alternative to using [XLSXChart.setTitle(String title)](#settitle) and a string formula.

#### Parameters

##### sheetname

`string`

The name of the worksheet that contains the cell range.

##### row

`number`

The zero indexed row number of the range.

##### col

`number`

The zero indexed column number of the range.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
chart2.setTitleRange("Worksheet1", 0, 1);
```
