# Export Android APK packages for release

## Adobe recommends

> ### ![](../img/ATrice.png) [Build and export Android applications for various Android ecosystems](https://www.youtube.com/watch?v=H1iUiIcbqEk)
>
> [Andrew Trice](https://web.archive.org/web/20150328072526mp_/http://www.tricedesigns.com/)
>
> Workflow to develop Android applications in Flash Builder and export to
> various Android ecosystems, like Google Android Market and Amazon Appstore

Before you export a mobile application, you can customize the Android
permissions. Customize the settings manually in the application descriptor file.
These settings are in the `<android>` block of the bin-debug/_app_name_-app.xml
file. For more information, see
[Setting AIR application properties](https://web.archive.org/web/20150328072526mp_/http://help.adobe.com/en_US/air/build/WS5b3ccc516d4fbf351e63e3d118666ade46-7ff1.html).

If you export the application for later installation on a device, install the
application package using the tools provided by the device's OS provider.

1.  In Flash Builder, select Project \> Export Release Build.

2.  Select the project and application that you want to export.

3.  Select the target platforms and the location to export the project.

4.  Export and sign a platform-specific application package.

    You can package your application with a digital signature for each target
    platform or as a digitally signed AIR application for the desktop.

    You can also export the application as intermediate AIRI file that can be
    signed later. If you select that option, use the AIR adt command line tool
    later to package the AIRI as an APK file. Then install the APK file on the
    device using platform-specific tools (for example, with the Android SDK, use
    adb). For information on using command line tools to package your
    application, see
    [Create, test, and deploy using the command line](./create-test-and-deploy-using-the-command-line.md).

5.  On the Packaging Settings page, you can select the digital certificate,
    package contents, and any native extensions.

    **Deployment**  
    If you also want to install the application on a device, click the
    Deployment page and select Install And Launch Application On Any Connected
    Devices. Ensure that you have connected one or more devices to your
    computer's USB ports.

    - **Export application with captive runtime**

      Select this option if you want to embed the AIR runtime within the APK
      file while exporting the application package. Users can then run the
      application even on a device that does not have AIR already installed on
      it.

    - **Export application that uses a shared runtime**

      Select this option if you do not want to embed the AIR runtime within the
      APK file while exporting the application package. You can select or
      specify a URL to download Adobe AIR for the application package if AIR is
      not already installed on a user's device.

      The default URL points to the Android Market. You can, however, override
      the default URL and select the URL that points to a location on the Amazon
      Appstore, or enter your own URL.

    **Digital Signature**  
    Click the Digital Signature tab to create or browse to a digital certificate
    that represents the application publisher's identity. You can also specify a
    password for the selected certificate.

    If you create a certificate, the certificate is _self-signed_. You can
    obtain a commercially signed certificate from a certificate provider. See
    [Digitally sign your AIR applications](https://web.archive.org/web/20150328072526mp_/http://help.adobe.com/en_US/flashbuilder/using/WSe4e4b720da9dedb5-13a250c812e8e9b5533-7fed.html).

    **Package Contents**  
    (Optional) Click the Package Contents tab to specify which files to include
    in the package.

    **Native Extensions**  
    (Optional) Select the native extensions that you want to include in the
    application package.

    For more information about native extensions, see
    [Use native extensions](../development-environment/using-native-extensions.md#use-native-extensions).

6.  Click Finish.

    Flash Builder creates _`ApplicationName`_`.apk` in the directory specified
    in the first panel (the default is the top level of your project). If the
    device was connected to your computer during export, Flash Builder installs
    the application on the device.
