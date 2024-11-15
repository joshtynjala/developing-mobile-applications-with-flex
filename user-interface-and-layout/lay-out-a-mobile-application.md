# Lay out a mobile application

## Use views and sections to lay out a mobile application

A mobile application is made up of one or more screens, or _views_. For example,
mobile application could have three views:

1.  A home view that lets you add contact information

2.  A contacts view containing a list of existing contacts

3.  A search view to search your list of contacts

**A simple mobile application**

The following image shows the main screen of a simple mobile application built
in Flex:

<p><i>Image Missing: fmc_single_section_fmc.png</i></p>

**A.** ActionBar control **B.** Content area

This figure shows the main areas of a mobile application:

ActionBar control  
The
[ActionBar](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/ActionBar.html)
control lets you display contextual information about the current state of the
application. This information includes a title area, an area for controls to
navigate the application, and an area for controls to perform an action. You can
add global content in the ActionBar control that applies to the entire
application, and you can add items specific to an individual view.

Content area  
The content area displays the individual screens, or _views_, that make up the
application. Users navigate the views of the application by using the components
built in to the application and the input controls of the mobile device.

**A mobile application with sections**

A more complex application could define several areas, or _sections_, of the
application. For example, the application could have a contacts section, an
e-mail section, a favorites section, and other sections. Each section of the
application contains one or more views. Individual views can be shared across
sections so that you do not have to define the same view multiple times.

The following figure shows a mobile application that includes a tab bar at the
bottom of the application window:

<p><i>Image Missing: fmc_sections_fmc.png</i></p>

**A.** ActionBar control **B.** Content area **C.** Tab bar

Flex uses the
[ButtonBarBase](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/supportClasses/ButtonBarBase.html)
control to implement the tab bar. Each button of the tab bar corresponds to a
different section. Select a button in the tab bar to change the current section.

Each section of the application defines its own ActionBar. Therefore, the tab
bar is global to the entire application, and the ActionBar is specific to each
section.

## Lay out a simple mobile application

The following figure shows the architecture of a simple mobile application:

<p><i>Image Missing: fmc_single_section_diagram_fmc.png</i></p>

The figure shows an application made up of four files. A mobile application
contains a main application file, and one file for each view. There is no
separate file for the ViewNavigator; the ViewNavigatorApplication container
creates it.

