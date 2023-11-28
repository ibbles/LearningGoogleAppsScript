See also [[Reading Calendar Events]].

```js
function createCalendarEvents()
{
	const calendar = CalenarApp.getCalendarById("somehexstring@group.calendar.google.com");
	const title = "My Event";
	const timeZone = calendar.getTimeZone();
	const startTime = new Date("2023-11-28 11:45 ${timeZone}");
	const endTime = new Date("2023-11-28 15:45 ${timeZone}");
	const options = {
		location: "My Street 123, My City",
		description: "Come Party!"
	}
	calendar.createEvent(title, startTime, endTime, options);
}
```

# References

- [_Class Calendar - createEvent(title, startTime, endTime, options)_ by Google @ developers.google.com](https://developers.google.com/apps-script/reference/calendar/calendar#createEvent(String,Date,Date,Object))
