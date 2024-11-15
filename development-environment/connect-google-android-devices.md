# Connect Google Android devices

You can connect a Google Android device to your development computer to preview
or debug the application on the Android device.

## Supported Android devices

Flex mobile projects and ActionScript mobile projects require AIR 2.6 or a
higher version of AIR. You can run or debug mobile projects only on physical
devices that support AIR 2.6 or a higher version.

You can install AIR 2.6 on supported Android devices running Android 2.2 or a
higher version. For a list of supported devices, see
[http://www.adobe.com/flashplatform/certified_devices/](https://web.archive.org/web/20150219035517mp_/http://www.adobe.com/flashplatform/certified_devices/).
Also, review the minimum system requirements to run Adobe AIR on Android devices
at
[Mobile System Requirements](https://web.archive.org/web/20150219035517mp_/http://www.adobe.com/products/air/systemreqs/#mobile).

## Configure Android devices

To run and debug Flex mobile applications from an Android device, enable USB
debugging as indicated below:

1.  On the device, follow these steps to ensure that USB debugging is enabled:

    1.  Tap the Home button to display the home screen.

    2.  Go to Settings, and select Applications \> Development.

    3.  Enable USB debugging.

2.  Connect the device to your computer with a USB cable.

3.  Pull down the notification area at the top of the screen. You see either USB
    Connected or USB Connection.

    1.  Tap USB Connected or USB Connection.

    2.  If a set of options appears that includes Charge Only mode, select
        Charge Only and tap OK.

    3.  If you see a button for turning off mass storage mode, click the button
        to turn off mass storage.

4.  (Windows only) Install the appropriate USB driver for your device. See
    [Install USB device drivers for Android devices (Windows)](#install-usb-device-drivers-for-android-devices-windows).

5.  Pull down the notification area at the top of the screen.

    If USB Debugging does not appear as an entry, check the USB mode as
    described in step 3 above. Make sure that the USB mode is not set to PC
    Mode.

> **Note:** Additional configuration is needed when debugging. See
> [Test and debug a mobile application on a device](../test-and-debug/test-and-debug-a-mobile-application-on-a-device.md).

## Install USB device drivers for Android devices (Windows)

#### Device drivers and configurations

Windows platforms require installation of a USB driver to connect an Android
device to your development computer. Flash Builder provides a device driver and
configuration for several Android devices.

These device driver configurations are listed in the `android_winusb.inf`.
Windows Device Manager accesses this file when installing the device driver.
Flash Builder installs `android_winusb.inf` at the following location:

    <Adobe Flash Builder 4.6 Home>\utilities\drivers\android\android_winusb.inf

For the complete list of supported devices, see
[Certified devices](https://web.archive.org/web/20150219035517mp_/http://www.adobe.com/flashplatform/certified_devices/).
For Android devices that are not listed, you can update `android_winusb.inf`
with USB drivers. See
[Add Android USB device driver configurations](#add-android-usb-device-driver-configurations).

#### Install USB device driver

1.  Connect your Android device to your computer's USB port.

2.  Go to the following location:

    `<Flash Builder>/utilities/drivers/android/`

    Install the USB driver using either the Windows Found New Hardware wizard or
    the Windows Device Manager.

Important: If Windows is still unable to recognize your device, you need to
install the appropriate USB driver from your device manufacturer. See
[OEM USB drivers](https://web.archive.org/web/20150219035517mp_/http://developer.android.com/sdk/oem-usb.html)
for links to the websites of several device manufacturers from where you can
download the appropriate USB driver for your device.

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
<td width="60%"><div class="iframe">
<div id="player" class="full-frame">
&#10;</div>
<div id="player-unavailable" class="ytp-error hid">
<div id="unavailable-submessage" class="ytp-error-content">
&#10;</div>
</div>
<div class="player-unavailable">
<h1 id="an-error-occurred." class="message">An error occurred.</h1>
<div class="submessage">
<a
href="https://web.archive.org/web/20150816085704/http://www.youtube.com/watch?v=KE-t2obmhpM">Try
watching this video on www.youtube.com</a>, or enable JavaScript if it
is disabled in your browser.
</div>
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
<td width="85%"><h3
id="troubleshooting-android-device-connections-on-windows"><a
href="https://www.youtube.com/watch?v=KE-t2obmhpM">Troubleshooting
Android device connections on Windows</a></h3>
<span>Brent Arnold</span><br />
<span>If Windows is unable to recognize the Android device connected to
your computer, watch this video for troubleshooting tips.</span></td>
</tr>
<tr class="even">
<td colspan="2"><h3 id="have-a-tutorial-you-would-like-to-share"><img
src="../img/TinyBlueTutIcon.png" /><a
href="https://web.archive.org/web/20150219035517mp_/http://www.adobe.com/community/publishing/download.html">Have
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

## Add Android USB device driver configurations

If you have a supported Android device not listed in
[Install USB device drivers for Android devices (Windows)](#install-usb-device-drivers-for-android-devices-windows),
update the `android_winusb.inf` file to include the device.

1.  Plug the device into a USB port of your computer. Windows informs you that
    it cannot find the driver.

2.  Using the Windows Device Manager, open the Details tab of the device
    properties.

3.  Select the Hardware IDs property to view the hardware ID.

4.  Open `android_winusb.inf` in a text editor. Find `android_winusb.inf` at the
    following location:

        <Adobe Flash Builder 4.6 Home>\utilities\drivers\android\android_winusb.inf

5.  Note the listings in the file that apply to your architecture, either
    `[Google.NTx86]` or `[Google.NTamd64]`. The listings contain a descriptive
    comment and one or more lines with the hardware ID, as shown here:

        . . .
        [Google.NTx86]
        ; HTC Dream
        %CompositeAdbInterface% = USB_Install, USB\VID_0BB4&PID_0C02&MI_01
        . . .

6.  Copy and paste a comment and hardware listing. For the device driver you
    want to add, edit the listing as follows:

    1.  For the comment, specify the name of the device.

    2.  Replace the hardware ID with the hardware ID identified in Step 3 above.

    For example:

        . . .
        [Google.NTx86]
        ; NEW ANDROID DEVICE
        %CompositeAdbInterface%     = USB_Install, NEW HARDWARE ID. . .

7.  Use the Windows Device Manager to install the device, as described in
    [Install USB device drivers for Android devices (Windows)](#install-usb-device-drivers-for-android-devices-windows)
    above.

    During the installation, Windows displays a warning that the driver is from
    an unknown publisher. However, the driver allows Flash Builder to access
    your device.
