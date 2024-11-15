# Embed fonts in a mobile application

You can embed fonts for use in mobile applications with some restrictions.

Because the
[Label](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/Label.html)
control uses FTE (and therefore CFF fonts), use the
[TextArea](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TextArea.html)
or
[TextInput](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TextInput.html)
controls with their TextField-based skins when embedding fonts in a mobile
application. You cannot embed fonts with StageText-based skins. In general,
avoid using FTE in a mobile application.

In your CSS, set `embedAsCFF` to `false` and apply the TextField-based skin, as
the following example shows:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- mobile_text/Main.mxml -->
    <s:ViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
                         xmlns:s="library://ns.adobe.com/flex/spark"
                         firstView="views.EmbeddingFontsView">
        <fx:Style>
            @namespace s "library://ns.adobe.com/flex/spark";

            @font-face {
                src: url("../assets/MyriadWebPro.ttf");
                fontFamily: myFontFamily;
                embedAsCFF: false;
            }
            .customStyle {
                fontFamily: myFontFamily;
                fontSize: 24;
                skinClass: ClassReference("spark.skins.mobile.TextAreaSkin");
            }
        </fx:Style>
    </s:ViewNavigatorApplication>

The TextArea control in the EmbeddingFontView view applies the type selector:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- mobile_text/EmbeddingFontsView.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
            xmlns:s="library://ns.adobe.com/flex/spark" title="Embedded Fonts">

        <s:layout>
            <s:VerticalLayout paddingTop="20" paddingLeft="20" paddingRight="20"/>
        </s:layout>

        <s:TextArea id="ta1"
                    width="100%"
                    styleName="customStyle"
                    text="This is a TextArea control that uses an embedded font."/>

        <s:TextArea id="ta2"
                    width="100%"
                    text="This TextArea control does not use an embedded font."/>

    </s:View>

If you use class selectors (such as `s|TextArea`) to apply styles (or to embed
fonts), define the class selector in the main application file. You cannot
define class selectors in a view of a mobile application.

For more information, see
[Embed fonts](https://web.archive.org/web/20150329004837mp_/http://help.adobe.com/en_US/flex/using/WS2db454920e96a9e51e63e3d11c0bf69084-7f5f.html).
