# Install an application on a Google Android device

During the development, testing, and deployment phases of your project, you can
install your application directly on a device.

You can use Flash Builder to install an application directly on an Android
device. When you install a package on a device on which Adobe AIR is not
installed, Flash Builder installs AIR automatically.

## Adobe recommends

> ### ![](../img/JStallons.png) [Article and video tutorial: Package applications for Google Android devices](https://web.archive.org/web/20150811060341/http://www.adobe.com/devnet/air/articles/packaging-air-apps-android.html)
>
> [Jeanette Stallons](https://web.archive.org/web/20130528230130/http://www.stallons.com/consulting/index.html)
>
> Using Flash Builder to install applications on Google Android devices

1.  Connect the Google Android device to your development computer.

    Flash Builder accesses the device connected to your computer's USB port.
    Ensure that you have configured the necessary USB device drivers. See
    [Connect Google Android devices](../development-environment/connect-google-android-devices.md)

2.  In Flash Builder, select Run \> Run Configurations. In the Run
    Configurations dialog box, select the mobile application that you want to
    deploy.

3.  Select the launch configuration method as On Device.

4.  (Optional) Specify whether to clear application data on each launch.

5.  Click Apply.

Flash Builder installs and launches the application on your Android device. If
you installed the package on a device on which Adobe AIR is not installed, Flash
Builder installs AIR automatically.

![](../img/byline.png) Adobe Certified Expert in Flex, Brent Arnold, created a
video tutorial on
[setting up and running your application on an Android device](https://www.youtube.com/watch?v=xhvAine7Neo).
