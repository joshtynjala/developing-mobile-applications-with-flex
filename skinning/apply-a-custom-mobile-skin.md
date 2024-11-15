# Apply a custom mobile skin

You can apply a custom skin to your mobile component in the same way that you
apply a custom skin to a component in a desktop application.

**Apply a skin in ActionScript**

    // Call the setStyle() method:
    myButton.setStyle("skinClass", "MyButtonSkin");

**Apply a skin in MXML**

    <!-- Set the skinClass property: -->
    <s:Button skinClass="MyButtonSkin"/>

**Apply a skin in CSS**

    // Use type selectors for mobile skins, but only in the root document:
    s|Button {
        skinClass: ClassReference("MyButtonSkin");
    }

or

    // Use class selectors for mobile skins in any document:
    .myStyleClass {
        skinClass: ClassReference("MyButtonSkin");
    }

**Example of applying a custom mobile skin**

The following example shows all three methods of applying a custom mobile skin
to mobile components:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- mobile_skins/views/ApplyingMobileSkinsView.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
            xmlns:s="library://ns.adobe.com/flex/spark" title="Home">
        <s:layout>
            <s:VerticalLayout/>
        </s:layout>

        <fx:Script>
            <![CDATA[
                import customSkins.CustomButtonSkin;
                private function changeSkin():void {
                    b3.setStyle("skinClass", customSkins.CustomButtonSkin);
                }
            ]]>
        </fx:Script>

        <fx:Style>
            @namespace s "library://ns.adobe.com/flex/spark";
            .customButtonStyle {
                skinClass: ClassReference("customSkins.CustomButtonSkin");
            }
        </fx:Style>

        <s:Button id="b1" label="Click Me" skinClass="customSkins.CustomButtonSkin"/>
        <s:Button id="b2" label="Click Me" styleName="customButtonStyle"/>
        <s:Button id="b3" label="Click Me" click="changeSkin()"/>

    </s:View>

When you use a CSS _type_ selector to apply a custom skin, set it in the root
mobile application file. You cannot set type selectors in a mobile view, which
is the same as a custom component. You can still set styles in ActionScript,
MXML, or CSS with a class selector in any view or document in your mobile
application.
