# Define transitions in a mobile application

Spark view transitions define how a change from one
[View](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/View.html)
container to another appears as it occurs on the screen. Transitions work by
applying an animation during the view change. Use transitions to create
compelling interfaces for your mobile applications.

By default, the existing View container slides off the screen as the new view
slides onto the screen. Alternatively, you can customize the change. For
example, your application defines a form in a View container that shows only a
few fields, but a subsequent View container shows additional fields. Rather than
sliding from view to view, you can use a flip or fade transition.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td colspan="3"><h2 id="adobe-recommends">Adobe recommends</h2></td>
</tr>
<tr class="even">
<td width="60%">
</div>
</div></td>
<td colspan="2"><table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td width="15%"><span><img
src="../img/BArnold.png" /></span></td>
<td width="85%"><h3
id="define-view-transitions-in-a-mobile-application"><a
href="https://www.youtube.com/watch?v=An7EiUmYfl4">Define
view transitions in a mobile application</a></h3>
<span>Brent Arnold</span><br />
<span>Learn how to define transitions in a mobile application
</span></td>
</tr>
<tr class="even">
<td colspan="2"><h3 id="have-a-tutorial-you-would-like-to-share"><img
src="../img/TinyBlueTutIcon.png" /><a
href="https://web.archive.org/web/20150222020256mp_/http://www.adobe.com/community/publishing/download.html">Have
a tutorial you would like to share?</a></h3></td>
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td colspan="2"><h2 id="adobe-recommends-1">Adobe recommends</h2></td>
<td colspan="2"><h3 id="have-a-tutorial-you-would-like-to-share-1"><img
src="../img/TinyBlueTutIcon.png" /><a
href="https://web.archive.org/web/20150222020256mp_/http://www.adobe.com/community/publishing/download.html">Have
a tutorial you would like to share?</a></h3></td>
</tr>
<tr class="even">
<td colspan="4" height="10"></td>
</tr>
<tr class="odd">
<td width="5%"><span><img
src="../img/HSchinsky.png" /></span></td>
<td width="45%"><h3
id="article-and-video-customizing-mobile-view-transitions"><a
href="https://web.archive.org/web/20111008172604/http://devgirl.org/2011/05/12/flex-4-5-using-mobile-view-transitions/">Article
and video: Customizing mobile view transitions</a></h3>
<span>Holly Schinsky</span><br />
<span>Learn how to customize transitions using the Flex view transition
classes</span></td>
<td width="5%"></td>
<td width="45%"></td>
</tr>
</tbody>
</table>

Flex supplies the following view transition classes that you can use when
changing View containers:

| Transition                                                                                                                                    | Description                                                                                                                                                                                                                        |
| --------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [CrossFadeViewTransition](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/transitions/CrossFadeViewTransition.html) | Performs a crossfade transition between the existing and new views. The the existing view fades out as the new view fades in.                                                                                                      |
| [FlipViewTransition](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/transitions/FlipViewTransition.html)           | Performs a flip transition between the existing and new views. You can define the flip direction and type.                                                                                                                         |
| [SlideViewTransition](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/transitions/SlideViewTransition.html)         | Performs a slide transition between the existing and new views. The existing view slides out as the new view slides in. You can control the slide direction and type. This transition is the default view transition used by Flex. |
| [ZoomViewTransition](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/transitions/ZoomViewTransition.html)           | Performs a zoom transition between the existing and new views. You can either zoom out the existing view or zoom in to the new view.                                                                                               |

> **Note:** View transitions in mobile applications are not related to standard
> Flex transitions. Standard Flex transitions define the effects played during a
> change of state. Navigation operations of the ViewNavigator container trigger
> View transitions. View transitions cannot be defined in MXML, and they do not
> interact with states.

## Apply a transition

You apply a transition when you change the active View container. Because view
transitions occur when you change View containers, you control them through the
[ViewNavigator](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/ViewNavigator.html)
container.

For example, you can use the following methods of the ViewNavigator class to
change the current view:

- `pushView()`

- `popView()`

- `popToFirstView()`

