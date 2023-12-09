# WinExeCommander	
WinExeCommander is an AutoHotkey script to simplify the execution of functions upon process/window creation/termination and device connection/disconnection.

- [Requirement](#requirement)
- [Features](#features)
- [Supported devices](#supported-devices)
- [How to use it?](#how-to-use-it)
- [Event Parameters](#event-parameters)
	- [Window Parameters](#window-parameters)
  	- [Process Parameters](#process-parameters)
  	- [Device Parameters](#device-parameters)

## Requirement
* AutoHotkey v2

## Features
* Execute fonctions upon:
  - Process creation/termination.
  - Window creation/termination.
  - Device connection/disconnection.

* Select from various criteria, including wintitle, winclass, process name, process path, active/maximize/hidden window and additional parameters.
* Enable or disable the monitoring of individual events using the tray menu, user interface (GUI), or method call.
* Save profiles and load them via the tray menu, user interface (GUI), or method call.
* Themes Customization.

## Supported devices
USB, Bluetooth, HDMI etc...

## How to use it?

* Add an Event
  - Double-click the tray icon or right-click on it and choose "Event Manager".
  - Click the "Add Event" button.
  - Choose Window, Process, or Device from the top dropdown list.
  - To fill the edit fields, you can manually enter data, double-click on a listview item, or right-click on an item and select "Copy Row Data to Edit Fields".
  - Some programs generate various windows and processes, some of which can be visible or hidden and may share the same name. This has the potential to cause confusion when the mode is set to 1, as the event function may execute multiple times. To eliminate this potential confusion, the default mode is set to 2.

* Edit an Event
  - Either double-click on it in the list or right-click and choose "Edit Event".
  
* Write a function associated with the event.
  - In the file WinExeCommander.ahk, create a function to be called when the event is created or terminated. Append "_Created" or "_Terminated" to the event function name.

For example:
 
Function name:
Notepad
 
	Notepad_Created(mEvent)
	{
		<Insert code here>
	}
	
	Notepad_Terminated(mEvent)
	{
		<Insert code here>
	}	
	
* Reload the script.	

* To identify a device
  - Open the "Event Manager"
  - Click "Add Event"
  - In the device section, check if the device is listed.
  - Alternatively, run "DeviceInfoFinder.ahk", found in the "Tools" tray menu, menubar, and the device section.
  
* Loading Profiles
  - The profile contains events, period WMI and the windows events. By default, when loading a profile, the existing events will remain the same, and only the event states are loaded. In the settings, you can choose whether to load the period WMI and windows events or not. Enabling "Replace All Events" will replace all existing events with those from the profile.

* Applying Changes
  - To apply modifications, make sure to click the "Apply" button after creating or modifying an event, changing the WMI period, loading a profile from the event manager GUI etc...

* Themes Creation
  - If not already present, create a "Themes" folder in the root directory.
  - Within that folder, create another folder and place 14 icons named: "about", "checkmark", "edit", "events", "exit", "folder", "loading", "main", "plus", "profile", "reload", "select", "settings", "tools".
  - To apply, select it from the dropdown menu in the settings. 

* Notification Sounds
 - If not already present, create a "Sounds" folder in the root directory. 
 - Place WAV files within that folder.
 
* Start with Windows
  - To automatically run this script on startup, add its shortcut to the Startup folder.  
  
  
## Event Parameters
  > - **Event Name**
  >
  > - **Function**
  >    - The name of the function to call upon event creation or termination. To call the function, append "_Created" or "_Terminated" to the function name.
  >
  > - **Tooltip**
  >    - Display a tooltip in the top-left corner containing event information upon event creation or termination.
  >  
  > - **Notify**
  >    - Display a notification GUI in the bottom-right corner upon event creation or termination.
  >  
  > - **Log**
  >    - Write the event information to 'EventsLog.txt' upon event creation or termination.
  >   
  > - **Sound**
  >    - Notification Sounds upon event creation or termination.


### Window Parameters
  > - **WinTitle**
  > - **WinClass**
  > - **Process Name**
  > - **Process Path**
  > 
  > - **WinTitleMatchMode**   
  >    - **1:** A window's title must start with the specified WinTitle to be a match.
  >    - **2:** A window's title can contain WinTitle anywhere inside it to be a match. (Default)
  >    - **3:** A window's title must exactly match WinTitle.
  >    - **RegEx:** Regular expression WinTitle matching.
  >	
  > - **DetectHiddenWindows** 
  >    - **0:** Hidden windows are not detected. (Default)
  >    - **1:** Hidden windows are detected.
  > 
  > - **WinActive**   
  >    - **0:** Not monitoring if the window is active or not. (Default)
  >    - **1:** Call "Function_Created" on window activation. Call "Function_Terminated" when it deactivates. Setting WinActive to 1 automatically sets the mode to 4, and vice versa.
  > 
  > - **WinMinMax** 
  >    - **Null:** Not monitoring WinMinMax
  >    - **0:** The window is neither minimized nor maximized.
  >    - **1:** The window is maximized.
  >    - **-1:** The window is minimized.
  >    - **Limitation:** Only one window can be monitored.
  >   
  > - **Monitoring** 
  >    - **WinEvent** (Default)
  >        - SetWinEventHook. Sets an event hook function for a range of Windows Events.
  >    - **Timer**
  >        - Check for the existence of the window at a specified time interval.
  >
  > - **Mode** 			
  >    - **1:** Call "Function_Created" for every window ID created. Call "Function_Terminated" for every window ID terminated.
  >    - **2:** Call "Function_Created" only for the initial window ID created. Call "Function_Terminated" only when the last window ID is terminated. (Default)	
  >    - **3:** Call "Function_Created" for every window ID created. Call "Function_Terminated" only when the last window ID is terminated.		
  >    - **4:** Call "Function_Created" for every window created. Call "Function_Terminated" for every window terminated.
  >    - **5:** Call "Function_Created" only for the initial window created. Call "Function_Terminated" only when the last window is terminated.
  >    - **6:** Call "Function_Created" for every window created. Call "Function_Terminated" only when the last window is terminated.
  >    
  >    *Some programs generate various windows, some of which can be visible or hidden. This has the potential to cause confusion when the mode is set to 1, as the event function will execute multiple times. To eliminate this potential confusion, the default mode is set to 2. 
  >   
  > - **Period/Delay**
  >    - Period: The interval (in milliseconds) to check for the window's existence.
  >    - Delay (WinEvent): The approximate delay (in milliseconds) for checking the existence of the window after a window event message is fired by the SetWinEventHook function.


* Window Event Information
  - An example of window event information that can be retrieved when a window event is created or terminated.
		
  		[detectHiddenWindows] => 0
		[elevated] => 0
		[eventName] => Explorer_Columns_Fit
		[eventType] => window
		[function] => Explorer_Columns_Fit
		[id] => 7341506
		[log] => 1
		[mode] => 4
		[monitoring] => WinEvent
		[period] => 125
		[pid] => 1168
		[processName] => explorer.exe
		[processPath] => C:\Windows\explorer.exe
		[status] => terminated
		[tooltip] => 0
		[winActive] => 1
		[winClass] => CabinetWClass
		[winMinMax] => 
		[winTitle] => Exes
		[winTitleMatchMode] => 2
  

### Process Parameters
  > - **Process Name**
  > - **Process Path**
  >
  > - **Monitoring** 
  >    - **WMI** (Default)
  >    		- Check for the existence of the process at a specified time interval using WMI Provider Host process.
  >    - **Timer**
  >        - Check for the existence of the process at a specified time interval using Autohotkey SetTimer function.
  >
  > - **Period**
  >    - Period: The interval (in milliseconds) to check for the presence of the process.
  >
  > - **Mode**
  >    - **1:** Call "Function_Created" for every process ID created. Call "Function_Terminated" for every process ID terminated.
  >    - **2:** Call "Function_Created" only for the initial process ID created. Call "Function_Terminated" only when the last process ID is terminated. (Default)
  >    - **3:** Call "Function_Created" for every process ID created. Call "Function_Terminated" only when the last process ID is terminated.
  > 
  >    * Some programs generate various processes with the same name. This has the potential to cause confusion when the mode is set to 1, as the event function will execute multiple times. To eliminate this potential confusion, the default mode is set to 2.
  
* Process Event Information:
  - An example of process event information that can be retrieved when a process event is created or terminated.

		[cmdLine] => "C:\Program Files\Google\Chrome\Application\chrome.exe" --type=renderer --extension-process
		[elevated] => 0
		[eventName] => Chrome_exe
		[eventType] => process
		[function] => Chrome_exe
		[log] => 1
		[mode] => 1
		[monitoring] => WMI
		[period] => 1500
		[pid] => 15244
		[processName] => chrome.exe
		[processPath] => C:\Program Files\Google\Chrome\Application\chrome.exe
		[status] => terminated
		[tooltip] => 0


### Device Parameters
  > - **DeviceName**
  >    - Names of the device.
  >
  > - **DeviceID**
  >    - ID of the device.
  >
  > - **Monitoring** 
  >    - **DeviceChange** (Default)
  >        - Send message notifications when there is a change to the hardware configuration of a device or the computer.
  >    - **Timer**
  >        - Check for the existence of the window at a specified time interval.
  > 
  > - **Period/Delay**
  >    - Period: The interval (in milliseconds) to check for the device's existence.
  >    - Delay (DeviceChange): The approximate delay (in milliseconds) for checking the existence of the device after a device event message is fired by the DeviceChange function.
  >  
  > - **Mode**
  >    - **1:** Call "Function_Created" for every device connected. Call "Function_Terminated" for every device disconnected. (Default)
  >    - **2:** Call "Function_Created" only for the initial device connected. Call "Function_Terminated" only when the last device is disconnected.
  >    - **3:** Call "Function_Created" for every device connected. Call "Function_Terminated" only when the last device is disconnected.
  
 
* Device Event Information:
  - An example of device event information that can be retrieved when a device event is created or terminated.
 
		[deviceId] => SWD\MMDEVAPI\{0.0.0.00000000}.{3278E776-26F1-4931-AFFB-06D6C653C12E}
		[deviceName] => A90 Pro (A90 Pro Stereo)
		[eventName] => Bluetooth_Earbuds
		[eventType] => device
		[function] => Bluetooth_Earbuds
		[logToFile] => 1
		[mode] => 1
		[monitoring] => DeviceChange
		[period] => 1250
		[status] => created
		[tooltip] => 1
  
  
  
# Methods


## SetProfile

	SetProfile(Profile Name)
  
  > - **Profile Name**	
  >    - Type: String
  
For example:

	!1::WinExeCmd.SetProfile('Disable All Events')


## SetEvent
	SetEvent(State, Event Name)

  > - **State**
  >    - Type: Integer or String
  >    - **0:** Disable
  >    - **1:** Enable
  >
  > - **Event Name**
  >    - Type: String

For example:

	!2::WinExeCmd.SetEvent(1, 'Calculator_WinSetAlwaysOnTop')	
	
	
## SetEventMonitoring
	SetEventMonitoring(EventName, Monitoring, Period)

  > - **EventName**
  >    - Type: String
  >    - Name of the Event.
  >
  > - **Monitoring**
  >    - Type: String, Case-sensitive
  >    - Method for Monitoring event. Process (Timer or WMI), Window (Timer or WinEvent) and Device (Timer or DeviceChange)
  >  
  > - **Period/Delay**
  >    - Type: Integer or String
  >    - Period: The interval (in milliseconds) to check for the event's existence.
  >    - Delay (WinEvent, DeviceChange): The approximate delay (in milliseconds) to check for the event's existence.

For example:
	
	^o:: WinExeCmd.SetEventMonitoring('Notepad, 'WinEvent', 1500)


## SetPeriodWMI
	SetPeriodWMI(Period)

  > - **Period**
  >    - Integer or String
  
 For example:
  
	!o:: WinExeCmd.SetPeriodWMI(2000)


## ProcessFinder
Returns an array containing objects with all existing processes that match the specified parameters. If there are no matching processes, an empty array is returned.
        
	ProcessFinder(ProcessName, ProcessPath) 

  > - **Process Name**
  >    - Type: String
  > 
  > - **Process Path**
  >    - Type: String    

For example:

	^8:: 
	{
		aObjProcessFinder := WinExeCmd.ProcessFinder("notepad.exe") 
		Tooltip(WinExeCmd.Displayobj(aObjProcessFinder), 0, 0), SetTimer(ToolTip, -8000)
	}


## WindowFinder
Returns an array containing objects with all existing windows that match the specified parameters. If there are no matching windows, an empty array is returned.
        
	WindowFinder(WinTitle, WinClass, ProcessName, ProcessPath, WinTitleMatchMode, DetectHiddenWindows, WinActive, WinMinMax)

  > - **WinTitle**
  >    - Type: String
  >
  > - **WinClass**
  >    - Type: String
  >
  > - **Process Name**
  >    - Type: String
  >
  > - **Process Path**
  >    - Type: String
  > 
  > - **WinTitleMatchMode**
  >    - Type: Integer or String
  >    - **1:** A window's title must start with the specified WinTitle to be a match.
  >    - **2:** A window's title can contain WinTitle anywhere inside it to be a match. (Default)
  >    - **3:** A window's title must exactly match WinTitle.
  >    - **RegEx:** Regular expression WinTitle matching.
  > 
  > - **DetectHiddenWindows**
  >    - Type: Integer or String
  >    - **0:** Hidden windows are not detected. (Default)
  >    - **1:** Hidden windows are detected.
  > 
  > - **WinActive**
  >    - Type: Integer or String
  >    - **0**
  >    - **1**  
  > 
  > - **WinMinMax**
  >    - Type:Integer or String
  >    - **0:** The window is neither minimized nor maximized.
  >    - **1:** The window is maximized.
  >    - **-1:** The window is minimized.  
  
For example:
        
	^9:: 
	{
		aObjWindowFinder := WinExeCmd.WindowFinder(, 'Chrome_WidgetWin_1', 'chrome.exe') 
		Tooltip(WinExeCmd.Displayobj(aObjWindowFinder), 0, 0), SetTimer(ToolTip, -8000)
	}


## DeviceFinder
Returns an array containing objects with the device matching the specified parameters. If there are no matching device, an empty array is returned.

	DeviceFinder(DeviceName, DeviceID)
  
String
  
  > - **DeviceName**
  >    - Names of the device.
  >
  > - **DeviceID**
  >    - ID of the device.

For example:

 	^0::
	{
		aObjDeviceFinder := WinExeCmd.DeviceFinder(,'USBSTOR\DISK&VEN_KINGSTON&PROD_DATATRAVELER_3.0&REV_\E0D55EA573DCF450E97C104C&0')
		Tooltip(WinExeCmd.Displayobj(aObjDeviceFinder), 0, 0), SetTimer(ToolTip, -8000)
	}
  
Check if device is connected:  
 	
	if DeviceFinder(,'SCSI\DISK&VEN_WDC&PROD_WD15EARX-22PASB0\5&25248246&0&000000').Length
 	 	MsgBox('The device is connected')
  
  
 ## IsProcessElevated(PID)
 Check if a process is elevated.
  
  > - **PID**
  >    - Type: Integer
  
  For example:
  
	MsgBox IsProcessElevated(25884)
  
  
 ## GetCommandLine(PID)
 Retrieves a start-up command-line of an application
  
  > - **PID**
  >    - Type: Integer
  
 For example:
  
	MsgBox GetCommandLine(25884)
  
 
 
# Known Issue, Limitation, Additional Notes

- How do I work around problems caused by User Account Control (UAC)?
By default, User Account Control (UAC) protects "elevated" programs (that is, programs which are running as admin) from being automated by non-elevated programs, since that would allow them to bypass security restrictions. Common workarounds can be found here:

Frequently Asked Questions (FAQ)
https://www.autohotkey.com/docs/v2/FAQ.htm




- Since AHK is not multithreaded It is strongly reccomended lauch another script when event function execute
The script is constanly checking/looping through all the events

AHK Single threaded

Priority is assigned to critical monitoring methods, which may result in GUIs freezing briefly and not resizing properly.




## Window
- WinEvent, When Universal Windows Platform (UWP) apps are maximized or unmaximized, WinMinMax monitoring fails to function correctly. This is the result of the SetWinEventHook function not sending messages thus the function not being called.

## Device
- The device ID of certain devices might change. I'm not sure which device ID is affected or the reason behind it. I tested about a dozen devices, and the issue only occurred with a TV connected via HDMI.



## Process

Caveat: It's absolutely essential that Sink.Cancel is called. If the script terminates unexpectedly, WMI will continue to poll in the background, and restarting the WMI service is the only way to get rid of the polling loop.

If the script closes abruptly, the script's WMI event registrations might not unregister properly. 
This can cause "WMI Provider Host" (WmiPrvSE.exe) to continue consuming CPU usage even if the script is no longer running. You can monitor it 
by checking the CPU usage of "WMI Provider Host" in Task Manager. To restore "WMI Provider Host" to its normal behavior, you can either restart the 
Windows Management Instrumentation service or restart the computer.

Restart wmi button

Press the Windows Key + R, type in services.msc and press Enter. Locate the Service    Windows Management Instrumentation to WMI Performance Adapter (Windows changes the wmi service name ?)

Command to restart the Windows Management Instrumentation service:
RunWait('*RunAs Powershell.exe -Command "Restart-Service -Name winmgmt -Force"',, 'Hide')

Fix with window update ?

These window updates below seem to have fix this issue of duplicate WMI event registrations mentionned above.
orphaned WMI events

November 14, 2023—KB5032189 (OS Builds 19044.3693 and 19045.3693)
November 14, 2023-KB5032339 Cumulative Update for .NET Framework 3.5, 4.8 and 4.8.1 for Windows 10 Version 22H2



## Donation (PayPal)
  - If you found this script useful and would like to donate. It would be greatly appreciated. Thank you!
    https://www.paypal.com/paypalme/martinchartier  

## Credits
* **AutoHotkey**
  - Authors: Chris Mallett and Steve Gray (Lexikos), with portions by AutoIt Team and various AHK community members.
  - License: GNU General public license
  - Info and source code at: https://autohotkey.com/
  
* **JSON.ahk by thqby, HotKeyIt.**
  - https://github.com/thqby/ahk2_lib/blob/master/JSON.ahk
  - https://github.com/HotKeyIt/Yaml
  
* **EnumDeviceInfo by teadrinker. (based on JEE_DeviceList by jeeswg)**
  - https://www.autohotkey.com/boards/viewtopic.php?t=121125&p=537515  
  
* **GetCommandLine by teadrinker. (based on Sean and SKAN v1 code)**
  - https://www.autohotkey.com/boards/viewtopic.php?p=526409#p526409
  - https://www.autohotkey.com/board/topic/15214-getcommandline/
	
* **WTSEnumProcesses by SKAN.**
  - https://www.autohotkey.com/boards/viewtopic.php?t=4365	
	
* **GuiButtonIcon by FanaticGuru.**	
  - https://www.autohotkey.com/boards/viewtopic.php?f=83&t=115871
  
* **DisplayObj by FanaticGuru. (inspired by tidbit and Lexikos v1 code)**
  - https://www.autohotkey.com/boards/viewtopic.php?p=507896#p507896
 
* **IsProcessElevated by jNizM**    
  - https://github.com/jNizM/ahk-scripts-v2/blob/main/src/ProcessThreadModule/IsProcessElevated.ahk
 
* **HasVal by jNizM.**
  - https://www.autohotkey.com/boards/viewtopic.php?p=109617#p109617

* **MoveControls by Descolada. (from UIATreeInspector.ahk)**
  - https://github.com/Descolada/UIA-v2
  
* **Code snippets taken from NotifyV2 by the-Automator.com**
  - https://www.the-automator.com/downloads/maestrith-notify-class-v2/ 
