You need permission to open calendars from Apps Script.
See [[Permission Restrictions]].
In short, we can't use the calendar API from Apps Script functions called from a cell formula.
Instead we must create a [[Creating Menu Items|Menu Item]] that calls the function.
This means that the function can populate arbitrary cells with generated contents.
Not sure how to handle that...

Access the Google Calendar with `CalendarApp`.
Get a particular calendar with `CalendarApp.getCalendarById` or `getCalendarByName`.

A Google Calendar user has a single "`CalendarApp`", which is what you see when you go to calendar.google.com
The calendar view may display events from many calendars.
Each calendar is associated with a color, so you may have your green calendar and your blue calendar, and so on.
The different calendars are listed to the left.
To find the ID of a calendar hover over in the list, click the three dots, and select Settings And Sharing.
Scroll down to Integrate Calendar and you will see Calendar ID and a very long string of letters and numbers, including the `@` and URL bit at the end.

```js
function onOpen() {
  var ui = SpreadsheetApp.getUi();
  ui.createMenu("Learning Apps Script")
    .addItem("Get calendar events", "getMyCalendarEvents")
    .addToUi();
}

function getMyCalendarEvents() {
	const calendar = CalendarApp.getCalendarById("somehexstring@group.calendar.google.com");
}
```

Once we have a calendar we can get a list of all events for a range of dates using `getEvents(Date start, Date end)`.
```js
function getMyCalendarEvents() {
	const calendar = CalendarApp.getCalendarById("somehexstring@group.calendar.google.com");
	const events = calendar.getEvents(new Date("2023-11-01"), new Date("2023-11-30"));
	const firstTitle = events[0].getTitle();
}
```

Dates are really time points and without a time it means 0:00:00.
So if you type dates without a time then the date range is an closed-open interval, i.e. the start day is included but the end day is not.

See also [[Writing Calendar Events]].

# References

- [_Class CalendarApp_ by Google @ developers.google.com](https://developers.google.com/apps-script/reference/calendar/calendar-app?hl=en)
- [_Class Calendar_ by Google @ developers.google.com](https://developers.google.com/apps-script/reference/calendar/calendar?hl=en)
- [_Class CalendarEvent_ by Google @ developers.google.com](https://developers.google.com/apps-script/reference/calendar/calendar-event?hl=en)
- [_Google Sheets - Apps Script Google Calendar API Integration Tutorial - Get Events - Part 10_ by Learn Google Sheets & Excel Spreadsheets @ youtube.com 2017](https://www.youtube.com/watch?v=qXG-i_sG8CI&list=PLv9Pf9aNgemv62NNC5bXLR0CzeaIj5bcw&index=10)
