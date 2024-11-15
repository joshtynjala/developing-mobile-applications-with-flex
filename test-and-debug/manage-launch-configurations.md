# Manage launch configurations

Flash Builder uses launch configurations when you run or debug mobile
applications. You can specify whether to launch the application on the desktop
or on a device connected to your computer.

To create a launch configuration, follow these steps:

1.  Select Run \> Run Configurations to open the Run Configurations dialog.

    To open the Debug Configurations dialog, select Run \> Debug Configurations.
    See
    [Test and debug a mobile application on a device](./test-and-debug-a-mobile-application-on-a-device.md).

    You can also access the Run or Debug Configurations in the drop-down list of
    the Run button or the Debug button in the Flash Builder toolbar.

2.  Expand the Mobile Application node. Click the New Launch Configuration
    button in the dialog toolbar.

3.  Specify a target platform in the drop-down list.

4.  Specify a launch method:

    - **On Desktop**

      Runs or debugs the application on your desktop using the AIR Debug
      Launcher (ADL), according to a device configuration that you have
      specified. This launch method is not a true emulation of the application
      running on a device. However, it does let you view the application layout
      and interact with the application. See
      [Preview applications with ADL](./test-and-debug-a-mobile-application-on-the-desktop.md#preview-applications-with-adl).

      Click Configure to edit device configurations. See
      [Configure device information for desktop preview](./test-and-debug-a-mobile-application-on-the-desktop.md#configure-device-information-for-desktop-preview).

    - **On Device**

      Installs and runs the application on the device.

      For the Google Android platform, Flash Builder installs the application on
      your device and launches the application. Flash Builder accesses the
      device connected to your computer's USB port. See
      [Test and debug a mobile application on a device](./test-and-debug-a-mobile-application-on-a-device.md)
      for more information.

      Windows requires a USB driver to connect an Android device to your
      computer. For more information, see
      [Install USB device drivers for Android devices (Windows)](../development-environment/connect-google-android-devices.md#install-usb-device-drivers-for-android-devices-windows).

5.  Specify whether to clear application data on each launch, if applicable.
