# Use text in a mobile application

## Guidelines for text in a mobile application

Some Spark text controls have been optimized for use in mobile applications.
When possible, use the following text controls:

- Spark
  [TextArea](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TextArea.html)

- Spark
  [TextInput](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TextInput.html)

- Spark
  [Label](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/Label.html)

The text controls that allow user interaction (TextArea and TextInput) use the
[StageText](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/text/StageText.html)
class as the underlying input mechanism. StageText hooks into the native text
controls of the underlying OS. As a result, these text controls behave like
native controls rather than typical Flex controls.

The benefits of using StageText include the following on devices that support
them:

- Native performance and look and feel of the soft keyboard

- Auto-completion

- Auto-correction

- Touch-based text selection

- Customizable soft keyboards

- Key restrictions

Adobe evangelist Christian Cantrell
[describes the advantages and disadvantages of using StageText-based controls](https://web.archive.org/web/20150331233114mp_/http://blogs.adobe.com/cantrell/archives/2011/09/native-text-input-with-stagetext.html).

[TextField](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/text/TextField.html)-based
versions of the TextArea and TextInput control are also available. You can use
these versions to embed fonts or use some other functionality that is not
available on the StageText-based versions.

**Skins for mobile text controls**

When you create a mobile application, Flex automatically applies the mobile
theme. As a result, the Spark TextInput and TextArea controls use the following
StageText-based mobile skins by default:

- [StageTextAreaSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/StageTextAreaSkin.html)

- [StageTextInputSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/StageTextInputSkin.html)

The StageTextAreaSkin and StageTextInputSkin classes are optimized for mobile
applications and are based on the
[StageTextSkinBase](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/supportClasses/StageTextSkinBase.html)
class. They act as a wrapper around the native text input classes. However, they
do not support the following features of the non-TextField-based skins:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Supported by TextField-based controls</p></th>
<th><p>Not supported by TextField-based controls either</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Scrolling forms</p>
<p>Text measurement</p>
<p>Clipping</p>
<p>Embedded fonts</p>
<p>Fractional alpha values</p>
<p>Flash Text Engine (FTE)</p>
<p>Access to low-level keyboard events such as <samp>keyUp</samp> and
<samp>keyDown</samp></p></td>
<td><p>Text Layout Framework (TLF)</p>
<p>Bi-directionality and mirroring</p>
<p>Compact Font Format (CFF)</p>
<p>RichEditableText for text rendering</p>
<p>HTML text</p></td>
</tr>
</tbody>
</table>

Some of these limitations can be worked around by using the TextField-based
versions. To use the TextField-based versions of the text input controls, point
their skin classes to the TextField versions,
[TextInputSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/TextInputSkin.html)
and
[TextAreaSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/TextAreaSkin.html);
for example:

    <s:TextInput skinClass="spark.skins.mobile.TextInputSkin" text="TextField-based Skin"/>

The Spark Label control does not use a skin, but also does not use TLF.

**TLF in a mobile application**

In general, avoid text controls that use Text Layout Framework (TLF) in mobile
applications. The mobile skins of the TextArea and TextInput controls are
optimized for mobile applications and do not use TLF as their desktop and
web-based counterparts do. TLF is used in applications for providing a rich set
of controls over text rendering.

Avoid the following text controls in a mobile application, because they use TLF
and their skins are not optimized for mobile applications:

- Spark
  [RichText](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/RichText.html)

- Spark
  [RichEditableText](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/RichEditableText.html)

**Input with soft keyboards**

When a user places the focus on a text control that takes input, mobile devices
without keyboards display a soft keyboard. You have some control over the
available keys and other properties of the soft keyboard. For example, you can
enable auto-correction and auto-capitalization, and you can select among several
predetermined keyboard layouts.

For more information, see
[Use the soft keyboard in a mobile application](./use-the-soft-keyboard-in-a-mobile-application.md).

**Scrolling with text input controls**

The default mobile skins for the TextInput and TextArea controls do not support
scrolling forms. In other words, you cannot display these controls in forms or
views that require the control to scroll. If you do, visual artifacts appear
that are a result of the way the controls are implemented.

To use text input controls in a scrolling container, use the
[TextField](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/text/TextField.html)-based
skins rather than the StageText-based skins. For more information, see
[Scrolling considerations with StageText](../user-interface-and-layout/use-scroll-bar-in-a-mobile-application.md).

**Transitions with text input controls**

To animate smoothly, the runtime replace StageText controls with bitmaps
captured from them whenever an animation plays. This can cause a slight delay at
the beginning of transition animations and can also cause some visual artifacts
at the beginning and the end of the animations.

The slight delay is the time taken to capture bitmap representations of the text
in the components. This delay increases as the area and number of
StageText-based controls increases. To reduce the delay, avoid animating large
or numerous StageText-based components.

**Popups with text input controls**

StageText-based text inputs outside of the topmost popup are replaced with
bitmap representations when a popup appears. As a result:

- Use modal popups rather than non-modal popups. When a modal popup is shown,
  components outside of the popup are expected to lose their interactivity. In
  these cases, the replacement of StageTexts with bitmaps is less noticeable.

- StageText-based components should only be used inside popups that implement
  the IFocusManagerContainer interface. For example, use SkinnableContainer or
  one of its derivatives as the basis for popups.

- Use a
  [Callout](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/Callout.html)
  container when text components in lower layers should remain active. If a text
  component owns a callout, the text component remains active and sets the
  callout's arrow to point to that text component. This is a natural cue to the
  user that the text component can still be used.

- Avoid using multiple popups simultaneously. When more than one popup is
  visible at one time, only the topmost popup is interactive. If popups do not
  overlap, however, users will not be able to determine which popup is topmost.

- When non-modal popups overlap text controls, position the popup so that the
  overlap is near-total. If the user cannot see the text, they will be less
  likely to assume that the text control should still be interactive.

**Embed fonts in a mobile application**

You cannot use embedded fonts in a text input control that uses StageText.
Instead, use the TextField-based skins for the text input controls. You also
cannot use the Label control with embedded fonts because it uses FTE, which
requires CFF-based fonts. CFF fonts do not perform well in mobile applications.

For more information, see
[Embed fonts in a mobile application](./embed-fonts-in-a-mobile-application.md).

**StageText control class hierarchy**

The StageText classes (TextInput and TextArea) have a complex class hierarchy.
The base classes themselves have the following hierarchy:

        UIComponent
            |
    SkinnableComponent
            |
    SkinnableTextBase
            |
    TextInput/TextArea

As with all Spark classes, the skin classes have their own hierarchy:

        UIComponent
            |
        MobileSkin    StyleableStageText
            |              |
    StageTextSkinBase: textDisplay
            |
    StageTextInputSkin/StageTextAreaSkin

In the base skin class, the `textDisplay` property provides the hook to the
native text input as a
[StyleableStageText](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/supportClasses/StyleableStageText.html)
object. This class is also responsible for defining which styles are available
on the StageText-based text input controls.

## Use a Label control in a mobile application

The Spark
[Label](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/Label.html)
control is ideally suited to single lines of non-editable, non-selectable text.

The following example uses a simple Label control in a mobile application:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- mobile_text/views/SimpleLabel.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    		xmlns:s="library://ns.adobe.com/flex/spark" title="Simple Label">
    	<fx:Declarations>
    		<!-- Place non-visual elements (e.g., services, value objects) here -->
    	</fx:Declarations>

    	<s:layout>
    		<s:VerticalLayout/>
    	</s:layout>

    	<s:Label text="This is a simple Label control."/>

    </s:View>

The Label control uses FTE, which is not as performant as text controls that
have been optimized for mobile applications such as TextInput and TextArea.
However, the Label control does not use TLF, so it generally performs better
than controls such as RichText and RichEditableText, which do implement TLF.

In general, use Spark Label controls in mobile applications sparingly. Do not
use the Spark Label control in skins or item renderers. When creating an
ActionScript based item renderer, use the
[StyleableTextField](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/supportClasses/StyleableTextField.html)
class for rendering text. For an MXML-based component, you can still use Label.

Do not use the Label control when you embed fonts in a mobile application,
because the Label control uses CFF. Use the TextField-based version of the
[TextArea](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TextArea.html)
control instead. For more information, see
[Embed fonts in a mobile application](./embed-fonts-in-a-mobile-application.md).

## Use a TextArea control in a mobile application

The Spark
[TextArea](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TextArea.html)
control is a text-entry control that lets users enter and edit multiple lines of
text. It is optimized for mobile applications.

The default behavior of the TextArea control is to use the soft keyboard that
provides hooks into native methods of the underlying OS. As a result, it
supports features such as auto-correction, auto-completion, and soft keyboard
customization.

The following example uses a TextArea control in a mobile application:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- mobile_text/views/SimpleTextArea.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    		xmlns:s="library://ns.adobe.com/flex/spark"
    		title="Simple TextArea">
    	<fx:Declarations>
    		<!-- Place non-visual elements (e.g., services, value objects) here -->
    	</fx:Declarations>

    	<s:layout>
    		<s:VerticalLayout/>
    	</s:layout>

    	<fx:Script>
    		<![CDATA[
    			// Note the use of \n to add line feeds/carriage returns
    			// and \" to add quotation marks.
    			[Bindable]
    			public var myText:String ="\"Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.\"\n\n\"Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.\"";
    		]]>
    	</fx:Script>

    	<!-- Basic TextArea control with multiple lines of text. -->
    	<s:TextArea id="myTA" height="75%" text="{myText}"
    				paddingLeft="20" paddingTop="20"
    				paddingRight="20" paddingBottom="20"/>

    </s:View>

In a mobile application, the TextArea control uses the
[StageTextAreaSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/TextAreaSkin.html)
class for its skin by default. This skin uses the
[StyleableStageText](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/supportClasses/StyleableTextField.html)
class rather than the
[RichEditableText](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/RichEditableText.html)
class for rendering text. As a result, the TextArea control does not support
TLF. It supports only a subset of styles that are available on the TextArea
control with the non-mobile skin.

If you want a non-interactive, multi-line block of text, set the TextArea
control's `editable` property to `false`. (The runtime does not honor the
`selectable` property.) You can also remove the border by setting the
`borderVisible` property to `false`. You can change the background color by
setting the `contentBackgroundColor` and `contentBackgroundAlpha` properties.

