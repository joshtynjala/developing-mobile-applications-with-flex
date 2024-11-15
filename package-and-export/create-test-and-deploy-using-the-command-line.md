# Create, test, and deploy using the command line

You can create a mobile application without Flash Builder. You use the mxmlc,
adl, and adt command line tools instead.

Here is the general process for developing and installing a mobile application
on a device using command line tools. Each of these steps is described in more
detail later:

1.  Compile the application with the mxmlc tool. mxmlc +configname=airmobile
    MyMobileApp.mxml

    This step requires that you pass the `configname` parameter set to
    "airmobile".

2.  Test the application in AIR Debug Launcher (ADL) with the adl tool. adl
    MyMobileApp-app.xml -profile mobileDevice

    This step requires that you create an application descriptor file and pass
    it as an argument to the adl tool. You also specify the `mobileDevice`
    profile.

3.  Package the application using the adt tool.

        adt -package -target apk SIGN_OPTIONS MyMobileApp.apk MyMobileApp-app.xml MyMobileApp.swf

    This step requires that you first create a certificate.

4.  Install the application on your mobile device. To install your application
    on an Android device, you use the adb tool. adb install -r MyMobileApp.apk

    This step requires that you first connect your mobile device to your
    computer via USB.

5.  Deploy the mobile application to online stores.

## Compile a mobile application with mxmlc

You can compile mobile applications with the mxmlc command-line compiler. To use
mxmlc, pass the `configname` parameter the value `airmobile`; for example:

    mxmlc +configname=airmobile MyMobileApp.mxml

By passing `+configname=airmobile`, you instruct the compiler to use the
airmobile-config.xml file. This file is in the sdk/frameworks directory. This
file performs the following tasks:

- Applies the mobile.swc theme.

- Makes the following library path changes:

  - Removes libs/air from the library path. Mobile applications do not support
    the Window and WindowedApplication classes.

  - Removes libs/mx from the library path. Mobile applications do not support MX
    components (other than charts).

  - Adds libs/mobile to the library path.

- Removes the ns.adobe.com/flex/mx and www.adobe.com/2006/mxml namespaces.
  Mobile applications do not support MX components (other than charts).

- Disables accessibility.

- Removes RSL entries; mobile applications do not support RSLs.

The mxmlc compiler generates a SWF file.

## Test a mobile application with adl

You can use AIR Debug Launcher (ADL) to test a mobile application. You use ADL
to run and test an application without having to first package and install it on
a device.

**Debug with the adl tool**

ADL prints trace statements and runtime errors to the standard output, but does
not support breakpoints or other debugging features. You can use an integrated
development environment such as Flash Builder for complex debugging issues.

**Launch the adl tool**

To launch the adl tool from the command line, pass your mobile application's
application descriptor file and set the `profile` parameter to `mobileDevice`,
as the following example shows:

    adl MyMobileApp-app.xml -profile mobileDevice

