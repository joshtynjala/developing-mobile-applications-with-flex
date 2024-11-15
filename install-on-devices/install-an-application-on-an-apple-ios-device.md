# Install an application on an Apple iOS device

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
href="https://web.archive.org/web/20160102030104mp_/http://www.adobe.com/community/publishing/download.html">Have
a tutorial you would like to share?</a></h3></td>
</tr>
<tr class="even">
<td colspan="4" height="10"></td>
</tr>
<tr class="odd">
<td width="5%"><span><img
src="../img/JStallons.png" /></span></td>
<td width="45%"><h3
id="article-and-video-tutorial-package-applications-for-apple-ios-devices"><a
href="https://web.archive.org/web/20150906021013/http://www.adobe.com/devnet/air/articles/packaging-air-apps-ios.html">Article
and video tutorial: Package applications for Apple iOS devices</a></h3>
<span>Jeanette Stallons</span><br />
<span>Using Flash Builder to install applications to Apple iOS
devices</span></td>
<td width="5%"></td>
<td width="45%"></td>
</tr>
</tbody>
</table>

On an iOS device, you install an application (IPA file) manually, because the
Apple iOS platform does not support auto-deployment.

Important: Before you install an application on an iOS device, you need the
Apple iOS development certificate (in P12 format) and a development-version of
the provisioning profile. Ensure that you follow the steps described in
[Prepare to build, debug, or deploy an iOS application](../development-environment/apple-ios-development-process-using-flash-builder.md#prepare-to-build-debug-or-deploy-an-ios-application).

1.  Connect the Apple iOS device to your development computer.

2.  Launch iTunes on your development computer.

    > **Note:** You need iTunes to install your application on your iOS device
    > and to obtain the Unique Device Identifier (UDID) of your iOS device.

3.  In Flash Builder, select Run \> Run Configurations.

4.  In the Run Configurations dialog, follow these steps:

    1.  Select the application that you want to install.

    2.  Select the target platform as Apple iOS.

    3.  Select the launch method as On Device.

    4.  Select one of the following packaging methods:

        Standard  
        Use this method to package a release-quality version of your application
        that can run on Apple iOS devices.

        The Standard method of packaging translates the bytecode of the
        application's SWF file into ARM instructions before packaging. Because
        of this additional translation step before packaging, this method of
        creating an application (IPA) file takes several minutes. The Standard
        method takes longer than the Fast method. However, the application
        performance with the Standard method is release-quality, and it is
        suitable for submission to the Apple App Store.

        Fast  
        Use this method to create an IPA file quickly.

        The Fast method of packaging bypasses the translation of bytecode and
        just bundles the application SWF file and assets with the pre-compiled
        AIR runtime. The Fast method of packaging is quicker than the Standard
        method. However, the application performance with the Fast method is not
        release-quality, and it is not suitable for submission to the Apple App
        Store.

        > **Note:** There are no runtime or functional differences between the
        > Standard and Fast methods of packaging.

    5.  Click Configure to select the appropriate code signing certificate,
        provisioning file, and package contents.

    6.  Click Run. Flash Builder displays a dialog requesting a password. Enter
        your P12 certificate password.

    Flash Builder generates the IPA file and places it in the bin-debug folder.

5.  On your development computer, follow these steps:

    1.  In iTunes, select File \> Add To Library, and browse to the mobile
        provisioning profile file (.mobileprovision filename extension) that you
        obtained from Apple.

        You can also drag-and-drop the mobile provisioning profile file into
        iTunes.

    2.  In iTunes, select File \> Add To Library, and browse to the IPA file
        that you generated in step 4.

        You can also drag-and-drop the IPA file into iTunes.

    3.  Sync your iOS device with iTunes by selecting File \> Sync.

The application is deployed on your iOS device and you can launch it.
