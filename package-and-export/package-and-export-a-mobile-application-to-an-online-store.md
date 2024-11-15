# Package and export a mobile application to an online store

Use Flash Builder's Export Release Build feature to package and export the
release build of a mobile application. A release build is generally the final
version of the application that you want to upload to an online store like, the
Android Market, Amazon Appstore, or Apple's App store.

When exporting an application, you can choose to install the application on a
device. If the device is connected to your computer during export, Flash Builder
installs the application on the device. You can also choose to export a
platform-specific application package for later installation on a device. The
resulting package can be deployed and installed in the same way as a native
application.

For detailed information on exporting an Android application to the Android
Market or Amazon App Store, see
[Export Android APK packages for release](./export-android-apk-packages-for-release.md).

For detailed information on exporting an iOS application to the Apple App store,
see
[Export Apple iOS packages for release](./export-apple-ios-packages-for-release.md).

#### Exporting the application with captive runtime

When you use the Export Release Build feature to export a mobile application,
you can choose to embed the AIR runtime within the application package.

Users can then run the application even on a device that does not already have
AIR installed on it. Depending on the platform to which you are exporting the
package, you can use a captive runtime or a shared runtime.