- `popAll()`

- `replaceView()`

These methods all take an optional argument that defines the transition to play
when changing views.

You can also change the current view by using hardware navigation keys on your
device, such as the back button. When you change the view by using a hardware
key, the ViewNavigator uses the default transitions defined by the
`ViewNavigator.defaultPopTransition` and `ViewNavigator.defaultPushTransition`
properties. By default, these properties specify to use the SlideViewTransition
class.

The following example shows the main application file that initializes the
`defaultPopTransition` and `defaultPushTransition` properties to use a
FlipViewTransition:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\SparkViewTrans.mxml -->
    <s:ViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
        xmlns:s="library://ns.adobe.com/flex/spark"
        firstView="views.EmployeeMainViewTrans"
        creationComplete="creationCompleteHandler(event);">

        <fx:Script>
            <![CDATA[
                import mx.events.FlexEvent;
                import spark.transitions.FlipViewTransition;

                // Define a flip transition.
                public var flipTrans:FlipViewTransition = new FlipViewTransition();

                // Set the default push and pop transitions of the navigator
                // to use the flip transition.
                protected function creationCompleteHandler(event:FlexEvent):void {
                    navigator.defaultPopTransition = flipTrans;
                    navigator.defaultPushTransition = flipTrans;
                }

                protected function button1_clickHandler(event:MouseEvent):void {
                    // Switch to the first view in the section.
                    // Use the default pop view transition defined by
                    // the ViewNavigator.defaultPopTransition property.
                    navigator.popToFirstView();
                }
            ]]>
        </fx:Script>

        <s:navigationContent>
            <s:Button icon="@Embed(source='assets/Home.png')"
                click="button1_clickHandler(event)"/>
        </s:navigationContent>
    </s:ViewNavigatorApplication>

The first view, the EmployeeMainViewTrans.mxml, defines a
CrossFadeViewTransition. It then passes the CrossFadeViewTransition as an
argument to the `pushView()` method on a change to the EmployeeView:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\views\EmployeeMainViewTrans.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
        xmlns:s="library://ns.adobe.com/flex/spark"
        title="Employees">
        <s:layout>
            <s:VerticalLayout paddingTop="10"/>
        </s:layout>

        <fx:Script>
            <![CDATA[
                import spark.events.IndexChangeEvent;
                import spark.transitions.CrossFadeViewTransition;

                // Define two transitions: a cross fade and a flip.
                public var xFadeTrans:CrossFadeViewTransition = new CrossFadeViewTransition();

                // Use the cross fade transition on a push(),
                // with a duration of 100 ms.
                protected function myList_changeHandler(event:IndexChangeEvent):void {
                    xFadeTrans.duration = 1000;
                    navigator.pushView(views.EmployeeView, myList.selectedItem, null, xFadeTrans);
                }
            ]]>
        </fx:Script>

        <s:Label text="Select an employee name"/>
        <s:List id="myList"
            width="100%" height="100%"
            labelField="firstName"
            change="myList_changeHandler(event);">
            <s:ArrayCollection>
                <fx:Object firstName="Bill" lastName="Smith" companyID="11233"/>
                <fx:Object firstName="Dave" lastName="Jones" companyID="13455"/>
                <fx:Object firstName="Mary" lastName="Davis" companyID="11543"/>
                <fx:Object firstName="Debbie" lastName="Cooper" companyID="14266"/>
            </s:ArrayCollection>
        </s:List>
    </s:View>

The EmployeeView is defined in the file EmployeeView.mxml, as shown in the
following example:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\views\EmployeeView.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
        xmlns:s="library://ns.adobe.com/flex/spark"
        title="Employee View">
        <s:layout>
            <s:VerticalLayout paddingTop="10"/>
        </s:layout>

        <s:VGroup>
            <s:Label text="{data.firstName}"/>
            <s:Label text="{data.lastName}"/>
            <s:Label text="{data.companyID}"/>
        </s:VGroup>
    </s:View>

## Apply a transition to the ActionBar control

