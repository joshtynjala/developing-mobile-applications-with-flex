# Select dates and times in a mobile application

The
[DateSpinner](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/DateSpinner.html)
control lets users select dates and times in a mobile application. It uses the
familiar mobile interface of a series of adjacent scroll wheels, with each wheel
showing a different part of the date and/or time.

There are three basic types of DateSpinner controls that you can use. The
following figure shows the three types of DateSpinner controls:

<p><i>Image Missing: main_types.png</i></p>

A. Date. B. Time. C. Date and Time

The following table describes the DateSpinner types:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Type</p></th>
<th><p>Constant (String equivalent)</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Date</p></td>
<td><p><samp>DateSelectorDisplayMode.DATE</samp> ("date")</p></td>
<td><div>
Displays the month, day of month, and year. For example:
<pre><code>|| June || 11 || 2011 ||</code></pre>
</div>
<p>Date is the default type. If you do not set the
<samp>displayMode</samp> property of a DateSpinner control, Flex sets it
to date.</p>
<p>The current date is highlighted with the color defined by the
<samp>accentColor</samp> style property.</p>
<p>The earliest date supported is January 1, 1601. The latest supported
date is December 31, 9999.</p></td>
</tr>
<tr class="even">
<td><p>Time</p></td>
<td><p><samp>DateSelectorDisplayMode.TIME</samp> ("time")</p></td>
<td><div>
Displays the hours and minutes. For locales that use 12-hour time, also
displays the AM/PM indicator. For example:
<pre><code>|| 2 || 57 || PM ||</code></pre>
</div>
<p>The current time is not highlighted.</p>
<p>You cannot display seconds in the DateSpinner control.</p>
<p>You cannot toggle between the 12 hour and 24 hour time formats. The
DateSpinner uses the format that is typical for the current
locale.</p></td>
</tr>
<tr class="odd">
<td><p>Date and Time</p></td>
<td><p><samp>DateSelectorDisplayMode.DATE_AND_TIME</samp>
("dateAndTime")</p></td>
<td><div>
Displays the day, hours, and minutes. For locales that use 12-hour time,
also displays the AM/PM indicator. For example:
<pre><code>|| Mon Jun 13 || 2 || 57 || PM ||</code></pre>
</div>
<p>The current date is highlighted with the color defined by the
<samp>accentColor</samp> style property. The current time is not
highlighted.</p>
<p>You cannot display seconds in the DateSpinner control.</p>
<p>The month name is displayed in a shortened format. Does not display
the year.</p></td>
</tr>
</tbody>
</table>

The DateSpinner control is made up of several
[SpinnerList](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/SpinnerList.html)
controls. Each SpinnerList displays a list of valid values for a particular
place in the DateSpinner control. For example, a DateSpinner control that shows
the date has three SpinnerLists: one for the date, one for the month, and one
for the year. A DateSpinner that shows only the time will have two or three
SpinnerLists: one for hours, one for minutes, and optionally one for AM/PM (if
the time is represented in 12 hour increments).

## Change the type of a DateSpinner control

You select the type of
[DateSpinner](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/DateSpinner.html)
by setting the value of the `displayMode` property on the control. You can set
the `displayMode` property to the constants defined by the
[DateSelectionDisplayMode](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/calendarClasses/DateSelectorDisplayMode.html)
class or their string equivalents.

The following example lets you toggle the different DateSpinner types:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- datespinner/views/DateSpinnerTypes.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    		xmlns:s="library://ns.adobe.com/flex/spark"
    		title="DateSpinner Types">
    	<s:layout>
    		<s:VerticalLayout/>
    	</s:layout>

    	<fx:Script>
    		<![CDATA[
    			import spark.components.calendarClasses.DateSelectorDisplayMode;
    		]]>
    	</fx:Script>

    	<s:ComboBox id="modeList" selectedIndex="0" change="ds1.displayMode=modeList.selectedItem.value">
    		<s:ArrayList>
    			<fx:Object value="date" label="Date"/>
    			<fx:Object value="time" label="Time"/>
    			<fx:Object value="dateAndTime" label="Date and Time"/>
    		</s:ArrayList>
    	</s:ComboBox>

    	<s:DateSpinner id="ds1" displayMode="{DateSelectorDisplayMode.DATE}"/>

    	<s:Label text="{ds1.selectedDate}"/>

    </s:View>