> **Note:** While this diagram shows the application architecture, it does not
> represent the application at runtime. At runtime, only one view is active and
> resident in memory. For more information, see
> [Navigate the views of a mobile application](#navigate-the-views-of-a-mobile-application).

**Classes used in a mobile application**

Use the following classes to define a mobile application:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Class</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ViewNavigatorApplication</p></td>
<td><p>Defines the main application file. The ViewNavigatorApplication
container does not take any children.</p></td>
</tr>
<tr class="even">
<td><p>ViewNavigator</p></td>
<td><p>Controls navigation among the views of an application. The
ViewNavigator also creates the ActionBar control.</p>
<p>The ViewNavigatorApplication container automatically creates a single
ViewNavigator container for the entire application. Use methods of the
ViewNavigator container to switch between the different views.</p></td>
</tr>
<tr class="odd">
<td><p>View</p></td>
<td><p>Defines the views of the application, where each view is defined
in a separate MXML or ActionScript file. An instance of the View
container represents each view of the application. Define each view in a
separate MXML or ActionScript file.</p></td>
</tr>
</tbody>
</table>

Use the
[ViewNavigatorApplication](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/ViewNavigatorApplication.html)
container to define the main application file, as the following example shows:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\SparkSingleSectionSimple.mxml -->
    <s:ViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
    	xmlns:s="library://ns.adobe.com/flex/spark"
    	firstView="views.HomeView">

    </s:ViewNavigatorApplication>

The ViewNavigatorApplication container automatically creates a single
[ViewNavigator](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/ViewNavigator.html)
object that defines the ActionBar. You use the ViewNavigator to navigate the
views of the application.

**Add a View container to a mobile application**

Every mobile application has at least one view. While the main application file
creates the ViewNavigator, it does not define any of the views used in the
application.

Each view in an application corresponds to a
[View](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/View.html)
container defined in an ActionScript or MXML file. Each View contains a `data`
property that specifies the data associated with that view. Views can use the
`data` property to pass information to each other as the user navigates the
application.

Use the `ViewNavigatorApplication.firstView` property to specify the file that
defines the first view in the application. In the previous application, the
`firstView` property specifies `views.HomeView`. The following example shows the
HomeView.mxml file that defines that view:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\views\HomeView.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    	xmlns:s="library://ns.adobe.com/flex/spark"
    	title="Home">
    	<s:layout>
    		<s:VerticalLayout paddingTop="10"/>
    	</s:layout>

    	<s:Label text="The home screen"/>
    </s:View>

![](../img/byline.png) Blogger David Hassoun blogged about
[ViewNavigator basics](https://web.archive.org/web/20150219083429mp_/http://www.realeyes.com/blog/2011/05/15/mobile-flex-viewnavigator-basics/).

## Lay out a mobile application with multiple sections

A mobile application can collect related views in different sections of the
application. For example, the following figure shows the organization of a
mobile application with three sections.

<p><i>Image Missing: fmc_section_diagram_fmc.png</i></p>

Any section can use any
[View](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/View.html).
That is, a view does not belong to a specific section. The section just defines
a way to arrange and navigate a collection of views. In the figure, the Search
view is part of every section of the application.

At runtime, only one view is active and resident in memory. For more
information, see
[Navigate the views of a mobile application](#navigate-the-views-of-a-mobile-application).

**Classes used in a mobile application with multiple sections**

The following table lists the classes that you use to create a mobile
application with multiple sections:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Class</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TabbedViewNavigatorApplication</p></td>
<td><p>Defines the main application file. The only allowable child of
the TabbedViewNavigatorApplication container is ViewNavigator. Define
one ViewNavigator for each section of the application.</p></td>
</tr>
<tr class="even">
<td><p>TabbedViewNavigator</p></td>
<td><p>Controls navigation among the sections that make up the
application.</p>
<p>The TabbedViewNavigatorApplication container automatically creates a
single TabbedViewNavigator container for the entire application. The
TabbedViewNavigator container creates the tab bar that you use to
navigate among the sections.</p></td>
</tr>
<tr class="odd">
<td><p>ViewNavigator</p></td>
<td><p>Define one ViewNavigator container for each section. The
ViewNavigator controls navigation among the views that make up the
section. It also creates the ActionBar control for the section.</p></td>
</tr>
<tr class="even">
<td><p>View</p></td>
<td><p>Defines the views of the application. An instance of the View
container represents each view of the application. Define each view in a
separate MXML or ActionScript file.</p></td>
</tr>
</tbody>
</table>

A sectioned mobile application contains a main application file, and a file that
defines each view. Use the
[TabbedViewNavigatorApplication](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TabbedViewNavigatorApplication.html)
container to define the main application file, as the following example shows:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\SparkMultipleSectionsSimple.mxml -->
    <s:TabbedViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
    	xmlns:s="library://ns.adobe.com/flex/spark">

    	<s:ViewNavigator label="Contacts" firstView="views.ContactsHome"/>
    	<s:ViewNavigator label="Email" firstView="views.EmailHome"/>
    	<s:ViewNavigator label="Favorites" firstView="views.FavoritesHome"/>

    </s:TabbedViewNavigatorApplication>

**Use the ViewNavigator in an application with multiple sections**

The only allowable child component of the TabbedViewNavigatorApplication
container is ViewNavigator. Each section of the application corresponds to a
different ViewNavigator container.

Use the
[ViewNavigator](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/ViewNavigator.html)
container to navigate the views of each section, and to define the ActionBar
control for the section. Use the `ViewNavigator.firstView` property to specify
the file that defines the first view in the section.

**Use the TabbedViewNavigator in an application with multiple sections**

The TabbedViewNavigatorApplication container automatically creates a single
container of type TabbedViewNavigator. The
[TabbedViewNavigator](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TabbedViewNavigator.html)
container then creates a tab bar at the bottom of the application. You do not
have to add logic to the application to navigate among the sections.

## Navigate the views of a mobile application

A stack of
[View](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/View.html)
objects controls navigation in a mobile application. The top View object on the
stack defines the currently visible view.

The
[ViewNavigator](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/ViewNavigator.html)
container maintains the stack. To change views, push a new View object onto the
stack, or pop the current View object off the stack. Popping the currently
visible View object off the stack destroys the View object and returns the user
to the previous view on the stack.

In an application with sections, use the tab bar to navigate the sections.
Because a different ViewNavigator defines each section, changing sections
corresponds to changing the current ViewNavigator and stack. The View object at
the top of the stack of the new ViewNavigator becomes the current view.

To conserve memory, by default the ViewNavigator ensures that only one view is
in memory at a time. However, it maintains the data for previous views on the
stack. Therefore, when the user navigates back to the previous view, the view
can be reinstantiated with the appropriate data.

> **Note:** The View container defines the `destructionPolicy` property. If set
> to `auto`, the default, the ViewNavigator destroys the view when it is not
> active. If set to `none`, the view is cached in memory.

![](../img/byline.png) Blogger Mark Lochrie
[blogged about ViewNavigator](https://web.archive.org/web/20150219083429mp_/http://www.uimobile.co.uk/flash-builder-viewnavigator/).

**ViewNavigator navigation methods**

Use the following methods of the ViewNavigator class to control navigation:

**pushView()**  
Push a View object onto the stack. The View passed as an argument to the
`pushView()` method becomes the current view.

**popView()**  
Pop the current View object off the navigation stack and destroy the View
object. The previous View object on the stack becomes the current view.

**popToFirstView()**  
Pop all View objects off the stack and destroy them, except for the first View
object on the stack. The first View object on the stack becomes the current
view.

**popAll()**  
Empty the stack of the ViewNavigator, and destroy all View objects. Your
application displays a blank view.

The following figure shows two views. To change the current view, use the
`ViewNavigator.pushView()` method to push a View object that represents the new
view onto the stack. The `pushView()` method causes the ViewNavigator to switch
the display to the new View object.

<p><i>Image Missing: fmc_push_pop_fmc.png</i></p>

Push and pop View objects to change views.

Use the `ViewNavigator.popView()` method to remove the current View object from
the stack. The ViewNavigator returns display to the previous View object on the
stack.

> **Note:** The mobile device itself controls much of the navigation in a mobile
> application. For example, mobile applications built in Flex automatically
> handle the back button on mobile devices. Therefore, you do not have to add
> support for the back button to the application. When the user presses the back
> button on the mobile device, Flex automatically calls the `popView()` method
> to restore the previous view.

![](../img/byline.png) Blogger David Hassoun blogged about
[managing data in a view](https://web.archive.org/web/20150219083429mp_/http://www.realeyes.com/blog/2011/05/16/mobile-flex-view-data/).

**Create navigation for an application with multiple sections**

In the following figure, the Views are arranged in multiple sections. A
different ViewNavigator container defines each section. Within each section are
one or more views:

<p><i>Image Missing: fmc_sections_fmc.png</i></p>

**A.** ActionBar **B.** Content area **C.** Tab bar

To change the view in the current section, which corresponds to the current
ViewNavigator, use the `pushView()` and `popView()` methods.

To change the current section, use the tab bar. When you switch sections, you
switch to the ViewNavigator container of the new section. The display changes to
show the View object currently at the top of the stack for the new
ViewNavigator.

You can also change sections programmatically by using the
`TabbedViewNavigator.selectedIndex` property. This property contains the 0-based
index of the selected view navigator.
