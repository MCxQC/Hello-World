[Markdown - Style Text](#[Link](https://github.com/fefong/markdown_readme#anchor-links))


# WinExeCommander	
WinExeCommander is an AutoHotkey script to simplify the calling of functions when windows/processes are created/terminated. Devices are connected/disconnected.

## Requirement
* AutoHotkey v2

## Features
* Select from various criteria, including WinTitle, WinClass, WinTitleMatchMode, ProcessName, ProcessPath, Active/Maximize/Hidden Window and additional parameters.
* Enable or disable the monitoring of individual events using the tray menu, GUI, or method call.
* Save monitoring profiles and switch between them using the tray menu, GUI, or method call.
* Select themes.

## How to use it?

* Create an Event
  - Double click on the tray icon or right-click on the icon, click "Event Manager" and click on the button "Add Event".
  - Select window, process or device from the top dropdownlist.
  - To fill the edit fields, you can manually enter data, double-click on a listview item, or right-click on an item and select "Fill Edit Fields with Row Content.

* Create function associated with the Event
  - Append "_Created" and/or "_Terminated" to the event function name. (see examples)


to be called when an Event is created and/or Terminated. 

Device
Check if see device in the list when connected altenatively getinfofinder from tray menu tools

## Event Parameters
  > - **Event Name**
  >    - Name of the Event.
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
  >    - **1** Call "Function_Created" when the window becomes active. Call "Function_Terminated" when the window stops being active.
  > 
  > - **WinMinMax** 
  >    - **Null:** Not monitoring WinMinMax
  >    - **0:** The window is neither minimized nor maximized.
  >    - **1:** The window is maximized.
  >    - **-1:** The window is minimized.
  >   
  > - **Monitoring** 
  >    - **Timer**
  >        - Check for the existence of the window at a specified time interval.
  >    - **WinEvent**
  >        - SetWinEventHook. Sets an event hook function for a range of Windows Events, which means the script doesn't have to waste resources by constantly checking for the existence of the window.
  >
  > - **Mode** 			
  >    - **1:** Call "Function_Created" when a new window handle (ID) is detected. Call "Function_Terminated" for every window handle (ID) terminated. (Default)
  >    - **2:** Call "Function_Created" only for the initial window handle (ID) detected. Call "Function_Terminated" only when the last window handle (ID) is terminated.	
  >    - **3:** Call "Function_Created" when a new window handle (ID) detected. Call "Function_Terminated" only when the last window handle (ID) is terminated.		
  >    - **4:** Call "Function_Created" when the window is activated. Call "Function_Terminated" when the window is desactivated. Vice versa
  >    - **5:** Call "Function_Created" for every window detected. Call "Function_Terminated" for every window that is not detected anymore.
  >    - **6:** Call "Function_Created" only for the initial window detected. Call "Function_Terminated" only when the last window is not detected anymore.
  >    - **7:** Call "Function_Created" for every window detected. Call "Function_Terminated" only when the last window is not detected anymore.
  >   
  > - **Period/Delay**
  >    - Period: The interval, in milliseconds, for checking the existence of the event.
  >    - Delay (WinEvent, DeviceChange): The maximum delay, in milliseconds, for checking the existence of the event.

### Process Parameters
  > - **Process Name**
  > - **Process Path**
  >
  > - **Monitoring** 
  >    - **Timer**
  >        - Check for the existence of the event at a specified time interval using Autohotkey SetTimer function.
  >    - **WMI**
  >        - Check for the existence of the event at a specified time interval using WMI Provider Host process.
  >
  > - **Period**
  >    - Polling Interval, in milliseconds, at which WMI checks for the presence of the process.
  >
  > - **Mode**
  >    - **1:** Call "Function_Created" when a new process ID (PID) is created. Call "Function_Terminated" for every process ID (PID) terminated. (Default)
  >    - **2:** Call "Function_Created" only for the initial process ID (PID) created. Call "Function_Terminated" only when the last process ID (PID) is terminated.
  >    - **3:** Call "Function_Created" for every process ID (PID) created. Call "Function_Terminated" only when the last process ID (PID) is terminated.

# Methods

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
Returns an array containing objects with the device matching the specified parameters. If there are no matching device, an empty array is Returned.

	DeviceFinder(DeviceID, DeviceName)
  
  > - **DeviceID**
  >    - ID of the device
  >
  > - **DeviceName**
  >    - Names of the device. The same name is used to launch the associated device's actions.
  >

For example:

 	^0::
	{
		aObjDeviceFinder := WinExeCmd.DeviceFinder('USBSTOR\DISK&VEN_KINGSTON&PROD_DATATRAVELER_3.0&REV_\E0D55EA573DCF450E97C104C&0')
		Tooltip(WinExeCmd.Displayobj(aObjDeviceFinder), 0, 0), SetTimer(ToolTip, -8000)
	}

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
  > - **Period/Delay**
  >    - Type: Integer
  >    - Period: The interval, in milliseconds, for checking the existence of the event.
  >    - Delay (WinEvent, DeviceChange): The maximum delay, in milliseconds, for checking the existence of the event.

## Profiles
By default
enabling profileLoadEvents will remove all currents events and replce and load all event in the profiles
	
	
	
## Themes
Create a folder named "Themes" in the root directory. Within that folder, create another folder and place 12 icons named "Main", "Exit", "Reload", "About", "Settings", "Tools", "Edit Script", "Open Script Folder", "Select Profile", "Select", "Events" and "Checkmark". To apply, select it from the dropdown menu in the GUI settings and press the "Save and Exit" or "Save" button.



## Additional Notes

Notes
Single instance

;==============================================

Elevated issue:
Run with UI acces ?
UI acces is returning command line
wmi elevated process not returning command line
timer elevated process not returning command line and PPID
WMI Limitation:
When monitoring a process with Administrator rights (elevated), selecting the process path will not work. 
Instead, only select the process name or monitor the process with a timer.
This limitation does not apply when using a timer
WMI Limitation:
When monitoring a process with Administrator rights (elevated). Can't retrieve the command line

Limitation- Process timer. program run as admin are not detected.
New mode for Process timer admin ? timer mode 4

wmi doesnt work with elevated 
TileIconifier.exe wmi doesnt work ?
elevated  exe doesn't get process path. fixed

Elevated Process and Window ?
The script to also run elevated
Run scripts as administrator
Administrator rights (elevated)

By default, User Account Control (UAC) protects "elevated" programs (that is, programs which are running as admin) from being automated by non-elevated programs, since that would allow them to bypass security restrictions.
Recommended: Launch another script as admin to interact with the "elevated" program.

;==============================================

test sending object to another script. mod doc accordingly


Window

window events not sending message game fullscreen tester.

  > - Known issues and limitations
  > - WinMinMax - Universal Windows Platform (UWP) apps encounter an issue, as it fails to send window events messages when clicking the Maximize/Restore Down button, resulting in the function not being called.

Process


WMI Limitation:
When monitoring a process with Administrator rights (elevated), selecting the process path will not work. 

Instead, only select the process name or monitor the process with a timer.
This limitation does not apply when using a timer



Device

The device ID of certain devices might change, so it could be better to select only the device name. I'm not sure which device is affected or the reason behind it. I tested about a dozen devices, and the issue only occurred with TVs connected via HDMI.


Ressouce usage

* Monitoring processes use a higher amount of resources (WMI Provider Host process), consuming approximately 0.5/1% of CPU usage on a budget CPU. To minimize resource usage, always consider monitoring the window instead of the process when possible.

If you have the choice, monitoring the window uses slightly fewer resources than monitoring the process.

SetWinEventHook. Sets an event hook function for a range of Windows Events, which means the script doesn't have to waste resources by constantly checking for the existence of the window.

tips/tkings to know
intended to run as a standalone script.
avoid. msgbox/dialog box. 
multithreads limitation. more complex function. dont hesitate launch anothet script.



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
