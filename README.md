# How-To: Formatting Dates <!-- omit in toc -->

In Stadium controls, we can manipulate a wide range of values in expressions. To format dates, we can use the [DayJS date library](https://day.js.org/en/). DayJS is a JavaScript library that parses, validates, manipulates, and displays dates and times for modern browsers. 

The code snippets section in the Stadium Expression Editor contain a variety of additional options for manipulating dates as well as other data types. 

![](images/ExpressionEditor.png)

To format a date, we first need to call the DayJS function to turn the string into a JavaScript date. DayJS can handle a wide range of input formats. 

Examples:
```javascript
dayjs('2018-04-04T16:00:00.000Z')
dayjs('2018-04-13 19:18:17.040+02:00')
dayjs('2018-04-13 19:18')
```

Once our string is a valid Javascript date, we can define a format: 

Examples:
```javascript
dayjs('2019-01-25').format('DD/MM/YYYY')
dayjs('2019-25-01').format('DD-MM-YYYY')
dayjs('2019-25-01').format('YYYY-DD-MM')
```

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

