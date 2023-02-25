# DeviceIDPnP 2.0.0
AutoHotkey script to launch scripts when devices are connected/disconnected.

# DeviceIDFinder 2.0.0
Find your device's unique IDs.

### Requirement:
* AutoHotkey v2

### New:
* Support for the same actions for multiple devices and "DevicesMatchMode" option.
* Option to not run actions when the script starts/run actions when the script starts (Default).

### Instructions:

* **How to use:**
* Run "DeviceIDFinder.ahk" to identify your device.
* Add your devices IDs and devices names at the top of the script. (DeviceIDPnP.ahk) The device's name doesn't have to exactly match the name found with "DeviceIDFinder.ahk". You can name it whatever you want.
* Add the devices names and the scripts/programs that you want to run/close when the devices are connecting/disconnecting.

### Options:

* **DeviceName:**

Name of device. The device's name doesn't have to exactly match the name found with "DeviceIDFinder.ahk". You can name it whatever you want.
associated action launch

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
