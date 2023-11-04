# WinExeCommander	
WinExeCommander is an AutoHotkey script to simplify the calling of functions when windows/processes are created/terminated. Devices are connected/disconnected.

## Requirement
* AutoHotkey v2

## Features
* Select from various criteria, including WinTitle, WinClass, WinTitleMatchMode, Process Name, Process Path, Active/Maximize/Hidden Window and additional parameters.
* Enable or disable the monitoring of individual events using the tray menu, user interface (GUI), or method call.
* Save profiles and load them via the tray menu, user interface (GUI), or method call.
* Themes Customization.

# Supported devices
USB, Bluetooth, HDMI etc...

## How to use it?

* Add an Event
  - Double-click the tray icon or right-click on it and choose "Event Manager".
  - Click the "Add Event" button.
  - Choose Window, Process, or Device from the top dropdown list.
  - To fill the edit fields, you can manually enter data, double-click on a listview item, or right-click on an item and select "Fill Edit Fields with Row Content.

* Edit an Event
  - Either double-click on it in the list or right-click and choose "Edit Event."

* Write a function associated with the Event.
  - Write a function to call when the Event is created and/or terminated. Append "_Created" or "_Terminated" to the event function name.

For example:
 
Function name:
Notepad
 
	Notepad_Created(obj)
	{
		<Insert code here>
	}
	
* Start with Windows

* To identify a device
  - Open the "Event Manager"
  - Click "Add Event"
  - In the device section, check if the device is listed.
  - Alternatively, run "DeviceInfoFinder.ahk", which is accessible from the "Tools" tray menu item.
  
* Loading Profiles
The profile contains Events, Period WMI and Windows Events. By default, when loading a profile, the existing events will remain the same, and only the event states are loaded. In the settings, you can choose whether to load the Period WMI and Windows Events or not. Enabling "Replace All Events" will replace all existing events with those from the profile.

	
	
	 
# Modes
Tooltip debug masure sure function is not trigere twive


	
	
	
# Themes
  - Create a folder named 'Themes' in the root directory if it has not already been created.
  - Within that folder, create another folder and place 14 icons named: 'Main', 'Loading', 'Exit', 'Reload', 'About', 'Settings', 'Tools', 'Edit Script', 'Open Script Folder', 'Select Profile', 'Select', 'Events', 'Checkmark' and 'Plus'.
  - To apply, select it from the dropdown menu in the settings.  
  
## Event Parameters
  > - **Event Name**
  >
  > - **Function**
  >    - The name of the function to call when the Event is created/terminated. To call the function, append "_Created" and/or "_Terminated" to the function name.
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
  >    - **1** Call "Function_Created" on window activation. Call "Function_Terminated" when it deactivates. Setting WinActive to 1 automatically sets the mode to 4, and vice versa.
  > 
  > - **WinMinMax** 
  >    - **Null:** Not monitoring WinMinMax
  >    - **0:** The window is neither minimized nor maximized.
  >    - **1:** The window is maximized.
  >    - **-1:** The window is minimized.
  >   
  > - **Monitoring** 
  >    - **WinEvent** (Default)
  >        - SetWinEventHook. Sets an event hook function for a range of Windows Events.
  >    - **Timer**
  >        - Check for the existence of the window at a specified time interval.
  >
  > - **Mode** 			
  >    - **1:** Call "Function_Created" when a new window handle (ID) is detected. Call "Function_Terminated" for every window handle (ID) terminated. (Default)
  >    - **2:** Call "Function_Created" only for the initial window handle (ID) detected. Call "Function_Terminated" only when the last window handle (ID) is terminated.	
  >    - **3:** Call "Function_Created" when a new window handle (ID) detected. Call "Function_Terminated" only when the last window handle (ID) is terminated.		
  >    - **4:** Call "Function_Created" for every window detected. Call "Function_Terminated" for every window that is not detected anymore.
  >    - **5:** Call "Function_Created" only for the initial window detected. Call "Function_Terminated" only when the last window is not detected anymore.
  >    - **6:** Call "Function_Created" for every window detected. Call "Function_Terminated" only when the last window is not detected anymore.
  >   
  > - **Period/Delay**
  >    - Period: The interval (in milliseconds) to check for the window's existence.
  >    - Delay (WinEvent): The maximum delay (in milliseconds) to check for the window's existence.
  
  
  remove
    >    - **4:** Call "Function_Created" on window activation. Call "Function_Terminated" when it deactivates. Setting the mode to 4 automatically sets WinActive to 1, and vice versa.
  
  
  Function obj param
  
