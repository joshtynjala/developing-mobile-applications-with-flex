# Handle user input in a mobile application

User input requires different handling in a mobile application compared to a
desktop or browser application. In a desktop application built for AIR, or in a
browser application built for Flash Player, the primary input devices are a
mouse and a keyboard. For mobile devices, the primary input device is a touch
screen. A mobile device often has some type of keyboard, and some devices also
include a five-way directional input method (left, right, up, down, and select).

The
[mx.core.UIComponent](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/mx/core/UIComponent.html)
class defines the `interactionMode` style property that you use to configure
components for the type of input used in the application. For the Halo and Spark
themes, the default value is `mouse` to indicate that the mouse is the primary
input device. For the Mobile theme, the default value is `touch` to indicate
that the primary input device is the touch screen.

## Hardware key support in a mobile application

Applications defined by the
[ViewNavigatorApplication](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/ViewNavigatorApplication.html)
or
[TabbedViewNavigatorApplication](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TabbedViewNavigatorApplication.html)
containers respond to the back and menu hardware keys of a device. When the user
presses the back key, the application navigates to the previous view. If there
is no previous view, the application exits and displays the home screen of the
device.

When the user presses the back button, the active view of the application
receives a `backKeyPressed` event. You can cancel the action of the back key by
calling `preventDefault()` in the event handler for the `backKeyPressed` event.

When the user presses the menu button, the current view's
[ViewMenu](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/ViewMenu.html)
container appears, if defined. The ViewMenu container defines a menu at the
bottom of a View container. Each View container defines its own menu specific to
that view.

The current
[View](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/View.html)
container dispatches a `menuKeyPressed` event when the user presses the menu
key. To cancel the action of the menu button, and prevent the ViewMenu from
appearing, call the `preventDefault()` method in the event handler for the
`menuKeyPressed` event.

For more information, see
[Define menus in a mobile application](./define-menus-in-a-mobile-application.md).

## Handle hardware keyboard events in a mobile application

In a mobile application built in Flex, you can detect when the user presses a
hardware key on a mobile device. For example, on an Android device you can
detect when the user presses the Home button, Back button, or Menu button.

To detect when the user presses a hardware key, create an event handlers for the
`KEY_UP` or `KEY_DOWN` event. Typically, you attach the event handlers to the
application object as defined by the Application, ViewNavigatorApplication, or
TabbedViewNavigatorApplication containers.

The Stage object defines the drawing area of an application. Each application
has one Stage object. Therefore, an application container is actually a child
container of the Stage object.

The `Stage.focus` property specifies the component that currently has keyboard
focus, or contains `null` if no component has focus. The component with keyboard
focus is the one that receives event notification when the user interacts with
the keyboard. Therefore, if `Stage.focus` is set to the application object, the
application object's event handlers are invoked.

On a mobile device, your application can be interrupted by another application.
For example, the mobile device can receive a phone call while your application
is running, or the user can switch to a different application. When the user
switches back to your application, the `Stage.focus` property is set to null.
Therefore, event handlers assigned to the application object do not respond to
the keyboard.

Because the `Stage.focus` property can be null on a mobile application, listen
for keyboard events on the Stage object itself to guarantee that your
application recognizes the event. The following example assigns keyboard event
handlers to the Stage object:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\SparkHWEventHandler.mxml -->
    <s:ViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
    	xmlns:s="library://ns.adobe.com/flex/spark"
    	firstView="views.SparkHWEventhandlerHomeView"
    	applicationComplete="appCompleteHandler(event);">

    	<fx:Script>
    		<![CDATA[
    			import mx.events.FlexEvent;

    			// Add the hardware key event handlers to the stage.
    			protected function appCompleteHandler(event:FlexEvent):void {
    				stage.addEventListener("keyDown", handleButtons, false,1);
    				stage.addEventListener("keyUp", handleButtons, false, 1);
    			}

    			// Event handler to handle hardware keyboard keys.
    			protected function handleButtons(event:KeyboardEvent):void
    			{
    				if (event.keyCode == Keyboard.HOME) {
    					// Handle Home button.
    				}
    				else if (event.keyCode == Keyboard.BACK) {
    					// Hanlde back button.
    				}
    			}
    		]]>
    	</fx:Script>
    </s:ViewNavigatorApplication>

