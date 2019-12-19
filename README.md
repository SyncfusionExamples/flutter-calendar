# Getting Started
This section explains the steps required to add the calendar widget and populate appointments to the calendar widget. This section covers only basic features needed to get started with Syncfusion calendar widget.

## Add flutter calendar to an application
Create a simple project using the instructions given in the [Getting Started with your first Flutter app](https://flutter.dev/docs/get-started/test-drive?tab=vscode#create-app) documentation.

**Add dependency**

Add the Syncfusion flutter calendar dependency to your pubspec.yaml file.

```Dart
dependencies:
syncfusion_flutter_calendar: ^17.4.39-beta
```

**Get packages** 

Run the following command to get the required packages.

```Dart

$ flutter pub get

```

**Import package**

Import the following package in your Dart code.

```Dart

import 'package:syncfusion_flutter_calendar/calendar.dart';

```

## Initialize calendar

After importing the package, initialize the calendar widget as a child of any widget. Here, the calendar widget is added as a child of the scaffold widget.

```Dart
@override
Widget build(BuildContext context) {
	return Scaffold(
		body: Container(
			child: SfCalendar(),
		)
	);
}	
```

## Change different calendar views

The SfCalendar widget provides seven different types of views to display dates. It can be assigned to the widget constructor by using the [view](https://pub.dev/documentation/syncfusion_flutter_calendar/latest/calendar/SfCalendar/view.html) property. By default, the widget is assigned day view. The current date will be displayed initially for all the calendar views.

```Dart
@override
Widget build(BuildContext context) {
	return Scaffold(
		body: SfCalendar(
			view: CalendarView.month,
		)
	);
}
```

## Add data source

The calendar widget has a built-in capability to handle appointment arrangement internally based on the appointment collections. You need to assign the created collection to the [dataSource](https://pub.dev/documentation/syncfusion_flutter_calendar/latest/calendar/SfCalendar/dataSource.html) property.
You can also map custom appointment data to our calendar.

```Dart
@override
Widget build(BuildContext context) {
	return Scaffold(
		body: SfCalendar(
			view: CalendarView.month,
				dataSource: MeetingDataSource(_getDataSource()),
				monthViewSettings: MonthViewSettings(
				appointmentDisplayMode: MonthAppointmentDisplayMode.appointment),
		)
	);
}

List<Meeting> _getDataSource() {
	meetings = <Meeting>[];
	final DateTime today = DateTime.now();
	final DateTime startTime =
		DateTime(today.year, today.month, today.day, 9, 0, 0);
	final DateTime endTime = startTime.add(const Duration(hours: 2));
	meetings.add(
		Meeting('Conference', startTime, endTime, const Color(0xFF0F8644), false));
	return meetings;
}


class MeetingDataSource extends CalendarDataSource {
	MeetingDataSource(this.source);

	List<Meeting> source;

	@override
	List<dynamic> get appointments => source;

	@override
	DateTime getStartTime(int index) {
		return source[index].from;
	}

	@override
	DateTime getEndTime(int index) {
		return source[index].to;
	}

	@override
	String getSubject(int index) {
		return source[index].eventName;
	}

	@override
	Color getColor(int index) {
		return source[index].background;
	}

	@override
	bool isAllDay(int index) {
		return source[index].isAllDay;
	}
}

class Meeting {
	Meeting(this.eventName, this.from, this.to, this.background, this.isAllDay);

	String eventName;
	DateTime from;
	DateTime to;
	Color background;
	bool isAllDay;
}
```

## Change first day of week

The calendar widget will be rendered with Sunday as the first day of the week, but you can customize it to any day by using the [firstDayOfWeek](https://pub.dev/documentation/syncfusion_flutter_calendar/latest/calendar/SfCalendar/firstDayOfWeek.html) property.

```Dart
@override
Widget build(BuildContext context) {
	return Scaffold(
		body: SfCalendar(
			view: CalendarView.week,
			firstDayOfWeek: 1, // Monday
		)
	);
}

```

## Initial selected date

You can programmatically select the specific calendar month cell, and time slot by setting corresponding date and time value to the [initialSelectedDate](https://pub.dev/documentation/syncfusion_flutter_calendar/latest/calendar/SfCalendar/initialSelectedDate.html) property of calendar. By default, it is null.

```Dart
@override
Widget build(BuildContext context) {
return MaterialApp(
	home: Scaffold(
		body: Container(
			child: SfCalendar(
				view: CalendarView.week,
				initialSelectedDate: DateTime(2019, 12, 20, 12),
				),
			),
		),
	);
}
```

## Initial display date

You can change the initial display date of calendar by using the [initialDisplayDate](https://pub.dev/documentation/syncfusion_flutter_calendar/latest/calendar/SfCalendar/initialDisplayDate.html) property of calendar, which displays the calendar based on the given date time. By default, current date will be set as `initialDisplayDate`.

```Dart
@override
Widget build(BuildContext context) {
	return MaterialApp(
		home: Scaffold(
			body: Container(
				child: SfCalendar(
					view: CalendarView.week,
					initialDisplayDate: DateTime(2019, 12, 20, 12),
				),
			),
		),
	);
}
```

## Selection decoration

You can decorate the selection view of calendar by using the [selectionDecoration](https://pub.dev/documentation/syncfusion_flutter_calendar/latest/calendar/SfCalendar/selectionDecoration.html) property of Calendar.

```Dart
@override
Widget build(BuildContext context) {
	return MaterialApp(
		home: Scaffold(body: Container(child: SfCalendar(view: CalendarView.week, 
    selectionDecoration: BoxDecoration(
						color: Colors.transparent,
						border: Border.all(
						color: Colors.red, width: 2),
						borderRadius: const BorderRadius.all(Radius.circular(4)),
						shape: BoxShape.rectangle,
					),
				),
			),
		),
	);
}
```

## Today highlight color

You can customize the today highlight color of calendar by using the [todayHighlightColor](https://pub.dev/documentation/syncfusion_flutter_calendar/latest/calendar/SfCalendar/todayHighlightColor.html) property in calendar, which will highlight the today text in calendar view header, month cell, and agenda view.

```Dart
@override
Widget build(BuildContext context) {
	return MaterialApp(
		home: Scaffold(
			body: Container(
				child: SfCalendar(
					view: CalendarView.week,
					todayHighlightColor: Colors.red,
				),
			),
		),
	);
}
```

## Cell border color

You can customize the vertical and horizontal line color of calendar by using the [cellBorderColor](https://pub.dev/documentation/syncfusion_flutter_calendar/latest/calendar/SfCalendar/cellBorderColor.html) property in calendar.

```Dart
@override
Widget build(BuildContext context) {
	return MaterialApp(
		home: Scaffold(
			body: Container(
				child: SfCalendar(
					view: CalendarView.week,
					cellBorderColor: Colors.blue,
				),
			),
		),
	);
}
```

## Background color

The calendar widgets background color can be customized by using the [backgroundColor](https://pub.dev/documentation/syncfusion_flutter_calendar/latest/calendar/SfCalendar/backgroundColor.html) property in calendar.

```Dart
@override
Widget build(BuildContext context) {
	return MaterialApp(
		home: Scaffold(
			body: Container(
				child: SfCalendar(
					view: CalendarView.week,
					backgroundColor: Colors.lightBlue,
				),
			),
		),
	);
}
```
