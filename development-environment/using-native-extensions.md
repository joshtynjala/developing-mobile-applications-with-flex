# Use native extensions

Native extensions let you include native platform capabilities into your mobile
application.

A native extension contains ActionScript classes and native code. Native code
implementation lets you access device-specific features, which cannot be
accessed using pure ActionScript classes. For example, accessing the device's
vibration functionality.

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
href="https://web.archive.org/web/20150301200240mp_/http://www.adobe.com/community/publishing/download.html">Have
a tutorial you would like to share?</a></h3></td>
</tr>
<tr class="even">
<td colspan="4" height="10"></td>
</tr>
<tr class="odd">
<td width="5%"><span><img
src="../img/OGoldman.png" /></span></td>
<td width="45%"><h3 id="article-extending-adobe-air"><a
href="https://web.archive.org/web/20150323134348/http://www.adobe.com/devnet/air/articles/extending-air.html#articlecontentAdobe_numberedheader_4">Article:
Extending Adobe AIR</a></h3>
<span><a
href="https://web.archive.org/web/20150301200240mp_/http://blogs.adobe.com/simplicity/">Oliver
Goldman</a></span><br />
<span>Learn more about creating, using, and packaging native
extensions</span></td>
<td width="5%"></td>
<td width="45%"></td>
</tr>
</tbody>
</table>

Native code implementation can be defined as the code that executes outside the
AIR runtime. You define platform-specific ActionScript classes and native code
implementation in the extension. The ActionScript extension classes access and
exchange data with the native code using the ActionScript class
ExtensionContext.

Extensions are specific to a device's hardware platform. You can create
platform-specific extensions or you can create a single extension that targets
multiple platforms. For example, you can create a native extension that targets
both Android and iOS platforms. Native extensions are supported by the following
mobile devices:

- Android devices running Android 2.2 or a later version

- iOS devices running iOS 4.0 or a later version

For detailed information on creating cross-platform native extensions, see
[Developing Native Extensions for Adobe AIR](https://web.archive.org/web/20150301200240mp_/http://help.adobe.com/en_US/air/extensions/index.html).

For a collection of native extension samples, contributed by Adobe and the
community, see
[Native extensions for Adobe AIR](https://web.archive.org/web/20150301200240mp_/http://www.adobe.com/devnet/air/native-extensions-for-air.html).

## Package native extensions

To provide your native extension to application developers, you package all the
necessary files into an ActionScript Native Extension (ANE) file by following
these steps:

1.  Build the extension's ActionScript library into a SWC file.

2.  Build the extension's native libraries. If the extension has to support
    multiple platforms, build one library for each target platform.

3.  Create a signed certificate for your extension. If the extension is not
    signed, Flash Builder displays a warning when you add the extension to your
    project.

4.  Create an extension descriptor file.

5.  Include any external resources for the extension, such as images.

6.  Create the extension package using the Air Developer Tool. For more
    information, see the
    [AIR documentation](https://web.archive.org/web/20150301200240mp_/http://help.adobe.com/en_US/air/build/WS5b3ccc516d4fbf351e63e3d118666ade46-7fd9.html).

For detailed information on packaging ActionScript extensions, see
[Developing Native Extensions for Adobe AIR](https://web.archive.org/web/20150301200240mp_/http://help.adobe.com/en_US/air/extensions/index.html).

## Add native extensions to a project

You include an ActionScript Native Extension (ANE) file in the project's build
path the same way as you would include a SWC file.

1.  In Flash Builder, when you create a Flex mobile project, select the Native
    Extensions tab in the Build Paths settings page.

    You can also add extensions from the Project Properties dialog box by
    selecting Flex Build Path.

2.  Browse to the ANE file or the folder containing the ANE files to add to the
    project. When you add an ANE file, the extension ID is added to the
    project's application descriptor file (_project name_-app.xml) by default.

Flash Builder displays an error symbol for the added extension in the following
scenarios:

- The AIR runtime version of the extension is later than the application's
  runtime version.

- The extension does not include all the selected platforms that the application
  is targeting.

> **Note:** You can create an ActionScript native extension that targets
> multiple platforms. To test an application that includes this ANE file on your
> development computer using the AIR Simulator, ensure that the ANE file
> supports the computer's platform. For example, to test the application using
> the AIR Simulator on Windows, ensure that the ANE file supports Windows.

## Include ActionScript native extensions in an application package

When you use the Export Release Build feature to export the mobile application,
the extensions used in the project are included within the application package
by default.

To change the default selection, follow these steps:

1.  In the Export Release Build dialog box, select the Native Extensions tab
    under Package Settings.

2.  The ActionScript native extension files referenced in your project are
    listed, indicating if the ANE file is used in the project or not.

    If the ANE file is used in the project, it is selected by default in the
    application package.

    If the ANE file is included in the project but not used, the compiler does
    not recognize the ANE file. It is then not included in the application
    package. To include the ANE file in the application package, do the
    following:

    1.  In the Project Properties dialog box, select Flex Build Packaging and
        the required platform.

    2.  Select the extensions that you want to include in the application
        package.

## Support for iOS5 native extensions

To package native extensions that use iOS5 SDK features, the AIR Developer Tool
(ADT) requires the location of the iOS5 SDK.

On Mac OS, Flash Builder lets you select the location of the iOS5 SDK using the
Package Settings dialog. After you select the location of the iOS SDK, the
selected location is passed through the `-platformsdk`ADT command.

> **Note:** This functionality is currently not supported on Windows.

For more information, see
[Developing Native Extensions for Adobe AIR](https://web.archive.org/web/20150301200240mp_/http://help.adobe.com/en_US/air/extensions/index.html).
