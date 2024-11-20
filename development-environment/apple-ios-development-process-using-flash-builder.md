# Apple iOS development process using Flash Builder

Before developing an iOS application using Flash Builder, it is important to
understand the iOS development process and how to obtain the required
certificates from Apple.

## Adobe recommends

> ### ![](../img/ATrice.png) [Developing Apple iOS applications in Flash Builder](https://web.archive.org/web/20150314060546/http://tv.adobe.com/watch/adc-presents/build-ios-applications-using-flex-and-flash-builder-453)
>
> [Andrew Trice](https://web.archive.org/web/20150321023249mp_/http://www.tricedesigns.com/)
>
> Workflow to develop iOS applications - from development in Flash Builder to
> publishing in Apple's App Store

## Overview of the iOS development and deployment process

This table provides a quick list of steps in the iOS development process, how to
obtain the required certificates, and prerequisites to each step.

For detailed information on each of these steps, see
[Prepare to build, debug, or deploy an iOS application](#prepare-to-build-debug-or-deploy-an-ios-application).

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Step no.</p></th>
<th><p>Step</p></th>
<th><p>Location</p></th>
<th><p>Prerequisites</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1.</p></td>
<td><p>Join the Apple developer program.</p></td>
<td><p><a
href="https://web.archive.org/web/20150321023249mp_/http://developer.apple.com/programs/register/">Apple
Developer site</a></p></td>
<td><p>None</p></td>
</tr>
<tr class="even">
<td><p>2.</p></td>
<td><p>Register the Unique Device Identifier (UDID) of your iOS
device.</p></td>
<td><p><a
href="https://web.archive.org/web/20150321023249mp_/http://developer.apple.com/devcenter/ios">iOS
Provisioning Portal</a></p></td>
<td><p>Apple developer ID (step 1)</p></td>
</tr>
<tr class="odd">
<td><p>3.</p></td>
<td><p>Generate a Certificate Signing Request (CSR) file
(*.certSigningRequest).</p></td>
<td><div>
<ul class="incremental">
<li><p>On Mac OS, use the Keychain Access program</p></li>
<li><p>On Windows, use OpenSSL</p></li>
</ul>
</div></td>
<td><p>None</p></td>
</tr>
<tr class="even">
<td><p>4.</p></td>
<td><p>Generate an iOS developer/distribution certificate
(*.cer).</p></td>
<td><p><a
href="https://web.archive.org/web/20150321023249mp_/http://developer.apple.com/devcenter/ios">iOS
Provisioning Portal</a></p></td>
<td><div>
<ul class="incremental">
<li><p>Apple developer ID (step 1)</p></li>
<li><p>CSR file (step 3)</p></li>
</ul>
</div></td>
</tr>
<tr class="odd">
<td><p>5.</p></td>
<td><p>Convert the iOS developer/distribution certificate into P12
format.</p></td>
<td><div>
<ul class="incremental">
<li><p>On Mac OS, use the Keychain Access program</p></li>
<li><p>On Windows, use OpenSSL</p></li>
</ul>
</div></td>
<td><div>
<ul class="incremental">
<li><p>Apple developer ID (step 1)</p></li>
<li><p>iOS developer/distribution certificate (step 4)</p></li>
</ul>
</div></td>
</tr>
<tr class="even">
<td><p>6.</p></td>
<td><p>Generate the Application ID.</p></td>
<td><p><a
href="https://web.archive.org/web/20150321023249mp_/http://developer.apple.com/devcenter/ios">iOS
Provisioning Portal</a></p></td>
<td><p>Apple developer ID (step 1)</p></td>
</tr>
<tr class="odd">
<td><p>7.</p></td>
<td><p>Generate a provisioning profile (*.mobileprovision)</p></td>
<td><p><a
href="https://web.archive.org/web/20150321023249mp_/http://developer.apple.com/devcenter/ios">iOS
Provisioning Portal</a></p></td>
<td><div>
<ul class="incremental">
<li><p>Apple developer ID (step 1)</p></li>
<li><p>UDID of your iOS device (step 2)</p></li>
<li><p>Application ID (step 6)</p></li>
</ul>
</div></td>
</tr>
<tr class="even">
<td><p>8.</p></td>
<td><p>Build the application.</p></td>
<td><p>Flash Builder</p></td>
<td><div>
<ul class="incremental">
<li><p>Apple developer ID (step 1)</p></li>
<li><p>P12 developer/distribution certificate (step 5)</p></li>
<li><p>Application ID (step 6)</p></li>
</ul>
</div></td>
</tr>
<tr class="odd">
<td><p>9.</p></td>
<td><p>Deploy the application.</p></td>
<td><p>iTunes</p></td>
<td><div>
<ul class="incremental">
<li><p>Provisioning profile (step 7)</p></li>
<li><p>Application package (step 8)</p></li>
</ul>
</div></td>
</tr>
</tbody>
</table>

## Prepare to build, debug, or deploy an iOS application

Before you build an iOS application using Flash Builder and deploy the
application on an iOS device or submit to the Apple App store, follow these
steps:

1.  Join the
    [Apple iOS Developer Program](https://web.archive.org/web/20150321023249mp_/http://developer.apple.com/programs/register/).

    You can log in using your existing Apple ID or create an Apple ID. The Apple
    Developer Registration guides you through the necessary steps.

2.  Register the Unique Device Identifier (UDID) of the device.

    This step is applicable only if you are deploying your application to an iOS
    device and not the Apple App Store. If you want to deploy your application
    on several iOS devices, register the UDID of each device.

    **Obtain the UDID of your iOS device**

    1.  Connect the iOS device to your development computer and launch iTunes.
        The connected iOS device appears under the Devices section in iTunes.

    2.  Click the device name to display a summary of the iOS device.

    3.  In the Summary tab, click Serial Number to display the 40-character UDID
        of the iOS device.

        > ![](../img/tip_help.png) You can copy the UDID from iTunes using the
        > keyboard shortcut Ctrl+C (Windows) or Cmd+C (Mac).

    **Register the UDID of your device**

    Log in to the
    [iOS Provisioning Portal](https://web.archive.org/web/20150321023249mp_/http://developer.apple.com/devcenter/ios)
    using your Apple ID and register the device's UDID.

3.  Generate a Certificate Signing Request (CSR) file (\*.certSigningRequest).

    You generate a CSR to obtain a iOS developer/distribution certificate. You
    can generate a CSR by using Keychain Access on Mac or OpenSSL on Windows.
    When you generate a CSR you only provide your user name and email address;
    you don't provide any information about your application or device.

    Generating a CSR creates a public key and a private key as well as a
    \*.certSigningRequest file. The public key is included in the CSR, and the
    private key is used to sign the request.

    For more information on generating a CSR, see
    [Generating a certificate signing request](https://web.archive.org/web/20141008090043/http://help.adobe.com/en_US/as3/iphone/WS144092a96ffef7cc-371badff126abc17b1f-8000.html).

4.  Generate an iOS developer certificate or an iOS distribution certificate
    (\*.cer), as required.

    > **Note:** To deploy an application to a device, you need a developer
    > certificate. To deploy the application to the Apple App Store, you need a
    > distribution certificate.

    **Generate an iOS developer certificate**

    1.  Log in to the
        [iOS Provisioning Portal](https://web.archive.org/web/20150321023249mp_/http://developer.apple.com/devcenter/ios)
        using your Apple ID, and select the Development tab.

    2.  Click Request Certificate and browse to the CSR file that you generated
        and saved on your computer (step 3).

    3.  Select the CSR file and click Submit.

    4.  On the Certificates page, click Download.

    5.  Save the downloaded file (\*.developer_identity.cer).

    **Generate an iOS distribution certificate**

    1.  Log in to the
        [iOS Provisioning Portal](https://web.archive.org/web/20150321023249mp_/http://developer.apple.com/devcenter/ios)
        using your Apple ID, and select the Distribution tab

    2.  Click Request Certificate and browse to the CSR file that you generated
        and saved on your computer (step 3).

    3.  Select the CSR file and click Submit.

    4.  On the Certificates page, click Download.

    5.  Save the downloaded file (\*.distribution_identity.cer).

5.  Convert the iOS developer certificate or the iOS distribution certificate to
    a P12 file format (\*.p12).

    You convert the iOS developer or iOS distribution certificate to a P12
    format so that Flash Builder can digitally sign your iOS application.
    Converting to a P12 format combines your iOS developer/distribution
    certificate and the associated private key into a single file.

    > **Note:** If you are testing the application on the desktop using the AIR
    > Debug Launcher (ADL), you don't have to convert the iOS
    > developer/distribution certificate into a P12 format.

    Use Keychain Access on Mac or OpenSSL on Windows to generate a Personal
    Information Exchange (\*.p12) file. For more information, see
    [Convert a developer certificate into a P12 file.](https://web.archive.org/web/20141008090048/http://help.adobe.com/en_US/as3/iphone/WS144092a96ffef7cc-371badff126abc17b1f-7fff.html)

6.  Generate the Application ID by following these steps:

    1.  Log in to the
        [iOS Provisioning Portal](https://developer.apple.com/account/) using
        your Apple ID.

    2.  Go to the App IDs page, and click New App ID.

    3.  In the Manage tab, enter a description for your application, generate a
        new Bundle Seed ID, and enter a Bundle Identifier.

        Every application has a unique Application ID, which you specify in the
        application descriptor XML file. An Application ID consists of a
        ten-character "Bundle Seed ID" that Apple provides and a "Bundle
        Identifier" suffix that you specify. The Bundle Identifier you specify
        must match the application ID in the application descriptor file. For
        example, if your Application ID is com.myDomain.\*, the ID in the
        application descriptor file must start with com.myDomain.

        > **Important:** Wildcard Bundle Identifiers are good for developing and
        > testing iOS applications but can't be used to deploy applications to
        > the Apple App Store.

7.  Generate a Developer Provisioning Profile file or a Distribution
    Provisioning Profile File (\*.mobileprovision).

    > **Note:** To deploy an application to a device, you need a Developer
    > Provisioning Profile. To deploy the application to the Apple App Store,
    > you need a Distribution Provisioning Profile. You use a Distribution
    > Provisioning Profile to sign your application.

    **Generate a Developer Provisioning Profile**

    1.  Log in to the
        [iOS Provisioning Portal](https://web.archive.org/web/20150321023249mp_/http://developer.apple.com/devcenter/ios)
        using your Apple ID.

    2.  Go to Certificate \> Provisioning, and click New Profile.

    3.  Enter a profile name, select the iOS developer certificate, the App ID,
        and the UDIDs on which you want to install the application.

    4.  Click Submit.

    5.  Download the generated Developer Provisioning Profile file
        (\*.mobileprovision)and save it on your computer.

    **Generate a Distribution Provisioning Profile**

    1.  Log in to the
        [iOS Provisioning Portal](https://web.archive.org/web/20150321023249mp_/http://developer.apple.com/devcenter/ios)
        using your Apple ID.

    2.  Go to Certificate \> Provisioning, and click New Profile.

    3.  Enter a profile name, select the iOS distribution certificate and the
        App ID. If you want to test the application before deployment, specify
        the UDIDs of the devices on which you want to test.

    4.  Click Submit.

    5.  Download the generated Provisioning Profile file (\*.mobileprovision)and
        save it on your computer.

## Files to select when you test, debug, or install an iOS application

To run, debug, or install an application for testing on an iOS device, you
select the following files in the Run/Debug Configurations dialog box:

- iOS developer certificate in P12 format (step 5)

- Application descriptor XML file that contains the Application ID (step 6)

- Developer Provisioning Profile (step 7)

For more information, see
[Debug an application on an Apple iOS device](../test-and-debug/test-and-debug-a-mobile-application-on-a-device.md#debug-an-application-on-an-apple-ios-device)
and
[Install an application on an Apple iOS device](../install-on-devices/install-an-application-on-an-apple-ios-device.md).

## Files to select when you deploy an application to the Apple App Store

To deploy an application to the Apple App Store, select the Package Type in the
Export Release Build dialog box as Final Release Package For Apple App Store,
and select the following files:

- iOS distribution certificate in P12 format (step 5)

- Application descriptor XML file that contains the Application ID (step 6).

  > **Note:** You can't use a wildcard Application ID while submitting an
  > application to the Apple App Store.

- Distribution Provisioning Profile (step 7)

For more information, see
[Export Apple iOS packages for release](../package-and-export/export-apple-ios-packages-for-release.md).

More Help topics

[Create an iOS application in Flash Builder](../development-environment/create-an-ios-application-in-flash-builder.md)
