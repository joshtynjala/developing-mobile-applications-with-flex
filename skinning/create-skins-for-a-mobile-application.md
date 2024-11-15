# Create skins for a mobile application

When customizing mobile skins, you create a custom mobile skin class. In some
cases, you also edit the assets that a mobile skin class uses.

When you edit a mobile skin class, you can change state-based interactions,
implement support for new styles, or add or remove child components to the skin.
You typically start with the source code of an existing skin and save it as a
new class.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td colspan="2"><h2 id="adobe-recommends">Adobe recommends</h2></td>
<td colspan="2"><h3 id="have-a-tutorial-you-would-like-to-share"><img
src="../img/TinyBlueTutIcon.png" /><a
href="https://web.archive.org/web/20150319055419mp_/http://www.adobe.com/community/publishing/download.html">Have
a tutorial you would like to share?</a></h3></td>
</tr>
<tr class="even">
<td colspan="4" height="10"></td>
</tr>
<tr class="odd">
<td width="5%"><span><img
src="../img/JSanHose.png" /></span></td>
<td width="45%"><h3 id="creating-skins-for-flex-mobile-applications"><a
href="https://web.archive.org/web/20151002222046/http://www.adobe.com/devnet/flex/articles/mobile-skinning-part1.html">Creating
skins for Flex mobile applications</a></h3>
<span><a
href="https://web.archive.org/web/20150319055419mp_/http://blogs.adobe.com/jasonsj/">Jason
San Jose</a></span><br />
<span>Read through this article-series to learn about mobile-optimized
skinning and handling of different pixel densities </span></td>
<td width="5%"></td>
<td width="45%"></td>
</tr>
</tbody>
</table>

You can also edit the assets used by mobile skins to change the visual
properties of the skin, such as size, color, or gradients and backgrounds. In
this case, you also edit the FXG assets used by the skins. The source \*.fxg
files used by mobile skins are located in the spark/skins/mobile/assets
directory.

Not all visual properties for mobile skins are defined in \*.fxg files. For
example, the Button skin's background color is defined by the `chromeColor`
style property in the ButtonSkin class. It is not defined in an FXG asset. In
this case, you would edit the skin class to change the background color.

## Create a mobile skin class

When creating a custom mobile skin class, the easiest approach is to use an
existing mobile skin class as a base. Then change that class and use it as a
custom skin.

To create a custom skin class:

1.  Create a directory in your project (for example, customSkins). This
    directory is the package name for your custom skins. While creating a
    package is not required, it's a good idea to organize custom skins in a
    separate package.

2.  Create a custom skin class in the new directory. Name the new class whatever
    you want, such as CustomButtonSkin.as.

3.  Copy the contents of the skin class that you are using as a base for the new
    class. For example, if you are using
    [ButtonSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/ButtonSkin.html)
    as a base class, copy the contents of the spark.skins.mobile.ButtonSkin file
    into the new custom skin class.

4.  Edit the new class. For example, make the following minimum changes to the
    CustomButtonSkin class:

    - Change the package location:

          package customSkins
          // was: package spark.skins.mobile

    - Change the name of the class in the class declaration. Also, extend the
      class your new skin is based on, not the base skin class:

          	public class CustomButtonSkin extends ButtonSkin
          	// was: public class ButtonSkin extends ButtonSkinBase

    - Change the class name in the constructor:

          	public function CustomButtonSkin()
          	// was: public function ButtonSkin()

5.  Change the custom skin class. For example, add support for additional states
    or new child components. Also, some graphical assets are defined in the skin
    class itself, so you can change some assets.

    To make your skin class easier to read, you typically remove any methods
    from the custom skin that you do not override.

    The following custom skin class extends ButtonSkin and replaces the
    `drawBackground()` method with custom logic. It replaces the linear gradient
    with a radial gradient for the background fill.

        	package customSkins {
        		import mx.utils.ColorUtil;
        		import spark.skins.mobile.ButtonSkin;
        		import flash.display.GradientType;
        		import spark.skins.mobile.supportClasses.MobileSkin;
        		import flash.geom.Matrix;

        		public class CustomButtonSkin extends ButtonSkin {

        			public function CustomButtonSkin() {
        				super();
        			}

        			private static var colorMatrix:Matrix = new Matrix();
        			private static const CHROME_COLOR_ALPHAS:Array = [1, 1];
        			private static const CHROME_COLOR_RATIOS:Array = [0, 127.5];

        			override protected function drawBackground(unscaledWidth:Number, unscaledHeight:Number):void {
        				super.drawBackground(unscaledWidth, unscaledHeight);

        				var chromeColor:uint = getStyle("chromeColor");
        				/*
        				if (currentState == "down") {
        					graphics.beginFill(chromeColor);
        				} else {
        				*/
        				var colors:Array = [];
        				colorMatrix.createGradientBox(unscaledWidth, unscaledHeight, Math.PI / 2, 0, 0);
        				colors[0] = ColorUtil.adjustBrightness2(chromeColor, 70);
        				colors[1] = chromeColor;
        				graphics.beginGradientFill(GradientType.RADIAL, colors, CHROME_COLOR_ALPHAS, CHROME_COLOR_RATIOS, colorMatrix);
        				// }
        				graphics.drawRoundRect(layoutBorderSize, layoutBorderSize,
        					unscaledWidth - (layoutBorderSize * 2),
        					unscaledHeight - (layoutBorderSize * 2),
        					layoutCornerEllipseSize, layoutCornerEllipseSize);
        				graphics.endFill();
        			}

        		}
        	}

