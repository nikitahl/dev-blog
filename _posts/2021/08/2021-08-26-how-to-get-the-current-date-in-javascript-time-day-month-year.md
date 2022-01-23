---
layout: post
permalink: get-the-current-date-in-javascript
title: How to get the current date in JavaScript (Time, Day, Month, Year)
date: 2021-08-26T12:21:12.144Z
description: To get the current date in JavaScript you’ll only need the Vanilla
  JavaScript Date API. All the information about the current date can be
  accessed in one line of code in various formats.
tags: [javascript]
---

To get the current date in JavaScript you’ll only need the Vanilla JavaScript [Date API](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date). All the information about the current date can be accessed in one line of code in various formats.

1. [Get Current Day](#get-current-day)
2. [Get Current Month](#get-current-month)
3. [Get Current Year](#get-current-year)
4. [Get Current Time](#get-current-time)
5. [Get Current Date](#get-current-date)

You’ll need to create a new Date object using the [`Date()` constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/Date) to get the current date. The `Date` constructor is [supported in all browsers](https://caniuse.com/mdn-javascript_builtins_date_date). Instantiate it without any parameters:

> *“When no parameters are provided, the newly-created Date object represents the current date and time as of the time of instantiation.”*
>
> \- MDN 

```javascript
const currentDate = new Date()
```

<figure>
  <img class="shadow lozad" data-src="/images/dev-tools/current-date-object.png" alt="Current Date object output">
  <noscript>
    <img class="shadow" src="/images/dev-tools/current-date-object.png" alt="Current Date object output">
  </noscript>
  <figcaption>Current Date object output</figcaption>
</figure>

## Get Current Day

### Get current week day

To get the current weekday use the [`getDay()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getDay) method on the `currentDate` object. The return value is an integer number.

```javascript
const currentDate = new Date()
currentDate.getDay()
```

<figure>
  <img class="shadow lozad" data-src="/images/dev-tools/get-current-week-day.png" alt="Current week day output">
  <noscript>
    <img class="shadow" src="/images/dev-tools/get-current-week-day.png" alt="Current week day output">
  </noscript>
  <figcaption>Current week day output</figcaption>
</figure>

**NOTE: The weekday index starts from 0, and the 0 represents Sunday.**

### Get current week day name

If you want to get the name of the weekday use the [`toLocaleString()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleString) method with properties. The return value is a string with a language-sensitive representation of this date.

```javascript
const currentDate = new Date()
currentDate.toLocaleString('en-US', { weekday: 'long' })
```

<figure>
  <img class="shadow lozad" data-src="/images/dev-tools/get-current-week-day-name.png" alt="Current week day name output">
  <noscript>
    <img class="shadow" src="/images/dev-tools/get-current-week-day-name.png" alt="Current week day name output">
  </noscript>
  <figcaption>Current week day name output</figcaption>
</figure>

The first argument is the `locale` which represents the language. The second is the `options` object, where you can set the weekday property with a value of long.

### Get current day of the month

To get the day of the month use the [`getDate()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getDate) method. The return value is an integer number.

```javascript
const currentDate = new Date()
currentDate.getDate()
```

<figure>
  <img class="shadow lozad" data-src="/images/dev-tools/get-current-day-of-the-month.png" alt="Current day of the month output">
  <noscript>
    <img class="shadow" src="/images/dev-tools/get-current-day-of-the-month.png" alt="Current day of the month output">
  </noscript>
  <figcaption>Current day of the month output</figcaption>
</figure>

## Get Current Month

### Get current month number

To get the current month use the [`getMonth()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getMonth) method. The return value is an integer number.

**NOTE: Month index starts from 0, and 0 represents January.**

```javascript
const currentDate = new Date()
currentDate.getMonth()
```

<figure>
  <img class="shadow lozad" data-src="/images/dev-tools/get-current-month.png" alt="Current month output">
  <noscript>
    <img class="shadow" src="/images/dev-tools/get-current-month.png" alt="Current month output">
  </noscript>
  <figcaption>Current month output</figcaption>
</figure>

### Get current month name

To get the name of the month use the [`toLocaleString()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleString) method with properties. The return value is a string with a language-sensitive representation of this date.

```javascript
const currentDate = new Date()
currentDate.toLocaleString('en-US', { month: 'long' })
```

<figure>
  <img class="shadow lozad" data-src="/images/dev-tools/get-current-month-name.png" alt="Current month name output">
  <noscript>
    <img class="shadow" src="/images/dev-tools/get-current-month-name.png" alt="Current month name output">
  </noscript>
  <figcaption>Current month name output</figcaption>
</figure>

The first argument is the `locale` which represents the language. The second is the `options` object, where you can set the month property with a value of long.

## Get Current Year

To get the current year use the [`getFullYear()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getFullYear) method. The return value is an integer number.

```javascript
const currentDate = new Date()
currentDate.getFullYear()
```

<figure>
  <img class="shadow lozad" data-src="/images/dev-tools/get-current-year.png" alt="Current year output">
  <noscript>
    <img class="shadow" src="/images/dev-tools/get-current-year.png" alt="Current year output">
  </noscript>
  <figcaption>Current year output</figcaption>
</figure>

## Get Current Time

To get current time you can use one of the following methods.

### Get current hours

To get current hours use the [`getHours()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getHours) method. The return value is an integer number.

```javascript
const currentDate = new Date()
currentDate.getHours()
```

<figure>
  <img class="shadow lozad" data-src="/images/dev-tools/get-current-hours.png" alt="Current hours output">
  <noscript>
    <img class="shadow" src="/images/dev-tools/get-current-hours.png" alt="Current hours output">
  </noscript>
  <figcaption>Current hours output</figcaption>
</figure>

### Get current minutes

To get current minutes use the [`getMinutes()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getMinutes) method. The return value is an integer number.

```javascript
const currentDate = new Date()
currentDate.getMinutes()
```

<figure>
  <img class="shadow lozad" data-src="/images/dev-tools/get-current-minutes.png" alt="Current minutes output">
  <noscript>
    <img class="shadow" src="/images/dev-tools/get-current-minutes.png" alt="Current minutes output">
  </noscript>
  <figcaption>Current minutes output</figcaption>
</figure>

### Get current seconds

To get current seconds use the [`getSeconds()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getSeconds) method. The return value is an integer number.

```javascript
const currentDate = new Date()
currentDate.getSeconds()
```

<figure>
  <img class="shadow lozad" data-src="/images/dev-tools/get-current-seconds.png" alt="Current seconds output">
  <noscript>
    <img class="shadow" src="/images/dev-tools/get-current-seconds.png" alt="Current seconds output">
  </noscript>
  <figcaption>Current seconds output</figcaption>
</figure>

### Get current time in a specific format

To get the current time in a specific time format (AM/PM or 24H) use the [`toLocaleTimeString()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleTimeString) method with properties. The return value is a string in a specific format.

```javascript
const currentDate = new Date()
currentDate.toLocaleTimeString('en-US', { hour12: false })
```

<figure>
  <img class="shadow lozad" data-src="/images/dev-tools/get-current-time-format.png" alt="Current time in format output">
  <noscript>
    <img class="shadow" src="/images/dev-tools/get-current-time-format.png" alt="Current time in format output">
  </noscript>
  <figcaption>Current time in format output</figcaption>
</figure>

The first argument is the `locale` which represents the language. The second is the `options` object, where you can set the desired time format.

## Get Current Date

Finally to get the current date in a string format including weekday, month, month day, and a year, use the `toLocaleString()` method with parameters including the options object containing all of these values.

```javascript
const currentDate = new Date()
const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
currentDate.toLocaleString('en-US', options)
```

<figure>
  <img class="shadow lozad" data-src="/images/dev-tools/get-current-date-string.png" alt="Current date in string format output">
  <noscript>
    <img class="shadow" src="/images/dev-tools/get-current-date-string.png" alt="Current date in string format output">
  </noscript>
  <figcaption>Current date in string format output</figcaption>
</figure>