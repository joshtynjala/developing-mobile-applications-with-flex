# Basics of mobile skinning

## Compare desktop and mobile skins

Mobile skins are more lightweight than their desktop counterparts. As a result,
they have many differences; for example:

- Mobile skins are written in ActionScript. ActionScript-only skins provide the
  best performance on mobile devices.

- Mobile skins extend the
  [spark.skins.mobile.supportClasses.MobileSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/supportClasses/MobileSkin.html)
  class. This class extends
  [UIComponent](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/mx/core/UIComponent.html),
  as compared to the
  [SparkSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/SparkSkin.html)
  class which extends the
  [Skin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/supportClasses/Skin.html)
  class.

- Mobile skins use compiled FXG or simple ActionScript drawing for their
  graphical assets to improve performance. Skins for desktop applications, by
  contrast, typically use MXML graphics for much of their drawing.

- Mobile skins do not need to declare any of the skin states. Because the skins
  are written in ActionScript, states must be implemented procedurally.

- Mobile skins do not support state transitions.

- Mobile skins are laid out manually. Because mobile skins do not extend Group,
  they do not support the Spark layouts. As a result, their children are
  positioned manually in ActionScript.

- Mobile skins do not support all styles. The mobile theme omits some styles
  based on performance or other differences in the mobile skins.

