# Enable persistence in a mobile application

An application for a mobile device is often interrupted by other actions, such
as a text message, a phone call, or other mobile applications. Typically, when
an interrupted application is relaunched, the user expects the previous state of
the application to be restored. The persistence mechanism allows the device to
restore the application to its previous state.

The Flex framework provides two kinds of persistence for mobile application.
_In-memory_ persistence saves view data as the user navigates the application.
_Session persistence_ restores data if the user quits the application and then
restarts it. Session persistence is important in mobile applications because a
mobile operating system can quit applications at any time (for example, when
memory is low).

![](../img/byline.png) Blogger Steve Mathews
[created a cookbook entry on simple data persistence in a Flex mobile application](https://web.archive.org/web/20150329020956mp_/http://cookbooks.adobe.com/post_Simple_data_persistence_in_a_Flex_4_5_mobile_appli-18856.html).

![](../img/byline.png) Blogger Holly Schinsky
[blogged about persistence and data handling in Flex Mobile Data Handling](https://web.archive.org/web/20130817134922/http://devgirl.org/2011/05/18/flex-4-5-mobile-data-handling/).

## In-memory persistence

[View](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/View.html)
containers support in-memory persistence by using the `View.data` property. An
existing view's `data` property is automatically saved when the selected section
changes or when a new view is pushed onto the ViewNavigator stack, causing the
existing view to be destroyed. The `data` property of the view is restored when
control returns to the view and the view is re-instantiated and activated.
Therefore, in-memory persistence lets you maintain state information of a view
at runtime.

## Session persistence

Session persistence maintains application state information between application
executions. The
[ViewNavigatorApplication](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/ViewNavigatorApplication.html)
and
[TabbedViewNavigatorApplication](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TabbedViewNavigatorApplication.html)
containers define the `persistNavigatorState` property to implement session
persistence. Set `persistNavigatorState` to `true` to enable session
persistence. By default, `persistNavigatorState` is `false`.

When enabled, session persistence writes the state of the application to disk
using a local shared object named `FxAppCache`. Your application can also use
methods of the
[spark.managers.PersistenceManager](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/managers/PersistenceManager.html)
to write additional information to the local shared object.

**ViewNavigator session persistence**

The
[ViewNavigator](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/ViewNavigator.html)
container supports session persistence by saving the state of its view stack to
disk when the application quits. This save includes the `data` property of the
current View.

When the application restarts, the stack of the ViewNavigator is reinitialized
and the user sees the same view and content visible when the application quit.
Because the stack contains a copy of the `data` property for each view, previous
views on the stack can be recreated as they become active.

**TabbedViewNavigator session persistence**

For the
[TabbedViewNavigator](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/spark/components/TabbedViewNavigator.html)
container, session persistence saves the currently selected tab of the tab bar
when the application quits. The tab corresponds to the ViewNavigator and view
stack that defines the tab. Included in the save is the `data` property of the
current View. Therefore, when the application restarts, the active tab and
associated ViewNavigator is set to the state that it had when the application
quit.

> **Note:** For an application defined by the TabbedViewNavigatorApplication
> container, only the stack for the current ViewNavigator is saved. Therefore,
> when the application restarts, only the state of the current ViewNavigator is
> restored.

**Session persistence data representation**

The persistence mechanism used by Flex is not encrypted or protected. Therefore,
persisted data is stored in a format that can be interpreted by another program
or user. Do not persist sensitive information, such as user credentials, using
this mechanism. You have the option of writing your own persistence manager that
provides better protection. For more information, see
[Customize the persistence mechanism](#customize-the-persistence-mechanism).

### Use session persistence

The following example sets the `persistNavigatorState` property to `true` for an
application to enable session persistence:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\SparkSingleSectionPersist.mxml -->
    <s:ViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
    	xmlns:s="library://ns.adobe.com/flex/spark"
    	firstView="views.EmployeeMainView"
    	persistNavigatorState="true">

    	<fx:Script>
    		<![CDATA[
    			protected function button1_clickHandler(event:MouseEvent):void {
    				// Switch to the first view in the section.
    				navigator.popToFirstView();
    			}
    		]]>
    	</fx:Script>

    	<s:navigationContent>
    		<s:Button icon="@Embed(source='assets/Home.png')"
    				  click="button1_clickHandler(event)"/>
    	</s:navigationContent>
    </s:ViewNavigatorApplication>

This application uses EmployeeMainView.mxml as its first view.
EmployeeMainView.mxml defines a List control that lets you select a user name:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\views\EmployeeMainView.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    	xmlns:s="library://ns.adobe.com/flex/spark"
    	title="Employees">
    	<s:layout>
    		<s:VerticalLayout paddingTop="10"/>
    	</s:layout>

    	<fx:Script>
    		<![CDATA[
    			import spark.events.IndexChangeEvent;

    			protected function myList_changeHandler(event:IndexChangeEvent):void {
    				navigator.pushView(views.EmployeeView,myList.selectedItem);
    			}

    		]]>
    	</fx:Script>

    	<s:Label text="Select an employee name"/>
    	<s:List id="myList"
    		width="100%" height="100%"
    		labelField="firstName"
    		change="myList_changeHandler(event)">
    		<s:ArrayCollection>
    			<fx:Object firstName="Bill" lastName="Smith" companyID="11233"/>
    			<fx:Object firstName="Dave" lastName="Jones" companyID="13455"/>
    			<fx:Object firstName="Mary" lastName="Davis" companyID="11543"/>
    			<fx:Object firstName="Debbie" lastName="Cooper" companyID="14266"/>
    		</s:ArrayCollection>
    	</s:List>
    </s:View>

To see session persistence, open the application, and then select "Dave" in the
List control to navigate to the EmployeeView.mxml view:

    <?xml version="1.0" encoding="utf-8"?>
    <!-- containers\mobile\views\EmployeeView.mxml -->
    <s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
    	xmlns:s="library://ns.adobe.com/flex/spark"
    	title="Employee View">
    	<s:layout>
    		<s:VerticalLayout paddingTop="10"/>
    	</s:layout>

    	<s:VGroup>
    		<s:Label text="{data.firstName}"/>
    		<s:Label text="{data.lastName}"/>
    		<s:Label text="{data.companyID}"/>
    	</s:VGroup>
    </s:View>

The EmployeeView.mxml view displays the data about "Dave". Then, quit the
application. When you restart the application, you again see the
EmployeeView.mxml view displaying the same data as when you quit the
application.

### Access data in a local shared object

Information in a local shared object is saved as a key:value pair. The methods
of the PeristenceManager, such as `setPropery()` and `getProperty()`, rely on
the key to access the associated value in the local shared object.

You can use the `setProperty()` method to write your own key:value pairs to the
local shared object. The `setProperty()` method has the following signature:

    setProperty(key:String, value:Object):void

Use the `getProperty()` method to access the value for a specific key. The
`getProperty()` method has the following signature:

    getProperty(key:String):Object

When the `persistNavigatorState` property is `true`, the persistence manager
automatically saves two key:value pairs to the local shared object when the
application quits:

- `applicationVersion`

  The version of the application as described by the application.xml file.

- `navigatorState`

  The view state of the navigator, corresponding to the stack of the current
  ViewNavigator.

### Perform manual persistence

When the `persistNavigatorState` property is `true`, Flex automatically performs
session persistence. You can still persist application data when the
`persistNavigatorState` property is `false`. In that situation, implement your
own persistence mechanism by using methods of the PeristenceManager.

Use the `setProperty()` and `getProperty()` methods to write and read
infomration in the local shared object. Call the `load()` method to initialize
the PeristenceManager. Call the `save()` methods to write any data to disk.

> **Note:** When the `persistNavigatorState` property is `false`, Flex does not
> automatically save the view stack of the current ViewNavigator when the
> aplication quits, or restore it when the application starts.

### Handle persistence events

You can use the following events of the mobile application containers to develop
a custom persistence mechanism:

- `navigatorStateSaving`

- `navigatorStateLoading`

You can cancel the saving of an applications state to disk by calling the
`preventDefault()` method in the handler for the `navigatorStateSaving` event.
Cancel application loading on restart by calling the `preventDefault()` method
in the handler for the `navigatorStateLoading` event.

### Customize the persistence mechanism

When session persistence is enabled, the application opens to the view that was
displayed when the application quit. You must store enough information in the
view's `data` property, or elsewhere such as in a shared object, to be able to
completely restore the application state.

For example, the restored view might have to perform calculations based on the
view's `data` property. Your application must then recognize when the
application restarts, and perform the necessary calcualtions. One option is to
override the `serializeData()` and `deserializePersistedData()` methods of the
View to perform your own actions when the application quits or restarts.

**Built-in data type support for session persistence**

The persistence mechanism automatically supports all built-in data types,
including: Number, String, Array, Vector, Object, uint, int, and Boolean. These
data types are automatically saved by the persistence mechanism.

**Custom class support for session persistence**

Many applications use custom classes to define data. If a custom class contains
properties defined by the built-in data types, the persistence mechanism can
automatically save and load the class. However, you must first register the
class with the persistence mechanism by calling the
[flash.net.registerClassAlias()](<https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/package.html#registerClassAlias()>)
method. Typically you call this method in the `preinitialize` event of the
application, before the persistence storage is initialized or any data is saved
to it.

If you define a complex class, one that uses data types other than the built-in
data types, you must convert that data to a supported type, such as a String.
Also, if the class defines any private variables, they are not automatically
persisted. To support the complex class in the persistence mechanism, the class
must implement the
[flash.utils.IExternalizable](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/utils/IExternalizable.html)
interface. This interface requires that the class implements the
`writeExternal()` and `readExternal()` methods to save and restore an instance
of the class.