When users interact with the DateSpinner control, the spinners snap to the
closest item in the list. At rest, the spinners are never between selections.

## Bind a DateSpinner control selection to other controls

You can bind the `selectedDate` property of a
[DateSpinner](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/DateSpinner.html)
control to other controls in a mobile application. The `selectedDate` property
is a pointer to a Date object, so methods of a Date object are accessible in
this manner.

The following example binds the day, month, and year to the Label controls:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- datespinner/views/DateSpinnerBinding.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    		xmlns:s="library://ns.adobe.com/flex/spark"
    		title="DateSpinner Binding" creationComplete="initAC()">
    	<s:layout>
    		<s:VerticalLayout/>
    	</s:layout>

    	<fx:Script>
    		<![CDATA[
    			import spark.components.calendarClasses.DateSelectorDisplayMode;
    			import mx.collections.ArrayCollection;

    			[Bindable]
    			private var dayArrayC:ArrayCollection = new ArrayCollection();

    			[Bindable]
    			private var selectedDateProperty:Date;

    			private function initAC():void {
    				dayArrayC.addItem("Sunday");
    				dayArrayC.addItem("Monday");
    				dayArrayC.addItem("Tuesday");
    				dayArrayC.addItem("Wednesday");
    				dayArrayC.addItem("Thursday");
    				dayArrayC.addItem("Friday");
    				dayArrayC.addItem("Saturday");
    			}

    		]]>
    	</fx:Script>

    	<s:DateSpinner id="ds1" displayMode="{DateSelectorDisplayMode.DATE}"/>

    	<fx:Binding source="ds1.selectedDate" destination="selectedDateProperty"/>

    	<s:Label id="label1" text="Day: {dayArrayC.getItemAt(ds1.selectedDate.day)}"/>
    	<s:Label id="label2" text="Day of month: {selectedDateProperty.getDate()}"/>
    	<s:Label id="label3" text="Month: {ds1.selectedDate.getMonth() + 1}"/>
    	<s:Label id="label4" text="Year: {selectedDateProperty.getFullYear()}"/>

    </s:View>

## Select dates programmatically in a DateSpinner control

You can change the date in a
[DateSpinner](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/DateSpinner.html)
control programmatically by assigning a new Date object to the value of the
`selectedDate` property.

The following example prompts you to enter a day, month, and year. When you
click the button, the DateSpinner changes to the new date:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- datespinner/views/DateSpinnerProgrammaticSelection.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    		xmlns:s="library://ns.adobe.com/flex/spark"
    		title="DateSpinner Programmatic Selection"
    		creationComplete="init()">
    	<s:layout>
    		<s:VerticalLayout/>
    	</s:layout>

    	<fx:Script>
    		<![CDATA[
    			import mx.events.FlexEvent;
    			import spark.components.calendarClasses.DateSelectorDisplayMode;

    			private function init():void {
    				// change event is dispatched when DateSpinner changes from user interaction
    				ds1.addEventListener("change", spinnerEventHandler);
    				// valueCommit event is dispatched when DateSpinner programmatically changes
    				ds1.addEventListener("valueCommit", spinnerEventHandler);
    			}

    			private function b1_clickHandler(e:Event):void {
    				ds1.selectedDate = new Date(ti3.text,ti1.text,ti2.text);
    			}

    			protected function spinnerEventHandler(event:Event):void {
    				eventLabel.text = event.type;
    			}
    		]]>
    	</fx:Script>

    	<s:TextInput id="ti1" prompt="Enter a Month"/>
    	<s:TextInput id="ti2" prompt="Enter a Day"/>
    	<s:TextInput id="ti3" prompt="Enter a Year"/>
    	<s:Button id="b1" label="Go!" click="b1_clickHandler(event)"/>

    	<s:DateSpinner id="ds1" displayMode="{DateSelectorDisplayMode.DATE}"/>

    	<s:Label id="eventLabel"/>

    </s:View>