## Handle mouse and touch events in a mobile application

AIR generates different events to indicate different types of inputs. These
events include the following:

Mouse events  
Events generated by user interaction generated by a mouse or touch screen. Mouse
events include `mouseOver`, `mouseDown`, and `mouseUp`.

Touch events  
Events generated on devices that detect user contact with the device, such as a
finger on a touch screen. Touch events include `touchTap`, `touchOver`, and
`touchMove`. When a user interacts with a device with a touch screen, the user
typically touches the screen with a finger or a pointing device.

Gesture events  
Events generated by multi-touch interactions, such as pressing two fingers on a
touch screen at the same time. Gesture events include `gesturePan`,
`gestureRotate`, and `gestureZoom`. For example, on some devices you can use a
pinch gesture to zoom out from an image.

**Built in support for mouse events**

The Flex framework and the Flex component set have built-in support for mouse
events, but not for touch or gesture events. For example, the user interacts
with Flex components in a mobile application by using the touch screen. The
components respond to mouse events, such as `mouseDown` and `mouseOver`, but not
to touch or gesture events.

For example, the user presses the touch screen to select the Flex Button
control. The Button control uses the `mouseUp` and `mouseDown` events to signal
that the user has interacted with the control. The Scroller control uses the
`mouseMove` and `mouseUp` events to indicate that the user is scrolling the
display.

![](../img/byline.png) Adobe Developer Evangelist Paul Trani explains handling
touch and gesture events in
[Touch Events and Gesture on Mobile](https://web.archive.org/web/20141103023343mp_/http://www.paultrani.com/blog/index.php/2011/02/touch-events-and-gestures-on-mobile/).

**Control events generated by AIR**

The `flash.ui.Multitouch.inputMode` property controls the events generated by
AIR and Flash Player. The `flash.ui.Multitouch.inputMode` property can have one
of the following values:

- `MultitouchInputMode.NONE` AIR dispatches mouse events, but not touch or
  gesture events.

- `MultitouchInputMode.TOUCH_POINT` AIR dispatches mouse and touch events, but
  not gesture events. In this mode, the Flex framework receives the same mouse
  events as it does for `MultitouchInputMode.NONE`.

- `MultitouchInputMode.GESTURE` AIR dispatches mouse and gesture events, but not
  touch events. In this mode, the Flex framework receives the same mouse events
  as it does for `MultitouchInputMode.NONE`.

As the list shows, regardless of the setting of the
`flash.ui.Multitouch.inputMode` property, AIR always dispatches mouse events.
Therefore, Flex components can always respond to user interactions made by using
a touch screen.

Flex lets you use any value of `flash.ui.Multitouch.inputMode` property in your
application. Therefore, while the Flex components do not respond to touch and
gesture events, you can add functionality to your application to respond to any
event. For example, you can add an event handler to the Button control to handle
touch events, such as the `touchTap`, `touchOver`, and `touchMove` events.

The ActionScript 3.0 Developer's Guide provides an overview of handling user
input on different devices, and on working with touch, multitouch, and gesture
input. For more information, see:

- [Basics of user interaction](https://web.archive.org/web/20141110234045/http://help.adobe.com/en_US/as3/dev/WS5b3ccc516d4fbf351e63e3d118a9b90204-7e3b.html)

- [Touch, multitouch and gesture input](https://web.archive.org/web/20141110234040/http://help.adobe.com/en_US/as3/dev/WSb2ba3b1aad8a27b0-6ffb37601221e58cc29-8000.html)
