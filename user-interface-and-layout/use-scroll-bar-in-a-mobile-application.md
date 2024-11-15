# Use scroll bars in a mobile application

## Considerations when using scroll bars in a mobile application

Typically, if content takes up more than the visible area of the screen, the
application displays scroll bars. Use the
[Scroller](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/Scroller.html)
control to add scroll bars to your application. Some components, such as the
Spark List control, support scrolling without the need of using the Scroller
component. For more information, see
[Scrolling Spark containers](https://web.archive.org/web/20150306074754mp_/http://help.adobe.com/en_US/flex/using/WSC5AF600B-9793-4dfd-AD9D-B9FC098869A8.html).

The hit area of a scroll bar is the area of the screen in which you position the
mouse to perform a scroll. In a desktop or browser-based application, the hit
area is the visible area of the scroll bar. In a mobile application, scroll bars
are hidden even when the content is larger than the visible area of the screen.
Hiding the scroll bars enables the application to use the full width and height
of the screen.

A mobile application must differentiate between when the user interacts with a
control, such as by selecting a Button control, from when the user wants to
scroll. One consideration with scroll bars in a mobile application is that Flex
components often change their appearance in response to a user interaction.

For example, when the user presses a
[Button](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/Button.html)
control, the button changes its appearance to indicate that it is selected. When
the user releases the button, the button changes its appearance back to the
deselected state. However, when scrolling, if the user touches the screen over
the Button, you do not want the button to change its appearance.

![](../img/byline.png) Adobe engineer Steven Shongrunden shows an example of
working with scroll bars in
[Saving scroll position between views in a mobile Flex Application](https://web.archive.org/web/20150306074754mp_/http://flexponential.com/2010/12/05/saving-scroll-position-between-views-in-a-mobile-flex-application/).

### Scrolling terms

The following terms are used to describe scrolling in a mobile application:

Content  
For a scrollable component, such as a Group container or List control, the
entire area of the component. Depending on the screen size and application
layout, only a subset of the content might be visible.

Viewport  
The subset of the content area of a component that is currently visible.

Drag  
A touch gesture that occurs when the user touches a scrollable area and then
moves their finger so that the content moves along with the gesture.

Velocity  
The rate and direction of movement of a drag gesture. Measured in
pixels-per-millisecond along the X and Y axis.

Throw  
A drag gesture where the user lifts their finger once the drag gesture has
reached a certain velocity, and the scrollable content continues to move.

Bounce  
A drag or throw gesture can move the viewport of a scrollable component outside
the component's content. The viewport then displays an empty area. When you
release your finger, or the velocity of a throw reaches zero, the viewport
bounces back to its resting point with the viewport filled with content. The
movement slows as the viewport reaches the resting point so that it comes to a
smooth stop.

### Scrolling modes in a mobile application

Scrollable components, such as List and Scroller, support different types of
scrolling based on the setting of the `pageScrollingEnabled` and
`scrollSnappingMode` properties of the component. These properties are only
valid when the `interactionMode` style is set to `touch`.

The following table describes the scrolling modes:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>pageScrollingEnabled</p></th>
<th><p>scrollSnappingMode</p></th>
<th><p>Mode</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>false (default)</p></td>
<td><p>none (default)</p></td>
<td><p>By default, scrolling is pixel-based. The final scroll position
is any pixel location based on the drag or throw gesture. For example,
you scroll a List control. Scrolling ends when you lift your finger even
if a partial List item is visible.</p></td>
</tr>
<tr class="even">
<td><p>false</p></td>
<td><p>leadingEdge, center, trailingEdge</p></td>
<td><p>Scrolling is pixel-based, but the content snaps to a final
position based on the value of <samp>scrollSnappingMode</samp>.</p>
<p>For example, you scroll a List vertically with
<samp>scrollSnappingMode</samp> set to a value of
<samp>leadingEdge</samp>. The List control snaps to a final scroll
position where the top list element is aligned to the top of the
list.</p></td>
</tr>
<tr class="odd">
<td><p>true</p></td>
<td><p>none</p></td>
<td><p>Scrolling is page-based. The size of the viewport of the
scrollable component determines the size of the page. You can only
scroll a single page at a time, regardless of the gesture.</p>
<p>Scroll at least 50% of the visible area of the component to cause the
page to scroll to the next page. If you scroll less than 50%, the
component remains on the current page. Alternatively, if the velocity of
the scroll is high enough, the next page displays. If the velocity is
not high enough, the component remains on the current page.</p>
<p>When content size is not an exact multiple of the viewport size,
additional padding is added to the last page to make it fit completely
in the viewport.</p></td>
</tr>
<tr class="even">
<td><p>true</p></td>
<td><p>leadingEdge, center, trailingEdge</p></td>
<td><p>Scrolling is page-based, but the component snaps to a final
position based on the value of <samp>scrollSnappingMode</samp>. To
guarantee that the snapping mode is respected, the scrolling distance is
not always exactly equal to the size of the page.</p></td>
</tr>
</tbody>
</table>

### Scrolling examples in a mobile application

In the following example, you use a Scroller component to wrap a Group container
in a mobile application. The Group container has as its child an Image control
containing a large image. By wrapping the Group container in the Scroller, you
can scroll the image:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\views\SparkMobilePixelScrollerHomeView.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
        xmlns:s="library://ns.adobe.com/flex/spark" title="HomeView">

        <s:Scroller width="200" height="200">
            <s:Group>
                <s:Image width="300" height="400"
                    source="@Embed(source='../assets/logo.jpg')"/>
            </s:Group>
        </s:Scroller>
    </s:View>

Notice that in this example, you omit any settings for of the
`pageScrollingEnabled` and `scrollSnappingMode` properties. Therefore, this
example uses the default pixel scrolling mode, and you can scroll to any pixel
location in the image.

The next example shows a List control that sets the `pageScrollingEnabled` and
`scrollSnappingMode` properties:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\views\SparkMobilePageScrollHomeView.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
        xmlns:s="library://ns.adobe.com/flex/spark"
        title="Adobe Product List">
        <s:layout>
            <s:VerticalLayout paddingTop="10" paddingLeft="10" paddingRight="10"/>
        </s:layout>

        <fx:Script>
            <![CDATA[
                import spark.events.IndexChangeEvent;

                protected function myList_changeHandler(event:IndexChangeEvent):void {
                    navigator.pushView(views.ProductPricelView,myList.selectedItem);
                }

            ]]>
        </fx:Script>

        <s:List id="myList" labelField="Product"
            height="200" width="100%"
            borderVisible="true"
            scrollSnappingMode="leadingEdge"
            pageScrollingEnabled="true"
            change="myList_changeHandler(event);">
            <s:dataProvider>
                <s:ArrayCollection>
                    <fx:Object Product="Adobe AIR" Price="11.99"/>
                    <fx:Object Product="Adobe BlazeDS" Price="11.99"/>
                    <fx:Object Product="Adobe ColdFusion" Price="11.99"/>
                    <fx:Object Product="Adobe Flash Player" Price="11.99"/>
                    <fx:Object Product="Adobe Flex" Price="Free"/>
                    <fx:Object Product="Adobe LiveCycleDS" Price="11.99"/>
                    <fx:Object Product="Adobe LiveCycle ES2" Price="11.99"/>
                    <fx:Object Product="Open Source Media Framework"/>
                    <fx:Object Product="Adobe Photoshop" Price="11.99"/>
                    <fx:Object Product="Adobe Illustrator" Price="11.99"/>
                    <fx:Object Product="Adobe Reader" Price="11.99"/>
                    <fx:Object Product="Adobe Acrobat" Price="11.99"/>
                    <fx:Object Product="Adobe InDesign" Price="Free"/>
                    <fx:Object Product="Adobe Connect" Price="11.99"/>
                    <fx:Object Product="Adobe Dreamweaver" Price="11.99"/>
                    <fx:Object Product="Open Framemaker"/>
                </s:ArrayCollection>
            </s:dataProvider>
        </s:List>
    </s:View>

This example uses page scrolling with a snap setting of `leadingEdge`.
Therefore, as you scroll the List, the List can scroll a single page at a time.
On a change of page, the control snaps to a final scroll position where the top
list element is aligned to the top of the list.

### Scrolling considerations with StageText

StageText lets you use native text inputs in a mobile application, rather than
using the standard text field controls. However, a scrollable container cannot
hold a text input control, such as the TextInput or Text Area control, that uses
StageText. Therefore, to use a text input control in a scrollable container,
reskin the control so it does not use StageText.

Flex ships with skins for the TextInput and TextArea controls that do not rely
on StageText. Use the following skins with these controls in a scrollable
container:

- [spark.skins.mobile.TextInputSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/TextInputSkin.html) Skin
  for TextInput that does not use StageText.

- [spark.skins.mobile.TextAreaSkin](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/skins/mobile/TextAreaSkin.html) Skin
  for TextArea that does not use StageText.

The following example shows a View container that uses a TextInput and TextArea
control in a scrollable container:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\SparkMobileStageTextScrollHomeView.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
        xmlns:s="library://ns.adobe.com/flex/spark"
        title="HomeView">
        <s:layout>
            <s:VerticalLayout/>
        </s:layout>

        <!-- Create CSS class selectors that reference the skins
             that do not rely on StageText. -->
        <fx:Style>
            @namespace s "library://ns.adobe.com/flex/spark";

            .myTextInputStyle {
                skinClass: ClassReference("spark.skins.mobile.TextInputSkin");
            }
            .myTextAreaStyle {
                skinClass: ClassReference("spark.skins.mobile.TextAreaSkin");
            }
        </fx:Style>

        <!-- Apply the class selectors to the TextInput and TextArea controls. -->
        <s:Scroller width="100%" height="100%">
            <s:VGroup height="250" width="100%"
                      paddingTop="10" paddingLeft="5" paddingRight="10">
                <s:HGroup verticalAlign="middle">
                    <s:Label text="Text Input 1: "
                        fontWeight="bold"/>
                    <s:TextInput width="225"
                        styleName="myTextInputStyle"/>
                </s:HGroup>
                <s:HGroup verticalAlign="middle">
                    <s:Label text="Text Input 2: "
                        fontWeight="bold"/>
                    <s:TextInput width="225"
                        styleName="myTextInputStyle"/>
                </s:HGroup>
                <s:HGroup verticalAlign="middle">
                    <s:Label text="Text Input 3: "
                        fontWeight="bold"/>
                    <s:TextInput width="225"
                        styleName="myTextInputStyle"/>
                </s:HGroup>
                <s:HGroup verticalAlign="middle">
                    <s:Label text="Text Input 4: "
                        fontWeight="bold"/>
                    <s:TextInput width="225"
                        styleName="myTextInputStyle"/>
                </s:HGroup>
                <s:HGroup verticalAlign="middle">
                    <s:Label text="TextArea 1: "
                        fontWeight="bold"/>
                    <s:TextArea width="225" height="100"
                        styleName="myTextAreaStyle "/>
                </s:HGroup>
            </s:VGroup>
        </s:Scroller>
    </s:View>

## Events and scroll bars

Flex components rely on events to indicate that a user interaction has occurred.
In response to the user interaction, the component can then change its
appearance, or perform some other action.

Application developers rely on events to handle user interaction. For example,
you typically use the Button control's `click` event to run an event handler in
response to the user selecting the button. Use the List control's `change` event
to run an event handler when the user selects an item in the List.

The Flex scrolling mechanism relies on the `mouseDown` event. That means the
scrolling mechanism listens for `mouseDown` events to determine if a scroll
operation is to be initiated.

### Interpret a user gesture as a scroll operation

An application consists of multiple Button controls in a scrollable container:

1.  Use your finger to press a Button control. The button dispatches a
    `mouseDown` event.

2.  Flex delays responding to the user interaction for a predefined time period.
    The delay period ensures that the user is selecting the button and not
    attempting to scroll the screen.

    If, during the delay period, you move your finger more than a predefined
    amount, Flex interprets that gesture as a scroll action. The distance that
    you have to move your finger for the gesture to be interpreted as a scroll
    is approximately 0.08 inches. This distance corresponds to about 20 pixels
    on a 252 DPI device.

    Because you moved your finger before the delay period expires, the Button
    control never recognizes the interaction. The button never dispatches an
    event or changes its appearance.

3.  After the delay period expires, the Button control recognizes the user
    interaction. The button changes its appearance to indicate that it has been
    selected.

    Use the `touchDelay` property of the control to configure the duration of
    the delay. The default value is 100 ms. If you set the `touchDelay` property
    to 0, there is no delay and scrolling is initiated immediately.

4.  After the delay period expires and Flex has dispatched the mouse events, you
    then move your finger more than 20 pixels. The Button control returns to the
    normal state, and the scroll action is initiated.

    In this case, the button changed its appearance because the delay period
    expired. However, once you move your finger more than 20 pixels, even after
    the delay period expires, Flex interprets the gesture as a scroll action.

> **Note:** Flex components support many different types of events besides mouse
> events. When working with components, you decide how your application reacts
> to these events. At the time of the `mouseDown` event, the intended behavior
> of the user is ambiguous. The user could intend to interact with the component
> or they could scroll. Because of this ambiguity, Adobe recommends listening
> for `click` or `mouseUp` events instead of the `mouseDown` event.

### Handle scroll events in a mobile application

To signal the beginning of a scroll operation, the component that dispatches the
`mouseDown` event dispatches a bubbling `touchInteractionStarting` event. If
that event is not canceled, the component dispatches a bubbling
`touchInteractionStart` event.

When a component detects a `touchInteractionStart` event, it must not attempt to
respond to the user gesture. For example, when a Button control detects a
`touchInteractionStart` event, it turns off any visual indicators that it set
based on the initial `mouseDown` event.

If a component does not want to allow the scroll to start, the component can
call the `preventDefault()` method in the event handler for the
`touchInteractionStarting` event.

When the scroll operation completes, the component that dispatches the
`mouseDown` event dispatches a bubbling `touchInteractionEnd` event.

## Scroll behavior based on the initial touch point

The following table describes the way scrolling is handled based on the location
of the initial touch point:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Selected item</p></th>
<th><p>Behavior</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Empty space,</p>
<p>noneditable text,</p>
<p>unselectable text</p></td>
<td><p>No component recognizes the gesture. The Scroller waits for the
user to move the touch point more than 20 pixels before initiating
scrolling.</p></td>
</tr>
<tr class="even">
<td><p>Item in a List control</p></td>
<td><p>After the delay period, the item renderer for the selected item
changes the display to the selected state. However, if at any time the
user moves more than 20 pixels, then the item changes its appearance to
the normal state and scrolling is initiated.</p></td>
</tr>
<tr class="odd">
<td><p>Button,</p>
<p>CheckBox,</p>
<p>RadioButton,</p>
<p>DropDownList</p></td>
<td><p>After the delay period expires, show its <samp>mouseDown</samp>
state. However, if the user moves the touch point more than 20 pixels,
then the control changes its appearance to the normal state and
initiates scrolling.</p></td>
</tr>
<tr class="even">
<td><p>Button component inside a List item renderer</p></td>
<td><p>The item renderer never highlights. The Button or the Scroller
handles the gesture, the same as the normal Button case.</p></td>
</tr>
</tbody>
</table>