When the date is changed programmatically, the DateSpinner control dispatches
both a `change` and a `valueCommit` event. When the date is changed through user
interaction, the DateSpinner control dispatches a `change` event.

When the selected date is changed programmatically, the selected values snap
into view without animating through the intermediate values.

## Restrict date ranges in a DateSpinner control

You can restrict the dates that users can select in a
[DateSpinner](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/DateSpinner.html)
control with the `minDate` and `maxDate` properties. These properties take Date
objects. Any date earlier than the `minDate` property and any date after the
`maxDate` property are not accessible in the DateSpinner control. In addition,
invalid years are not shown in "date" mode and invalid dates are not shown in
"dateAndTime" mode.

The following example creates two DateSpinner controls that have different
ranges of available dates:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- datespinner/views/MinMaxDates.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    	xmlns:s="library://ns.adobe.com/flex/spark"
    	title="Min/Max Dates">
    	<s:layout>
    		<s:VerticalLayout/>
    	</s:layout>

    	<fx:Script>
    		<![CDATA[
    			import spark.components.calendarClasses.DateSelectorDisplayMode;
    		]]>
    	</fx:Script>

    	<!-- Min date today, max date October 31, 2012. -->
    	<s:Label text="{dateSpinner1.selectedDate}"/>
    	<s:DateSpinner id="dateSpinner1"
    		displayMode="{DateSelectorDisplayMode.DATE}"
    		minDate="{new Date()}"
    		maxDate="{new Date(2012,9,31)}"/>

    	<!-- Min date 3 days ago, max date 7 days from now. -->
    	<s:Label text="{dateSpinner2.selectedDate}"/>
    	<s:DateSpinner id="dateSpinner2"
    		displayMode="{DateSelectorDisplayMode.DATE}"
    		minDate="{new Date(new Date().getTime() - 1000*60*60*24*3)}"
    		maxDate="{new Date(new Date().getTime() + 1000*60*60*24*7)}"/>
    </s:View>

You can only set a single minimum date and a single maximum date. You cannot set
an array of dates or multiple selection ranges.

You can also use the `minDate` and `maxDate` properties to restrict a
DateSpinner in "time" mode. The following example limits the time selection to
between 8 AM and 2 PM:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- datespinner/views/MinMaxTime.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    		xmlns:s="library://ns.adobe.com/flex/spark"
    		title="Min/Max Time">
    	<s:layout>
    		<s:VerticalLayout/>
    	</s:layout>

    	<fx:Script>
    		<![CDATA[
    			import spark.components.calendarClasses.DateSelectorDisplayMode;
    		]]>
    	</fx:Script>

    	<!-- Limit time selection to between 8am and 2pm -->
    	<s:DateSpinner id="dateSpinner1"
    				   displayMode="{DateSelectorDisplayMode.TIME}"
    				   minDate="{new Date(0,0,0,8,0)}"
    				   maxDate="{new Date(0,0,0,14,0)}"/>

    </s:View>

## Respond to a DateSpinner control's events

The
[DateSpinner](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/DateSpinner.html)
control dispatches a `change` event when the user changes the date. The `target`
property of this `change` event holds a reference to the DateSpinner, which you
can use to access the selected date, as the following example shows:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- datespinner/views/DateSpinnerChangeEvent.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    		xmlns:s="library://ns.adobe.com/flex/spark"
    		title="DateSpinner Change Event">
    	<s:layout>
    		<s:VerticalLayout/>
    	</s:layout>

    	<fx:Script>
    		<![CDATA[
    			import spark.components.calendarClasses.DateSelectorDisplayMode;

    			private var dayArray:Array = new Array(
    				"Sunday","Monday","Tuesday",
    				"Wednesday","Thursday","Friday","Saturday");

    			private function ds1_changeHandler(e:Event):void {
    				// Optionally cast the DateSpinner's selectedDate as a Date
    				var d:Date = new Date(e.currentTarget.selectedDate);
    				ta1.text = "You selected:";
    				ta1.text += "\n Day of Week: " + dayArray[d.day];
    				ta1.text += "\n Year: " + d.fullYear;
    				// Month is 0-based in ActionScript, so add 1:
    				ta1.text += "\n Month: " + int(d.month + 1);
    				ta1.text += "\n Day: " + d.date;
    			}
    		]]>
    	</fx:Script>

    	<s:DateSpinner id="ds1"
    		displayMode="{DateSelectorDisplayMode.DATE}"
    		change="ds1_changeHandler(event)"/>

    	<s:TextArea id="ta1" height="200" width="350"/>
    </s:View>

