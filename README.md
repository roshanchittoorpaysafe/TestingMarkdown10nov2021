This document describes interfaces that are provided to access different aspects of the Gravity subsystem. These API&#39;s make it easy for a application developers to access various communications and database layers that are contained within the Gravity subsystem.

The interface to the Network Manager subsystems allows applications to access what devices are available on the mesh network as well as the capabilities of those devices to support various functions.

Interfacing to the Network Manager app on the Android platform, from other external apps, will be primarily through the use of Intents. To send messages to the Network Manager there are specific API calls that will package all of the data in the proper manner and send those messages via the Intent mechanism provided on the Android platform. It will be up to the application developer to configure and code a BroadcastReceiver() that will receive the response Intents from the Network Manager. Based on the type of response that is received there are specific API calls that will process that data and it will be returned to the application in easily processed objects. The specifics of these interfaces are defined later in this document for each API.

Later in this document are some example code that will help to clarify any questions on how to use the Network Manager API&#39;s.

> **NetworkManager class**

>> **class NetworkManager**

This is the main interface class that apps should use to communicate to the Network Manager. Any application that desires to interface to the Network Manager needs to create an instance of this class for use later.

```
public static NetworkManager get\_instance()
```

This method is a factory method to a global instance of the Network Manager class. This method MUST be called before any other methods as it is the only way to receive an instance of the class.

The Network Manger is a singleton type object that can be shared across all threads within the application. This class is thread safe so all threads that use this single instance do not have to write specific thread safe code when using the interfaces within this object.

> **Return:** Returns instance of the Network Manager class.

```
public void initialize(Context applicationContext)
```

This method can be called only once, and it is recommended that it is called immediately after the first call to the &quot; **get\_instance**** ()**&quot; method. This method completes the initialization of the Network Manager object. If it is called more than once it will throw a LibraryAlreadyInitializedException

This is the Android specific initialization call. Other platforms may require different arguments to complete the initialization of the object.

**Parameters:**

   `applicationContext` – allows the app to set the context that

this object is running within as defined in the Android developer documentation. [https://developer.android.com/reference/android/content/Context](https://developer.android.com/reference/android/content/Context)

**Return:** No return value

**Throws:** 
   `InvalidArgumentException`
   `LibraryAlreadyInitializedException`

```
public void requestGravityDevices(int capabilities, String commType)
```

This method allows the application to request a list of available devices on the mesh network. Based on the values of the arguments it is possible for the application to filter the resulting list by various capabilities and/or communications type being used by the devices. The valid values for these arguments are defined within the **NetworkManagerConstants** class defined later in this document.

The returned list will include all Gravity enabled devices regardless of the devices connection status to the mesh network.

**Parameters:**

   `capabilities` - This argument allows the application to filter for specifically advertised services on the mesh network. These are the same values as used in the    **addServiceCapability**** (…)** method.

Gravity reserved values are as follows:
     
     * `_CAPABILITY\_NONE_ (0)`
     * `_CAPABILITY\_FILE\_XFER_ (0x01)`
     * `_CAPABILITY\_AUDIO\_STREAMING_ (0x02)`
     * _CAPABILITY\_VIDEO\_STREAMING_ (0x04)
     * _CAPABILITY\_VIDEO\_SERVER (_0x08);
     * _CAPABILITY\_VIDEO\_RECEIVER_ (0x10);
     * _CAPABILITY\_REMOTE\_DESKTOP_ (0x20);
     * _CAPABILITY\_GRAVITY\_SMS_ (0x40);
     * _CAPABILITY\_ALL_ (1048575) or (0xFFFFF)
     

commType - This argument allows the application to request

a comprehensive list of all of the devices

visible on the mesh network or just those

devices that reside on a specific communication

protocol.

Valid values are as follows:

WIFI\_P2P\_COMMUNICATION\_TYPE = &quot;WIFI\_DIRECT&quot;

WIFI\_AP\_COMMUNICATION\_TYPE = &quot;WIFI\_AP&quot;

BLE\_COMMUNICATION\_TYPE = &quot;BLUETOOTH&quot;

UWBW\_COMMUNICATION\_TYPE = &quot;ULTRA\_WIDE&quot;

DEFAULT\_COMMUNICATION\_TYPE = &quot;DEFAULT&quot; \*\*

\*\* - Default value, if parameter is NULL

**Return:** No return value

**Throws:** InvalidArgumentException

LibraryUninitializedException

|
 |
 |
 |
| --- | --- | --- |
