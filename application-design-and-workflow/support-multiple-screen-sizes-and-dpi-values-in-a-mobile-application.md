# Support multiple screen sizes and DPI values in a mobile application

## Guidelines for supporting multiple screen sizes and DPI values

To develop an application that is platform independent, be aware of different
output devices. Devices can have different screen sizes or resolutions and
different DPI values, or densities.

Flex engineer Jason SJ describes two approaches to creating
resolution-independent mobile applications on
[his blog](https://web.archive.org/web/20150312073543mp_/http://blogs.adobe.com/jasonsj/2011/05/comparing-css-media-queries-vs-application-scaling.html).

**Terminology**

_Resolution_ is the number of pixels high by the number of pixels wide: that is,
the total number of pixels that a device supports.

_DPI_ is the number of dots per square inch: that is, the density of pixels on a
device's screen. The term DPI is used interchangeably with PPI (pixels per
inch).

**Flex support for DPIs**

The following flex features simplify the process of producing resolution- and
DPI-independent applications:

Skins  
DPI-aware skins for mobile components. The default mobile skins do not need
additional coding to scale well for most devices' resolutions.

applicationDPI  
A property that defines the size for which your custom skins are designed.
Suppose that you set this property at some DPI value, and a user runs the
application on a device with a different DPI value. Flex scales everything in
the application to the DPI of the device in use.

The default mobile skins are DPI-independent, both with and without DPI scaling.
As a result, if you do not use components with static sizes or custom skins, you
typically do not need to set the `applicationDPI` property.

**Dynamic layouts**

Dynamic layouts help you overcome differences in resolution. For example,
setting a control's width to 100% always fills the width of the screen, whether
the resolution is 480x854 or 480x800.

**Set applicationDPI property**

When you create density-independent applications, you can set the target DPI on
the root application tag. (For mobile applications, the root tag is
`<s:ViewNavigatorApplication>`, `<s:TabbedViewNavigatorApplication>`, or
`<s:Application>`.)

You set the value of the `applicationDPI` property to 160, 240, or 320,
depending on the approximate resolution of your target device. For example:

    <s:ViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
    	xmlns:s="library://ns.adobe.com/flex/spark"
    	firstView="views.DensityView1"
    	applicationDPI="320">

When you set the `applicationDPI` property, you effectively define a scale for
the application when it is compared to the target device's actual resolution
(the `runtimeDPI`) at runtime. For example, if you set the `applicationDPI`
property to 160 and the target device has a `runtimeDPI` of 160, the scale
factor is 1 (no scaling). If you set the `applicationDPI` property to 240, the
scale factor is 1.5 (Flex magnifies everything by 150%). At 320, the scale
factor is 2, so Flex magnifies everything by 200%.

In some cases, non-integer scaling can result in undesirable artifacts due to
interpolation, such as blurred lines.

**Disable DPI scaling**

To disable DPI scaling for the application, do not set the value of the
`applicationDPI` property.

#### Understand applicationDPI and runtimeDPI

The following table describes two properties of the
[Application](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/Application.html)
class that are integral to working with applications at different resolutions:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Property</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><samp>applicationDPI</samp></p></td>
<td><p>The target density or DPI of the application.</p>
<p>When you specify a value for this property, Flex applies a scale
factor to the root application. The result is an application designed
for one DPI value scales to look good on another device with a different
DPI value.</p>
<p>The scale factor is calculated by comparing the value of this
property with the <samp>runtimeDPI</samp> property. This scale factor is
applied to the entire application, including the preloader, pop-ups, and
all components on the stage.</p>
<p>When not specified, this property returns the same value as the
<samp>runtimeDPI</samp> property.</p>
<p>This property cannot be set in ActionScript; it can only be set in
MXML. You cannot change the value of this property at runtime.</p></td>
</tr>
<tr class="even">
<td><p><samp>runtimeDPI</samp></p></td>
<td><p>The density or DPI value of the device that the application is
currently running on.</p>
<p>Returns the value of the <samp>Capabilities.screenDPI</samp>
property, rounded to one of the constants defined by the
DPIClassification class.</p>
<p>This property is read-only.</p></td>
</tr>
</tbody>
</table>

#### Create resolution- and DPI-independent applications

Resolution- and DPI-independent applications have the following characteristics:

Images  
Vector images scale smoothly to match the target device's actual resolution.
Bitmaps, on the other hand, do not always scale as well. In these cases, you can
load bitmaps at different resolutions, depending on the device resolution by
using the
[MultiDPIBitmapSource](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/utils/MultiDPIBitmapSource.html)
class.

Text  
The font size of text (not the text itself) is scaled to match the resolution.

Layouts  
Use dynamic layouts to ensure that the application looks good when scaled. In
general, avoid using constraint-based layouts where you specify pixel boundaries
with absolute values. If you do use constraints, use the value of the
`applicationDPI` property to account for scaling.

Scaling  
Do not use the `scaleX` and `scaleY` properties on the Application object. When
you set the `applicationDPI` property, Flex does the scaling for you.

Styles  
You can use stylesheets to customize style properties for the target device's OS
and the application DPI settings.

Skins  
The Flex skins in the mobile theme use the application DPI value to determine
which assets to use at runtime. All visual skin assets defined by FXG files are
suited to the target device.

Application size  
Do not explicitly set the height and width of the application. Also, when
calculating sizes of custom components or popups, do not use the `stageWidth`
and `stageHeight` properties. Instead, use the `SystemManager.screen` property.

#### Determine runtime DPI

When your application starts, your application gets the value of the
`runtimeDPI` property from the `Capabilities.screenDPI` Flash Player property.
This property is mapped to one of the constants defined by the DPIClassification
class. For example, a Droid running at 232 DPI is mapped to the 240 runtime DPI
value. Device DPI values do not always exactly match the DPIClassification
constants (160, 240, or 320). Instead, they are mapped to those classifications,
based on a range of target values.

The mappings are as follows:

| DPIClassification constant | 160 DPI | 240 DPI          | 320 DPI |
| -------------------------- | ------- | ---------------- | ------- |
| Actual device DPI          | \<200   | \>=200 and \<280 | \>=280  |