The `change` event is dispatched (and the value of the `selectedDate` property
is updated) only when all spinners have stopped spinning from user interactions.

To capture the change of a date that was done programmatically, listen for the
`value_commit` event.

## Change the minute interval of a DateSpinner control

You can change the interval for the minutes that a
[DateSpinner](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/DateSpinner.html)
control displays by using the `minuteStepSize` property. This property only
applies to a DateSpinner control with the `displayMode` set to "time" or
"dateAndTime". For example, if you set the `minuteStepSize` property to 10, the
DateSpinner control shows the values 0, 10, 20, 30, 40, and 50 in the minutes
spinner.

The following example lets you set the value of the `minuteStepSize` property.
The minute spinner updates accordingly.

    <?xml version="1.0" encoding="utf-8"?>
    <!-- datespinner/views/DateSpinnerMinuteInterval.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    		xmlns:s="library://ns.adobe.com/flex/spark"
    		title="DateSpinner Minute Interval">
    	<s:layout>
    		<s:VerticalLayout/>
    	</s:layout>

    	<fx:Script>
    		<![CDATA[
    			import spark.components.calendarClasses.DateSelectorDisplayMode;
    		]]>
    	</fx:Script>

    	<s:Label text="Select an interval:"/>

    	<s:ComboBox id="intervalList" selectedIndex="0"
    		change="ds1.minuteStepSize=intervalList.selectedItem.value">
    		<s:ArrayList>
    			<fx:Object value="1" label="1"/>
    			<fx:Object value="2" label="2"/>
    			<fx:Object value="3" label="3"/>
    			<fx:Object value="4" label="4"/>
    			<fx:Object value="5" label="5"/>
    			<fx:Object value="6" label="6"/>
    			<fx:Object value="10" label="10"/>
    			<fx:Object value="12" label="12"/>
    			<fx:Object value="15" label="15"/>
    			<fx:Object value="20" label="20"/>
    			<fx:Object value="30" label="30"/>
    		</s:ArrayList>
    	</s:ComboBox>

    	<s:DateSpinner id="ds1" displayMode="{DateSelectorDisplayMode.TIME}"/>
    </s:View>

Valid values for the `minuteStepSize` property must be evenly divisible into 60.
If you specify a value that is not evenly divisible into 60 (such as 25), the
`minuteStepSize` property defaults to a value of 1.

If you specify a minute interval and the current time does not fall on a value
in the minute spinner, the DateSpinner control rounds the current selection down
to the closest interval. For example, if the time is 10:29, and the
`minuteStepSize` is 15, the DateSpinner rounds to 10:15, assuming that the value
of 10:15 does not violate the `minDate` setting.

## Customize the appearance of a DateSpinner control

The
[DateSpinner](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/DateSpinner.html)
control supports most text styles such as `fontSize`, `color`, and
`letterSpacing`. In addition, it adds a new style property called `accentColor`.
This style changes the color of the current date or time in the spinner lists.
The following example sets this color to red:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- datespinner/views/DateSpinnerStyles.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    		xmlns:s="library://ns.adobe.com/flex/spark"
    		title="DateSpinner Styles">
    	<s:layout>
    		<s:VerticalLayout/>
    	</s:layout>

    	<fx:Script>
    		<![CDATA[
    			import spark.components.calendarClasses.DateSelectorDisplayMode;
    		]]>
    	</fx:Script>

    	<!-- Acceptable style formats are color_name (e.g., 'red') or
    		hex colors (e.g., '0xFF0000') -->
    	<s:DateSpinner id="dateSpinner1" accentColor="0xFF0000"
    		displayMode="{DateSelectorDisplayMode.DATE}"/>
    </s:View>

