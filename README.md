# DeviceIDFinder
This AutoHotkey script allows to find your device's unique IDs.

### Requirement
* AutoHotkey v2

# MyEventsToMonitor
This AutoHotkey script allows for the automatic launching of actions when devices are connected or disconnected, and when processes or windows are created or terminated.

### Can monitor
* Device or groups of devices are connected or disconnected.
* Process or a group of processes are created or terminated.
* Window or a group of windows matching multiple criterias are created or terminated.
* Mix of processes and windows in one "event".

### Can't monitor
* Combining devices, processes, and windows in one "event" is not supported (It can be done by manual coding in "MyEventsActions()").
* Active Window.

### Examples, automatically :
* Launching steam when a bluetooth controller is connected.
* Switching audio when a device is connected or disconnected.
* Launching or closing a program when another one is launching or closing.
* Overclocking the GPU/CPU when a game is running. Undervolting when no game are running. (With MSI Afterburner's profiles)

### Supported devices
* USB, Bluetooth, HDMI etc...

### Instructions

* Add your device's IDs, processes, windows and "Eventname" that you want to monitor at the top of the script. You can name them whatever you want.
* In the function "MyEventsActions()". Add the "Eventname" and the actions when the events are created or terminated.
* DeviceID, Process and Window categories value required to be wrap in square brackets.
* An "event" must be created or terminated for at least 1 second to trigger a "Created" or terminated event.

An "EventName" is automatically assign when an event only contains one category and one "Process" or one category and one "Window" property:

        MyEvents.Add({Process:["wordpad.exe"], Tooltip:"false"})
        ...
        if thisEventStatus = "wordpad.exe Created"
        ...
        if thisEventStatus = "wordpad.exe Terminated"
        ...

        MyEvents.Add({Window:[{WinTitle:"Disk Management"}], ActionAtStartup:"false"})
        ...
        if thisEventStatus = "Disk Management Created"
        ...
        if thisEventStatus = "Disk Management Terminated"
        ...

An "EventName" is required in all other cases.

### Options

* **EventName**

Name of the event. The same name is used to launch the associated event's actions. Do not use quotation marks in the "EventName".

* **DeviceID**

IDs for the device(s).

  - For one device.

        MyEvents.Add({EventName:"EventName", DeviceID:["DeviceID"]})
        
  - For group of devices.

        MyEvents.Add({EventName:"EventName", DeviceID:["DeviceID", "DeviceID"], DeviceIDGroupMode:2})
        
* **Window properties options**
  - WinTitle
  - WinClass
  - WinTitleMatchMode
    - 1 = A window's title must start with the specified WinTitle to be a match.
    - 2 = A window's title can contain WinTitle anywhere inside it to be a match.
    - 3 = A window's title must exactly match WinTitle to be a match. (Default)
    - RegEx = Regular expression WinTitle matching.
  - detectHiddenWindows
    - 1 = On:  Hidden windows are detected
    - 2 = Off: Hidden windows are not detected (Default).

* **DeviceIDGroupMode, ProcessGroupMode, WindowGroupMode**

  - 1 = All the items in the category must be created (Default).

  - 2 = One item in the category must be created.

* **ActionAtStartup**

  - true = The event's actions are launched when the script starts (Default). 

  - false = The event's actions are not launched when the script starts.

* **Tooltip**

  - true = Show the tooltip in the top left corner (Default).

  - false = Don't show the tooltip in the top left corner.

* **Example**
    
	MyEvents.Add({EventName:"EventName", DeviceID:["DeviceID", "DeviceID"], DeviceIDGroupMode:2, ActionAtStartup:"false", Tooltip:"false"})

	MyEvents.Add({
		EventName:"OSK/Weather notepad/mspaint",
		Window:[{WinTitle:"On-Screen Keyboard", WinClass:"OSKMainClass"}, {WinTitle:"Weather", WinClass:"ApplicationFrameWindow"}],
		Process:["notepad.exe", "mspaint.exe"],
		ProcessGroupMode:1,
	})


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
