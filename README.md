# DeviceIDFinder
AutoHotkey script to find your device's unique IDs.

# DeviceIDPnP
AutoHotkey script to launch scripts when devices are connected/disconnected.

### Requirement
* AutoHotkey v2

### New
* Updated to AutoHotkey v2.
* Support for the same actions for multiple devices and "DevicesMatchMode" option.
* Option to not launch the device's actions when the script starts.
* Option to show or hide ToolTips in the top left corner.

### Instructions

* Run "DeviceIDFinder.ahk" to identify your devices.
* Add your device's IDs and device's names at the top of the script (DeviceIDPnP.ahk). The device's names doesn't have to exactly match the names found with "DeviceIDFinder.ahk". You can name them whatever you want.
* Add the device's names and the scripts that you want to launch when the devices are connected/disconnected.

### Options

* **DeviceName:**

Names of the device(s). Use the same name to launch the associated device's actions.

* **DeviceID:**

IDs for the device(s).

  - For one device:

        MyDevices.Add({DeviceName:"DeviceName", DeviceID:"DeviceID"})
        
  - For multiple devices: Use |&| as a separator.

        MyDevices.Add({DeviceName:"DeviceName", DeviceID:"DeviceID |&| DeviceID"})

* **DeviceMatchMode**

  - 1 = All the devices in "DeviceID" must be connected (Default).

  - 2 = One device in "DeviceID" must be connected.

* **ActionAtStartup**

  - true = The device's actions are launched when the script starts (Default). 

  - false = The device's actions are not launched when the script starts.

* **Tooltip**

  - true = Show the tooltip in the top left corner. (Default). 

  - false = Don't show the tooltip in the top left corner.

### Minor differences from DeviceIDPnP 1.2.0:

* **Syntax changes**

      oMyDevices.Push({"DeviceName":"DeviceName", "DeviceID":"DeviceID"}) 
       
      Now => MyDevices.Add({DeviceName:"DeviceName", DeviceID:"DeviceID"})

      DevicesActions(ThisDeviceStatusHasChanged) 

      Now => DevicesActions(thisDeviceStatus)
  
* **Copyright and License**
  - MIT License

### Credits:
* **AutoHotkey**
  - Authors: Chris Mallett and Lexikos, with portions by AutoIt Team and various AHK community members.
  - License: GNU General public license
  - Info and source code at: https://autohotkey.com/
* **jNizM**
  - Example 2: Detect / Monitor Plug and Play device connections and removes.
  - https://www.autohotkey.com/boards/viewtopic.php?f=83&t=105171

* **Thanks to AHK community members for the help**
  - mikeyww, teadrinker, swagfag, FanaticGuru, sofista, boiler etc...

* **Donations (PayPal)**
