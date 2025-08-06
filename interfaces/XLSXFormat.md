[**Portalscript API (internal)**](../README.md)

***

[Portalscript API (internal)](../globals.md) / XLSXFormat

# Interface: XLSXFormat

**The XLSXFormat class allows formatting cells in Excel.**  

An XLSXFormat object isn't created directly. Instead an XLSXFormat is created by calling 
the [XLSXWriter.addFormat(name)](../classes/XLSXWriter.md#addformat) function from an [XLSXWriter](../classes/XLSXWriter.md) object. 
The properties of a cell that can be formatted include: fonts, colors, patterns, borders, alignment and number formatting.

## Since

DOCUMENTS 5.0e

## Example

```ts
var writer = new XLSXWriter("c:\\tmp\\format.xlsx");
// Add a worksheet with a user defined sheet name.
var worksheet1 = writer.addWorksheet("Worksheet1");
// Add a cell format.
var format1 = writer.addFormat("format1");
// Set the font name for the format
format1.setFontName("Times New Roman");
// Set the bold property for the format.
format1.setFontStyle("bold");
// Set the alignment for the format
format1.setAlign(writer.ALIGN_CENTER);
// Wrap text in a cell
format1.setTextWrap();
// Set cell border color
format1.setBorderColor("right", writer.COLOR_RED);
// Set cell border style
format1.setBorderStyle("right", writer.BORDER_DOUBLE);
// Write a string using the format
worksheet1.writeCell("string", 0, 0, "Some long text to wrap in a cell", format1);
// Set a number format
format1.setNumberFormat("0 \"dollar and\" .00 \"cents\"");
// Write a number using the format.
worksheet1.writeCell("number", 0, 1, 1.87, format1);
// Change the column width
worksheet1.setColumn(1, 1, 30);
// Save the file.
if (!writer.save())
    throw writer.getLastError();
```

## Methods

### getLastError()

> **getLastError**(): `string`

**Function to get the description of the last error that occurred.**

#### Returns

`string`

Text of the last error as String

#### Since

DOCUMENTS 5.0e

***

### setAlign()

> **setAlign**(`alignment`): `boolean`

**Set the alignment for data in a cell.**  

As in Excel, vertical and horizontal alignments can be combined. Text can be aligned across two or more adjacent cells using the center_across property. 
However, for genuine merged cells it is better to use the `XLSXWorksheet.mergeRange()` method. The vertical justify option can be used to provide automatic 
text wrapping in a cell. The height of the cell will be adjusted to accommodate the wrapped text.

#### Parameters

##### alignment

`number`

The horizontal or vertical alignment direction (see constant group [\`Text alignments\`](../classes/XLSXWriter.md#align_center)).

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### See

[XLSXWorksheet.mergeRange](XLSXWorksheet.md#mergerange)  
[XLSXFormat.setTextWrap](#settextwrap)

#### Example

```ts
var format1 = writer.addFormat("format1");
// Vertical and horizontal alignments can be combined
format1.setAlign(writer.ALIGN_CENTER);
format1.setAlign(writer.ALIGN_VERTICAL_CENTER);
```

***

### setBackgroundColor()

> **setBackgroundColor**(`color`): `boolean`

**Set the background color of the pattern for a cell.**

#### Parameters

##### color

`number`

The cell pattern background color being a RGB integer value.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

***

### setBackgroundPattern()

> **setBackgroundPattern**(`pattern`): `boolean`

**Set the background fill pattern for a cell.**

#### Parameters

##### pattern

`number`

Pattern index from constant group [\`Background patterns\`](../classes/XLSXWriter.md#pattern_dark_down).

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
var format1 = writer.addFormat("format1");
// The most common pattern is a solid fill of the background color.
format1.setBackgroundPattern(writer.PATTERN_SOLID);
format1.setBackgroundColor(writer.COLOR_YELLOW);
```

***

### setBorderColor()

> **setBorderColor**(`border`, `color`): `boolean`

**Set the color of the cell border.**

#### Parameters

##### border

`string`

String specifying which cell border(s) the color to be set for. The following values are available: 
 
+ `left`: the left cell border
+ `right`: the right cell border
+ `top`: the top cell border
+ `bottom`: the bottom cell border
+ `all`: all cell borders

##### color

`number`

The desired cell border color being a RGB integer value.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
var format1 = writer.addFormat("format1");
format1.setBorderColor("bottom", writer.COLOR_RED);
format1.setBorderStyle("bottom", writer.BORDER_DOUBLE);
```

***

### setBorderStyle()

> **setBorderStyle**(`border`, `style`): `boolean`

**Set the cell border style.**

#### Parameters

##### border

`string`

String specifying which cell border(s) the style to be set for. The following values are available: 

+ `left`: the left cell border
+ `right`: the right cell border 
+ `top`: the top cell border 
+ `bottom`: the bottom cell border
+ `all`: all cell borders

##### style

`number`

Border style index from constant group [\`Cell border styles\`](../classes/XLSXWriter.md#border_dashed).

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
var format1 = writer.addFormat("format1");
format1.setBorderStyle("bottom", writer.BORDER_THIN);
```

***

### setFontColor()

> **setFontColor**(`color`): `boolean`

**Set the color of the font used in the cell.**

#### Parameters

##### color

`number`

The cell font color being a RGB integer value.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

***

### setFontName()

> **setFontName**(`name`): `boolean`

**Set the font used in the cell.**  

**Note:** Excel can only display fonts that are installed on the system that it is running on. Therefore it is generally best to 
use the fonts that come as standard with Excel such as Calibri, Times New Roman and Courier New. The default font in Excel 2007, and later, is Calibri.

#### Parameters

##### name

`string`

Optional String containing the cell font name. The default value is "Calibri".

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

***

### setFontScript()

> **setFontScript**(`style`): `boolean`

**Set the script style of the font.**

#### Parameters

##### style

`string`

Script style. The following styles are available: 

+ `super`:superscript style
+ `sub`: subscript style

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

***

### setFontSize()

> **setFontSize**(`size`): `boolean`

**Set the size of the font used in the cell.**  

**Note:** Excel adjusts the height of a row to accommodate the largest font size in the row. You can also explicitly 
specify the height of a row using the `XLSXWorksheet.setRow()` function.

#### Parameters

##### size

`number`

The cell font size.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

***

### setFontStyle()

> **setFontStyle**(`style`): `boolean`

**Set the font style for the format.**

#### Parameters

##### style

`string`

String containing the font style. The following font styles are available: 

+ `bold` 
+ `italic` 
+ `underline`
+ `strikeout`

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
var format1 = writer.addFormat("format1");
format1.setFontStyle("bold");
```

***

### setForegroundColor()

> **setForegroundColor**(`color`): `boolean`

**Set the foreground color of the pattern for a cell.**

#### Parameters

##### color

`number`

The cell pattern foreground color being a RGB integer value.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

***

### setIndent()

> **setIndent**(`level`): `boolean`

**Set the cell text indentation level.**  

**Note:** Indentation is a horizontal alignment property. It will override any other horizontal properties but it can be used in conjunction with vertical properties.

#### Parameters

##### level

`number`

Integer indentation level.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
var format1 = writer.addFormat("format1");
var format2 = writer.addFormat("format2");
format1.setIndent(1);
format2.setIndent(2);
worksheet1.writeString(0, 0, "This text is indented 1 level",  format1);
worksheet1.writeString(1, 0, "This text is indented 2 levels", format2);
```

***

### setNumberFormat()

> **setNumberFormat**(`numFormat`): `boolean`

**Set the number format for a cell.**  

This method is used to define the numerical format of a number in Excel. It controls whether a number is displayed as an integer, a floating point number, 
a date, a currency value or some other user defined format. For more information about number formats in Excel refer to the 
[Microsoft documentation for number formats](https://support.office.com/en-us/article/review-guidelines-for-customizing-a-number-format-c0a1d1fa-d3f4-4018-96b7-9c9354dd99f5).

#### Parameters

##### numFormat

`string`

The numerical format of a cell specified by using a format string.

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
var writer = new XLSXWriter("c:\\tmp\\numFormat.xlsx");
// Add a worksheet with a user defined sheet name.
var worksheet1 = writer.addWorksheet("Worksheet1");
// Widen the first column to make the text clearer. 
worksheet1.setColumn(0, 0, 30);
// Add some formats.
var format01 = writer.addFormat("format01"); 
var format02 = writer.addFormat("format02");
var format03 = writer.addFormat("format03");
var format04 = writer.addFormat("format04");
var format05 = writer.addFormat("format05");
var format06 = writer.addFormat("format06");
var format07 = writer.addFormat("format07");
var format08 = writer.addFormat("format08");
var format09 = writer.addFormat("format09");
var format10 = writer.addFormat("format10");
var format11 = writer.addFormat("format11");
// Set some example number formats.
format01.setNumberFormat("0.000");
format02.setNumberFormat("#,##0");
format03.setNumberFormat("#,##0.00");
format04.setNumberFormat("0.00");
format05.setNumberFormat("mm/dd/yyyy");
format06.setNumberFormat("mmm d yyyy");
format07.setNumberFormat("d mmmm yyyy");
format08.setNumberFormat("dd/mm/yyyy hh:mm AM/PM");
format09.setNumberFormat("0 \"dollar and\" .00 \"cents\"");
// Write data using the formats.
worksheet1.writeCell("number", 0, 0, 3.1415926); // 3.1415926
worksheet1.writeCell("number", 1, 0, 3.1415926, format01); // 3.142
worksheet1.writeCell("number", 2, 0, 1234.56, format02); // 1,235 
worksheet1.writeCell("number", 3, 0, 1234.56, format03); // 1,234.56
worksheet1.writeCell("number", 4, 0, 49.99, format04); // 49.99
worksheet1.writeCell("number", 5, 0, 36892.521, format05); // 01/01/2001
worksheet1.writeCell("number", 6, 0, 36892.521, format06); // Jan 1 2001
worksheet1.writeCell("number", 7, 0, 36892.521, format07); // 1 January 2001
worksheet1.writeCell("number", 8, 0, 36892.521, format08); // 01/01/2001 12:30 PM
worksheet1.writeCell("number", 9, 0, 1.87, format09); // 1 dollar and .87 cents
// Show limited conditional number formats.
format10.setNumberFormat("[Green]General;[Red]-General;General");
worksheet1.writeCell("number", 10, 0, 123, format10);  // > 0 Green
worksheet1.writeCell("number", 11, 0, -45, format10);  // < 0 Red
worksheet1.writeCell("number", 12, 0,   0, format10);  // = 0 Default color
// Format a Zip code.
format11.setNumberFormat("00000");
worksheet1.writeCell("number", 13, 0, 1209, format11);
worksheet1.setGridlines("showPrint");
// Save the file.
if (!writer.save())
    throw writer.getLastError();
```

***

### setShrink()

> **setShrink**(): `boolean`

**Turn on the text "shrink to fit" for a cell.**

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
var format1 = writer.addFormat("format1");
format1.setShrink();
worksheet1.writeCell("string", 0, 0, "Shrink text so that it fits in a cell", format1);
```

***

### setTextWrap()

> **setTextWrap**(): `boolean`

**Wrap text in a cell.**  

If you wish to control where the text is wrapped you can add newline characters to the string. Excel will adjust the height of the row 
to accommodate the wrapped text. A similar effect can be obtained without newlines using the [XLSXFormat.setAlign(alignment)](#setalign) 
function with [XLSXWriter.ALIGN\_VERTICAL\_JUSTIFY](../classes/XLSXWriter.md#align_vertical_justify).

#### Returns

`boolean`

`true` if successful, `false` in case of any error

#### Since

DOCUMENTS 5.0e

#### Example

```ts
var format1 = writer.addFormat("format1");
format1.setTextWrap();
worksheet1.writeCell("string", 0, 0, "Some long text to wrap in a cell", format1);
```
