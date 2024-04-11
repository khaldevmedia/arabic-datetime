# arabic-datetime - Arabic datetime formatter

_Author_: Khaldevmedia

_Description_: A python installable package that helps you output dates in Arabic as strings with a formatting that is specific to each Arab county.

## Month names in Arabic

There are 4 groups of month names in Arabic.

### Syriac names:

The **Syriac** names of months are used in Syria Palestine Lebanon, Jordan and Iraq:

> <p style=dir=rtl>كانون الثاني، شباط، آذار، نيسان، أيار، حزيران، تموز، آب، أيلول، تشرين الأول، تشرين الثاني، كانون الأول.</p>

### Roman names (group 1):

The **Roman names (group 1)** of months are used in Egypt, Yemen, Sudan, Libya, Djibouti, Comoro, Somalia, Saudi Arabia, United Arab Emirates, Qatar, Oman, Bahrain and Kuwait:

> <p style=dir=rtl>يناير، فبراير، مارس، أبريل، مايو، يونيو، يوليو، أغسطس، سبتمبر، أكتوبر، نوفمبر، ديسمبر.</p>

### Roman names (group 2):

The **Roman names (group 2)** of months are used in Morocco and Mauritania:

> <p style=dir=rtl>يناير، فبراير، مارس، أبريل، ماي، يونيو، يوليوز، غشت، شتنبر، أكتوبر، نونبر، دجنبر.</p>

### French names:

The **French** names of months are used in Algeria and Tunisia:

> <p style=dir=rtl>جانفي، فيفري، مارس، أفريل، ماي، جوان، جويلية، أوت، سبتمبر، أكتوبر، نوفمبر، ديسمبر.</p>

## Arabic Numerals

There are two groups of **Arabic numerals** used in the Arab countries.

### Eastern Arabic Numerals

They are used in all Arabe countries except Algeria, Tunisia, Morocco and Mauritania:

> ٠ ١ ٢ ٣ ٤ ٥ ٦ ٧ ٨ ٩

### Western Arabic Numerals

They are used in Algeria, Tunisia, Morocco and Mauritania. However, they are also used in the other Arabe countries that use the eastern Arabic numerals:

> 0 1 2 3 4 5 6 7 8 9

### Numeral Options

You can use the eastern or the western Arabic numeral regardless of the month names group you use. As demonstrated below, there is always a default numerals' type depending on the method used.

## Installation

```bash
pip install arabic-datetime
```

## Example & Usage

### 1. Date

The Arabic_Date class has several methods that return a date object as string using.

#### A specific method for every month names group

```python
import datetime
from arabic_datetime import Arabic_Date

# Create arabic_date object from a python date object
dt = datetime.date(1980, 8, 16)
arabic_date = Arabic_Date(dt)

# Use each method to creat the arabic date strings
syria_date_fromat = arabic_date.syriac_names()
egypt_date_fromat = arabic_date.roman1_names()
morrocco_date_fromat = arabic_date.roman2_names()
algeria_date_fromat = arabic_date.french_names()

print(syriac_date_fromat) # output 16 آب 1980
print(egypt_date_fromat) # output 16 أغسطس 1980
print(morrocco_date_fromat) # output  16 غشت 1980
print(algeria_date_fromat) # output  16 أوت 1980

# To use Eastern Arabic Numerals pass True to the function you use
syria_date_fromat_easter = arabic_date.syriac_names(True)
print(syria_date_fromat_easter) # output ١٦ آب ١٩٨٠
```

> ##### Note:
>
> When you combine Western arabic numerals or western ponctuations with arabic characters they appear messed up if the text direction in the target is set to `left to right` or `dir=ltr` in `HTML`.
>
> In order for the arabic date to appear properly especially, if it uses western arabic numeral the direction of the text in the interface you are using must be `right to left`. If you insert the date into an `HTML` elemnt set text direction to `rtl`. If the text direction in the whole `HTML` document is set `rtl` you should be OK.

```html
<p style="dir" ="rtl">16 آب 1980</p>
<p style="dir" ="rtl">16 أوت 1980</p>
```

> The resut will look like this:
>
> <p style=dir=rtl>16 آب 1980</p>
> <p style=dir=rtl>16 أوت 1980</p>

#### A dual date name method

It's very common that two month names are used at the same time to display the date, with the second one put between parentheses, like this:

