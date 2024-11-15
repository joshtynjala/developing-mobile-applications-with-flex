# Export Apple iOS packages for release

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
href="https://web.archive.org/web/20150526031616mp_/http://www.adobe.com/community/publishing/download.html">Have
a tutorial you would like to share?</a></h3></td>
</tr>
<tr class="even">
<td colspan="4" height="10"></td>
</tr>
<tr class="odd">
<td width="5%"><span><img
src="../img/ATrice.png" /></span></td>
<td width="45%"><h3
id="build-and-export-ios-applications-to-apples-app-store"><a
href="https://web.archive.org/web/20150504060449/http://tv.adobe.com/watch/adc-presents/build-ios-applications-using-flex-and-flash-builder-45/">Build
and export iOS applications to Apple's App Store</a></h3>
<span><a
href="https://web.archive.org/web/20150526031616mp_/http://www.tricedesigns.com/">Andrew
Trice</a></span><br />
<span>Workflow to develop iOS applications in Flash Builder and publish
to Apple's App Store</span></td>
<td width="5%"></td>
<td width="45%"></td>
</tr>
</tbody>
</table>

You can create and export an iOS package for ad hoc distribution or for
submission to the Apple App Store.

Important: Before exporting an iOS package, ensure that you obtain the required
certificates and a distribution provisioning profile from Apple. To do so,
follow the steps described in
[Prepare to build, debug, or deploy an iOS application](../development-environment/apple-ios-development-process-using-flash-builder.md#prepare-to-build-debug-or-deploy-an-ios-application).

1.  In Flash Builder, select Project \> Export Release Build.

2.  Select Apple iOS as the target platform to export and sign an IPA package.

    Click Next.

3.  Select the P12 certificate and the distribution provisioning profile that
    you obtained from Apple.

4.  On the Packaging Settings page, you can select the provisioning certificate,
    digital certificate, package contents, and any native extensions.

    **Deployment**  
    When you export an iOS package, the AIR runtime is embedded within the IPA
    file by default.

    **Digital Signature**  
    Select the P12 certificate and the distribution provisioning profile that
    you obtained from Apple.

    You can select one of the following package types:

    - **Ad Hoc Distribution For Limited Distribution** For a limited
      distribution of the application

    - **Final Release Package For Apple App Store** To submit the application to
      the Apple App Store

    **Package Contents**  
    (Optional) Click the Package Contents tab to specify which files to include
    in the package.

    **Native Extensions**  
    (Optional) Select the native extensions that you want to include in the
    application package.

    If the native extension uses iOS5 SDK features, select the location of the
    iOS SDK. For more information, see
    [Support for iOS5 native extensions](../development-environment/using-native-extensions.md#support-for-ios5-native-extensions).

5.  Click Finish.

    Flash Builder validates the configuration of the package settings and then
    compiles the application. Once the packaging is complete, you can install
    the IPA file on a connected Apple iOS device or submit to the Apple App
    Store.

To package the IPA file using the AIR Developer Tool (ADT), see
[iOS packages](https://web.archive.org/web/20150526031616mp_/http://help.adobe.com/en_US/air/build/WS901d38e593cd1bac35eb7b4e12cddc5fbbb-8000.html)
in _Building AIR Applications_.