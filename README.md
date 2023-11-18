# WinExeCommander	
WinExeCommander is an AutoHotkey script to simplify the execution of functions upon process/window creation/termination and device connection/disconnection.

## Requirement
* AutoHotkey v2

## Features
* Execute fonctions upon:
  - Process creation/termination.
  - Window creation/termination.
  - Device connection/disconnection.

* Select from various criteria, including WinTitle, WinClass, WinTitleMatchMode, Process Name, Process Path, active/maximize/hidden window and additional parameters.
* Enable or disable the monitoring of individual events using the tray menu, user interface (GUI), or method call.
* Save profiles and load them via the tray menu, user interface (GUI), or method call.
* Themes Customization.

## Supported devices
USB, Bluetooth, HDMI etc...

## How to use it?

* Add an Event
  - Double-click the tray icon or right-click on it and choose 'Event Manager'.
  - Click the "Add Event" button.
  - Choose Window, Process, or Device from the top dropdown list.
  - To fill the edit fields, you can manually enter data, double-click on a listview item, or right-click on an item and select 'Fill Edit Fields with Row Content'.

* Edit an Event
  - Either double-click on it in the list or right-click and choose 'Edit Event'.

* Write a function associated with the Event.
  - Write a function to call when the Event is created and/or terminated. Append '_Created' or '_Terminated' to the event function name.

For example:
 
Function name:
Notepad
 
	Notepad_Created(mEvent)
	{
		<Insert code here>
	}
	
* Reload the script.	

* To identify a device
  - Open the 'Event Manager'
  - Click 'Add Event'
  - In the device section, check if the device is listed.
  - Alternatively, run 'DeviceInfoFinder.ahk', which is accessible from the 'Tools' tray menu item.
  
* Loading Profiles
  - The profile contains Events, Period WMI and the Windows Events. By default, when loading a profile, the existing events will remain the same, and only the event states are loaded. In the settings, you can choose whether to load the Period WMI and Windows Events or not. Enabling 'Replace All Events' will replace all existing events with those from the profile.

* Themes cretation
  - Create a folder named 'Themes' in the root directory if it has not already been created.
  - Within that folder, create another folder and place 14 icons named: 'about', 'checkmark', 'edit', 'events', 'exit', 'folder', 'loading', 'main', 'plus', 'profile', 'reload', 'select', 'settings', 'tools'.
  - To apply, select it from the dropdown menu in the settings.  
  
* Start with Windows

To automatically run this script on startup, add its shortcut to the Startup folder.  
  
## Event Parameters
  > - **Event Name**
  >
  > - **Function**
  >    - The name of the function to call when the Event is created/terminated. To call the function, append '_Created' and/or '_Terminated' to the function name.
  >

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
  >    - **0** Not monitoring if the window is active or not. (Default)
  >    - **1** Call "Function_Created" on window activation. Call 'Function_Terminated' when it deactivates. Setting WinActive to 1 automatically sets the mode to 4, and vice versa.
  > 
  > - **WinMinMax** 
  >    - **Null:** Not monitoring WinMinMax
  >    - **0:** The window is neither minimized nor maximized.
  >    - **1:** The window is maximized.
  >    - **-1:** The window is minimized.
  >    - **Limitation:** only 1 window can be monitored. ?
  >   
  > - **Monitoring** 
  >    - **WinEvent** (Default)
  >        - SetWinEventHook. Sets an event hook function for a range of Windows Events.
  >    - **Timer**
  >        - Check for the existence of the window at a specified time interval.
  >
  > - **Mode** 			
  >    - **1:** Call 'Function_Created' when a new window handle is created. Call 'Function_Terminated' for every window handle terminated. (Default)
  >    - **2:** Call 'Function_Created' only for the initial window handle created. Call 'Function_Terminated' only when the last window handle is terminated.	
  >    - **3:** Call 'Function_Created' when a new window handle created. Call 'Function_Terminated' only when the last window handle is terminated.		
  >    - **4:** Call 'Function_Created' for every window created. Call 'Function_Terminated' for every window terminated.
  >    - **5:** Call 'Function_Created' only for the initial window created. Call 'Function_Terminated' only when the last window is terminated.
  >    - **6:** Call 'Function_Created' for every window created. Call 'Function_Terminated' only when the last window is terminated.
  >   
  > - **Period/Delay**
  >    - Period: The interval (in milliseconds) to check for the window's existence.
  >    - Delay (WinEvent): The maximum delay (in milliseconds) to check for the window's existence.
  >  