The following example creates a non-interactive block of text that blends in
with the application's background:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- mobile_text/views/BlockOfText.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    		xmlns:s="library://ns.adobe.com/flex/spark" title="Block of Text">
    	<fx:Declarations>
    		<!-- Place non-visual elements (e.g., services, value objects) here -->
    	</fx:Declarations>

    	<s:layout>
    		<s:VerticalLayout/>
    	</s:layout>

    	<s:HGroup>
    		<s:Image source="@Embed(source='../../assets/myImage.jpg')" width="30%"/>
    		<!-- Create a multi-line block of text. -->
    		<s:TextArea width="65%"
    				editable="false"
    				borderVisible="false"
    				contentBackgroundColor="0xFFFFFF"
    				contentBackgroundAlpha="0"
    				height="400"
    				text="Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat."/>
    	</s:HGroup>

    </s:View>

Because the TextArea control does not support TLF, you cannot use the
`textFlow`, `content`, or `selectionHighlighting` properties. In addition, you
cannot use the following methods:

- `getFormatOfRange()`

- `setFormatOfRange()`

## Use a TextInput control in a mobile application

The Spark
[TextInput](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TextInput.html)
control is a text-entry control that lets users enter and edit a single line of
text. It is optimized for mobile applications.

The default behavior of the TextInput control is to use the soft keyboard that
provides hooks into native methods of the underlying OS. As a result, it
supports features such as auto-correction, auto-completion, and soft keyboard
customization.

