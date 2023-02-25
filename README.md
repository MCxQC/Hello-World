# DeviceIDPnP 2.0.0
AutoHotkey script to launch scripts when devices are connected/disconnected.

# DeviceIDFinder 2.0.0
AutoHotkey script to find your device's unique IDs.

### Requirement:
* AutoHotkey v2

### New:
* Updated to AutoHotkey v2.
* Support for the same actions for multiple devices and "DevicesMatchMode" option.
* Option to not launch the device's actions when the script starts.

### Instructions:

* Run "DeviceIDFinder.ahk" to identify your devices.
* Add your device's IDs and device's names at the top of the script (DeviceIDPnP.ahk). The device's names doesn't have to exactly match the names found with "DeviceIDFinder.ahk". You can name them whatever you want.
* Add the device's names and the scripts that you want to launch when the devices are connected/disconnected.

### Options:

* **DeviceName:**

Name of device. The device's name doesn't have to exactly match the name found with "DeviceIDFinder.ahk". You can name it whatever you want.
Use the same name to launch the device's actions.

* **DeviceID:**

ID(s) of device(s).

For one device:

MyDevices.Push({DeviceName:"DeviceName", DeviceID:"DeviceID"})

For multiple devices: Use |&| as a separator.

MyDevices.Push({DeviceName:"DeviceName", DeviceID:"DeviceID |&| DeviceID"})

* **DeviceMatchMode:**

1 = All devices in "DeviceID" must be connected (Default).

2 = One device in "DeviceID" must be connected.

* **RunAtStartup:**

true = The device's actions are launched when the script starts (default). 

false = The device's actions are not launched when the script starts.


### Minor differences from DeviceIDPnP 1.2.0:
* **Removed tooltips.**

* **Syntax changes:**

oMyDevices := {} 

Now => MyDevices := []


oMyDevices.Push({"DeviceName":"DeviceName", "DeviceID":"DeviceID"}) 

Now => MyDevices.Push({DeviceName:"DeviceName", DeviceID:"DeviceID"})


DevicesActions(ThisDeviceStatusHasChanged) 

Now => DevicesActions(deviceNameStatus)
