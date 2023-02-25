# DeviceIDPnP 2.0.0
AutoHotkey script to launch scripts when devices are connected/disconnected.

### Requirement:
* AutoHotkey v2

### New:
* Support for the same actions for multiple devices and "DevicesMatchMode" option.
* Option to not run actions when the script starts/run actions when the script starts(Default).

### Options:

* DeviceName:

Name of device. The device's name doesn't have to exactly match the name found with "DeviceIDFinder.ahk". You can name it whatever you want.
associated action launch

* DeviceID:

ID(s) of device(s).
MyDevices.Push({DeviceName:"DeviceName", DeviceID:"DeviceID"})

For multiple devices:
MyDevices.Push({DeviceName:"DeviceName", DeviceID:"DeviceID |&| DeviceID"})

* DeviceMatchMode:

1 = All devices in "DeviceID" must be connected (Default).

2 = One device in "DeviceID" must be connected.

* RunAtStartup:

true = Launch device's actions when the script starts (Default). 
false = Don't Launch device's actions when the script starts.


### Minor differences from DeviceIDPnP 1.2.0:
* Removed tooltips.

* Syntax changes:
oMyDevices := {} 

Now => MyDevices := []


oMyDevices.Push({"DeviceName":"DeviceName", "DeviceID":"DeviceID"}) 

Now => MyDevices.Push({DeviceName:"DeviceName", DeviceID:"DeviceID"})


DevicesActions(ThisDeviceStatusHasChanged) 

Now => DevicesActions(deviceNameStatus)