The following example shows TextInput controls with prompt text and custom focus
rings in a mobile application:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- mobile_text/views/SimpleTextInput.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    		xmlns:s="library://ns.adobe.com/flex/spark" title="Simple TextInput">
    	<fx:Declarations>
    		<!-- Place non-visual elements (e.g., services, value objects) here -->
    	</fx:Declarations>

    	<s:layout>
    		<s:VerticalLayout
    			paddingTop="20"
    			paddingLeft="20"
    			paddingRight="20"/>
    	</s:layout>

    	<s:TextInput
    		prompt="Enter text here"
    		focusColor="green"
    		focusThickness="5"
    		focusAlpha=".1"/>
    	<s:TextInput
    		prompt="Enter text here, too"
    		focusColor="red"
    		focusThickness="5"
    		focusAlpha=".1"/>

    </s:View>

In a mobile application, the TextInput control uses the
[StageTextInputSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/TextInputSkin.html)
class for its skin by default. This skin uses the
[StyleableStageText](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/supportClasses/StyleableTextField.html)
class rather than the
[RichEditableText](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/RichEditableText.html)
class for rendering text. As a result, the TextInput control does not support
TLF. It supports only a subset of styles that are available on the TextInput
control with the non-mobile skin.

## Use the RichText and RichEditableText controls in a mobile application

