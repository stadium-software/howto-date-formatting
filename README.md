# How-To: Working With Dates <!-- omit in toc -->

In Stadium, we can manipulate a wide range of values in expressions. Here we can also use plain Javascript or the [DayJS](https://day.js.org/en/) date library to format and manipulate dates in a number of different ways. This guide describes some useful methods for working with dates in Stadium. 

Due to the large variety of date formats in use, it is impossible to determine the compatibility of all possible date formats with the Stadium controls that display and handle dates. Date formats must always be tested in the context of a specific implementations. 

## Table Of Contents <!-- omit in toc -->
- [Expression Editor](#expression-editor)
- [Converting Strings to Dates](#converting-strings-to-dates)
- [Defining Date Formats](#defining-date-formats)
- [Unupported Date Formats](#unupported-date-formats)
- [DayJS Formatting Guide](#dayjs-formatting-guide)
- [DatePicker Control](#datepicker-control)
- [DataGrid Dates](#datagrid-dates)
  - [Display](#display)
  - [Search](#search)

## Expression Editor

The code snippets section in the Stadium Expression Editor contain a variety of entries for manipulating various data types, including dates. 

![](images/ExpressionEditor.png)

## Converting Strings to Dates

DayJS can handle a wide range of input formats, but to make sure it understands a date, we need to call the DayJS wrapper. DayJS returns the string **"Invalid Date"** when a date is not understood.

```javascript
dayjs('2018-04-04T16:00:00.000Z')
dayjs('2018-04-13 19:18:17.040+02:00')
dayjs('2018-04-13 19:18')
```

## Defining Date Formats

Once a string has been converted to a date, we can define an output format for it: 

```javascript
dayjs('2019-01-25').format('DD/MM/YYYY')
dayjs('2019-25-01').format('DD-MM-YYYY')
dayjs('2019-25-01').format('YYYY-DD-MM')
```

## Unupported Date Formats

When DayJS returns **"Invalid Date"** we can pass the format of the date to DayJS: 

```javascript
dayjs('2019-01-25', 'YYYY-MM-DD')
dayjs('25-01-2925', 'DD-MM-YYYY')
dayjs('2019-01-11', 'YYYY-DD-MM')
dayjs('2019-01-11', 'YYYY-MM-DD')
```

## DayJS Formatting Guide

The [DayJS date formatting guide](https://day.js.org/docs/en/display/format#list-of-all-available-formats) provides a wide range of options for reformatting dates. 

List of all available formats

|Format |	Output |	Description|
| :--- | :------- | :------------ |
|YY |	18 |	Two-digit year|
|YYYY |	2018 |	Four-digit year|
|M |	1-12 |	The month, beginning at 1|
|MM |	01-12 |	The month, 2-digits|
|MMM |	Jan-Dec |	The abbreviated month name|
|MMMM |	January-December |	The full month name|
|D |	1-31 |	The day of the month|
|DD |	-31 |	The day of the month, 2-digits|
|d |	0-6 |	The day of the week, with Sunday as 0|
|dd |	Su-Sa |	The min name of the day of the week|
|ddd |	Sun-Sat |	The short name of the day of the week|
|dddd |	Sunday-Saturday |	 name of the day of the week|
|H |	0-23 |	 hour|
|HH |	00-23 |	The hour, 2-digits|
|h |	1-12 |	The hour, 12-hour clock|
|hh |	01-12 |	The hour, 12-hour clock, 2-digits|
|m |	0-59 |	The minute|
|mm |	00-59 |	The minute, 2-digits|
|s |	0-59 |	The second|
|ss |	00-59 |	The second, 2-digits|
|SSS |	000-999 |	The millisecond, 3-digits|
|Z |	+05:00 |	The offset from UTC, ±HH:mm|
|ZZ |	+0500 |	The offset from UTC, ±HHmm|
|A |	AM |	PM	|
|a |	am |	pm	|

## DatePicker Control

The DatePicker.Date property accepts DayJS dates as well as Javascript dates. It gets it's date format from a settings file on the Stadium Application Server (SAM). By default Stadium applications use the following format in the DatePicker: 

```javascript
'YYYY/MM/DD'
'2019/01/18'
```

Some dates are automatically converted to the DatePicker format by the DatePicker.Date property while others need to be converted in an expression first. How the DatePicker handles the date format used in a specific application needs to be evaluated in the context of that implementation. 

```javascript
dayjs('19/01/2025', 'DD/MM/YYYY').format('YYYY/MM/DD')
dayjs('01-19-2025', 'MM-DD-YYYY').format('YYYY/MM/DD')
dayjs('14.12.2025', 'DD.MM.YYYY').format('YYYY/MM/DD')
```

The DatePicker.Date property returns a DayJS date. Manipulate dates returned by the DatePicker.Date property with DayJS where necessary. 

## DataGrid Dates

The DataGrid control gets it's date format from a settings file on the Stadium Application Server (SAM). By default Stadium applications use the following format in the DataGrid: 

```javascript
'YYYY/MM/DD'
'2019/01/18'
```

### Display

The DataGrid natively understands dates in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601). By default, DateTime values are automatically converted to Dates before they are shown. In the Mapping Editor the format of dates can be manipulated before they are shown. 

![](images/MappingEditor.png)

### Search

Stadium uses [Lucene](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html) to index and search DataGrid data. When searching DataGrids, Stadium passes the search string to Lucene and displays either the data it returns in the DataGrid or an error below the search box. 

Lucene has it's [own syntax](https://docs.stadium.software/controls/data-grid-search#dates) to enable date searches and also natively understands dates in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601). How it handles other date formats is not described in the documentation and needs to be evaluated in the context of each specific implementation. 

While Lucene takes time into account when performing date-specific searches, including time in a date search string is not possible. However, using the [advanced date search syntax](https://docs.stadium.software/controls/data-grid-search#dates) of Lucene it is possible to consider time when performing date searches with Lucene. 