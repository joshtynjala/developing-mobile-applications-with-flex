# Test and debug a mobile application on the desktop

For initial testing or debugging, or if you don't have a mobile device, Flash
Builder lets you test and debug applications on the desktop using the AIR Debug
Launcher (ADL).

Before you test or debug a mobile application for the first time, you define a
launch configuration. Specify the target platform and On Desktop as the launch
method. See [Manage launch configurations](./manage-launch-configurations.md).

## Configure device information for desktop preview

The properties of a device configuration determine how the application appears
in the ADL and in Flash Builder Design mode.

[Set device configurations](../development-environment/set-mobile-project-preferences.md#set-device-configurations)
lists the supported configurations. Device configurations do not affect the
application's appearance on the device.

## Screen density

You can preview your application on your development desktop or view the layout
of the application in Flash Builder Design mode. Flash Builder uses a screen
density of 240 DPI. An application's appearance during preview sometimes differs
from its appearance on a device that supports a different pixel density.

## Preview applications with ADL

When you preview applications on the desktop, Flash Builder launches the
application using the ADL. The ADL provides a Device menu with corresponding
shortcuts to emulate buttons on the device.

For example, to emulate the back button on a device, select Device \> Back.
Select Device \> Rotate Left or Device \> Rotate Right to emulate rotating the
device. Rotate options are disabled if you have not selected auto orientation.

Drag in a list to emulate scrolling the list on a device.

![](../img/byline.png) Adobe Certified Expert in Flex, Brent Arnold, created a
video tutorial on
[using ADL to preview a mobile application on the desktop](https://www.youtube.com/watch?v=0kpgtgyLRKU).
