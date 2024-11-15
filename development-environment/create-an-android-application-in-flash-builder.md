# Create an Android application in Flash Builder

Here is a general workflow for creating a Flex mobile application for the Google
Android platform. This workflow assumes that you have already designed your
mobile application. See
[Design a mobile application](../getting-started/getting-started-with-mobile-applications.md#design-a-mobile-application)
for more information.

![](../img/byline.png) Adobe evangelist Mike Jones shares some lessons learned
while developing a multi-platform game Mode by offering
[10 tips when developing for multiple devices](https://web.archive.org/web/20150426004800mp_/http://blog.flashgen.com/2011/07/16/my-10-tips-when-developing-for-multiple-devices/).

## AIR requirements

Flex mobile projects and ActionScript mobile projects require AIR 2.6 or a
higher version. You can run mobile projects on physical devices that support AIR
2.6 or a higher version of AIR.

You can install AIR 2.6 or a higher version only on supported Android devices
that run Android 2.2 or a higher version. For the complete list of supported
Android devices, see
[Certified Devices](https://web.archive.org/web/20150426004800mp_/http://www.adobe.com/flashplatform/certified_devices/).
Also, review the minimum system requirements to run Adobe AIR on Android devices
at
[Mobile System Requirements](https://web.archive.org/web/20150426004800mp_/http://www.adobe.com/products/air/systemreqs/#mobile).

> **Note:** If you do not have a device that supports AIR 2.6 or a higher
> version of AIR, you can use Flash Builder to launch and debug mobile
> applications on the desktop.

Each version of the Flex SDK includes the required Adobe AIR version. If you
have installed mobile applications on a device from an earlier version of the
Flex SDK, uninstall AIR from the device. Flash Builder installs the correct
version of AIR when you run or debug a mobile application on a device.

## Create an application

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td colspan="3"><h2 id="adobe-recommends">Adobe recommends</h2></td>
</tr>
<tr class="even">
<td width="60%">
</div>
</div></td>
<td colspan="2"><table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td width="15%"><span><img
src="../img/BArnold.png" /></span></td>
<td width="85%"><h3 id="create-a-simple-android-application"><a
href="https://www.youtube.com/watch?v=oJKQh7grRYc">Create
a simple Android application</a></h3>
<span>Brent Arnold</span><br />
<span>Create a simple mobile application for the Android platform using
mobile- optimized MXML components.</span></td>
</tr>
<tr class="even">
<td colspan="2"><h3 id="have-a-tutorial-you-would-like-to-share"><img
src="../img/TinyBlueTutIcon.png" /><a
href="https://web.archive.org/web/20150426004800mp_/http://www.adobe.com/community/publishing/download.html">Have
a tutorial you would like to share?</a></h3></td>
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table></td>
</tr>
</tbody>
</table>

1.  In Flash Builder, select File \> New \> Flex Mobile Project.

    A Flex Mobile Project is a special type of AIR project. Follow the prompts
    in the new project wizard as you would for any other AIR project in Flash
    Builder. For more information, see
    [Flex mobile projects](https://web.archive.org/web/20150426004800mp_/http://help.adobe.com/en_US/flashbuilder/using/WSc5cd04c102ae3e972ff2927b12e1411968f-7ff8.html).

    To set Android-specific mobile preferences, see
    [Set mobile project preferences](./set-mobile-project-preferences.md).

    When you create a Flex Mobile Project, Flash Builder generates the following
    files for the project:

    - _`ProjectName`_`.mxml`

      The default application file for the project.

      By default, Flash Builder names this file with the same name as the
      project. If the project name contains illegal ActionScript characters,
      Flash Builder names this file Main.mxml. This MXML file contains the base
      Spark application tag for the project. The base Spark application tag can
      be ViewNavigatorApplication or TabbedViewNavigatorApplication.

      Typically, you do not add content to the default application file
      directly, other than ActionBar content that is displayed in all views. To
      add content to the ActionBar, set the `navigatorContent`, `titleContent`,
      or `actionContent` properties.

    - _`ProjectName`_`HomeView.mxml`

      The file representing the initial view for the project. Flash Builder
      places the file in a views package. The `firstView` attribute of the
      ViewNavigatorApplication tag in _`ProjectName`_`.mxml` specifies this file
      as the default opening view of the application.

    For more information on defining views, see
    [Define views in a mobile application](../user-interface-and-layout/define-views-in-a-mobile-application.md).

    You can also create an ActionScript-only mobile project. See
    [Create an ActionScript mobile project](./create-an-actionscript-mobile-project.md).

2.  (Optional) Add content to the ActionBar of the main application file.

    The ActionBar displays content and functionality that apply to the
    application or to the current view of the application. Here, add content
    that you want to display in all views of the application. See
    [Define navigation, title, and action controls in a mobile application](../user-interface-and-layout/define-navigation-title-and-action-controls-in-a-mobile-application.md).

3.  Lay out the content of the initial view of your application.

    Use Flash Builder in Design mode or Source mode to add components to a view.

    Only use components that Flex supports for mobile development. In both
    Design mode and Source mode, Flash Builder guides you to use supported
    components. See
    [User interface and layout](../user-interface-and-layout/index.md).

    Within the view, add content to the ActionBar that is visible only in that
    view.

4.  (Optional) Add any other views that you want to include in your application.

    In the Flash Builder Package Explorer, from the context menu for the views
    package in your project, select New MXML Component. The New MXML Component
    wizard guides you as you create the view.

    For more information on views, see
    [Define views in a mobile application](../user-interface-and-layout/define-views-in-a-mobile-application.md).

5.  (Optional) Add mobile-optimized item renderers for List components.

    Adobe provides IconItemRenderer, an ActionScript-based item renderer for use
    with mobile applications. See
    [Using a mobile item renderer with a Spark list-based control](https://web.archive.org/web/20150426004800mp_/http://help.adobe.com/en_US/flex/using/WS77c1dbb1bd80d3836663fb6012af31eb8a5-8000.html).

6.  Configure launch configurations to run and debug the application.

    You can run or debug the application on the desktop or on a device.

    A launch configuration is required to run or debug an application from Flash
    Builder. The first time you run or debug a mobile application, Flash Builder
    prompts you to configure a launch configuration.

    When running or debugging a mobile application on a device, Flash Builder
    installs the application on the device.

    See [Test and debug](../test-and-debug/index.md).

7.  Export the application as an installer package.

    Use Export Release Build to create packages that can be installed on mobile
    devices. Flash Builder creates packages for platform you select for export.
    See
    [Export Android APK packages for release](../package-and-export/export-android-apk-packages-for-release.md).

![](../img/byline.png) Adobe Certified Expert in Flex, Brent Arnold, created the
following video tutorials that can help you:

- [Create a Flex mobile application with multiple views](https://www.youtube.com/watch?v=1Y7KknM4ZTg)

- [Create a Flex mobile application using a Spark-based List control](hhttps://www.youtube.com/watch?v=_VFe5ASJsRk)