> <p style=dir=rtl>16 آب (أغسطس) 1980</p>
> <p style=dir=rtl>١٦ آب (أغسطس) ١٩٨٠</p>

To get the Arabic date formated like this, use the `dual_names` method:

```python
import datetime
from arabic_datetime import Arabic_Date

# Create arabic_date object from a python date object
dt = datetime.date(1980, 8, 16)
arabic_date = Arabic_Date(dt)

# Use the dual_names() method to create Arabic date string that shows two names of the month.
# This method takes 3 arguments: 2 strings for the month group names  (the second one
# will be put between parentheses), and a boolean to determine whether to format the
# Arabic date with the Eastern Numerals or not:
dual_date_ro_sy = arabic_date.dual_names("syriac", "roman1", False)
print(dual_date_ro_sy) # output 16 أغسطس (آب) 1980

# If you don't pass the third argument, the default is False. Also you can use
# keyword arguments to make them more readable:
# arabic_date.dual_names(first="syriac", second="roman1", east_nums=False)

# To use Eastern Arabic Numerals, pass True to the function you use as a third argument.
# We will also switch the month names in this example:
dual_date_sy_ro = arabic_date.dual_names(first="syriac", second="roman1", east_nums=True)
print(dual_date_sy_ro) # output ١٦ آب (أغسطس) ١٩٨٠
```

##### Accepted values for group names (Look above to see which Arab country uses which names):

```
"syriac" : For Syriac names
"roman1" : For Roman names (group 1)
"roman2" : For Roman names  (group 2)
"french" : For French names
```

#### A method that takes the country code to return the corresponding date format

```python
import datetime
from arabic_datetime import Arabic_Date

# Create arabic_date object from a python date object
dt = datetime.date(1980, 8, 16)
arabic_date = Arabic_Date(dt)

# Use of by_country_code() method. It takes country_code as a string
# If you don't pass True or False besides the county code string
# the method will return the numeral type that is most common in that country
syria_date_fromat = arabic_date.by_country_code("SY")
algeria_date_fromat_easter = arabic_date.by_country_code("DZ")
print(syriac_date_fromat) # output ١٦ آب ١٩٨٠
print(algeria_date_fromat) # output 16 أوت 1980

# But if you want to force the numeral type, pass as a second argument
# True for eastern numerals and False for western numerals
syria_date_fromat_western = arabic_date.by_country_code("SY", True)
algeria_date_fromat_easter = arabic_date.by_country_code("DZ", False)
print(syriac_date_fromat) # output 16 آب 1980
print(algeria_date_fromat_easter) # output ١٦ أوت ١٩٨٠
```

##### List of country codes:

```
DZ: Algeria
BH: Bahrain
KM: Comoros
DJ: Djibouti
EG: Egypt
IQ: Iraq
JO: Jordan
KW: Kuwait
LB: Lebanon
LY: Libya
MR: Mauritania
MA: Morocco
OM: Oman
PS: Palestine
QA: Qatar
SA: Saudi Arabia
SO: Somalia
SD: Sudan
SY: Syria
TN: Tunisia
AE: United Arab Emirates
YE: Yemen
```

### 2. Time

The Arabic_Time class has one method that returns a time object as a string using the Eastern Arabic numerals. It takes two parameters: `format` with default value as `"HMS"` and `separator` with default value as `":"`.

```python
import datetime
from arabic_datetime import Arabic_Time
dt = datetime.time(12, 30, 45)
arabic_time = Arabic_Time(dt)
print(arabic_time.time("HMS")) # output ١٢:٣٠:٤٥
print(arabic_time.time("HM")) # output ١٢:٣٠
print(arabic_time.time("HM", "/")) # output ١٢/٣٠
```

##### Valid `format` values:

```
"H": Shows hour only.
"HM": Shows hour and minute.
"HMS": Shows hour, minute and second.
"HMSF": Shows hour, minute, second and microsecond.
```

> #### Note:
>
> As explained above, make sure that the direction of the text in which the Arabic time is inserted is `right to left`.

```html
<p style="dir" ="rtl">١٢:٣٠:٤٥</p>
<p style="dir" ="rtl">الساعة حالياً: ١٢:٣٠:٤٥</p>
```

> The resut will look like this:
>
> <p style=dir=rtl>١٢:٣٠:٤٥</p>
> <p style=dir=rtl>الساعة حالياً: ١٢:٣٠:٤٥</p>

## License

MIT license.

## Contact

<khaldevmedia@gmail.com>