The DateSpinner control does not support the `textAlign` property. Text
alignment is set by the control.

To customize other aspects of a DateSpinner control's appearance, you can create
a custom skin for the control or modify some of the subcomponents with CSS.

The
[DateSpinnerSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/DateSpinnerSkin.html)
class controls the sizing of the DateSpinner control. Each spinner within a
DateSpinner control is a
[SpinnerList](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/SpinnerList.html)
object with its own
[SpinnerListSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/SpinnerListSkin.html).
All spinners in a single DateSpinner control are children of a single
[SpinnerListContainer](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/SpinnerListContainer.html),
which has its own skin, the
[SpinnerListContainerSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/SpinnerListContainerSkin.html).

You can explicitly set the `height` property of a DateSpinner control. If you
set the `width` property, the control centers itself in an area that is sized to
the requested width.

To modify the settings of the spinners within a DateSpinner control, you can
also use the SpinnerList, SpinnerListContainer, and
[SpinnerListItemRenderer](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/SpinnerListItemRenderer.html)
CSS type selectors. For example, the SpinnerList type selector controls the
padding properties in the spinners.

The following example changes the padding in the spinners:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- datespinner/DateSpinnerExamples2.mxml -->
    <s:ViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
    	xmlns:s="library://ns.adobe.com/flex/spark"
    	firstView="views.CustomSpinnerListSkinExample">

    	<fx:Style>
    		@namespace s "library://ns.adobe.com/flex/spark";

    		s|SpinnerListItemRenderer {
    			paddingTop: 7;
    			paddingBottom: 7;
    			paddingLeft: 5;
    			paddingRight: 5;
    		}
    	</fx:Style>

    </s:ViewNavigatorApplication>

In mobile applications, type selectors must be in the top-level application file
and not in a child view of the application. If you try to set the
SpinnerListItemRenderer type selector in a style block inside a view, Flex
throws a compiler warning.

You can extend the SpinnerListContainerSkin class to further customize the
appearance of the spinners in a DateSpinner control. The following example
applies a custom skin to the SpinnerListContainer:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- datespinner/DateSpinnerExamples3.mxml -->
    <s:ViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
    							xmlns:s="library://ns.adobe.com/flex/spark"
    							firstView="views.CustomSpinnerListSkinExample">
    	<fx:Style>
    		@namespace s "library://ns.adobe.com/flex/spark";

    		/* Change SpinnerListContainer for all DateSpinner controls */
    		s|SpinnerListContainer {
    			skinClass: ClassReference("customSkins.CustomSpinnerListContainerSkin");
    		}

    		/* Change padding for all DateSpinner controls */
    		s|SpinnerListItemRenderer {
    			paddingTop: 7;
    			paddingBottom: 7;
    			paddingLeft: 5;
    			paddingRight: 5;
    			fontSize: 12;
    		}
    	</fx:Style>

    </s:ViewNavigatorApplication>

