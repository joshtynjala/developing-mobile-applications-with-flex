# Set mobile project preferences

## Set device configurations

Flash Builder uses device configurations to display device screen size previews
in Design View or to launch applications on the desktop using the AIR Debug
Launcher (ADL). See
[Configure device information for desktop preview](../test-and-debug/test-and-debug-a-mobile-application-on-the-desktop.md#configure-device-information-for-desktop-preview).

To set device configurations, open Preferences and select Flash Builder \>
Device Configurations.

Flash Builder provides several default device configurations. You can add, edit,
or remove additional device configurations. You cannot modify the default
configurations that Flash Builder provides.

Clicking the Restore Defaults button restores default device configurations but
does not remove any configurations that you have added. Also, if you added a
device configuration with a name that matches one of the defaults, Flash Builder
overrides the added configuration with the default settings.

Device configurations contain the following properties:

| Property           | Description                                                                                                                                                                                 |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Device Name        | A unique name for the device.                                                                                                                                                               |
| Platform           | Device platform. Select a platform from the list of supported platforms.                                                                                                                    |
| Full Screen Size   | Width and height of the device's screen.                                                                                                                                                    |
| Usable Screen Size | The standard size of an application on the device. This size is the expected size of an application launched in non-full screen mode, accounting for system chrome, such as the status bar. |
| Pixels per Inch    | Pixels per inch on the device's screen.                                                                                                                                                     |

## Choose target platforms

Flash Builder supports target platforms based on the application type.

To select a platform, open Preferences and select Flash Builder \> Target
Platforms.

For all third-party plug-ins, see the associated documentation.

## Choose an application template

When you create a mobile application, you can select from the following
application templates:

Blank  
Uses the Spark Application tag as the base application element.

Use this option if you want to create a custom application without using the
standard view navigation.

View-Based Application  
Uses the Spark ViewNavigatorApplication tag as the base application element to
create an application with a single view.

You can specify the name of the initial view.

Tabbed Application  
Uses the Spark TabbedViewNavigatorApplication tag as the base application
element to create a tab-based application.

To add a tab, enter a name for the tab, and click Add. You can change the order
of the tabs by clicking Up and Down. To remove a tab from the application,
select a tab and click Remove.

The name of the view is the tab name with "View" appended. For example, if you
name a tab as FirstTab, Flash Builder generates a view named FirstTabView.

For each tab that you create, a new MXML file is generated in the "views"
package.

> **Note:** The package name is not configurable through the Flex Mobile Project
> wizard.

The MXML files are generated according to the following rules:

- If the tab name is a valid ActionScript class name, Flash Builder generates
  the MXML file using the tab name with "View" appended.

- If the tab name is not a valid class name, Flash Builder modifies the tab name
  by removing invalid characters and inserting valid starting characters. If the
  modified name is unacceptable, Flash Builder changes the MXML filename to
  "ViewN", where N is the position of the view, starting with N=1.

![](../img/byline.png) Adobe Certified Expert in Flex, Brent Arnold, created a
video tutorial about
[using the Tabbed Application template](https://www.youtube.com/watch?v=TpJIrkgvqzI).

## Choose mobile application permissions

When you create a mobile application, you can specify or change the default
permissions for a target platform. The permissions are specified at the time of
compiling, and they cannot be changed at runtime.

First select the target platform, and then set the permissions for each
platform, as required. You can edit the permissions later in the application
descriptor XML file.

Third-party plug-ins provide additional platform support for both Flex and
ActionScript projects. For platform-specific permissions, see the device's
associated documentation.

#### Permissions for the Google Android platform

For the Google Android platform, you can set the following permissions:

INTERNET  
Allows network requests and remote debugging

The INTERNET permission is selected by default. If you deselect this permission,
you cannot debug your application on a device.

WRITE_EXTERNAL_STORAGE  
Allows writing to an external device

Select this permission to let the application write to an external memory card
on the device.

READ_PHONE_STATE  
Mutes the audio during an incoming call

Select this permission to let the application mute the audio during phone calls.
For example, you can select this permission if your application plays audio in
the background.

ACCESS_FINE_LOCATION  
Allows access to a GPS location

Select this permission to let the application access GPS data using the
Geolocation class.

DISABLE_KEYGUARD and WAKE_LOCK  
Disallows sleep mode on the device

Select this permission to prevent the device from going to sleep using the
SystemIdleMode class settings.

CAMERA  
Allows access to a camera

Select this permission to let the application access a camera.

RECORD_AUDIO  
Allows access to a microphone

Select this permission to let the application access a microphone.

ACCESS_NETWORK_STATE and ACCESS_WIFI_STATE  
Allows access to information about network interfaces associated with the device

Select this permission to let the application access network information using
the NetworkInfo class.

For more information about setting mobile application properties, see the
[Adobe AIR documentation](https://web.archive.org/web/20141103135807/http://help.adobe.com/en_US/air/build/WSfffb011ac560372f-5d0f4f25128cc9cd0cb-7ffe.html#WS901d38e593cd1bac1e63e3d12991865ede-8000).

#### Permissions for the Apple iOS platform

The Apple iOS platform uses runtime validation for permissions instead of
predefined permissions. That is, if an application wants to access a specific
feature of the Apple iOS platform that requires user permission, a pop-up
appears requesting permission.

## Choose platform settings

Platform settings let you select a target device family. Depending on the
platform that you select, you can select the target device or a target device
family. You can select a specific device or all the devices that the platform
supports.

Third-party plug-ins provide additional platform support for both Flex and
ActionScript projects. For platform-specific settings, see the device's
associated documentation.

#### Platform settings for the Google Android platform

There are no platform-specific settings for the Google Android platform.

#### Platform settings for the Apple iOS platform

For a Flex mobile project or an ActionScript mobile project, you can specify the
following target devices for the Apple iOS platform:

iPhone/iPod Touch  
Applications using this target family are listed as compatible with only iPhone
and iPod Touch devices in the Apple App store.

iPad  
Applications using this target family are listed as compatible only with iPad
devices in the Apple App store.

All  
Applications using this target family are listed as compatible with both iPhone
or iPod Touch, and iPad devices in the Apple App store. This option is the
default.

## Choose application settings

Automatically Reorient  
Rotates the application when the user rotates the device. When this setting is
not enabled, your application always appears in a fixed orientation.

Full Screen  
Displays your application in fullscreen mode on the device. When this setting is
enabled, the device's status bar does not appear above your application. Your
application fills the entire screen.

If you want to target your application across multiple device types with varying
screen densities, select Automatically Scale Application For Different Screen
Densities. Selecting this option automatically scales the application and
handles density changes, as required, for the device. See
[Set application scaling](#set-application-scaling).

## Set application scaling

You use mobile application scaling to build a single mobile application that is
compatible with devices with different screen sizes and densities.

Mobile device screens have varying screen densities, or DPI (dots per inch). You
can specify the DPI value as 160, 240, or 320, depending on the screen density
of the target device. When you enable automatic scaling, Flex optimizes the way
it displays the application for the screen density of each device.

For example, suppose that you specify the target DPI value as 160 and enable
automatic scaling. When you run the application on a device with a DPI value of
320, Flex automatically scales the application by a factor of 2. That is, Flex
magnifies everything by 200%.

To specify the target DPI value, set it as the `applicationDPI` property of the
`<s:ViewNavigatorApplication>` tag or `<s:TabbedViewNavigatorApplication>` tag
in the main application file:

    <s:ViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
    	xmlns:s="library://ns.adobe.com/flex/spark"
    	firstView="views.HomeView"
    	applicationDPI="160">

If you choose to not auto-scale your application, you must handle the density
changes for your layout manually, as required. However, Flex adapts the skins to
the density of each device.

For more information about creating density-independent mobile applications, see
[Support multiple screen sizes and DPI values in a mobile application](../application-design-and-workflow/support-multiple-screen-sizes-and-dpi-values-in-a-mobile-application.md).