* Window Event Information
  - An example of window event information that can be retrieved when a window event is created or terminated.
		
  		[detectHiddenWindows] => 0
		[elevated] => 0
		[eventName] => Explorer_Columns_Fit
		[eventType] => window
		[function] => Explorer_Columns_Fit
		[id] => 7341506
		[logToFile] => 1
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
  >    - **1:** Call 'Function_Created' when a new process ID (PID) is created. Call 'Function_Terminated' for every process ID (PID) terminated. (Default)
  >    - **2:** Call 'Function_Created only for the initial process ID (PID) created. Call 'Function_Terminated' only when the last process ID (PID) is terminated.
  >    - **3:** Call 'Function_Created' for every process ID (PID) created. Call 'Function_Terminated' only when the last process ID (PID) is terminated.


* Process Event Information:
  - An example of process event information that can be retrieved when a process event is created or terminated.

		[cmdLine] => "C:\Program Files\Google\Chrome\Application\chrome.exe" --type=renderer --extension-process
		[elevated] => 0
		[eventName] => Chrome_exe
		[eventType] => process
		[function] => Chrome_exe
		[logToFile] => 1
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
  >    - Delay (DeviceChange): The maximum delay (in milliseconds) to check for the device's existence.
  >  
  > - **Mode**
  >    - **1:** Call 'Function_Created' when a device is connected. Call 'Function_Terminated' for every device matching the evnt criterions is disconnected. (Default)
  >    - **2:** Call 'Function_Created' only for the initial device is connected. Call 'Function_Terminated' only when the last device is disconnected.
  >    - **3:** Call 'Function_Created' when a device is connected. Call 'Function_Terminated' only when the last device is disconnected.
  
 
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
  >    - Type: String, Case-sensitive
  
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
  >    - Type: String, Case-sensitive

For example:

	!2::WinExeCmd.SetEvent(1, 'Calculator_WinSetAlwaysOnTop')	
	
	
## SetEventMonitoring
	SetEventMonitoring(EventName, Monitoring, Period)

  > - **EventName**
  >    - Type: String, Case-sensitive
  >    - Name of the Event.
  >
  > - **Monitoring**
  >    - Type: String
  >    - Method for Monitoring event. Process (Timer or WMI), Window (Timer or WinEvent) and Device (Timer or DeviceChange)
  >  
  > - **Period/Delay**
  >    - Type: Integer or String
  >    - Period: The interval (in milliseconds) to check for the event's existence.
  >    - Delay (WinEvent, DeviceChange): The maximum delay (in milliseconds) to check for the event's existence.

For example:
	
	^o:: WinExeCmd.SetEventMonitoring('Notepad, 'WinEvent', 1500)


## SetWMIperiodInterval
	SetWMIperiodInterval(Period)

  > - **Period**
  >    - Integer or String
  
 For example:
  
	!o:: WinExeCmd.SetWMIperiodInterval(2000)


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
  
  
  
 ## DisplayObj(Obj)
 Display contents of objects
 
  > - **Obj**
  >    - Type: Object
  
  
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
  
	MsgBox IsProcessElevated(25884)
  
 
# Additional Notes

- Since AHK is not multithreaded It is strongly reccomended lauch another script when event function execute
The script is constanly checking/looping through all the events

# Modes
Tooltip debug masure sure function is not trigere twive



- How do I work around problems caused by User Account Control (UAC)?
By default, User Account Control (UAC) protects "elevated" programs (that is, programs which are running as admin) from being automated by non-elevated programs, since that would allow them to bypass security restrictions. Common workarounds can be found here:

Frequently Asked Questions (FAQ)
https://www.autohotkey.com/docs/v2/FAQ.htm

## Device
- The device ID of certain devices might change, so it could be better to select only the device name. I'm not sure which device is affected or the reason behind it. I tested about a dozen devices, and the issue only occurred with a TV connected via HDMI.

# Known Issue:
If the script closes abruptly, the script's WMI event registrations might not unregister properly. 
This can cause "WMI Provider Host" (WmiPrvSE.exe) to continue consuming CPU usage even if the script is no longer running. You can monitor it 
by checking the CPU usage of "WMI Provider Host" in Task Manager. To restore "WMI Provider Host" to its normal behavior, you can either restart the 
Windows Management Instrumentation service or restart the computer.

Restart wmi button

Press the Windows Key + R, type in services.msc and press Enter. Locate the Service    Windows Management Instrumentation to WMI Performance Adapter (Windows changes the wmi service name ?)

Command to restart the Windows Management Instrumentation service:
RunWait('*RunAs Powershell.exe -Command "Restart-Service -Name winmgmt -Force"',, 'Hide')

Fix with window update ?

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
