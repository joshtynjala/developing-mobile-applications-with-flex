# Differences in mobile, desktop, and browser application development

Use Flex to develop applications for the following deployment environments:

Browser  
Deploy the application as a SWF file for use in Flash Player running in a
browser.

Desktop  
Deploy a standalone AIR application for a desktop computer, such as a Windows
computer or Macintosh.

Mobile  
Deploy a standalone AIR application for a mobile device, such as a phone or a
tablet.

The Flash Player and AIR runtimes are similar. You can perform most of the same
operations in either runtime. Besides allowing you to deploy standalone
applications outside a browser, AIR provides close integration with the host
platform. This integration enables such features as access to the file system of
the device, the ability to create and work with local SQL databases, and more.

## Considerations in designing and developing mobile applications

Applications for mobile touchscreen devices differ from desktop and browser
applications in several ways:

- To allow for easy manipulation by touch input, mobile components generally
  have larger hit areas than they do in desktop or browser applications.

- The interaction patterns for actions like scrolling are different on
  touchscreen devices.

- Because of the limited screen area, mobile applications are typically designed
  with only a small amount of the user interface visible on the screen at one
  time.

- User interface designs must take into account differences in screen resolution
  across devices.

- CPU and GPU performance is more limited on phones and tablets than on desktop
  devices.

- Owing to the limited memory available on mobile devices, applications must be
  careful to conserve memory.

- Mobile applications can be quit and restarted at any time, such as when the
  device receives a call or text message.

Therefore, building an application for a mobile device is not just a matter of
scaling down a desktop application to a different screen size. Flex lets you
create separate user interfaces appropriate for each form factor, while sharing
underlying model and data access code among mobile, browser, and desktop
projects.

## Restrictions on using Spark and MX components in a mobile application

Use the Spark component set when creating mobile applications in Flex. The Spark
components are defined in the spark.components.\* packages. However, for
performance reasons or because not all Spark components have skins for the
Mobile theme, mobile applications do not support the entire Spark component set.

Except for the MX charting controls and the MX Spacer control, mobile
applications do not support the MX component set defined in the mx.\* packages.

The following table lists the components that you can use, that you cannot use,
or that require care to use in a mobile application:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Component</p></th>
<th><p>Component</p></th>
<th><p>Use in mobile?</p></th>
<th><p>Notes</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Spark ActionBar</p>
<p>Spark BusyIndicator</p>
<p>Spark Callout</p>
<p>Spark CalloutButton</p>
<p>Spark DateSpinner</p>
<p>Spark SpinnerList</p>
<p>Spark SpinnerListContainer</p></td>
<td><p>Spark TabbedViewNavigator</p>
<p>Spark TabbedViewNavigatorApplication</p>
<p>Spark ToggleSwitch</p>
<p>Spark View</p>
<p>Spark ViewMenu</p>
<p>Spark ViewNavigator</p>
<p>Spark ViewNavigatorApplication</p></td>
<td><p>Yes</p></td>
<td><p>These new components support mobile applications.</p></td>
</tr>
<tr class="even">
<td><p>Spark Button</p>
<p>Spark CheckBox</p>
<p>Spark DataGroup</p>
<p>Spark Group/HGroup/VGroup/TileGroup</p>
<p>Spark Image/BitmapImage</p>
<p>Spark Label</p></td>
<td><p>Spark List</p>
<p>Spark RadioButton/RadioButtonGroup</p>
<p>Spark SkinnableContainer</p>
<p>Spark Scroller</p>
<p>Spark TextArea</p>
<p>Spark TextInput</p></td>
<td><p>Yes</p></td>
<td><p>Most of these components have skins for the Mobile theme. Label,
Image, and BitmapImage can be used even though they do not have a mobile
skin.</p>
<p>Some Spark layout containers, such as Group and its subclasses, do
not have skins. Therefore, you can use them in a mobile
application.</p></td>
</tr>
<tr class="odd">
<td><p>Other Spark skinnable components</p></td>
<td> </td>
<td><p>Discouraged</p></td>
<td><p>Skinnable Spark components other than the ones listed above are
discouraged because they do not have a skin for the Mobile theme. If the
component does not have a skin for the Mobile theme, you can create one
for your application.</p></td>
</tr>
<tr class="even">
<td><p>Spark DataGrid</p></td>
<td><p>Spark RichEditableText</p>
<p>Spark RichText</p></td>
<td><p>Discouraged</p></td>
<td><p>These components are discouraged for performance reasons. While
you can use them in a mobile application, doing so can affect
performance.</p>
<p>For the DataGrid control, performance is based on the amount of data
that you render. For the RichEditableText and RichText controls,
performance is based on the amount of text, and the number of controls
in the application.</p></td>
</tr>
<tr class="odd">
<td><p>MX components other than Spacer and charts</p></td>
<td> </td>
<td><p>No</p></td>
<td><p>Mobile applications do not support MX components, such as the MX
Button, CheckBox, List, or DataGrid. These components correspond to the
Flex 3 components in the mx.controls.* and mx.containers.*
packages.</p></td>
</tr>
<tr class="even">
<td><p>MX Spacer</p></td>
<td> </td>
<td><p>Yes</p></td>
<td><p>Spacer does not use a skin, so it can be used in a mobile
application.</p></td>
</tr>
<tr class="odd">
<td><p>MX chart components</p></td>
<td> </td>
<td><p>Yes, but with performance implications</p></td>
<td><p>You can use the MX chart controls, such as the AreaChart and
BarChart, in a mobile application. The MX chart controls are in the
mx.charts.* packages.</p>
<p>However, performance on a mobile device can be less than optimal
depending on the size and type of charting data.</p>
<p>By default, Flash Builder does not include the MX components in the
library path of mobile projects. To use the MX charting components in an
application, add the mx.swc and charts.swc to your library
path.</p></td>
</tr>
</tbody>
</table>