Try to avoid using the
[RichText](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/RichText.html)
and
[RichEditableText](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/RichEditableText.html)
controls in mobile applications. These controls do not have mobile skins, and
they are not optimized for mobile applications. If you do use these controls,
you are using TLF, which is computationally expensive.

## MX text controls

You cannot use MX text controls such as MX Text and MX Label in mobile
applications. Use the Spark equivalents instead.

## Set styles on text input controls in a mobile application

The
[TextInput](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TextInput.html)
and
[TextArea](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TextArea.html)
controls support only a subset of styles in the mobile theme. The
[StyleableStageText](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/supportClasses/StyleableTextField.html)
class defines these styles.

The following styles are the only styles supported by TextInput and TextArea in
a mobile application:

- `color`

- `contentBackgroundAlpha`

- `contentBackgroundColor`

- Focus ring styles: `focusAlpha`, `focusBlendMode`, `focusColor`, and
  `focusThickness`

- `fontFamily`

- `fontStyle`

- `fontSize`

- `fontWeight`

- `locale`

- Padding styles: `paddingBottom`, `paddingLeft`, `paddingRight`, and
  `paddingTop`

- `showPromptWhenFocused`

- `textAlign`

In a mobile application, the Label control supports these styles, plus the
`textDecoration` style.

**Use the fontFamily style**

In the default mobile skins, the `fontFamily` property does not support a
comma-separated list of fonts. Instead, you can specify only one font, and the
runtime tries to map that font to a font that exists on the device.

For example, if you specify "Arial", the device renders the text in Arial if
that font is available. The runtime makes a best guess to determine what type of
font to substitute if the font is not available. If you specify a font name that
the runtime does not recognize, then the device renders the text in its default
font. The default on a mobile device is usually a sans-serif font.

You can specify `_sans`, `_serif`, or `_typewriter` to always get a sans-serif,
serif, or code font on a mobile device, respectively.

