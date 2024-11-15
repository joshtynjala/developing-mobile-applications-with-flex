# Define a mobile application and a splash screen

## Create a mobile application container

The first tag in a mobile application is typically one of the following:

- The `<s:ViewNavigatorApplication>` tag defines a mobile application with a
  single section.

- The `<s:TabbedViewNavigatorApplication>` tag defines a mobile application with
  multiple sections.

When you develop applications for a tablet, screen size limits are not as
important as they are with phones. Therefore, for a tablet, you do not have to
structure your application around small views. Instead, you can build your
application using the standard Spark Application container with the supported
mobile components and skins.

> **Note:** When developing any mobile application, you can use the Spark
> Application container, even for phones. However, the Spark Application
> container does not include support for view navigation, data persistence, and
> the device's back and menu buttons. For more information, see:
>
> [Differences between the mobile application containers and the Spark Application container](#differences-between-the-mobile-application-containers-and-the-spark-application-container)
>
> [About the Application container](https://web.archive.org/web/20150509012659mp_/http://help.adobe.com/en_US/flex/using/WS2db454920e96a9e51e63e3d11c0bf62d75-7fff.html).

The mobile application containers have the following default characteristics:

| Characteristic  | Spark ViewNavigatorApplication and TabbedViewNavigatorApplication containers                                                                                                                                                                                                                                                                                               |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Default size    | 100% high and 100% wide to take up all available screen space.                                                                                                                                                                                                                                                                                                             |
| Child layout    | Defined by the individual View containers that make up the views of the application.                                                                                                                                                                                                                                                                                       |
| Default padding | 0 pixels.                                                                                                                                                                                                                                                                                                                                                                  |
| Scroll bars     | None. If you add scroll bars to the application container's skin, users can scroll the entire application. That includes the ActionBar and tab bar area of the application. You typically do not want those areas of the view to scroll. Therefore, add scroll bars to the individual View containers of the application, rather than to the application container's skin. |

## Differences between the mobile application containers and the Spark Application container

The Spark mobile application containers have much of the same functionality as
the Spark Application container. For example, you apply styles to the mobile
application containers in the same way that you apply them to the Spark
Application container.

The Spark mobile application containers have several characteristics that differ
from the Spark Application container:

- **Support for persistence**

  Supports data storage to and loading from a disk. Persistence lets users
  interrupt a mobile application, for example to answer a phone call, and then
  restore the state of the application when the call ends.

- **Support for view navigation**

  The
  [ViewNavigatorApplication](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/ViewNavigatorApplication.html)
  container automatically creates a single ViewNavigator container to control
  navigation among views.

  The
  [TabbedViewNavigatorApplication](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TabbedViewNavigatorApplication.html)
  container automatically creates a single TabbedViewNavigator container to
  control navigation among sections.

- **Support for the device's back and menu buttons**

  When the user presses the back button, the application navigates back to the
  previous view on the stack. When the user presses the menu button, the current
  view's
  [ViewMenu](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/ViewMenu.html)
  container appears, if defined.

For more information on the Spark application container, see
[About the Application container](https://web.archive.org/web/20150509012659mp_/http://help.adobe.com/en_US/flex/using/WS2db454920e96a9e51e63e3d11c0bf62d75-7fff.html).

## Handle application-level events

The NativeApplication class represents an AIR application. It provides
application information and application-wide functions, and it dispatches
application-level events. You can access the instance of the NativeApplication
class that corresponds to your mobile application by using the static property
`NativeApplication.nativeApplication`.

For example, the NativeApplication class defines the `invoke` and `exiting`
events that you can handle in your mobile application. The following example
references the NativeApplication class to define an event handler for the
`exiting` event:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\SparkNativeApplicationEvent.mxml -->
    <s:ViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
    	xmlns:s="library://ns.adobe.com/flex/spark"
    	firstView="views.EmployeeMainView"
    	creationComplete="creationCompleteHandler(event);">

    	<fx:Script>
    		<![CDATA[
    			import mx.events.FlexEvent;

    			protected function creationCompleteHandler(event:FlexEvent):void {
    				// Reference NativeApplication to assign the event handler.
    				NativeApplication.nativeApplication.addEventListener(Event.EXITING, myExiting);
    			}

    			protected function myExiting(event:Event):void {
    				// Handle exiting event.
    			}
    		]]>
    	</fx:Script>

    </s:ViewNavigatorApplication>

Notice that you access the ViewNavigator by using the
`ViewNavigatorApplication.navigator` property.

## Add a splash screen to an application

The Spark Application container is a base class for the ViewNavigatorApplication
and TabbedViewNavigatorApplication containers. When used with the Spark theme,
the Spark Application container supports an application preloader to show the
download and initialization progress of an application SWF file.

When used with the Mobile theme, you can display a splash screen instead. The
splash screen appears during application startup.

> **Note:** To use the splash screen in a desktop application, set the
> `Application.preloader` property to spark.preloaders.SplashScreen. Also add
> the frameworks\libs\mobile\mobilecomponents.swc to the library path of the
> application.

![](../img/byline.png) Blogger Joseph Labrecque
[blogged about AIR for Android Splash Screen with Flex](https://web.archive.org/web/20150509012659mp_/http://inflagrantedelicto.memoryspiral.com/2011/04/air-for-android-splash-screen-with-flex-4-5/).

![](../img/byline.png) Blogger Brent Arnold
[created a video about adding a splash screen to an Android application](https://www.youtube.com/watch?v=Cp25EShGlP4).

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
href="https://web.archive.org/web/20150509012659mp_/http://www.adobe.com/community/publishing/download.html">Have
a tutorial you would like to share?</a></h3></td>
</tr>
<tr class="even">
<td colspan="4" height="10"></td>
</tr>
<tr class="odd">
<td width="5%"><span><img
src="../img/RenaunErickson.png" /></span></td>
<td width="45%"><h3
id="customizing-flex-applicationdpi-for-a-multiple-screen-size-application"><a
href="https://web.archive.org/web/20150509012659mp_/http://renaun.com/blog/2011/10/customizing-flex-applicationdpi-for-a-multiple-screen-size-application/">Customizing
Flex applicationDPI for a multiple screen size application</a></h3>
<span>Renaun Erickson</span><br />
<span>Building a Flex mobile application that works across smartphones
and tablets takes an understanding of screen sizes, screen dots per inch
(DPI) and screen resolutions.</span></td>
<td width="5%"></td>
<td width="45%"></td>
</tr>
</tbody>
</table>

### Add a splash screen from an image file

You can load a splash screen directly from an image file. To configure the
splash screen, you use the `splashScreenImage`, `splashScreenScaleMode`, and
`splashScreenMinimumDisplayTime` properties of the application class.

For example, the following example loads a splash screen from a JPG file using
the letterbox format:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\SparkMobileSplashScreen.mxml -->
    <s:ViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
    	xmlns:s="library://ns.adobe.com/flex/spark"
    	firstView="views.EmployeeMainView"
    	splashScreenImage="@Embed('assets/logo.jpg')"
    	splashScreenScaleMode="letterbox">

    </s:ViewNavigatorApplication>

### Add a splash screen from a custom component

The example in the previous section used a JPG file to define the splash screen.
The disadvantage of that mechanism is that the application uses the same image
regardless of the capabilities of the mobile device on which the application
runs.

Mobile devices have different screen resolutions and sizes. Rather than using a
single image as the splash screen, you can instead define a custom component.
The component determines the capabilities of the mobile device and uses the
appropriate image for the splash screen.

Use the
[SplashScreenImage](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/preloaders/SplashScreenImage.html)
class to define the custom component, as the following example shows:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\myComponents\MySplashScreen.mxml -->
    <s:SplashScreenImage xmlns:fx="http://ns.adobe.com/mxml/2009"
    	xmlns:s="library://ns.adobe.com/flex/spark">

    	<!-- Default splashscreen image. -->
    	<s:SplashScreenImageSource
    		source="@Embed('../assets/logoDefault.jpg')"/>

    	<s:SplashScreenImageSource
    		source="@Embed('../assets/logo240Portrait.jpg')"
    		dpi="240"
    		aspectRatio="portrait"/>

    	<s:SplashScreenImageSource
    		source="@Embed('../assets/logo240Landscape.jpg')"
    		dpi="240"
    		aspectRatio="landscape"/>

    	<s:SplashScreenImageSource
    		source="@Embed('../assets/logo160.jpg')"
    		dpi="160"
    		aspectRatio="portrait"
    		minResolution="960"/>
    </s:SplashScreenImage>

Within the definition of the component, use the
[SplashScreenImageSource](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/preloaders/SplashScreenImageSource.html)
class to define each of the splash screen images. The
`SplashScreenImageSource.source` property specifies the image file. The
SplashScreenImageSource `dpi`, `aspectRatio`, and `minResolution` properties
define the capabilities of a mobile device that are required to display the
image.

For example, the first SplashScreenImageSource definition specifies only the
`source` property for the image. Because there are no settings for the `dpi`,
`aspectRatio`, and `minResolution` properties, this image can be used on any
device. Therefore, it defines the default image displayed when no other image
matches the capabilities of the device.

The second and third SplashScreenImageSource definitions specify an image for a
240 DPI device in either portrait or landscape modes.

The final SplashScreenImageSource definition specifies an image for a 160 DPI
device in portrait mode with a minimum resolution of 960 pixels. The value of
the `minResolution` property is compared against the larger of the values of the
`Stage.stageWidth` and `Stage.stageHeight` properties. The larger of the two
values must be equal to or greater than the `minResolution` property.

The following mobile application uses this component:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\SparkMobileSplashComp.mxml -->
    <s:ViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
    	xmlns:s="library://ns.adobe.com/flex/spark"
    	firstView="views.EmployeeMainView"
    	splashScreenImage="myComponents.MySplashScreen">
    </s:ViewNavigatorApplication>

The SplashScreenImage class automatically determines the image that best matches
the capabilities of the device. This matching is based on the `dpi`,
`aspectRatio` and `minResolution` properties of each SplashScreenImageSource
definition.

The procedure for determining the best match is as follows:

1.  Determine all of the SplashScreenImageSource definitions that match the
    settings of the mobile device. A match occurs when:

    1.  The SplashScreenImageSource definition does not have that setting
        explicitly defined. For example, no setting for the `dpi` property
        matches any device's DPI.

    2.  For the `dpi` or `aspectRatio` property, the property must exactly match
        the corresponding setting of the mobile device.

    3.  For the `minResolution` property, the property matches a setting on the
        device when the larger of the `Stage.stageWidth` and `Stage.stageHeight`
        properties is equal to or greater than `minResolution`.

2.  If there's more than one SplashScreenImageSource definition that matches the
    device then:

    1.  Choose the one with largest number of explicit settings. For example, a
        SplashScreenImageSource definition that specifies both the `dpi` and
        `aspectRatio` properties is a better match than one that only species
        the `dpi` property.

    2.  If there is still more than one match, choose the one with highest
        `minResolution` value.

    3.  If there is still more than one match, choose the first one defined in
        the component.

### Explicitly select the splash screen image

The `SplashScreenImage.getImageClass()` method determines the
SplashScreenImageSource definition that best matches the capabilities of a
mobile device. You can override this method to add your own custom logic, as the
following example shows.

In this example, you add a SplashScreenImageSource definition for an iOS splash
screen. In the body of the override of the `getImageClass()` method, you first
determine of the application is running on iOS. If so, you display the image
specific for iOS.

If the application is not running on iOS, then call the `super.getImageClass()`
method. This method uses the default implementation to determine the
SplashScreenImageSource instance to display:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\myComponents\MyIOSSplashScreen.mxml -->
    <s:SplashScreenImage xmlns:fx="http://ns.adobe.com/mxml/2009"
    	xmlns:s="library://ns.adobe.com/flex/spark">

    	<fx:Script>
    		<![CDATA[
    			// Override getImageClass() to return an image for iOS.
    			override public function getImageClass(aspectRatio:String, dpi:Number, resolution:Number):Class {
    				// Is the application running on iOS?
    				if (Capabilities.version.indexOf("IOS") == 0)
    					return iosImage.source;

    				return super.getImageClass(aspectRatio, dpi, resolution);
    			}
    		]]>
    	</fx:Script>

    	<!-- Default splashscreen image. -->
    	<s:SplashScreenImageSource
    		source="@Embed('../assets/logoDefault.jpg')"/>

    	<s:SplashScreenImageSource
    		source="@Embed('../assets/logo240Portrait.jpg')"
    		dpi="240"
    		aspectRatio="portrait"/>

    	<s:SplashScreenImageSource
    		source="@Embed('../assets/logo240Landscape.jpg')"
    		dpi="240"
    		aspectRatio="landscape"/>

    	<s:SplashScreenImageSource
    		source="@Embed('../assets/logo160.jpg')"
    		dpi="160"
    		aspectRatio="portrait"
    		minResolution="960"/>

    	<!-- iOS splashscreen image. -->
    	<s:SplashScreenImageSource id="iosImage"
    		source="@Embed('../assets/logoIOS.jpg')"/>
    </s:SplashScreenImage>

More Help topics

![](../img/flexLinkIndicator.png) 
[Showing the download progress of an application](https://web.archive.org/web/20150509012659mp_/http://help.adobe.com/en_US/flex/using/WS2db454920e96a9e51e63e3d11c0bf69084-7e3c.html)