The following Flex features are not supported in mobile applications:

- No support for drag-and-drop operations

- No support for the ToolTip control

- No support for RSLs

## Performance considerations with mobile applications

Owing to the performance constraints of mobile devices, some aspects of mobile
application development differ from development for browser and desktop
applications. Some performance considerations include the following:

- **Write item renderers in ActionScript**

  For mobile applications, you want list scrolling to have the highest
  performance possible. Write item renderers in ActionScript to achieve the
  highest performance. While you can write item renderers in MXML, your
  application performance can suffer.

  Flex provides two item renderers that are optimized for use in a mobile
  application:
  [spark.components.LabelItemRenderer](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/LabelItemRenderer.html)
  and
  [spark.components.IconItemRenderer](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/IconItemRenderer.html).
  For more information on these item renderers, see
  [Using a mobile item renderer with a Spark list-based control](https://web.archive.org/web/20150216025044mp_/http://help.adobe.com/en_US/flex/using/WS77c1dbb1bd80d3836663fb6012af31eb8a5-8000.html).

  For more information on creating custom item renderers in ActionScript, see
  [Custom Spark item renderers](https://web.archive.org/web/20150216025044mp_/http://help.adobe.com/en_US/flex/using/WS4bebcd66a74275c3-fc6548e124e49b51c4-8000.html).
  For more information on the differences between mobile and desktop item
  renderers, see
  [Differences between mobile and desktop item renderers](https://web.archive.org/web/20150216025044mp_/http://help.adobe.com/en_US/flex/using/WS684a1733bf2efe8a4bab272a129d72a6e2f-7ffe.html).

- **Use ActionScript and compiled FXG graphics or bitmaps to develop custom
  skins**

  The mobile skins shipped with Flex are written in ActionScript with compiled
  FXG graphics to provide the highest performance. You can write skins in MXML,
  but your application performance can suffer depending on the number of
  components that use MXML skins. For the highest performance, write skins in
  ActionScript and use compiled FXG graphics. For more information, see
  [Spark Skinning](https://web.archive.org/web/20150216025044mp_/http://help.adobe.com/en_US/flex/using/WS53116913-F952-4b21-831F-9DE85B647C8A.html)
  and
  [FXG and MXML graphics](https://web.archive.org/web/20150216025044mp_/http://help.adobe.com/en_US/flex/using/WS145DAB0B-A958-423f-8A01-12B679BA0CC7.html).

- **Use text input components that use StageText**

  When adding text input components such as TextInput and TextArea, use the
  defaults. These controls use StageText as the underlying mechanism for text
  input, which hooks into the native text input classes. This gives you better
  performance and access to native features such as auto-correction,
  auto-capitalization, text restriction, and custom soft keyboards.

  There are some drawbacks to using StageText including not being able to scroll
  the view that the controls are in. In addition, you can't use embedded fonts
  or use custom sizing for the StageText-based controls. If these are necessary,
  you can use text input controls based on the TextField class.

  For more information, see
  [Use text in a mobile application](../text/use-text-in-a-mobile-application.md).

- **Take care when using MX chart components in a mobile application**

  You can use the MX chart controls, such as the AreaChart and BarChart
  controls, in a mobile application. However, they can affect performance
  depending on the size and type of charting data.

![](../img/byline.png) Blogger Nahuel Foronda
[created a series of articles on Mobile ItemRenderer in ActionScript](https://web.archive.org/web/20150216025044mp_/http://www.asfusion.com/blog/entry/mobile-itemrenderer-in-actionscript-part-5).

![](../img/byline.png) Blogger Rich Tretola
[created a cookbook entry on Creating a List with an ItemRenderer for a mobile application](https://web.archive.org/web/20150216025044mp_/http://cookbooks.adobe.com/post_Creating_a_List_with_an_ItemRenderer-18852.html).