The following example shows how the text is rendered based on the value of the
`fontFamily` style:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- mobile_text/views/FontFamilyExample.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    		xmlns:s="library://ns.adobe.com/flex/spark" title="The fontFamily style">
    	<fx:Declarations>
    		<!-- Place non-visual elements (e.g., services, value objects) here -->
    	</fx:Declarations>

    	<s:layout>
    		<s:VerticalLayout/>
    	</s:layout>

    	<s:TextInput prompt="This is _sans" fontSize="14" fontFamily="_sans"/>
    	<s:TextInput prompt="This is _serif" fontSize="14" fontFamily="_serif"/>
    	<s:TextInput prompt="This is _typewriter" fontSize="14" fontFamily="_typewriter"/>
    	<s:TextInput prompt="This is Arial" fontSize="14" fontFamily="arial"/>
    	<s:TextInput prompt="This is Times" fontSize="14" fontFamily="times"/>
    	<s:TextInput prompt="This is Times New Roman" fontSize="14" fontFamily="Times New Roman"/>

    	<!-- Try a gibberish font name to see what the device's default font is: -->
    	<s:TextInput prompt="This is bugblatter" fontSize="14" fontFamily="bugblatter"/>

    </s:View>

## Create a custom mobile skin on a text input control

By using MXML and ActionScript, you can control some of the visual appearance
and behavior of text input controls in a mobile application. For example, you
can set the border color or toggle the appearance of the borders on the TextArea
and TextInput controls. In some cases, you must create a custom skin to change
the appearance of certain parts of the text controls.

The
[StageTextAreaSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/StageTextAreaSkin.html)
and
[StageTextInputSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/StageTextInputSkin.html)
classes define the default TextInput and TextArea skins in the mobile theme.
These skins get most of their layout and chrome logic from the
[StageTextSkinBase](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/supportClasses/StageTextSkinBase.html)
class.

To create a custom skin, create a custom StageTextSkinBase class that defines
the new appearance. Then create a custom StageTextAreaSkin or StageTextInputSkin
class that extends this custom class.

For more information about creating custom skins for the mobile theme, see
[Basics of mobile skinning](../skinning/basics-of-mobile-skinning.md).

## Restrict keys in a text input control

When you use StageText-based skins for text input controls, you can restrict the
characters that are allowed by using the `restrict` property of the
[TextInput](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TextInput.html)
or
[TextArea](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TextArea.html)
controls.

The default value of the `restrict` property is `null`, which means the user can
enter any character by default.

The `restrict` property takes a string of allowed characters. For ranges, use
the hyphen (-). Do not separate ranges with a space, comma, or other character,
unless you want to include that character in the definition. The following
example shows several examples of using the restriction syntax:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- mobile_text/views/RestrictStrings.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    		xmlns:s="library://ns.adobe.com/flex/spark" title="Examples of restrict">
    	<fx:Declarations>
    		<!-- Place non-visual elements (e.g., services, value objects) here -->
    	</fx:Declarations>

    	<s:layout>
    		<s:VerticalLayout paddingTop="20" paddingLeft="20" paddingRight="20"/>
    	</s:layout>

    	<s:TextInput prompt="Alpha-numeric only" restrict="a-zA-Z0-9"/>

    	<s:TextInput prompt="Numbers only" restrict="0-9"/>

    	<s:TextInput prompt="All chars, only uppercase alpha" restrict="^a-z"/>

    	<!-- ASCII chars 32 (space) through 126 (tilde) only: -->
    	<s:TextInput prompt="" restrict="\u0020-\u007E"/>

    	<s:TextInput prompt="All chars but not the caret or hyphen" restrict="^\^\-"/>

    </s:View>

The string value of the `restrict` property is read left to right; all
characters following a caret (^) are disallowed. For example:

    ta1.restrict = "A-Z^Q"; // All uppercase alpha characters, but exclude Q

If the first character in the string is a caret (^), then all characters are
allowed except characters that follow the caret. For example:

    ta1.restrict = "^a-z"; // All characters, but exclude lowercase alpha

You can use the backslash character to escape special characters. For example,
to restrict the use of the caret character:

    ta1.restrict = "^\^"; // All characters, but exclude the caret

You can use \u to enter ASCII key codes; for example:

    ta1.restrict = "\u0020-\u007E"; // ASCII chars 32 through 126 only