![](../img/byline.png) In addition to performance-related differences, Flash
Builder also uses some mobile skin files differently. This is especially true of
mobile themes used on library projects. Blogger Jeffry Houser
[describes how to fix this](https://web.archive.org/web/20150301024137mp_/https://www.flextras.com/blog/index.cfm/2011/5/2/Why-cant-I-access-mobile-skins-in-my-Flex-Library-Project).

## Mobile host component

Mobile skins typically declare a public `hostComponent` property. This property
is not required, but is recommended. The `hostComponent` property must be of the
same type as the component that uses the skin. For example, the
[ActionBarSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/ActionBarSkin.html)
declares the `hostComponent` to be of type ActionBar:

    public var hostComponent:ActionBar;

Flex sets the value of the `hostComponent` property when the component first
loads the skin.

As with desktop skins, you can use the host component to access properties and
methods of the component to which the skin is attached. For example, you could
access the host component's public properties or add an event listener to the
host component from within the skin class.

## Mobile styles

Mobile skins support a subset of style properties that their desktop
counterparts support. The mobile theme defines this set of styles.

The following table defines the style properties available to components when
using the mobile theme:

| Style Property           | Supported By                                                 | Inheriting/Non-inheriting |
| ------------------------ | ------------------------------------------------------------ | ------------------------- |
| `accentColor`            | Button, ActionBar, ButtonBar                                 | Inheriting                |
| `backgroundAlpha`        | ActionBar                                                    | Non-inheriting            |
| `backgroundColor`        | Application                                                  | Non-inheriting            |
| `borderAlpha`            | List                                                         | Non-inheriting            |
| `borderColor`            | List                                                         | Non-inheriting            |
| `borderVisible`          | List                                                         | Non-inheriting            |
| `chromeColor`            | ActionBar, Button, ButtonBar, CheckBox, HSlider, RadioButton | Inheriting                |
| `color`                  | All components with text                                     | Inheriting                |
| `contentBackgroundAlpha` | TextArea, TextInput                                          | Inheriting                |
| `contentBackgroundColor` | TextArea, TextInput                                          | Inheriting                |
| `focusAlpha`             | All focusable components                                     | Non-inheriting            |
| `focusBlendMode`         | All focusable components                                     | Non-inheriting            |
| `focusColor`             | All focusable components                                     | Inheriting                |
| `focusThickness`         | All focusable components                                     | Non-inheriting            |
| `locale`                 | All components                                               | Inheriting                |
| `paddingBottom`          | TextArea, TextInput                                          | Non-inheriting            |
| `paddingLeft`            | TextArea, TextInput                                          | Non-inheriting            |
| `paddingRight`           | TextArea, TextInput                                          | Non-inheriting            |
| `paddingTop`             | TextArea, TextInput                                          | Non-inheriting            |
| `selectionColor`         | ViewMenuItem                                                 | Inheriting                |

Text-based components also support the standard text styles such as
`fontFamily`, `fontSize`, and `fontWeight`.

To see whether the mobile theme supports a style property, open the component's
description in the
[ActionScript Language Reference](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/index.html).
Many of these style limitations are because text-based mobile components do not
use TLF (Text Layout Framework). Instead, the mobile skins replace TLF-based
text controls with more lightweight components. For more information, see
[Use text in a mobile application](../text/use-text-in-a-mobile-application.md).

The mobile theme does not support the `rollOverColor`, `cornerRadius`, and
`dropShadowVisible` style properties.

Flex engineer Jason SJ describes styles and themes for mobile applications in
[his blog](https://web.archive.org/web/20150301024137mp_/http://blogs.adobe.com/jasonsj/?p=149).

## Mobile skin parts

For skin parts, mobile skins must adhere to the same skinning contract as
desktop skins. If a component has a required skin part, then the mobile skin
must declare a public property of the appropriate type.

**Exceptions**

Not all skin parts are required. For example, the Spark
[Button](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/Button.html)
has optional `iconDisplay` and `labelDisplay` skin parts. As a result, the
mobile
[ButtonSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/ButtonSkin.html)
class can declare an `iconDisplay` property of type
[BitmapImage](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/primitives/BitmapImage.html).
It can also declare a `labelDisplay` property of type
[StyleableTextField](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/supportClasses/StyleableTextField.html).

The `labelDisplay` part does not set an `id` property because the styles it uses
are all inheriting text styles. Also, the StyleableTextField is not a
UIComponent and therefore does not have an `id` property. The `iconDisplay` part
does not support styles so it does not set an `id` property either.

**Set styles with advanced CSS**

If you want to set styles on the skin part with the advanced CSS `id` selector,
the skin must also set the skin part's `id` property. For example, the
[ActionBar's](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/ActionBar.html)`titleDisplay`
skin part sets an `id` property so that it can be styled with advanced CSS; for
example:

    @namespace s "library://ns.adobe.com/flex/spark";
    s|ActionBar #titleDisplay {
    	color:red;
    }

## Mobile theme

The mobile theme determines which styles a mobile application supports. The
number of styles that are available with the mobile theme is a subset of the
Spark theme (with some minor additions). You can see a complete list of styles
supported by the mobile theme in [Mobile styles](#mobile-styles).

**Default theme for mobile applications**

The theme for mobile applications is defined in the themes/Mobile/mobile.swc
file. This file defines the global styles for mobile applications, as well as
the default settings for each of the mobile components. Mobile skins in this
theme file are defined in the spark.skins.mobile.\* package. This package
includes the MobileSkin base class.

The mobile.swc theme file is included in Flash Builder mobile projects by
default, but the SWC file does not appear in the Package Explorer.

When you create a new mobile project in Flash Builder, this theme is applied by
default.

**Change the theme**

To change the theme, use the `theme` compiler argument to specify the new theme;
for example:

    -theme+=myThemes/NewMobileTheme.swc

For more information on themes, see
[About themes](https://web.archive.org/web/20150301024137mp_/http://help.adobe.com/en_US/flex/using/WS2db454920e96a9e51e63e3d11c0bf69084-7f85.html).

Flex engineer Jason SJ describes how to create and overlay a theme in a mobile
application on
[his blog](https://web.archive.org/web/20150301024137mp_/http://blogs.adobe.com/jasonsj/?p=149).

## Mobile skin states

The
[MobileSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/supportClasses/MobileSkin.html)
class overrides the states mechanism of the UIComponent class and does not use
the view states implementation of desktop applications. As a result, mobile
skins only declare the host component's skin states that the skin implements.
They change state procedurally, based only on the state name. By contrast,
desktop skins must declare all states, regardless of whether they are used.
Desktop skins also use the classes in the mx.states.\* package to change states.

Most mobile skins implement fewer states than their desktop counterparts. For
example, the
[spark.skins.mobile.ButtonSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/ButtonSkin.html)
class implements the `up`, `down` and `disabled` states. The
[spark.skins.spark.ButtonSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/spark/ButtonSkin.html)
implements all of these states and the `over` state. The mobile skin does not
define behavior for the `over` state because that state would not commonly be
used on a touch device.

**commitCurrentState() method**

The mobile skin classes define their state behaviors in the
`commitCurrentState()` method. You can add behavior to a mobile skin to support
additional states by editing the `commitCurrentState()` method in your custom
skin class.

**currentState property**

The appearance of a skin depends on the value of the `currentState` property.
For example, in the mobile ButtonSkin class, the value of the `currentState`
property determines which FXG class is used as the border class:

    if (currentState == "down")
    	return downBorderSkin;
    else
    	return upBorderSkin;

For more information about the `currentState` property, see
[Create and apply view states](https://web.archive.org/web/20150301024137mp_/http://help.adobe.com/en_US/flex/using/WS2db454920e96a9e51e63e3d11c0bf63611-7ffa.html).

## Mobile graphics

Mobile skins typically use compiled FXG for their graphical assets. Skins for
desktop applications, by contrast, typically use MXML graphics for much of their
drawing.

**Embedded bitmap graphics**

You can use embedded bitmap graphics in your classes, which generally perform
well. However, bitmaps do not always scale well for multiple screen densities.
Creating several different assets, one for each screen density, can scale
better.

**Graphics in the default mobile theme**

The mobile skins in the default mobile theme use FXG graphics that are optimized
for the target device's DPI. The skins load graphics depending on the value of
the root application's `applicationDPI` property. For example, when a
[CheckBox](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/CheckBox.html)
control is loaded on a device with a DPI of 320, the
[CheckBoxSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/CheckBoxSkin.html)
class uses the spark.skins.mobile320.assets.CheckBox_up.fxg graphic for the
`upIconClass` property. At 160 DPI, it uses the
spark.skins.mobile160.assets.CheckBox_up.fxg graphic.

The following _desktop_ example shows the different graphics used by the
CheckBox skin at different DPIs:

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

For more information about resolutions and DPIs in mobile applications, see
[Support multiple screen sizes and DPI values in a mobile application](../application-design-and-workflow/support-multiple-screen-sizes-and-dpi-values-in-a-mobile-application.md).

In ActionScript skins, you can also use vectors cached as bitmaps. The only
drawback is that you cannot use any transitions that require the pixels to be
redrawn, such as alpha transitions. For more information, see
[www.adobe.com/devnet/air/flex/articles/writing_multiscreen_air_apps.html](https://web.archive.org/web/20150301024137mp_/http://www.adobe.com/devnet/air/flex/articles/writing_multiscreen_air_apps.html).