You can customize these mappings to override the default behavior or to adjust
devices that report their own DPI value incorrectly. For more information, see
[Override the default DPI](#override-the-default-dpi).

#### Choose autoscaling or non-autoscaling

Choosing to use autoscaling (by setting the value of the `applicationDPI`
property) is a tradeoff between convenience and pixel-accurate visual fidelity.
If you set the `applicationDPI` property to scale your application
automatically, Flex uses skins targeted at the `applicationDPI`. Flex scales the
skins up or down to fit the device's actual density. Other assets in your
application and layout positions are scaled as well.

If you want to use autoscaling, and you are creating your own skins or assets
targeted at a single DPI value, you typically do the following:

- Create a single set of skins and view/component layouts that are targeted at
  the `applicationDPI` you specify.

- Create multiple versions of any bitmap asset used in your skins or elsewhere
  in your application, and specify them using the MultiDPIBitmapSource class.
  Vector assets and text in your skins do not need to be density-aware if you
  are autoscaling.

- Don't use the `@media` rule in your stylesheets, because your application only
  considers a single target DPI value.

- Test your application on devices of different densities to ensure that the
  appearance of the scaled application is acceptable on each device. In
  particular, check devices that cause scaling by a non-integer factor. For
  example, if `applicationDPI` is 160, test your application on 240-DPI devices.

If you choose not to use autoscaling (by leaving the `applicationDPI` property
unset), get the `applicationDPI` value. Use this property to determine the
actual DPI classification of the device, and adapt your application at runtime
by doing the following:

- Make multiple sets of skins and layouts targeted at each runtime DPI
  classification, or make a single set of skins and layouts that dynamically
  adapts to different densities. (The built-in Flex skins take the latter
  approach—each skin class checks the `applicationDPI` property and sets itself
  up appropriately.)

- Use `@media` rules in your stylesheets to filter CSS rules based on the
  device's DPI classification. Typically, you customize font sizes and padding
  values for each DPI value.

- Test your application on devices of different densities to ensure that your
  skins and layouts are properly adapting.

## Select styles based on DPI

Flex includes support for applying styles based on the target OS and application
DPI value in CSS. You apply styles with the `@media` rule in your stylesheet.
The `@media` rule is part of the CSS specification; Flex extends this rule to
include additional properties: `application-dpi` and `os-platform`. You use
these properties to apply styles selectively based on the application DPI and
the platform on which the application is running.

The following example sets the Spark
[Button](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/Button.html)
control's default `fontSize` style property to 12. If the device uses 240 DPI
and is running on the Android operating system, the `fontSize` property is 10.

    <?xml version="1.0" encoding="utf-8"?>
    <!-- mobile_skins/MediaQueryValuesMain.mxml -->
    <s:ViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
    	 xmlns:s="library://ns.adobe.com/flex/spark" applicationDPI="320">

    	<fx:Style>
    		@namespace s "library://ns.adobe.com/flex/spark";
    		@namespace mx "library://ns.adobe.com/flex/mx";

    		s|Button {
    			fontSize: 12;
    		}

    		@media (os-platform: "Android") and (application-dpi: 240) {
    			s|Button {
    				fontSize: 10;
    			}
    		}

    	</fx:Style>

    </s:ViewNavigatorApplication>

**Values for application-dpi property**

The `application-dpi` CSS property is compared against the value of the
`applicationDPI` style property that is set on the root application. The
following are valid values for the `application-dpi` CSS property:

- `160`

- `240`

- `320`

Each of the supported values for `application-dpi` has a corresponding constant
in the DPIClassification class.

**Values for the os-platform property**

The `os-platform` CSS property is matched to the value of the
`flash.system.Capabilities.version` property of Flash Player. The following are
valid values for the `os-platform` CSS property:

- `Android`

- `iOS`

- `Macintosh`

- `Linux`

- `QNX`

- `Windows`

The matching is not case sensitive.

If none of the entries match, then Flex seeks a secondary match by comparing the
first three characters to the list of supported platforms.

**Defaults for application-dpi and os-platform properties**

If you do not explicitly define an expression containing the `application-dpi`
or `os-platform` properties, then all expressions are assumed to match.

**Operators in the @media rule**

The `@media` rule supports the common operators "and" and "not". It also
supports comma-separated lists. Separating expressions by a comma implies an
"or" condition.

When you use the "not" operator, the "not" must be the first keyword in the
expression. This operator negates the entire expression, not just the property
that follows the "not". Because of
[bug SDK-29191](https://web.archive.org/web/20150312073543mp_/http://bugs.adobe.com/jira/browse/SDK-29191),
the "not" operator must be followed by a media type, such as "all", before one
or more expressions.

The following example shows how to use some of these common operators:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- mobile_skins/MediaQueryValuesMain.mxml -->
    <s:ViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
    	 xmlns:s="library://ns.adobe.com/flex/spark" applicationDPI="320">

    	<fx:Style>
    		@namespace s "library://ns.adobe.com/flex/spark";
    		@namespace mx "library://ns.adobe.com/flex/mx";

    		/* Every os-platform @ 160dpi */
    		@media (application-dpi: 160) {
    			s|Button {
    				fontSize: 10;
    			}
    		}

    		/* IOS only @ 240dpi */
    		@media (application-dpi: 240) and (os-platform: "IOS") {
    			s|Button {
    				fontSize: 11;
    			}
    		}

    		/* IOS at 160dpi or Android @ 160dpi */
    		@media (os-platform: "IOS") and (application-dpi:160), (os-platform: "ANDROID") and (application-dpi: 160) {
    			s|Button {
    				fontSize: 13;
    			}
    		}

    		/* Every os-platform except Android @ 240dpi */
    		@media not all and (application-dpi: 240) and (os-platform: "Android") {
    			s|Button {
    				fontSize: 12;
    			}
    		}

    		/* Every os-platform except IOS @ any DPI */
    		@media not all and (os-platform: "IOS") {
    			s|Button {
    				fontSize: 14;
    			}
    		}
    	</fx:Style>

    </s:ViewNavigatorApplication>

## Select bitmap assets based on DPI

Bitmap image assets typically only render optimally at the resolution for which
they are designed. This limitation can present challenges when you design
applications for multiple resolutions. The solution is to create multiple
bitmaps, each at a different resolution, and load the appropriate one depending
on the value of the application's `runtimeDPI` property.

The Spark
[BitmapImage](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/primitives/BitmapImage.html)
and
[Image](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/Image.html)
components have a `source` property of type
[Object](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/Object.html).
Because of this property, you can pass a class that defines which assets to use.
In this case, you pass the
[MultiDPIBitmapSource](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/utils/MultiDPIBitmapSource.html)
class to map different sources, depending on the value of the `runtimeDPI`
property.

The following example loads a different image, depending on the DPI:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- mobile_skins/views/MultiSourceView3.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    		xmlns:s="library://ns.adobe.com/flex/spark"
    		title="Image with MultiDPIBitmapSource">

    	<s:layout>
    		<s:VerticalLayout/>
    	</s:layout>

    	<fx:Script>
    		<![CDATA[
    			import mx.core.FlexGlobals;

    			private function doSomething():void {
    				/* The MultiDPIBitmapSource's source data. */
    				myTA.text = myImage.source.getSource(FlexGlobals.topLevelApplication.applicationDPI).toString();
    			}


    		]]>
    	</fx:Script>

    	<s:Image id="myImage">
    		<s:source>
    			<s:MultiDPIBitmapSource
    					source160dpi="assets/low-res/bulldog.jpg"
    					source240dpi="assets/med-res/bulldog.jpg"
    					source320dpi="assets/high-res/bulldog.jpg"/>
    		</s:source>
    	</s:Image>

    	<s:Button id="myButton" label="Click Me" click="doSomething()"/>
    	<s:TextArea id="myTA" width="100%"/>

    </s:View>

When you use the
[BitmapImage](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/primitives/BitmapImage.html)
and
[Image](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/Image.html)
classes with MultiDPIBitmapSource in a _desktop_ application, the `source160dpi`
property is used for the source.

The Button control's `icon` property also takes a class as an argument. As a
result, you can also use a MultiDPIBitmapSource object as the source for the
Button's icon. You can define the source of the icon inline, as the following
example shows:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- mobile_skins/views/MultiSourceView2.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    		xmlns:s="library://ns.adobe.com/flex/spark" title="Icons Inline">

    	<s:layout>
    		<s:VerticalLayout/>
    	</s:layout>

    	<fx:Script>
    		<![CDATA[
    			import mx.core.FlexGlobals;

    			private function doSomething():void {
    				/* The MultiDPIBitmapSource's source data. */
    				myTA.text = dogButton.getStyle("icon").getSource(FlexGlobals.topLevelApplication.applicationDPI).toString();
    			}
    		]]>
    	</fx:Script>

    	<s:Button id="dogButton" click="doSomething()">
    		<s:icon>
    			<s:MultiDPIBitmapSource id="dogIcons"
    					source160dpi="@Embed('../../assets/low-res/bulldog.jpg')"
    					source240dpi="@Embed('../../assets/med-res/bulldog.jpg')"
    					source320dpi="@Embed('../../assets/high-res/bulldog.jpg')"/>
    		</s:icon>
    	</s:Button>
    	<s:TextArea id="myTA" width="100%"/>

    </s:View>

You can also define icons by declaring them in a `<fx:Declarations>` block and
assigning the source with data binding, as the following example shows:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- mobile_skins/views/MultiSourceView1.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    		xmlns:mx="library://ns.adobe.com/flex/mx"
    		xmlns:s="library://ns.adobe.com/flex/spark"
    		title="Icons in Declarations">

    	<fx:Declarations>
    		<s:MultiDPIBitmapSource id="dogIcons"
    				source160dpi="@Embed('../../assets/low-res/bulldog.jpg')"
    				source240dpi="@Embed('../../assets/med-res/bulldog.jpg')"
    				source320dpi="@Embed('../../assets/high-res/bulldog.jpg')"/>
    	</fx:Declarations>

    	<s:layout>
    		<s:VerticalLayout/>
    	</s:layout>

    	<fx:Script>
    		<![CDATA[
    			import mx.core.FlexGlobals;

    			private function doSomething():void {
    				/* The MultiDPIBitmapSource's source data. */
    				myTA.text = dogIcons.getSource(FlexGlobals.topLevelApplication.applicationDPI).toString();
    			}
    		]]>
    	</fx:Script>

    	<s:Button id="dogButton" icon="{dogIcons}" click="doSomething()"/>
    	<s:TextArea id="myTA" width="100%"/>
    </s:View>

If the `runtimeDPI` property maps to a `source`_`XXX`_`dpi` property that is
`null` or an empty string (""), Flash Player uses the next higher density
property as the source. If that value is also `null` or empty, the next lower
density is used. If that value is _also_`null` or empty, Flex assigns `null` as
the source, and no image is displayed. In other words, you cannot explicitly
specify that no image should be displayed for a particular DPI.

## Select skin assets based on DPI

Logic in the default mobile skins' constructors chooses assets based on the
value of the `applicationDPI` property. These classes select assets that most
closely match the target DPI value. When you design custom skins that work both
with and without DPI scaling, use the `applicationDPI` property and not the
`runtimeDPI` property.

For example, the
[spark.skins.mobile.ButtonSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/ButtonSkin.html)
class uses a switch/case statement that selects FXG assets that are designed for
particular DPI values, similar to the following:

    switch (applicationDPI) {
    	case DPIClassification.DPI_320: {
    		upBorderSkin = spark.skins.mobile320.assets.Button_up;
    		downBorderSkin = spark.skins.mobile320.assets.Button_down;
    		...
    		break;
    	}
    	case DPIClassification.DPI_240: {
    		upBorderSkin = spark.skins.mobile240.assets.Button_up;
    		downBorderSkin = spark.skins.mobile240.assets.Button_down;
    		...
    		break;
    	}
    }

In addition to conditionally selecting FXG assets, the mobile skin classes also
set the values of other style properties such as layout gap and layout padding.
These settings are based on the DPI of the target device.

**Not setting applicationDPI**

If you do not set the `applicationDPI` property, then skins default to using the
`runtimeDPI` property. This mechanism guarantees that a skin that bases its
values on the `applicationDPI` property rather than on the `runtimeDPI` property
uses the appropriate resource both with and without DPI scaling.

When creating custom skins, you can choose to ignore the `applicationDPI`
setting. The result is a skin that is still scaled to match the DPI of the
target device, but it might not appear optimally if its assets are not
specifically designed for that DPI value.

**Use applicationDPI in CSS**

Use the value of the `applicationDPI` property in the CSS `@media` selector to
customize the styles used by your mobile or tablet application without creating
custom skins. For more information, see
[Select styles based on DPI](#select-styles-based-on-dpi).

## Manually determine scale factor and current DPI

To manually instruct a mobile or tablet application to select assets based on
the target device's DPI value, you can calculate the scaling factor at runtime.
You do this by dividing the value of the `runtimeDPI` property by the
`applicationDPI` style property:

    import mx.core.FlexGlobals;
    var curDensity:Number = FlexGlobals.topLevelApplication.runtimeDPI;
    var curAppDPI:Number = FlexGlobals.topLevelApplication.applicationDPI;
    var currentScalingFactor:Number = curDensity / curAppDPI;

You can use the calculated scaling factor to manually select assets. The
following example defines custom locations of bitmap assets for each DPI value.
It then loads an image from that custom location:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- mobile_skins/DensityMain.mxml -->
    <s:ViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
    	 xmlns:s="library://ns.adobe.com/flex/spark"
    	 firstView="views.DensityView1"
    	 applicationDPI="240" initialize="initApp()">

    	<fx:Script>
    		<![CDATA[
    				[Bindable]
    				public var densityDependentDir:String;

    				[Bindable]
    				public var curDensity:Number;
    				[Bindable]
    				public var appDPI:Number;
    				[Bindable]
    				public var curScaleFactor:Number;

    				public function initApp():void {
    					curDensity = runtimeDPI;
    					appDPI = applicationDPI;
    					curScaleFactor  =  appDPI / curDensity;

    					switch (curScaleFactor) {
    						case 1: {
    							densityDependentDir = "../../assets/low-res/";
    							break;
    						}
    						case 1.5: {
    							densityDependentDir = "../../assets/med-res/";
    							break;
    						}
    						case 2: {
    							densityDependentDir = "../../assets/high-res/";
    							break;
    						}
    					}
    				}
    		]]>
    	</fx:Script>

    </s:ViewNavigatorApplication>

The view that uses the scaling factor is as follows:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- mobile_skins/views/DensityView1.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    		xmlns:s="library://ns.adobe.com/flex/spark"
    		title="Home"
    		creationComplete="initView()">
    	<s:layout>
    		<s:VerticalLayout/>
    	</s:layout>

    	<fx:Script>
    		<![CDATA[
    			import mx.core.FlexGlobals;

    			[Bindable]
    			public var imagePath:String;

    			private function initView():void {
    				label0.text = "App DPI:" + FlexGlobals.topLevelApplication.appDPI;
    				label1.text = "Cur Density:" + FlexGlobals.topLevelApplication.curDensity;
    				label2.text = "Scale Factor:" + FlexGlobals.topLevelApplication.curScaleFactor;

    				imagePath = FlexGlobals.topLevelApplication.densityDependentDir + "bulldog.jpg";

    				ta1.text = myImage.source.toString();
    			}
    		]]>
    	</fx:Script>

    	<s:Image id="myImage" source="{imagePath}"/>

    	<s:Label id="label0"/>
    	<s:Label id="label1"/>
    	<s:Label id="label2"/>

    	<s:TextArea id="ta1" width="100%"/>
    </s:View>

## Override the default DPI

After setting the application DPI value, your application is scaled based on the
DPI value reported by the device on which it is running. In some cases, devices
report incorrect DPI values, or you want to override the default DPI selection
method in favor of a custom scaling method.

You can override the default scaling behavior of an application by overriding
the default DPI mappings. For example, if a device incorrectly reports that it
is 240 DPI instead of 160 DPI, you can create a custom mapping that looks for
this device and classifies it as 160 DPI.

To override a particular device's DPI value, you point the Application class's
`runtimeDPIProvider` property to a subclass of the
[RuntimeDPIProvider](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/mx/core/RuntimeDPIProvider.html)
class. In your subclass, you override the `runtimeDPI` getter and add logic that
provides a custom DPI mapping. Do not add dependencies to other classes in the
framework such as
[UIComponent](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/mx/core/UIComponent.html).
This subclass can only call into Player APIs.

The following example sets a custom DPI mapping for a device whose
`Capabilities.os` property matches "Mac 10.6.5":

    package {
    	import flash.system.Capabilities;
    	import mx.core.DPIClassification;
    	import mx.core.RuntimeDPIProvider;

    	public class DPITestClass extends RuntimeDPIProvider {
    		public function DPITestClass() {
    		}

    		override public function get runtimeDPI():Number {
    			// Arbitrary mapping for Mac OS.
    			if (Capabilities.os == "Mac OS 10.6.5")
    				return DPIClassification.DPI_320;

    			if (Capabilities.screenDPI < 200)
    				return DPIClassification.DPI_160;

    			if (Capabilities.screenDPI <= 280)
    				return DPIClassification.DPI_240;

    			return DPIClassification.DPI_320;
    		}
    	}
    }

The following application uses the DPITestClass to determine a runtime DPI value
to use for scaling. It points to the
[ViewNavigatorApplication](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/ViewNavigatorApplication.html)
class's `runtimeDPIProvider` property:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- mobile_skins/DPIMappingOverrideMain.mxml -->
    <s:ViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
    	 xmlns:s="library://ns.adobe.com/flex/spark"
    	 firstView="views.DPIMappingView"
    	 applicationDPI="160"
    	 runtimeDPIProvider="DPITestClass">

    </s:ViewNavigatorApplication>

The following is another example of a subclass of the RuntimeDPIProvider class.
In this case, the custom class checks the device's x and y resolution to
determine if the device is incorrectly reporting its DPI value:

    package {
    	import flash.system.Capabilities;
    	import mx.core.DPIClassification;
    	import mx.core.RuntimeDPIProvider;

    	public class SpecialCaseMapping extends RuntimeDPIProvider {
    		public function SpecialCaseMapping() {
    		}

    		override public function get runtimeDPI():Number {
    			/* A tablet reporting an incorrect DPI of 240. We could use
    				Capabilities.manufacturer to check the tablet's OS as well. */
    			if (Capabilities.screenDPI == 240 &&
    				Capabilities.screenResolutionY == 1024 &&
    				Capabilities.screenResolutionX == 600) {
    				return DPIClassification.DPI_160;
    			}

    			if (Capabilities.screenDPI < 200)
    				return DPIClassification.DPI_160;

    			if (Capabilities.screenDPI <= 280)
    				return DPIClassification.DPI_240;

    			return DPIClassification.DPI_320;
    		}
    	}
    }
