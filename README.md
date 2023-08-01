# WinExeCommander	
WinExeCommander makes it easier to call functions when windows/processes are created/terminated. The script utilizes the Windows Management Instrumentation (WMI Provider Host process) to monitor processes creation/deletion and employs the SetWinEventHook function to monitor window events.

## Requirement
* AutoHotkey v2

## Features
* Select from various criteria, including WinTitle, WinClass, WinTitleMatchMode, ProcessName, ProcessPath, Active/Maximize/Hidden Window and additional parameters.
* Enable or disable the monitoring of individual events using the tray menu, GUI, or method call.
* Save monitoring profiles and switch between them using the tray menu, GUI, or method call.
* Select themes.

## How to use it?
* Install AutoHotKey v2.
* To launch the script, you need to have at least one theme. You can download themes from the GitHub repository or create your own.
* Include the processes and/or windows to be monitored, along with their corresponding created and/or terminated functions.
* To call the function when the event is created/terminated, append "_Created" and/or "_Terminated" to the function name.
* Monitoring processes use a higher amount of resources (WMI Provider Host process), consuming approximately 0.5/1% of CPU usage on a budget CPU. To minimize resource usage, always consider monitoring the window instead of the process when possible.

# Methods

## AddWindow
Adds a window event to monitor.

	Events.AddWindow(Window Criteria Object, Function, Event Name [, Mode, Delay])

### Parameters

* **Window Criteria Object**
  > Type: Object
  >
  > - WinTitle
  > - WinTitleMatchMode   
  >    - **1:** A window's title must start with the specified WinTitle to be a match.
  >    - **2:** A window's title can contain WinTitle anywhere inside it to be a match. (Default)
  >    - **3:** A window's title must exactly match WinTitle.
  >    - **RegEx:** Regular expression WinTitle matching.
  >	
  > - WinClass
  > - ProcessName
  > - ProcessPath
  > - DetectHiddenWindows
  >    - **0:** Hidden windows are not detected. (Default)
  >    - **1:** Hidden windows are detected.
  > 
  >
  > - WinActive  
  >    - **0**
  >    - **1**
  > 
  > - WinMinMax
  >    - **0:** The window is neither minimized nor maximized.
  >    - **1:** The window is maximized.
  >    - **-1:** The window is minimized.
  >   
  > - Limitations
  >    - WinMinMax - Universal Windows Platform (UWP) apps encounter an issue, as it fails to send window events messages when clicking the Maximize/Restore Down button, resulting in the function not being called.


* **Function**
  > Type: String
  > 
  > The name of the function to call when the event is created/terminated. To call the function, append "_Created" and/or "_Terminated" to the function name.

* **Event Name**
  > Type: String
  > 
  > Name of the Event.

* **Mode**
  > Type: Integer			
  > - **1:** Call "Function_Created" when a new window handle (ID) is detected. Call "Function_Terminated" for every window handle (ID) terminated. (Default)
  > - **2:** Call "Function_Created" only for the initial window handle (ID) detected. Call "Function_Terminated" only when the last window handle (ID) is terminated.	
  > - **3:** Call "Function_Created" when a new window handle (ID) detected. Call "Function_Terminated" only when the last window handle (ID) is terminated.		
  > - **4:** Call "Function_Created" when the window is activated. Call "Function_Terminated" when the window is desactivated.
  > - **5:** Call "Function_Created" for every window detected. Call "Function_Terminated" for every window that is not detected anymore.
  > - **6:** Call "Function_Created" only for the initial window detected. Call "Function_Terminated" only when the last window is not detected anymore.
  > - **7:** Call "Function_Created" for every window detected. Call "Function_Terminated" only when the last window is not detected anymore.

* **Delay**
  > Type: Positive integer
  > 
  > Maximum delay before checking for window(s) matching the event criteria (in milliseconds). This is not the delay at which the function will be called. It is strongly advised not to change this value, as it may potentially cause issues.



### Examples
#1: When the Wordpad app is opened, set the window to be always on top.
        
	Events.AddWindow({ProcessName:"wordpad.exe"}, "WordPad_WinSetAlwaysOnTop", "WordPad_WinSetAlwaysOnTop")
	WordPad_WinSetAlwaysOnTop_Created(obj) => WinSetAlwaysOnTop(1, obj.ID)	
		
		