<obj> = <Object>
.<DetectHiddenWindows> = 0
.<Elevated> = No
.<EventName> = DebugVars_WinMove
.<EventType> = Window
.<Function> = DebugVars_WinMove
.<ID> = 4930446
.<Mode> = 3
.<Monitoring> = WinEvent
.<Period> = 25
.<PID> = 13520
.<ProcessName> = Radial menu.exe
.<ProcessPath> = C:\Programmes\Radial menu v4\Radial menu.exe
.<Status> = Created
.<WinActive> = 0
.<WinClass> = AutoHotkeyGUI
.<WinMinMax> = 
.<WinTitle> = Variables
.<WinTitleMatchMode> = 2
  
  

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
  >    - **1:** Call "Function_Created" when a new process ID (PID) is created. Call "Function_Terminated" for every process ID (PID) terminated. (Default)
  >    - **2:** Call "Function_Created" only for the initial process ID (PID) created. Call "Function_Terminated" only when the last process ID (PID) is terminated.
  >    - **3:** Call "Function_Created" for every process ID (PID) created. Call "Function_Terminated" only when the last process ID (PID) is terminated.



<obj> = <Object>
.<CmdLine> = "C:\Windows\System32\notepad.exe" 
.<Elevated> = No
.<EventName> = Notepad
.<EventType> = Process
.<Function> = Notepad
.<Mode> = 3
.<Monitoring> = WMI
.<Period> = 1500
.<PID> = 8132
.<PPID> = 3900
.<ProcessName> = notepad.exe
.<ProcessPath> = C:\Windows\System32\notepad.exe
.<Status> = Terminated




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
  
  
  
<obj> = <Object>
.<DeviceID> = SWD\MMDEVAPI\{0.0.0.00000000}.{3278E776-26F1-4931-AFFB-06D6C653C12E}
.<DeviceName> = A90 Pro (A90 Pro Stereo)
.<EventName> = Bluetooth_Earbuds
.<EventType> = Device
.<Function> = Bluetooth_Earbuds
.<Monitoring> = DeviceChange
.<Period> = 1250
.<Status> = Terminated
  
  

# Methods

## SetProfile

	SetProfile(Profile Name)
  
  > - **Profile Name**	
  >    - Type: String
  
For example:

	!1::WinExeCmd.SetProfile("Disable All Events")

## SetEvent
	SetEvent(State, Event Name)

  > - **State**
  >    - Type: Integer
  >    - **0:** Disable
  >    - **1:** Enable
  >
  > - **Event Name**
  >    - Type: String

For example:

	!2::WinExeCmd.SetEvent(1, "Calculator_WinSetAlwaysOnTop")	
	
## SetEventMonitoring
	SetEventMonitoring(EventName, Monitoring, Period)

  > - **EventName**
  >    - Type: String
  >    - Name of the Event.
  >
  > - **Monitoring**
  >    - Type: String
  >    - Method for Monitoring event. Process (Timer or WMI), Window (Timer or WinEvent) and Device (Timer or DeviceChange)
  >  
  > - **Period**
  >    - Type: Integer
  >    - Period: The interval (in milliseconds) to check for the event's existence.

only for
process, windows device  timers

and process wmi

DeviceChange, ignore period set to default.



  > - **Period/Delay**
  >    - Type: Integer
  >    - Period: The interval (in milliseconds) to check for the event's existence.
  >    - Delay (WinEvent, DeviceChange): The maximum delay (in milliseconds) to check for the event's existence.



## SetWMIperiodInterval
	SetWMIperiodInterval(Period)

  > - **Period**
  >    - Type: Integer


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
  >    - Type: Integer, String
  >    - **1:** A window's title must start with the specified WinTitle to be a match.
  >    - **2:** A window's title can contain WinTitle anywhere inside it to be a match. (Default)
  >    - **3:** A window's title must exactly match WinTitle.
  >    - **RegEx:** Regular expression WinTitle matching.
  > 
  > - **DetectHiddenWindows**
  >    - Type: Integer
  >    - **0:** Hidden windows are not detected. (Default)
  >    - **1:** Hidden windows are detected.
  > 
  > - **WinActive**
  >    - Type: Integer
  >    - **0**
  >    - **1**  
  > 
  > - **WinMinMax**
  >    - Type: Integer
  >    - **0:** The window is neither minimized nor maximized.
  >    - **1:** The window is maximized.
  >    - **-1:** The window is minimized.  
  
For example:
        
	^9:: 
	{
		aObjWindowFinder := WinExeCmd.WindowFinder(, "Chrome_WidgetWin_1", "chrome.exe") 
		Tooltip(WinExeCmd.Displayobj(aObjWindowFinder), 0, 0), SetTimer(ToolTip, -8000)
	}

## DeviceFinder
Returns an array containing objects with the device matching the specified parameters. If there are no matching device, an empty array is returned.

	DeviceFinder(DeviceName, DeviceID)
  
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
