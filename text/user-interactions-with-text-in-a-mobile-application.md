# User interactions with text in a mobile application

You can use gestures such as swipe with text controls. The following example
listens for a swipe event, and tells you in which direction the swipe occurred:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- mobile_text/views/TextAreaEventsView.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
            xmlns:s="library://ns.adobe.com/flex/spark" title="TextArea swipe event"
            viewActivate="view1_viewActivateHandler()">
        <fx:Declarations>
            <!-- Place non-visual elements (e.g., services, value objects) here -->
        </fx:Declarations>
        <fx:Script>
            <![CDATA[
                import flash.events.TransformGestureEvent;
                import mx.events.FlexEvent;

                protected function swipeHandler(event:TransformGestureEvent):void {
                    // event.offsetX shows the horizontal direction of the swipe (1 is right, -1 is left)
                    swipeEvent.text = event.type + " " + event.offsetX;
                    if (swipeText.text.length == 0) {
                        swipeText.text = "Swipe again to make text go away."
                    }
                    else {
                        swipeText.text = "";
                    }
                }

                protected function view1_viewActivateHandler():void {
                    swipeText.addEventListener(TransformGestureEvent.GESTURE_SWIPE,swipeHandler);
                }

            ]]>
        </fx:Script>
        <s:VGroup>
            <s:TextArea id="swipeText" height="379"
                        editable="false" selectable="false"
                        text="Swipe to make text go away."/>
            <s:TextInput id="swipeEvent" />
        </s:VGroup>

    </s:View>

Touch+drag gestures always select text, but only if the text control is
selectable or editable. In some cases, you might not want to select text when
the user performs a touch+drag or swipe gesture on a text control. In this case,
either set the `selectable` and `editable` properties to `false` or reset the
selection with a call to the `selectRange(0,0)` method in the swipe event
handler.

If the text is inside a Scroller, the Scroller will only scroll if the gesture
is outside the text component.
