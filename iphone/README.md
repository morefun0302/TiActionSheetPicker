# TiActionSheetPicker

by Paul Mietz Egli (paul@obscure.com)
based on ActionSheetPicker by Tim Cinel (https://github.com/TimCinel/ActionSheetPicker)

**TiActionSheetPicker** is an Appcelerator Titanium module which wraps ActionSheetPicker, the library for
creating action sheets on iOS for choosing date/times and from a list of strings.

## Building

1. Clone this github repository.
2. In the same directory as this README.md file, run `git submodule init`, then `git submodule update`.
3. Open `titanium.xcconfig` and verify that the path to the Titanium SDK is correct for your system.
4. Run `./build.py` to generate the module ZIP file.

## Using the Module

If you have used [Ti.UI.OptionDialog](http://docs.appcelerator.com/titanium/latest/#!/api/Titanium.UI.OptionDialog),
you should feel right at home with the action sheets provided by this module.  Here's how to pop up a
sheet with a date picker and get the selected date back:

```javascript
var picker = TiActionSheetPicker.createDatePickerSheet({
  title: "Pick a Date",
  mode: Ti.UI.PICKER_TYPE_DATE,
  initialDate: new Date(2013, 4, 14),
  minDate: new Date(2012, 0, 1)
});
picker.addEventListener('change', function(e) {
  // e.selectedDate contains the date object that was chosen
  label.text = String.formatDate(e.selectedDate, 'medium');
})
picker.show();
```

Similarly, you can create an action sheet for selecting from a list of strings:
```javascript
var rows = ['aardvark', 'bandicoot', 'cougar', 'dugong', 'yak', 'zebra' ];
var picker = TiActionSheetPicker.createStringPickerSheet({
  title: "Pick an Animal",
  initialSelection: 4,
  rows: rows
});
picker.addEventListener('change', function(e) {
  label.text = rows[e.selectedIndex];
})
picker.show();
```

The date picker and string picker are displayed as a popover view on the iPad and require
an additional argument to the `show()` function to specify the origin of the popover:

```javascript
var button = Ti.UI.createButton({
  title: 'Select Date'
});
button.addEventListener('click', function() {
  var picker = TiActionSheetPicker.createDatePickerSheet({
    mode: Ti.UI.PICKER_TYPE_DATE,
  });
  picker.show({ origin: button });
});
```

The above code will result in a date picker popover anchored to the button.  If the origin
of the picker is not specified, the popover will not be shown.  The origin is ignored on
the iPhone.

## Requirements

* Titanium SDK 3.0.2 or later
* Xcode 4.5 or later

## License

* TiActionSheetPicker is under the Apache License 2.0
* ActionSheetPicker is under the BSD License. See that project for additional licenses.

## Development Status 

**1.0**

2013-04-15

Added minDate, maxDate, and locale properties to date picker

2013-03-29

Added support for date/time picker and string picker
