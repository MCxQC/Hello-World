# DeviceIDFinder
This AutoHotkey script allows to find your device's unique IDs.

### Requirement
* AutoHotkey v2

# MyEventsToMonitor
This AutoHotkey script allows for the automatic launching of actions when devices are connected or disconnected, and when processes or windows are created or terminated.

### Can monitor the following events
* Device or groups of devices are connected or disconnected.
* Process or a group of processes are created or terminated.
* Window or a group windows matching multiple criterias are created or terminated.
* Mix of process(es) and window(s)

### Can't monitor
* Mix of device(s), process(es) and window(s) in a single "Event" (It can be done by manual coding in "MyEventsActions").

### Supported devices
* USB, Bluetooth, HDMI etc...

### Instructions

* **Device**
* Run "DeviceIDFinder.ahk" to identify your devices.**
* Add your device's IDs and "Eventname" at the top of the script (DeviceIDPnP.ahk). You can name them whatever you want.
* Add the "Eventname" and the actions that you want to launch when the devices are connected or disconnected.

* **Process(es) and window(s)**

### Options

* **EventName**

Name of the event. The same name is used to launch the associated event's actions.

* **DeviceID**

IDs for the device(s).

  - For one device.

        MyEvents.Add({EventName:"EventName", DeviceID:["DeviceID"]})
        
  - For group of devices.

        MyEvents.Add({EventName:"EventName", DeviceID:["DeviceID", "DeviceID"], DeviceIDGroupMode:2})
        
* **Window properties**
  - WinTitle
  - WinClass
 
  - WinTitleMatchMode
    * 1 = A window's title must start with the specified WinTitle to be a match.
    * 2 = A window's title can contain WinTitle anywhere inside it to be a match.
    * 3 = A window's title must exactly match WinTitle to be a match. (Default)
  * RegEx = Regular expression WinTitle matching.

  - detectHiddenWindows
* 1 = On:  Hidden windows are detected
* 2 = Off: Hidden windows are not detected (Default).

* **DeviceIDGroupMode, ProcessGroupMode, WindowGroupMode**

  - 1 = All the items in the category must be created (Default).

  - 2 = One item in the category must be terminated.

* **ActionAtStartup**

  - true = The event's actions are launched when the script starts (Default). 

  - false = The event's actions are not launched when the script starts.

* **Tooltip**

  - true = Show the tooltip in the top left corner (Default).

  - false = Don't show the tooltip in the top left corner.

* **Options example**
    
      MyEvents.Add({DeviceName:"DeviceName", DeviceID:["DeviceID", "DeviceID"], DeviceIDGroupMode:2, ActionAtStartup:"false", Tooltip:"false"})

### Donations (PayPal)
  - If you found this script useful and would like to donate. It would be greatly appreciated. Thank you! :smiley:
    https://www.paypal.com/paypalme/martinchartier
  
### Copyright and License
  - MIT License

### Credits
* **AutoHotkey**
  - Authors: Chris Mallett and Steve Gray (Lexikos), with portions by AutoIt Team and various AHK community members.
  - License: GNU General public license
  - Info and source code at: https://autohotkey.com/
* **jNizM**
  - DeviceIDFinder is a modified version of his script. (Example 2: Detect / Monitor Plug and Play device connections and removes)
    https://www.autohotkey.com/boards/viewtopic.php?f=83&t=105171

* **Thanks to AHK community members for the help**
  - mikeyww, teadrinker, swagfag, just me, jNizM, FanaticGuru, sofista, boiler and others.