#2: Show a tooltip that displays some of the detected window information every time the Google Chrome window is activated/deactivated.

	Events.AddWindow({ProcessName:"chrome.exe", WinClass:"Chrome_WidgetWin_1", WinActive:1}, "Google_Chrome_Active", "Google_Chrome_Active")
	Google_Chrome_Active_Created(obj) {

		Tooltip(   
			"ID: "          obj.ID "`n"
			"WinTitle: "    obj.WinTitle "`n"
			"WinClass: "    obj.WinClass "`n"
			"ProcessPath: " obj.ProcessPath "`n"
			"Status: "      obj.Status
			,0,0), SetTimer(ToolTip, -8000)
	}

	Google_Chrome_Active_Terminated(obj) {

		Tooltip(   
			"ID: "          obj.ID "`n"
			"WinTitle: "    obj.WinTitle "`n"
			"WinClass: "    obj.WinClass "`n"
			"ProcessPath: " obj.ProcessPath "`n"
			"Status: "      obj.Status
			,0,0), SetTimer(ToolTip, -8000)
	}	

#3: Change the position/size of the Calculator window and show a tooltip that displays the keys/values of the event object.
	
	Events.AddWindow({WinTitle:"Calculator", WinClass:"ApplicationFrameWindow", ProcessName:"ApplicationFrameHost.exe"}, "Calculator_WinMove", "Calculator_WinMove")

	Calculator_WinMove_Created(obj) {

		if WinWaitActive(obj.ID,, 2)
			WinMove 300, 300, 600, 400, obj.ID

		Tooltip(Events.Displayobj(obj), 0, 0), SetTimer(ToolTip, -8000)
	}

	Calculator_WinMove_Terminated(obj) {

		Tooltip(Events.Displayobj(obj), 0, 0), SetTimer(ToolTip, -8000)
	}	
	
## AddProcess
Adds a process event to monitor.
        
	Events.AddProcess(Process Criteria Object, Function, Event Name [, Mode])

### Parameters

* **Process Criteria Object**
  > Type: Object
  > - ProcessName
  > - ProcessPath

* **Function**
  > Type: String
  >
  > The name of the function to call when the event is created/terminated. To call the function append "_Created" and/or "_Terminated" to the function name.

* **Event Name**
  > Type: String
  > 
  > Name of the Event.


* **Mode**
  > Type: Integer
  > - **1:** Call "Function_Created" when a new process ID (PID) is created. Call "Function_Terminated" for every process ID (PID) terminated. (Default)
  > - **2:** Call "Function_Created" only for the initial process ID (PID) created. Call "Function_Terminated" only when the last process ID (PID) is terminated.
  > - **3:** Call "Function_Created" for every process ID (PID) created. Call "Function_Terminated" only when the last process ID (PID) is terminated.

### Examples
#1: Change the priority level of "mspaint.exe" to "BelowNormal" when the process is created.
        
	Events.AddProcess({ProcessName:"mspaint.exe"}, "mspaint_ProcessSetPriority", "mspaint_ProcessSetPriority")
	mspaint_ProcessSetPriority_Created(obj) => ProcessSetPriority("BelowNormal", obj.PID)

#2: When the "notepad.exe" process is created, show a tooltip containing the process information.

	Events.AddProcess({ProcessName:"notepad.exe"}, "notepad", "notepad")
	notepad_Created(obj) {

		Tooltip(   
			"ID: "          obj.PID "`n"
			"PPID: "        obj.PPID "`n"
			"ProcessName: " obj.ProcessName "`n"
			"ProcessPath: " obj.ProcessPath "`n"			
			"Status: "      obj.Status
			,0,0), SetTimer(ToolTip, -8000)
	}

	notepad_Terminated(obj) {

		Tooltip(   
			"ID: "          obj.PID "`n"
			"PPID: "        obj.PPID "`n"
			"ProcessName: " obj.ProcessName "`n"
			"ProcessPath: " obj.ProcessPath "`n"
			"Status: "      obj.Status
			,0,0), SetTimer(ToolTip, -8000)
	}

#3: Show a tooltip that displays the keys/values of the event object when the Defragment Drives process (dfrgui.exe) is created/Terminated.

	Events.AddProcess({ProcessName:"dfrgui.exe"}, "dfrgui", "dfrgui")
	Defragment_Drives_Created(obj) {

		object_list_Tooltip(obj)
		Tooltip(Events.Displayobj(obj), 0, 0), SetTimer(ToolTip, -8000)
	}
	Defragment_Drives_Terminated(obj) {

		object_list_Tooltip(obj)
		Tooltip(Events.Displayobj(obj), 0, 0), SetTimer(ToolTip, -8000)
	}	
	
