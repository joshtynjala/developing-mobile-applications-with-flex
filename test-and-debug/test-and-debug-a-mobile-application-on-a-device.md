# Test and debug a mobile application on a device

You can use Flash Builder to test or debug a mobile application from your
development desktop or from a device.

You test and debug applications based on a launch configuration that you define.
Flash Builder shares the launch configuration between running and debugging the
application. When you use Flash Builder to debug an application on a device,
Flash Builder installs a debug version of the application on the device.

> **Note:** If you export a release build to a device, you install a non-debug
> version of the application. The non-debug version is not suitable for
> debugging.

For more information, see
[Manage launch configurations](https://web.archive.org/web/20150313221324mp_/http://help.adobe.com/en_US/flashbuilder/using/WSe4e4b720da9dedb5-15a3a08712e93a1ff8e-7fff.html).

## Debug an application on a Google Android device

On an Android device, debugging requires Android 2.2 or later.

You can debug in either of the following scenarios:

Debug over USB  
To debug an application over a USB connection, you connect the device to the
host machine via a USB port. When you debug over USB, Flash Builder always
packages the application, then installs and launches it on the device before the
debugging starts. Ensure that your device is connected to the host machine's USB
port during the entire debugging session.

Debug over a network  
When you debug an application over the network, the device and the host machine
must be on the same network. The device and the host machine can be connected to
the network via Wi-Fi, ethernet, or Bluetooth.

When you debug over a network, Flash Builder lets you debug an application that
is already installed on a connected device without reinstalling the application.
Connect the device to the host machine via a USB port only during packaging and
while installing the application on the device. You can unplug the device from
the USB port during debugging. However, ensure that there is a network
connection between the device and the host machine during the entire debugging
session.

### Prepare to debug the application

Before you begin debugging over USB or over a network, follow these steps:

1.  (Windows) Ensure that the proper USB driver is installed.

    On Windows, install the Android USB driver. See the documentation
    accompanying the Android SDK build for more information. For more
    information, see
    [Install USB device drivers for Android devices (Windows)](../development-environment/connect-google-android-devices.md#install-usb-device-drivers-for-android-devices-windows).

2.  Ensure that USB debugging is enabled on your device.

    In device Settings, go to Applications \> Development, and enable USB
    debugging.

### Check for connected devices

When you run or debug a mobile application on a device, Flash Builder checks for
connected devices. If Flash Builder finds a single connected device online,
Flash Builder deploys and launches the application. Otherwise, Flash Builder
launches the Choose Device dialog for these scenarios:

- No connected device found

- Single connected device found that is offline or its OS version is not
  supported

- Multiple connected devices found

If multiple devices are found, the Choose Device dialog lists the devices and
their state (online or offline). Select the device to launch.

The Choose Device dialog lists the OS version and the AIR version. If Adobe AIR
is not installed on the device, Flash Builder installs it automatically.

### Configure network debugging

Follow these steps only if you debug an application over a network.

#### Prepare to debug over the network

Before you debug an application over the network, follow these steps:

1.  On Windows, open port 7935 (Flash Player debugger port) and port 7
    (echo/ping port).

    For detailed instructions, see this
    [Microsoft TechNet article](https://web.archive.org/web/20150313221324mp_/http://technet.microsoft.com/en-us/library/cc875811.aspx#XSLTsection124121120120).

    On Windows Vista, deselect the Wireless Network Connection in Windows
    Firewall \> Change Settings \> Advanced.

2.  On your device, configure wireless settings in Settings \> Wireless and
    Network.

#### Select a primary network interface

Your host machine can be connected to multiple network interfaces
simultaneously. However, you can select a primary network interface to use for
debugging. You select this interface by adding a host address in the Android APK
package file.

1.  In Flash Builder, open Preferences.

2.  Select Flash Builder \> Target Platforms.

    The dialog lists all the network interfaces available on the host machine.

3.  Select the network interface that you want to embed in the Android APK
    package.

Ensure that the selected network interface is accessible from the device. If the
device cannot access the selected network interface while it establishes a
connection, Flash Builder displays a dialog requesting the IP address of the
host machine.

### Debug the application

1.  Connect the device over a USB port or over a network connection.

2.  Select Run \> Debug Configurations to configure a launch configuration for
    debugging.

    - For the Launch Method, select On Device.

    - Select Debug via USB or Debug via Network.

      The first time that you debug the application over a network, you can
      install the application on the device over USB. To do so, select Install
      The Application On The Device Over USB, and connect the device to the host
      machine via a USB port.

      Once the application is installed, if you don't want to connect over USB
      for subsequent debugging sessions, deselect Install The Application On The
      Device Over USB.

    - (Optional) Clear application data on each launch.

      Select this option if you want to keep the state of the application for
      each debugging session. This option applies only if sessionCachingEnabled
      is set to True in your application.

3.  Select Debug to begin a debugging session.

    The debugger launches and waits for the application to start. The debugging
    session starts when the debugger establishes a connection with the device.

    When you try to debug on a device over a network, the application sometimes
    displays a dialog requesting an IP address. This dialog indicates that the
    debugger could not connect. Ensure that the device is properly connected to
    the network, and that the computer running Flash Builder is accessible from
    that network.

    > **Note:** On a corporate, hotel, or other guest network, sometimes the
    > device cannot connect to the computer, even if the two are on the same
    > network.

    If you are debugging via network, and the application was previously
    installed on the device, start debugging by typing the IP address of the
    host machine.

![](../img/byline.png) Adobe Certified Expert in Flex, Brent Arnold, created a
video tutorial about
[debugging an application over USB for an Android device](https://www.youtube.com/watch?v=TvpvIIhvZ5s).

## Debug an application on an Apple iOS device

To debug an application on an Apple iOS device, deploy and install your debug
iOS package (IPA file) on the iOS device manually. Auto-deployment is not
supported for the Apple iOS platform.

Important: Before you debug an application on an iOS device, ensure that you
follow the steps described in
[Prepare to build, debug, or deploy an iOS application](../development-environment/apple-ios-development-process-using-flash-builder.md#prepare-to-build-debug-or-deploy-an-ios-application).

1.  Connect the Apple iOS device to your development computer.

2.  Launch iTunes on your iOS device.

    > **Note:** You need iTunes to install your application on your iOS device
    > and to obtain the device ID of your iOS device.

3.  In Flash Builder, select Run \> Debug Configurations.

4.  In the Debug Configurations dialog, follow these steps:

    1.  Select the application that you want to debug.

    2.  Select the target platform as Apple iOS.

    3.  Select the launch method as On Device.

    4.  Select one of the following packaging methods:

        **Standard**  
        Use this method to package a release-quality version of your application
        that can run on Apple iOS devices. The application performance with this
        method is similar to the performance of the final release package and
        can be submitted to the Apple App Store.

        However, this method of creating a debug iOS (IPA) file takes several
        minutes.

        **Fast**  
        Use this method to create an IPA file quickly, and then run and debug
        the file on the device. This method is suitable for application testing
        purposes. The application performance with this method is not release
        quality, and it is not suitable for submission to the Apple App Store.

    5.  Click Configure to select the appropriate code signing certificate,
        provisioning file, and package contents.

    6.  Click Configure Network Debugging to select the network interface that
        you want to add in the debug iOS package.

        > **Note:** Your host machine can be connected to multiple network
        > interfaces simultaneously. However, you can select a primary network
        > interface to use for debugging.

    7.  Click Debug. Flash Builder displays a dialog requesting for a password.
        Enter your P12 certificate password.

    Flash Builder generates the debug IPA file and places it in the bin-debug
    folder.

5.  On your iOS device, follow these steps:

    1.  (Optional) In iTunes, select File \> Add To Library, and browse to the
        mobile provisioning profile file (.mobileprovision filename extension)
        that you obtained from Apple.

    2.  In iTunes, select File \> Add To Library, and browse to the debug IPA
        file that you generated in step 4.

    3.  Sync your iOS device with iTunes by selecting File \> Sync.

6.  Flash Builder attempts connection to the host address specified in the debug
    IPA file. If the application cannot connect to the host address, Flash
    Builder displays a dialog requesting the IP address of the host machine.

    > **Note:** If you have not changed your code or assets since the last debug
    > IPA package was generated, Flash Builder skips the packaging and debugs
    > the application. That is, you can launch the installed application on your
    > device and click Debug to connect to the Flash Builder debugger. This way,
    > you can debug repeatedly without packaging the application every time.

More Help topics

[Debug and Package Apps for Devices (video)](https://web.archive.org/web/20150313221324mp_/http://tv.adobe.com/watch/adc-presents/flex-mobile-part-3-debug-and-package-apps-for-devices/)