By default, the
[ActionBar](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/ActionBar.html)
is not included in the transition from one view to another. Instead, the
ActionBar control uses a slide transition when the view changes, regardless of
the specified transition. To include the ActionBar in the transition when the
view changes, set the `transitionControlsWithContent` property of the transition
class to `true`.

## Use an easing class with a transition

A transition plays in two phases: an _acceleration phase_ followed by a
_deceleration phase_. You can change the acceleration and deceleration
properties of a transition by using an easing class. With easing, you can create
a more realistic rate of acceleration and deceleration. You can also use an
easing class to create a bounce effect or control other types of motion.

Flex supplies the Spark easing classes in the spark.effects.easing package. This
package includes classes for the most common types of easing, including Bounce,
Linear, and Sine easing. For more information on using these classes, see the
[Using Spark easing classes](https://web.archive.org/web/20150222020256mp_/http://help.adobe.com/en_US/flex/using/WS91E85D63-A025-4c46-B758-A275D4D3B3FC.html).

The following example shows a modification to the application defined in the
previous section. This version adds a Bounce easing class to the
FlipViewTransition:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\SparkViewTransEasier.mxml -->
    <s:ViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
        xmlns:s="library://ns.adobe.com/flex/spark"
        firstView="views.EmployeeMainViewTransEaser"
        creationComplete="creationCompleteHandler(event);">

        <fx:Script>
            <![CDATA[
                import mx.events.FlexEvent;
                import spark.transitions.FlipViewTransition;

                // Define a flip transition.
                public var flipTrans:FlipViewTransition = new FlipViewTransition();

                // Set the default push and pop transitions of the navigator
                // to use the flip transition.
                // Specify the Bounce class as the easer for the flip.
                protected function creationCompleteHandler(event:FlexEvent):void {
                    flipTrans.easer = bounceEasing;
                    flipTrans.duration = 1000;
                    navigator.defaultPopTransition = flipTrans;
                    navigator.defaultPushTransition = flipTrans;
                }

                protected function button1_clickHandler(event:MouseEvent):void {
                    // Switch to the first view in the section.
                    // Use the default pop view transition defined by
                    // the ViewNavigator.defaultPopTransition property.
                    navigator.popToFirstView();
                }
            ]]>
        </fx:Script>

        <fx:Declarations>
            <s:Bounce id="bounceEasing"/>
        </fx:Declarations>

        <s:navigationContent>
            <s:Button icon="@Embed(source='assets/Home.png')"
                      click="button1_clickHandler(event)"/>
        </s:navigationContent>
    </s:ViewNavigatorApplication>

To see the bounce, make sure to use the back button on the device.

## View transition lifecycle

A view transition goes through two main phases during execution: the
_preparation_ phase and the _execution_ phase.

Three methods of the transition class define the preparation phase. These
methods are called in the following order:

1.  `captureStartValues()`

    When this method is called, the ViewNavigator has created the new view but
    has not validated the new view or updated the content of the ActionBar
    control and the tab bar. Use this method to capture the start values for the
    components that play a role in the transition.

2.  `captureEndValues()`

    When this method is called, the new view has been fully validated, and the
    ActionBar control and the tab bar reflect the state of the new view. The
    transition can use this method to capture any values it requires from the
    new view.

3.  `prepareForPlay()`

    This method lets the transition initialize the effect instance that is used
    to animate the components of the transition.

The execution phase begins when the ViewNavigator calls the transition's
`play()` method. At this time, the new view has been created and validated, and
the ActionBar control and the tab bar have been initialized. The transition
dispatches a `start` event, and any effect instances created during the
preparation phase are now invoked by calling the effect's `play()` method.

When the view transition completes, the transition dispatches an `end` event.
The transitions base class,
[ViewTransitionBase](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/transitions/ViewTransitionBase.html),
defines the `transitionComplete()` method that you can call to dispatch the
`end` event. It is important that the transition cleans up any temporary objects
and remove listeners that it has created before dispatching the completion
event.

After the call to the `transitionComplete()` method, the ViewNavigator finalizes
the view changing process and resets the transition to its uninitialized state.