## SetProfile

	SetProfile(Profile Name)
* **Profile Name**	
  > Type: String
  
For example:

	!1::Events.SetProfile("Disable All Events")

## SetEvent

	SetEvent(State, Event Name)
* **State**
  > Type: Integer
  > - **0:** Disable
  > - **1:** Enable

* **Event Name**
  > Type: String

For example:

	!2::Events.SetEvent(1, "Calculator_WinSetAlwaysOnTop")

## ProcessFinder
Returns an array containing objects with all existing processes that match the specified parameters. If there are no matching processes, an empty array is returned.
        
	ProcessFinder(ProcessName, ProcessPath) 

* **ProcessName**
  > Type: String

* **ProcessPath**
  > Type: String    

For example:

	^8:: 
	{
		aObjProcessFinder := Events.ProcessFinder("notepad.exe") 
		Tooltip(Events.Displayobj(aObjProcessFinder), 0, 0), SetTimer(ToolTip, -8000)
	}

## WindowFinder
Returns an array containing objects with all existing windows that match the specified parameters. If there are no matching windows, an empty array is returned.
        
	WindowFinder(WinTitle, WinClass, ProcessName, ProcessPath, WinTitleMatchMode, DetectHiddenWindows, WinActive, WinMinMax)

* **WinTitle**
  > Type: String
  
* **WinClass**
  > Type: String

* **ProcessName**
  > Type: String

* **ProcessPath**
  > Type: String

* **WinTitleMatchMode**
  > Type: Integer, String
  > - **1:** A window's title must start with the specified WinTitle to be a match.
  > - **2:** A window's title can contain WinTitle anywhere inside it to be a match. (Default)
  > - **3:** A window's title must exactly match WinTitle.
  > - **RegEx:** Regular expression WinTitle matching.

* **DetectHiddenWindows**
  > Type: Integer
  > - **0:** Hidden windows are not detected. (Default)
  > - **1:** Hidden windows are detected.
  
* **WinActive**
  > Type: Integer
  > - **0**
  > - **1**  
  
* **WinMinMax**
  > Type: Integer
  >    - **0:** The window is neither minimized nor maximized.
  >    - **1:** The window is maximized.
  >    - **-1:** The window is minimized.  
  
For example:
        
	^9:: 
	{
		aObjWindowFinder := Events.WindowFinder(, "Chrome_WidgetWin_1", "chrome.exe") 
		Tooltip(Events.Displayobj(aObjWindowFinder), 0, 0), SetTimer(ToolTip, -8000)
	}
	
## Themes
Create a folder named "Themes" in the root directory. Within that folder, create another folder and place 11 icons named "Main", "Exit", "Reload", "About", "Settings", "Edit Script", "Open Script Folder", "Select Profile", "Select", "Events" and "Checkmark". To apply, select it from the dropdown menu in the GUI settings and press the "Save and Exit" or "Save" button.

## Donation (PayPal)
  - If you found this script useful and would like to donate. It would be greatly appreciated. Thank you!
    https://www.paypal.com/paypalme/martinchartier  

## Credits
* **AutoHotkey**
  - Authors: Chris Mallett and Steve Gray (Lexikos), with portions by AutoIt Team and various AHK community members.
  - License: GNU General public license
  - Info and source code at: https://autohotkey.com/
  
* **GetCommandLine by teadrinker. (based on Sean and SKAN v1 code)**
    https://www.autohotkey.com/boards/viewtopic.php?p=526409#p526409
  
* **Base64PNG_to_HICON by SKAN.**
    https://www.autohotkey.com/boards/viewtopic.php?p=168658#p168658
  
* **DisplayObj by FanaticGuru. (inspired by tidbit and Lexikos v1 code)**
    https://www.autohotkey.com/boards/viewtopic.php?p=507896#p507896
 
* **HasVal by jNizM.**
    https://www.autohotkey.com/boards/viewtopic.php?p=109617#p109617

* **MoveControls by Descolada. (from UIATreeInspector.ahk)**
    https://github.com/Descolada/UIA-v2
