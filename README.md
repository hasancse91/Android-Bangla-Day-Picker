# Bangla Day Picker for Android 
> Widget for selecting the Bangla weekdays

[![JitPack](https://jitpack.io/v/Gkemon/Android-Bangla-Day-Picker.svg)](https://jitpack.io/#Gkemon/Android-Bangla-Day-Picker)

## Screenshots

[Inspired by David Prodinger](https://github.com/DavidProdinger/Weekdays-Selector)

<img src="https://github.com/Gkemon/Android-Bangla-Day-Picker/blob/master/Screenshot_1558596994.png" width="250" height="444" />

## Installation

### Gradle

Add the JitPack repository to your root build.gradle file

```groovy
allprojects {
    repositories {
        // ...
        maven { url 'https://jitpack.io' }
    }
}
```

Add the dependency

```groovy
dependencies {
	        implementation 'com.github.Gkemon:Android-Bangla-Day-Picker:1.0.0'
	}
```

### Maven

Add the JitPack repository to your build file

```xml
<repositories>
    <repository>
        <id>jitpack.io</id>
        <url>https://jitpack.io</url>
    </repository>
</repositories>
```

Add the dependency

<dependency>
    <groupId>com.github.Gkemon</groupId>
    <artifactId>Android-Bangla-Day-Picker</artifactId>
    <version>1.0.0</version>
</dependency>


## Usage

### In your layout file
```xml
<com.gk.emon.android.BanglaDaysPicker
        android:id="@+id/weekdays"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:sunday_first_day="false"
        app:full_size="true"/>
```

### Your Java file
```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        
        // ...

        BanglaDaysPicker widget = (BanglaDaysPicker) findViewById(R.id.weekdays);
        widget.setOnWeekdaysChangeListener(new OnWeekdaysChangeListener() {
            @Override
            public void onChange(View view, int clickedDayOfWeek, List<Integer> selectedDays) {
                // Do Something
            }
        });
        
        // ...
    }
    
    // ...
}
```

## Configuration

### Layout file

* `enabled`: If user is allowed to select weekdays (default=true)
* `highlight_color`: Color of selected days and unselected Text (default=Color.RED)
* `background_color`: Background-Color of unselected days (default=Color.LTGRAY)
* `text_color`: Color of selected days text (default=Color.WHITE)
* `sunday_first_day`: Starting with Sunday or Monday (default=true)
* `show_weekend`: Display weekend (Satuarday and Sunday) (default=true)
* `weekenddarker`: Allows that weekend has another color (default=false)
* `weekend_color`: Background-Color from unselected Weekend (default=Color.GRAY)
* `weekend_text_color`: Set the unselected text color from the weekend (default=highlight_color)
* `full_size`: Shows the days with the dayname (f.e. Mo.) and in a rectangle form (default=false)
* `recurrence`: Shows a spinner to select the week recurrence (default=false)
* `border_color`: Set the Border-Color from unselected days (default=-1 no border)
* `border_thickness`: Set the Border-Thickness from unselected days (default=4)
* `border_highlight_color`: Set the Border-Color from selected days (default=-1 no border)
* `border_highlight_thickness`: Set the Border-Thickness from selected days (default=4)

## Methods and Functions

Assuming `widget` is an `WeekdaysPicker` object
```java
WeekdaysPicker widget = (WeekdaysPicker) findViewById(R.id.weekdays);
```
#### OnChange Listener

```java
widget.setOnWeekdaysChangeListener(new OnWeekdaysChangeListener() {
            @Override
            public void onChange(View view, int clickedDayOfWeek, List<Integer> selectedDays) {
                // Do Something
            }
        });
```

#### OnWeekRecurrenceChange Listener
```java
widget.setOnWeekRecurrenceChangeListener(new OnWeekRecurrenceChangeListener() {
            @Override
            public void onWeekChange(View view, List<Integer> selectedDays, int even_week) {
                // Do something else
                switch (even_week) {
                    case WeekdaysPicker.ALL:
                        // if all weeks selected
                        break;
                    case WeekdaysPicker.ODD:
                        // if odd weeks selected
                        break;
                    case WeekdaysPicker.EVEN:
                        // if even weeks selected
                        break;
                } 
            }
        });
```

### Get selected Days

Returns selected Days as Integer-List according to `Calendar.MONDAY`, `Calendar.TUESDAY` and so on

```java
List<Integer> selectedDays = widget.getSelectedDays();
```

### Get selected Days as Text

Returns selected Days as Text
Optional: Set locale

```java
List<String> selectedDays = widget.getSelectedDaysText();
```

### Select Days

Accept Integer-List of days you would like to select

```java
List<Integer> days = Arrays.asList(Calendar.MONDAY, Calendar.WEDNESDAY, Calendar.FRIDAY, Calendar.SUNDAY);

widget.setSelectedDays(days);
```

### Select one Day

Select day by Integer of Day (eg. `Calendar.SUNDAY`)

```java
widget.selectDay(Calendar.SUNDAY);
```

### Check if all Days are selected

#### onCreate

```java
if (widget.allDaysSelected()){
    // Do Something
}
```

#### onChange

```java
widget.setOnWeekdaysChangeListener(new OnWeekdaysChangeListener() {
    @Override
    public void onChange(View view, int clickedDayOfWeek, List<Integer> selectedDays) {
        if (selectedDays.size() == 7){
            // Do Something
        }
    }
});
```


### Check if no Day is selected

#### onCreate

```java
if (widget.noDaySelected()){
    // Do Something
}
```

#### onChange

```java
widget.setOnWeekdaysChangeListener(new OnWeekdaysChangeListener() {
    @Override
    public void onChange(View view, int clickedDayOfWeek, List<Integer> selectedDays) {
        if (selectedDays.size() == 0){
            // Do Something
        }
    }
});
```

### Check if Selector is editable

```java
if (widget.isInEditMode()){
    // Do Something
}
```

### Set editable

```java
// Enable the widget
widget.setEditable(true);

// Disable the widget
widget.setEditable(false);
```

### Set custom days:
```java
// Integer = CalendarDay, Boolean = selected
LinkedHashMap<Integer, Boolean> map = new LinkedHashMap<>();
mp.put(SUNDAY, true);
mp.put(SATURDAY, true); //counting
mp.put(THURSDAY, false);
mp.put(FRIDAY, true);
mp.put(TUESDAY, true);
mp.put(SATURDAY, false); //For duplicated values, the first one is counting, but the last one is updating the selected value

//Add the custom map
widget.setCustomDays(map);

// To disable the custom days:
widget.setCustomDays(null);
```

### Other Methods (for all Setter it gives a Getter):
```java
widget.setHighlightColor(Color.RED);
widget.setBackgroundColor(Color.LTGRAY);
widget.setWeekendColor(Color.GRAY);
widget.setTextColor(Color.WHITE);
widget.setSundayFirstDay(true);
widget.setShowWeekend(true);
widget.setRecurrence(true);
widget.setWeekendDarker(true);
widget.setWeekendTextColor(Color.WHITE);
widget.setBorderColor(Color.BLUE);
widget.setBorderThickness(3);
widget.setBorderHighlightColor(Color.MAGENTA);
widget.setBorderHighlightThickness(10);
widget.setFullSize(true);
widget.setSelectOnlyOne(true);
```