6.  In your application, apply the custom skin by using one of the methods that
    are described in
    [Apply a custom mobile skin](./apply-a-custom-mobile-skin.md). The following
    example uses the `skinClass` property on the component tag to apply the
    `customSkins.CustomButtonSkin` skin:

        <?xml version="1.0" encoding="utf-8"?>
        <!-- mobile_skins/views/CustomButtonSkinView.mxml -->
        <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
        	xmlns:s="library://ns.adobe.com/flex/spark" title="Home">
        	<fx:Declarations>
        		<!-- Place non-visual elements (e.g., services, value objects) here -->
        	</fx:Declarations>

        	<s:Button label="Click Me" skinClass="customSkins.CustomButtonSkin"/>

        </s:View>

## Lifecycle methods of mobile skins

When creating custom skin classes, familiarize yourself with the following
[UIComponent](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/mx/core/UIComponent.html)
methods. These inherited, protected methods define a skin's children and
members, as well as help it interact with other components on the display list.

- `createChildren()` — Create any child graphics or text objects needed by the
  skin.

- `commitProperties()` — Copy component data into the skin, if necessary.

- `measure()` — Measure the skin, as efficiently as possible, and store the
  results in the `measuredWidth` and `measuredHeight` properties of the skin.

- `updateDisplayList()` — Set the position and size of graphics and text. Do any
  ActionScript drawing required. This method calls the `drawBackground()` and
  `layoutContents()` methods on the skin.