The following CustomSpinnerListContainerSkin class reduces the size of the
"selection indicator" so that it more closely reflects the new size of the fonts
and padding in the rows of the spinner:

    // datespinner/customSkins/CustomSpinnerListContainerSkin.as
    package customSkins {
    	import mx.core.DPIClassification;

    	import spark.skins.mobile.SpinnerListContainerSkin;
    	import spark.skins.mobile.supportClasses.MobileSkin;
    	import spark.skins.mobile160.assets.SpinnerListContainerBackground;
    	import spark.skins.mobile160.assets.SpinnerListContainerSelectionIndicator;
    	import spark.skins.mobile160.assets.SpinnerListContainerShadow;
    	import spark.skins.mobile240.assets.SpinnerListContainerBackground;
    	import spark.skins.mobile240.assets.SpinnerListContainerSelectionIndicator;
    	import spark.skins.mobile240.assets.SpinnerListContainerShadow;
    	import spark.skins.mobile320.assets.SpinnerListContainerBackground;
    	import spark.skins.mobile320.assets.SpinnerListContainerSelectionIndicator;
    	import spark.skins.mobile320.assets.SpinnerListContainerShadow;

    	public class CustomSpinnerListContainerSkin extends SpinnerListContainerSkin
    	{
    		public function CustomSpinnerListContainerSkin() {
    			super();

    			switch (applicationDPI)
    			{
    				case DPIClassification.DPI_320:
    				{
    					borderClass = spark.skins.mobile320.assets.SpinnerListContainerBackground;
    					selectionIndicatorClass = spark.skins.mobile320.assets.SpinnerListContainerSelectionIndicator;
    					shadowClass = spark.skins.mobile320.assets.SpinnerListContainerShadow;

    					cornerRadius = 10;
    					borderThickness = 2;
    					selectionIndicatorHeight = 80; // was 120
    					break;
    				}
    				case DPIClassification.DPI_240:
    				{
    					borderClass = spark.skins.mobile240.assets.SpinnerListContainerBackground;
    					selectionIndicatorClass = spark.skins.mobile240.assets.SpinnerListContainerSelectionIndicator;
    					shadowClass = spark.skins.mobile240.assets.SpinnerListContainerShadow;

    					cornerRadius = 8;
    					borderThickness = 1;
    					selectionIndicatorHeight = 60; // was 90
    					break;
    				}
    				default: // default DPI_160
    				{
    					borderClass = spark.skins.mobile160.assets.SpinnerListContainerBackground;
    					selectionIndicatorClass = spark.skins.mobile160.assets.SpinnerListContainerSelectionIndicator;
    					shadowClass = spark.skins.mobile160.assets.SpinnerListContainerShadow;

    					cornerRadius = 5;
    					borderThickness = 1;
    					selectionIndicatorHeight = 40; // was 60

    					break;
    				}
    			}
    		}
    	}
    }

For more information about skinning mobile components, see
[Basics of mobile skinning](../skinning/basics-of-mobile-skinning.md).

## Use localized dates and times with a DateSpinner control

The
[DateSpinner](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/DateSpinner.html)
control supports all locales supported by the device on which the application is
running. If you set the locale to ja-JP, then the DateSpinner changes to
represent dates in the standard of the Japanese locale.

You can set the `locale` property on the DateSpinner control directly, or you
can set it on a container, such as the Application. The DateSpinner control
inherits the value of this property. The default locale is the locale of the
device on which the application is running, unless you override it with the
`locale` property.

The following example sets the default locale to "ja-JP". You can select a
locale to change the format of the DateSpinner:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- datespinner/LocalizedDateSpinner.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    		xmlns:s="library://ns.adobe.com/flex/spark"
    		title="Localized DateSpinner" locale="ja_JP">
    	<s:layout>
    		<s:VerticalLayout/>
    	</s:layout>

    	<fx:Script>
    		<![CDATA[
    			private function localeChangeHandler():void {
    				ds1.setStyle('locale',localeSelector.selectedItem);
    			}
    		]]>
    	</fx:Script>

    	<s:ComboBox id="localeSelector" change="localeChangeHandler()">
    		<s:ArrayList>
    			<fx:String>en-US</fx:String>
    			<fx:String>en-UK</fx:String>
    			<fx:String>es-AR</fx:String>
    			<fx:String>he-IL</fx:String>
    			<fx:String>ko-KR</fx:String>
    			<fx:String>ja-JP</fx:String>
    			<fx:String>vi-VN</fx:String>
    			<fx:String>zh-CN</fx:String>
    			<fx:String>zh-TW</fx:String>
    		</s:ArrayList>
    	</s:ComboBox>

    	<s:DateSpinner id="ds1" displayMode="dateAndTime"/>

    </s:View>
