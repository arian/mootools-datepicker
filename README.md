# Fork Improvements

- Months and years are now displayed in tables instead of divs.
- A bootstrap-like theme is available. Sources are written in SCSS and can be easily modified as the positionning is no longer done in absolute.

MooTools-DatePicker
===================

MooTools DatePicker is a nice modular and themable DatePicker. It has many features and options, such as
year, month, day or timepicker only modes, min and max dates, Localization and a lot more.

This Plugin makes use of MooTools' Locale and Date plugins in MooTools More, to provide a localized
datepicker, as well as easy formatting and parsing Dates.

This DatePicker is a fork of the original [MonkeyPhysics DatePicker](http://www.monkeyphysics.com/mootools/script/2/datepicker),
and has improved a lot since then. Though it should be (almost) backward compatible.

![Screenshot](https://github.com/arian/mootools-datepicker/raw/master/screenshot.png)

As of version 1.60 the datepicker will only work with MooTools 1.3.

How to use
----------

Below you will find a description and some docs how you can use the datepicker.
If you find any weird things, please create a ticket at github or fork and fix it!

The DatePicker consists out of three layers, a Picker class, which can be used to create  any form of Picker, a Picker.Attach class,
which handles stuff like attaching the Picker to a input or anchor element. Finally there is the DatePicker class, which you'll probably
use. Every option of the Picker or Picker.Attach classes can be used in the DatePicker class.

Basic Example
-------------

First you need to include the following html tags:

	#HTML
	<script src="../Source/Locale.en-US.DatePicker.js" type="text/javascript"></script>
	<script src="../Source/Picker.js" type="text/javascript"></script>
	<script src="../Source/Picker.Attach.js" type="text/javascript"></script>
	<script src="../Source/Picker.Date.js" type="text/javascript"></script>

	<link href="../Source/datepicker_dashboard/datepicker_dashboard.css" rel="stylesheet">

Then you can simply use, for example:

	#JS
	new Picker.Date($$('input'), {
		timePicker: true,
		positionOffset: {x: 5, y: 0},
		pickerClass: 'datepicker_dashboard',
		useFadeInOut: !Browser.ie
	});


### Theming:

Theming is done with CSS files, there are five themes available, which you can find in the Source folder.

Just include the CSS file and set the `pickerClass` option.


### Localization

The DatePicker uses the MooTools More Date Class, which already includes many localized strings.
For some specific strings DatePicker has its own localizations, which you can find in the Locale.__-__.DatePicker.js files.
Just include the file in your page with a script tag to use the translations.

Currently the following languages are supported

- af-ZA
- cs-CZ
- de-DE
- en-US
- es-ES
- fr-FR
- he-IL
- hu-HU
- it-IT
- nl-NL
- pl-PL
- pt-BR
- ru-RU
- sv-SE
- uk-UA

You can set the current language with:

	#JS
	Locale.use('nl-NL');


Class: DatePicker
-----------------

### Syntax

	#JS
	var dp = new DatePicker([element, options]);

### Arguments

1. element: (*element*, *string*, *array*) The element(s) to attach the datepicker to
2. options: (*object*, optional) The options object

### Options:

All the options of the Picker and Picker.Attach classes, and:

- minDate: (*Date instance*, *string*, defaults to `null`) Minimum date allowed to pick. Blocks anything before.
- maxDate: (*Date instance*, *string*, defaults to `null`) Maximum date allowed to pick. Blocks anything after.
- availableDates: (*object*, defaults to `null`) When only a few dates should be selectable. An object like `{2011: {1: [19, 29, 31], 3: [5, 19, 24]}}` with all the dates (year -> months -> days).
- invertAvailable: (*boolean*, defaults to `false`) Invert the `availableDates` option.
- format: (*string*, defaults to the default localized format) The format to output into the input field. Uses [Date.format](http://mootools.net/docs/more/Types/Date#Date:format)
- timePicker: (*boolean*, defaults to 1 `false`) Enable/disable timepicker functionality. Hours/Minutes values can be changed using the scrollwheel.
- timeWheelStep: (*number*, defaults to `1`) The number of minutes the minutes field will change in the timepicker when using the scrollwheel, for example 5, 10, 15. The value will always be k * timeWheelStep.
- yearPicker: (*boolean*, defaults to `true`) Enable/disable yearpicker functionality. Makes it much easier to change years.
- yearPerPage: (*number*, defaults to `20`) Amount of years to show in the year-picking view. Be aware that this may affect your layout.
- startView: (*string*, defaults to `days`) The view that will be showed when the picker opens. The options are `time`, `days`, `months` and `years`
- startDay: (*number*, defaults to 1) The day number for the start of the week. 0 - sunday, 1 - monday, etc.
- openLastView: (*boolean*, defaults to `false`) Opens the last opened view after the picker is opened again, instead of the `startView`
- pickOnly: (*string*, defaults to `false`) If you just want to pick a year, month, day or time. The options are `time`, `days`, `months` and `years`
- canAlwaysGoUp: (*array*, defaults to `['months', 'days']`) The views where you can click the title to go up. The options are `time`, `days`, `months` and `years`
- updateAll (*boolean*, defaults to `false`) whether or not to update all inputs when selecting a date
- weeknumbers (*boolean*, defaults to `false`) display weeknumbers for the `days` view
- daysToDayRangePerWeek (*boolean*, defaults to `false`) changes the selectors for single days, to a week selector
- months_abbr: (*array*) An array with the month name abbreviations. If nothing is set, it will automatically use MooTools Locale to get the abbreviations
- days_abbr: (*array*) An array with the day name abbreviations. If nothing is set, it will automatically use MooTools Locale to get the abbreviations
- years_title: (*function*, defaults to a function which returns `year + '-' + (year + options.yearsPerPage - 1)`) A function that returns the title for the yearpicker with as arguments the date object and the options object.
- months_title: (*function*, defaults to a function which returns `date.format('%b %Y')`) A function that returns the title for the monthpicker with as arguments the date object and the options object.
- days_title:  (*function*, defaults to a function which returns `date.format('%b %Y')`) A function that returns the title for the daypicker with as arguments the date object and the options object.
- time_title: (*function*, defaults to a function which returns `(options.pickOnly == 'time') ?	Locale.get('DatePicker.select_a_time') : date.format('%d %B, %Y')`) A function that returns the title for the timepicker with as arguments the date object and the options object.



### Events:

- onSelect: Will fire when the user has selected a date

#### signature

	#JS
	onSelect(date)

#### arguments

1. date - A Date object. You could use [Date.format](http://mootools.net/docs/more/Types/Date#Date:format) to format it into a string. For example to set it into a hidden field which will be sent to the server.


### Examples

	#JS
	new DatePicker('inputField', {
		timePicker: true,
		pickerClass: 'datepicker_jqui',
		onSelect: function(date){
			myHiddenField.set('value', date.format('%s'));
		}
	});

Picker.Date method: select
--------------------------

Selects a date manually.

### Syntax:

	picker.select(date[, all]);

### Arguments:

1. date (*Date instance*) the date instance of the new date
2. all (*boolean*, optional) Whether it should update all inputs (defaults to the *updateAll* option)

### Returns:

- Picker.Date instance.


Class: Picker.Date.Range
------------------------

The range picker can be used to select date ranges, with a start date and a end date.

### Syntax:

	#JS
	var dp = new Picker.Date.Range([element, options]);

### Arguments:

#### Options:

All `Picker.Date` options plus:

- getStartEndDate: (*function*) Parses the two dates in the input field to `Date` instances. Signature: `function(input)`
- setStartEndDate: (*function*) Formats the dates and sets the input field value. Signature: `function(input, dates)`
- columns: (*number*, defaults to `3`) Number of columns
- footer: (*boolean*, defaults to `true`) Creates an extra footer element


Class: Picker.Attach
--------------------

Picker.Attach handles all the links from elements to the Picker. It handles the onfocus events of input elements etc.
The Class itself is not very useful on its own, but it is useful to extend this Class.
This class adds a outerclick as well to close the Picker if you click outside the picker.

#### Syntax:

	#JS
	new Picker.Attach(attachTo, options);

#### Options:

- toggle: (*element*, *string*, *array*) A collection of elements which will toggle the picker when such a link is clicked.
- togglesOnly: (*boolean, defaults to `true`) If the `toggle` option is set, this option determines if the focus/blur events on the input fields are still added as well.
- blockKeydown: (*boolean*, defaults to `true`) Whether it should block keydown events, so the user can type into the input field or not.

### Picker.Attach Method: attach

This will attach links and input elements to the picker

#### Syntax

	#JS
	myPicker.attach(attachTo);

#### Arguments

1. attachTo: (*element*, *string*, *array*) The elements or element to attach to the Picker. Can be a input element for onfocus events or other elements for click events.


### Picker.Attach Method: detach

This will detach links and input elements from the picker

#### Syntax

	#JS
	myPicker.detach(detach);

#### Arguments

1. detach: (*element*, *string*, *array*) The elements or element to detach from the Picker. Can be a input element for onfocus events or other elements for click events.


Class: Picker
-------------

This is a generic Picker Class, which is used for the basic things, like positioning, Fx, open, close, stuff like that.

#### Syntax:

	#JS
	new Picker(options);

#### Options:

- pickerClass: (*string*, defaults to `datepicker`) CSS class for the main datepicker container element. You can use multiple classes by separating them by a space, e.g. `class1 class2 class3`
- inject: (*element*, defaults to `document.body`) This is where the Picker element will be injected to.
- anitmationDuration: (*number*, defaults to `400`) Duration of the slide/fade animations in milliseconds.
- useFadeInOut: (*boolean*, defaults to `true`) Whether to fade-in/out the datepicker popup. You might want to set this to `false` in IE.
- positionOffset: (*object*, defaults to `{x: 0, y: 0}`) Allows you to tweak the position at which the datepicker appears, relative to the input element. Formatted as an object with x and y properties. Values can be negative.
- pickerPosition: (*string*, defaults to `bottom`) If the picker is positioned relative to an element, you can choose to position it top, bottom, left or right.
- draggable: (*boolean*, defaults to `true`) Will make the picker draggable, if Drag from MooTools More is included.
- columns: (*number*, defaults to `1`) Number of columns
- footer: (*boolean*, defaults to `false`) Creates an extra footer element

#### Events:

- open - triggered when the Picker will open (before the fx)
- close - triggered after the Picker is will get closed (before the fx)
- show - triggered when the Picker is shown
- hide - triggered when the Picker is hidden



### Picker Method: show

A method to show the Picker manually, with a Fx.

#### Syntax

	#JS
	dp.show()

### Picker Method: close

Closes the Picker with a Fx.

#### Syntax

	#JS
	dp.close();


### Picker Method: toggle

Toggles the Picker with a Fx.

#### Syntax

	#JS
	picker.toggle();

### Picker Method: show

Opens the Picker directly.

#### Syntax

	#JS
	dp.show();


### Picker Method: hide

Hides the Picker directly.

#### Syntax

	#JS
	dp.hide();


### Picker Method: destroy

Destroys the Picker

	#JS
	picker.destroy();


### Picker Method: position

Positions the Picker.

#### Syntax:

	#JS
	picker.position(x, y);
	// or
	picker.position(myElement, where);

#### Arguments

1. x: (*number*) Number of pixels from the left
2. y: (*number*) Number of pixels from the top

Or

1. myElement - (*element*) A element the Picker should be positioned relative to.
2. where - (*string*, optional) Position the Picker `left` or `right` to the element.


### Picker Method: setContent

Set the content of the Picker, either elements or text.

#### Syntax:

	#JS
	picker.setContent(element, fx);

#### Arguments:

1. element: (*element*, *string*) Set the content of the Picker with this value
2. fx: (*string*, optional) Set the content of the picker, and apply it with this Fx. Options: 'fade', 'right', 'left'


### Picker Method: setTitle

Sets the Picker title text.

	#JS
	picker.setTitle(text);

#### Arguments:

1. text: (*string*) The text which will be set into the title.


License
-------

- [MIT License](http://www.opensource.org/licenses/mit-license.php)