The `mobileDevice` profile defines a set of capabilities for applications that
are installed on mobile devices. For specific information about the
`mobileDevice` profile, see
[Capabilities of different profiles](https://web.archive.org/web/20150219043714mp_/http://help.adobe.com/en_US/air/build/WS144092a96ffef7cc16ddeea2126bb46b82f-7ffe.html).

**Create an application descriptor**

If you did not use Flash Builder to compile your application, you create the
application descriptor file manually. You can use the
/sdk/samples/descriptor-sample.xml file as a base. In general, at a minimum,
make the following changes:

- Point the `<initialWindow><content>` element to the name of your mobile
  application's SWF file:

      <initialWindow>
          <content>MyMobileApp.swf</content>   
          ...
      </initialWindow>

- Change the title of the application, because that is how it appears under the
  application's icon on your mobile device. To change the title, edit the
  `<name><text>` element:

      <name>
          <text xml:lang="en">MyMobileApp by NickDanger</text>
      </name>

- Add an `<android>` block to set Android-specific permissions for the
  application. Depending on what services your device uses, you can often use
  the following permission:

      <application>
          ...
          <android>
              <manifestAdditions>
                  <![CDATA[
                      <manifest>
      			                <uses-permission android:name="android.permission.INTERNET"/>
                      </manifest>
                  ]]>
              </manifestAdditions>
          </android>
      </application>

You can also use the descriptor file to set the height and width of the
application, the location of icon files, versioning information, and other
details about the installation location.

For more information about creating and editing application descriptor files,
see
[AIR application descriptor files](https://web.archive.org/web/20150219043714mp_/http://help.adobe.com/en_US/air/build/WS5b3ccc516d4fbf351e63e3d118666ade46-7ff1.html).

## Package a mobile application with adt

You use AIR Developer Tool (ADT) to package mobile applications on the command
line. The adt tool can create an APK file that you can deploy to a mobile
Android device.

**Create a certificate**

Before you can create an APK file, create a certificate. For development
purposes, you can use a self-signed certificate. You can create a self-signed
certificate with the adt tool, as the following example shows:

    adt -certificate -cn SelfSign -ou QE -o "Example" -c US 2048-RSA newcert.p12 password

The adt tool creates the newcert.p12 file in the current directory. You pass
this certificate to adt when you package your application. Do not use
self-signed certificates for production applications. They only provide limited
assurance to users. For information on signing your AIR installation files with
a certificate issued by a recognized certification authority, see
[Signing AIR applications](https://web.archive.org/web/20150219043714mp_/http://help.adobe.com/en_US/air/build/WSfffb011ac560372f-19aa73f128cc9f05e8-8000.html).

**Create the package file**

To create the APK file for Android, pass the details about the application to
the adt tool, including the certificate, as the following example shows:

    adt -package -target apk -storetype pkcs12 -keystore newcert.p12 -keypass password MyMobileApp.apk MyMobileApp-app.xml MyMobileApp.swf

The output of the adt tool is an _appname_.apk file.

**Package for iOS**

To package mobile applications for iOS, you must get a developer certificate
from Apple, as well as a provisioning file. This requires that you join Apple's
developer program. For more information, see
[Prepare to build, debug, or deploy an iOS application](../development-environment/apple-ios-development-process-using-flash-builder.md#prepare-to-build-debug-or-deploy-an-ios-application).

![](../img/byline.png) Flex evangelist Piotr Walczyszyn explains
[how to package the application with ADT using Ant](https://web.archive.org/web/20150219043714mp_/http://www.riaspace.com/2011/03/packaging-air-application-for-ios-devices-with-adt-command-and-ant-script/)
for iOS devices.

![](../img/byline.png) Blogger Valentin Simonov provides
[additional information](https://web.archive.org/web/20150219043714mp_/http://va.lent.in/blog/2011/03/25/air2-6-app-for-ios/)
about how to publish your application on iOS.

## Install a mobile application on a device with adb

You use Android Debug Bridge (adb) to install the application (APK file) on a
mobile device running Android. The adb tool is part of the Android SDK.

**Connect the device to a computer**

Before you can run adb to install the APK file on your mobile device, connect
the device to your computer. On Windows and Linux systems, connecting a device
requires the USB drivers.

For information on installing USB drivers for your device, see
[Using Hardware Devices](https://web.archive.org/web/20150219043714mp_/http://developer.android.com/guide/developing/device.html).

**Install the application on a connected device**

After you connect the device to your computer, you can install the application
to the device. To install the application with the adb tool, use the `install`
option and pass the name of your APK file, as the following example shows:

    adb install -r MyMobileApp.apk

Use the `-r` option to overwrite the application if you have previously
installed it. Otherwise, you must uninstall the application each time you want
to install a newer version to the mobile device.

## Deploy the application to online stores

You can deploy your application to online app stores like, the Android Market,
Amazon Appstore, or Apple's App store.

![](../img/byline.png) Lee Brimlow
[shows how to deploy a new AIR for Android application to the Android Market](https://web.archive.org/web/20150219043714mp_/http://gotoandlearn.com/play.php?id=131).

![](../img/byline.png) Christian Cantrell
[explains how to deploy the application to the Amazon Appstore for Android](https://web.archive.org/web/20150219043714mp_/http://blogs.adobe.com/cantrell/archives/2011/03/air-2-6-applications-and-the-amazon-appstore-for-android.html).

More Help topics

![](../img/flexLinkIndicator.png) 
[Using mxmlc, the application compiler](https://web.archive.org/web/20150219043714mp_/http://help.adobe.com/en_US/flex/using/WS2db454920e96a9e51e63e3d11c0bf69084-7fcc.html)

![](../img/airLinkIndicator.png) 
[AIR Debug Launcher (ADL)](https://web.archive.org/web/20150219043714mp_/http://help.adobe.com/en_US/air/build/WSfffb011ac560372f-6fa6d7e0128cca93d31-8000.html)

![](../img/airLinkIndicator.png) 
[AIR Developer Tool (ADT)](https://web.archive.org/web/20150219043714mp_/http://help.adobe.com/en_US/air/build/WS5b3ccc516d4fbf351e63e3d118666ade46-7fd9.html)

[Android Debug Bridge](https://web.archive.org/web/20150219043714mp_/http://developer.android.com/guide/developing/tools/adb.html)
