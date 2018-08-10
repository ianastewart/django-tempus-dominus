# Django Tempus Dominus

This is a fork of django-tempus-dominus that fixes the following bugs:
* Date fields that use the DatePicker widget that are initialised with data are not rendered correctly if a custom date input format is in use.
* Time fields that use the TimePicker widget that are initialised with data do not display the preset time value.
* Date fields that use the DatePicker widget that are initialised with data do not display the preset time value.

This version correctly renders all dates and times, but you must make sure that any entries in Django's settings file for DATE_INPUT_FORMATS, TIME_INPUT_FORMATS and DATETIME_INPUT_FORMATS are compatible with any format options that you set for the  widget format.

The widget render() code has also been updated to be compatible with Django 2.1 which passes in a renderer parameter.

The original documentation follows below.

# Django Tempus Dominus

Django Tempus Dominus provides Django widgets for the [Tempus Dominus Bootstrap 4 DateTime](https://tempusdominus.github.io/bootstrap-4/ "Tempus Dominus") date and time picker. Why yet another date and time picker for Django? None supported the Tempus Dominus date and time picker, which is actively developed and feature rich. It is a successor to the popular `bootstrap-datetimepicker` JavaScript library.

## Installation

* From PyPI: `pip install django-tempus-dominus`

* From source:

```python
git clone git+https://github.com/FlipperPA/django-tempus-dominus.git
pip install -e django-tempus-dominus
```

## Usage

Three widgets are provided:

* `DatePicker`, which defaults to `YYYY-MM-DD`
* `DateTimePicker`, which defaults to `YYYY-MM-DD HH:mm:ss`
* `TimePicker`, which defaults to `HH:mm:ss`

In your Django form, you can use the widgets like this:

```python
import datetime

from django import forms
from tempus_dominus.widgets import DatePicker, TimePicker, DateTimePicker

class MyForm(forms.Form):
    date_field = forms.DateField(
        required=True,
        widget=DatePicker(
            options={
                'minDate': '2009-01-20',
                'maxDate': '2017-01-20',
            }
        ),
    )
    time_field = forms.TimeField(
        widget=TimePicker(
            options={
                'enabledHours': [9, 10, 11, 12, 13, 14, 15, 16],
            }
        ),
    )
    datetime_field = forms.DateTimeField(
        widget=DateTimePicker(
            options={
                'minDate': (datetime.date.today() + datetime.timedelta(days=1)).strftime('%Y-%m-%d'),  # Tomorrow
                'useCurrent': True,
                'collapse': False,
            }
        ),
    )
```

The `options` dictionary will be passed to Tempus Dominus. [A full list of options is available here](https://tempusdominus.github.io/bootstrap-4/Options/).

Then in your template, include jQuery, `{{ form.media }}`, and render the form:

```HTML+Django
<html>
    <head>
        <script crossorigin="anonymous" integrity="sha384-xBuQ/xzmlsLoJpyjoggmTEz8OWUFM0/RC5BsqQBDX2v5cMvDHcMakNTNrHIW2I5f" src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
        {{ form.media }}
    </head>
<body>
    <form method="post" action=".">
        {% csrf_token %}
        {{ form.as_p }}
    </form>
</body>
</html>
```

## Change Log

* 0.1.2: UX enhancement: auto-dismiss dialog if the input loses focus.
* 0.1.1: Bug fixes.
* 0.1.0: Initial release.

## Maintainer

* Timothy Allen (https://github.com/FlipperPA)

### Contributors (Thank You!)

* waymou (https://github.com/waymao)