For more information about using these methods, see
[Implementing the component](https://web.archive.org/web/20150319055419mp_/http://help.adobe.com/en_US/flex/using/WS2db454920e96a9e51e63e3d11c0bf68641-7ff1.html).

## Common methods to customize in mobile skins

Many mobile skins implement the following methods:

- `layoutContents()` — Positions the children for the skin, such as dropshadows
  and labels. Mobile skin classes do not support Spark layouts such as
  HorizontalLayout and VerticalLayout. Lay out the skin's children manually in a
  method such as `layoutContents()`.

- `drawBackground()` — Renders a background for the skin. Typical uses include
  drawing `chromeColor`, `backgroundColor` or `contentBackgroundColor` styles
  based on the shape of the skin. Can also be used for tinting, such as with the
  `applyColorTransform()` method.

- `commitCurrentState()` — Defines state behaviors for mobile skins. You can add
  or remove supported states, or change the behavior of existing states by
  editing this method. This method is called when the state changes. Most skin
  classes override this method. For more information, see
  [Mobile skin states](./basics-of-mobile-skinning.md#mobile-skin-states).

## Create custom FXG assets

Most visual assets of mobile skins are defined using FXG. FXG is a declarative
syntax for defining static graphics. You can use a graphics tool such as Adobe
Fireworks, Adobe Illustrator, or Adobe Catalyst to export an FXG document. Then
you can use the FXG document in your mobile skin. You can also create FXG
documents in a text editor, although complex graphics can be difficult to write
from scratch.

Mobile skins typically use FXG files to define states of a skin. For example,
the
[CheckBoxSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/CheckBoxSkin.html)
class uses the following FXG files to define the appearance of its box and
checkmark symbol:

- CheckBox_down.fxg

- CheckBox_downSymbol.fxg

- CheckBox_downSymbolSelected.fxg

- CheckBox_up.fxg

- CheckBox_upSymbol.fxg

- CheckBox_upSymbolSelected.fxg

If you open these files in a graphics editor, they appear as follows:

![](../img/fms_checkbox_states.png)

Checkbox states (down, downSymbol, downSymbolSelected, up, upSymbol, and
upSymbolSelected)

**FXG files for multiple resolutions**

Most mobile skins have three sets of FXG graphics files, one for each default
target resolution. For example, different versions of all six CheckBoxSkin
classes appear in the spark/skins/mobile160, spark/skins/mobile240, and
spark/skins/mobile320 directories.

When you create a custom skin, you can do one of the following:

- Use one of default skins as a base (usually 160 DPI). Add logic that scales
  the custom skin to fit the device the application is running on by setting the
  `applicationDPI` property on the Application object.

- Create all three versions of the custom skin (160, 240, and 320 DPI) for
  optimal display.

Some mobile skins use a single set of FXG files for their graphical assets and
do not have DPI-specific graphics. These assets are stored in the
spark/skins/mobile/assets directory. For example, the ViewMenuItem skins and
TabbedViewNavigator button bar skins do not have DPI-specific versions, so all
of their FXG assets are stored in this directory.

**Customize FXG file**

You can open an existing FXG file and customize it, or create one and export it
from a graphics editor such as Adobe Illustrator. After you edit the FXG file,
apply it to your skin class.

To create a custom skin by modifying an FXG file:

1.  Create a custom skin class and put it in the customSkins directory, as
    described in [Create a mobile skin class](#create-a-mobile-skin-class).

2.  Create a subdirectory under the customSkins directory; for example, assets.
    Creating a subdirectory is optional, but helps to organize your FXG files
    and skin classes.

3.  Create a file in the assets directory and copy the contents of an existing
    FXG file into it. For example, create a file named
    CustomCheckBox_upSymbol.fxg. Copy the contents of the
    spark/skins/mobile160/assets/CheckBox_upSymbol.fxg into the new
    CustomCheckBox_upSymbol.fxg file.

4.  Change the new FXG file. For example, replace the logic that draws a check
    with an "X" filled with gradient entries:

        <?xml version='1.0' encoding='UTF-8'?>
        <!-- mobile_skins/customSkins/assets/CustomCheckBox_upSymbol.fxg -->
        <Graphic xmlns="http://ns.adobe.com/fxg/2008" version="2.0"
        	viewWidth="32" viewHeight="32">

        	<!-- Main Outer Border -->
        	<Rect x="1" y="1" height="30" width="30" radiusX="2" radiusY="2">
        		<stroke>
        			<SolidColorStroke weight="1" color="#282828"/>
        		</stroke>
        	</Rect>

        	<!-- Replace check mark with an "x" -->
        	<Group x="2" y="2">
        		<Line xFrom="3" yFrom="3" xTo="25" yTo="25">
        			<stroke>
        				<LinearGradientStroke caps="none" weight="8" joints="miter" miterLimit="4">
        					<GradientEntry color="#FF0033"/>
        					<GradientEntry color="#0066FF"/>
        				</LinearGradientStroke>
        			</stroke>
        		</Line>
        		<Line xFrom="25" yFrom="3" xTo="3" yTo="25">
        			<stroke>
        			<stroke>
        				<LinearGradientStroke caps="none" weight="8" joints="miter" miterLimit="4">
        					<GradientEntry color="#FF0033"/>
        					<GradientEntry color="#0066FF"/>
        				</LinearGradientStroke>
        			</stroke>
        			</stroke>
        		</Line>
        	</Group>
        </Graphic>

5.  In the custom skin class, import the new FXG class and apply it to a
    property. For example, in the CustomCheckBox class:

    1.  Import the new FXG file:

            //import spark.skins.mobile.assets.CheckBox_upSymbol;
            import customSkins.assets.CustomCheckBox_upSymbol;

    2.  Add the new asset to the custom skin class. For example, change the
        value of the `upSymbolIconClass` property to point to your new FXG
        asset:

            upSymbolIconClass = CustomCheckBox_upSymbol;

The complete custom skin class looks like the following:

    // mobile_skins/customSkins/CustomCheckBoxSkin.as
    package customSkins {
    	import spark.skins.mobile.CheckBoxSkin;
    	import customSkins.assets.CustomCheckBox_upSymbol;

    	public class CustomCheckBoxSkin extends CheckBoxSkin {
    		public function CustomCheckBoxSkin() {
    			super();
    			upSymbolIconClass = CustomCheckBox_upSymbol; // was CheckBox_upSymbol
    		}
    	}
    }

For information about working with and optimizing FXG assets for skins, see
[Optimizing FXG](https://web.archive.org/web/20150319055419mp_/http://help.adobe.com/en_US/flex/using/WS19f279b149e7481c1ce62b4a12b7ceade98-8000.html).

## View FXG files in applications

Because FXG files are written in XML, it can be difficult to visualize what the
final product looks like. You can write a Flex application that imports and
renders FXG files by adding them as components and wrapping them in a Spark
container.

To add FXG files as components to your application, add the location of the
source files to your application's source path. For example, to show mobile FXG
assets in a web-based application, add the mobile theme to your source path.
Then the compiler can find the FXG files.

The following _desktop_ example renders the various FXG assets of the CheckBox
component when you use it in a mobile application. Add the
frameworks\projects\mobiletheme\src\\ directory to the compiler's `source-path`
argument when you compile this example.

    <?xml version="1.0"?>
    <!-- mobile_skins/ShowCheckBoxSkins.mxml -->
    <s:Application xmlns:fx="http://ns.adobe.com/mxml/2009"
    	xmlns:s="library://ns.adobe.com/flex/spark"
    	xmlns:mx="library://ns.adobe.com/flex/mx"
    	xmlns:skins160="spark.skins.mobile160.assets.*"
    	xmlns:skins240="spark.skins.mobile240.assets.*"
    	xmlns:skins320="spark.skins.mobile320.assets.*">
    	<s:layout>
    		<s:VerticalLayout/>
    	</s:layout>

    	<!--
    	NOTE: You must add the mobile theme directory to source path
    	to compile this example.

    	For example:
    	mxmlc -source-path+=\frameworks\projects\mobiletheme\src\ ShowCheckBoxSkins.mxml
    	-->

    	<s:Label text="160 DPI" fontSize="24" fontWeight="bold"/>
    	<s:HGroup>
    		<skins160:CheckBox_down/>
    		<skins160:CheckBox_downSymbol/>
    		<skins160:CheckBox_downSymbolSelected/>
    		<skins160:CheckBox_up/>
    		<skins160:CheckBox_upSymbol/>
    		<skins160:CheckBox_upSymbolSelected/>
    	</s:HGroup>

    	<mx:Spacer height="30"/>

    	<s:Label text="240 DPI" fontSize="24" fontWeight="bold"/>
    	<s:HGroup>
    		<skins240:CheckBox_down/>
    		<skins240:CheckBox_downSymbol/>
    		<skins240:CheckBox_downSymbolSelected/>
    		<skins240:CheckBox_up/>
    		<skins240:CheckBox_upSymbol/>
    		<skins240:CheckBox_upSymbolSelected/>
    	</s:HGroup>

    	<mx:Spacer height="30"/>

    	<s:Label text="320 DPI" fontSize="24" fontWeight="bold"/>
    	<s:HGroup>
    		<skins320:CheckBox_down/>
    		<skins320:CheckBox_downSymbol/>
    		<skins320:CheckBox_downSymbolSelected/>
    		<skins320:CheckBox_up/>
    		<skins320:CheckBox_upSymbol/>
    		<skins320:CheckBox_upSymbolSelected/>
    	</s:HGroup>

    	<s:Label text="down, downSymbol, downSymbolSelected, up, upSymbol, upSymbolSelected"/>

    </s:Application>

## Use text in custom mobile skins

To render text in mobile skins, you use the
[StyleableStageText](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/supportClasses/StyleableStageText.html)
or
[StyleableTextField](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/supportClasses/StyleableTextField.html)
class. These text classes are optimized for mobile applications.

StyleableStageText provides access to the native text inputs for the
[TextInput](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TextInput.html)
and
[TextArea](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TextArea.html)
controls. It extends the UIComponent class, and implements the
[IEditableText](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/core/IEditableText.html)
and ISoftKeyboardHintClient interfaces.

StyleableTextField is also used by the TextInput and TextArea controls when you
do not want access to the native inputs. It is also used by non-input text
controls such as ActionBar and Button. It extends the
[TextField](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/text/TextField.html)
class, and implements the
[ISimpleStyleClient](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/mx/styles/ISimpleStyleClient.html)
and
[IEditableText](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/core/IEditableText.html)
interfaces.

For more information about using text controls in mobile applications, see
[Use text in a mobile application](../text/use-text-in-a-mobile-application.md).

**TLF in mobile skins**

For performance reasons, try to avoid classes that use TLF in mobile skins. In
some cases, such as with the Spark Label component, you can use classes that use
FTE.

**htmlText in mobile skins**

You cannot use the `htmlText` property in mobile applications.

**Gestures with text**

Touch+drag gestures always select text (when text is selectable or editable). If
the text is inside a Scroller, the Scroller only scrolls if the gesture is
outside the text component. These gestures only work when the text is editable
and selectable.

**Make text editable and selectable**

To make the text editable and selectable, set the `editable` and `selectable`
properties to `true`:

    textDisplay.editable = true;
    textDisplay.selectable = true;

**Bi-directionality**

Bi-directionality is not supported for text in the StyleableStageText or
StyleableTextField class.
