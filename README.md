# WinExeCommander	
WinExeCommander makes it easier to call functions when processes/windows are created/terminated. The script is using Windows Management Instrumentation (WMI Provider Host process) to monitor process creation/deletion and the SetWinEventHook function to monitor windows events.

## Requirement
* AutoHotkey v2

## Features
* Specify various criteria, including WinTitle, WinClass, WinTitleMatchMode, ProcessName, ProcessPath, Active/Maximize/Hidden Window and additional parameters.
* Enabling or disabling the monitoring of each event using the tray menu, GUI, or method call.
* Saving monitoring profiles and switch between them using the tray menu, GUI, or method call.
* Select themes.

## How to use it?
* Install AutoHotKey v2.
* Include the processes and/or windows to be monitored, along with their corresponding functions.
* To call a function when the event is created/terminated, append "_Created" and/or "_Terminated" to the function name.
* Monitoring processes use a slightly higher amount of resources (WMI Provider Host process), consuming approximately 0.5% to 2% of CPU usage on a budget CPU. To minimize resource usage, always consider monitoring the window instead of the process when possible.


# Methods

## AddProcess
Adds a process event to monitor.
        
	Events.AddProcess(Process Criteria Object, Function, Event Name [, Created Mode, Terminated Mode])

### Parameters

* **Process Criteria Object**

  > Type: Object
  >
  > - ProcessName
  > - ProcessPath

* **Function**

  > Type: String
  >
  > The name of the function to call when the event is created/terminated.

* **Event Name**
  > Type: String
  > 
  > Name of the Event.

* **Created Mode**
  > Type: Integer
  > - **1:** Call "Function_Created" for every created instance of the process. (Default)
  > - **2:** Call "Function_Created" only for the initial creation of the process.

* **Terminated Mode**
  > Type: Integer
  > - **1:** Call "Function_Terminated" for every terminated instance of the process. (Default)
  > - **2:** Call "Function_Terminated" when the last instance of the process is terminated.

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
			"Status: "      obj.Status
			,0,0), SetTimer(ToolTip, -8000)
	}

	notepad_Terminated(obj) {

		Tooltip(   
			"ID: "          obj.PID "`n"
			"PPID: "        obj.PPID "`n"
			"ProcessName: " obj.ProcessName "`n"
			"Status: "      obj.Status
			,0,0), SetTimer(ToolTip, -8000)
	}

#3: Display a tooltip containing retrievable event parameters when the Defragment Drives (dfrgui.exe) process is created/Terminated.

	Events.AddProcess({ProcessName:"dfrgui.exe"}, "dfrgui", "dfrgui")
	Defragment_Drives_Created(obj) {

		object_list_Tooltip(obj)
		Tooltip(Events.Displayobj(obj), 0, 0), SetTimer(ToolTip, -8000)
	}
	Defragment_Drives_Terminated(obj) {

		object_list_Tooltip(obj)
		Tooltip(Events.Displayobj(obj), 0, 0), SetTimer(ToolTip, -8000)
	}


## AddWindow
Adds a window event to monitor.

	Events.AddWindow(Window Criteria Object, Function, Event Name [, Created Mode, Terminated Mode, Delay])

### Parameters

* **Window Criteria Object**
  > Type: Object
  >
  > - WinTitle
  > - WinTitleMatchMode   
  >    - **1:** A window's title must start with the specified WinTitle to be a match.
  >    - **2:** A window's title can contain WinTitle anywhere inside it to be a match. (Default)
  >    - **3:** A window's title must exactly match WinTitle to be a match.
  >    - **RegEx:** Regular expression WinTitle matching.
  >	
  > - WinClass
  > - ProcessName
  > - ProcessPath
  > - DetectHiddenWindows
  >    - **0:** Hidden windows are not detected. (Default)
  >    - **1:** Hidden windows are detected
  >
  > - WinActive  
  >    - **0**
  >    - **1**
  > 
  > - WinMinMax
  >    - **0:** The window is neither minimized nor maximized.
  >    - **1:** The window is maximized.
  >    - **-1:** The window is minimized.

* **Function**
  > Type: String
  > 
  > The name of the function to call when the event is created/terminated.

* **Created Mode**
  > Type: Integer
  > - **1:** Call "Function_Created" for every created instance of the window (Default)
  > - **2:** Call "Function_Created" when a new window handle(ID) is created.
  > - **3:** Call "Function_Created" for every instance of the window or when a new window handle(ID) is created.
  > - **4:** Call "Function_Created" for the initial instance of the window.

* **Terminated Mode**
  > Type: Integer
  > - **1:** Call "Function_Terminated" for every terminated instance the window. (Default)
  > - **2:** Call "Function_Terminated" when the window handle(ID) is terminated.
  > - **3:** Call "Function_Terminated" when the window is terminated or the window handle(ID) is terminated.
  > - **4:** Call "Function_Terminated" when the last instance of the window is terminated.
  
Mode 4 for Created/Terminated Modes is intended for monitoring the active window or the initial instance/last instance of the window. It should not be mixed with other modes. Created/Terminated Modes are automatically set to 4 when the "Window Criteria Object" contains the key/value "WinActive:1". If the Created/Terminated Modes are manually set to 4 and there is no "WinActive:1" criterion, the functions will be called by either the initial instance or the last instance of the window.

* **Delay**
  > Type: Positive integer
  > 
  > Delay before checking for window(s) matching the event criteria (ms).

### Examples
#1: Set WordPad to always be on top when the window is created.
        
	Events.AddWindow({ProcessName:"wordpad.exe"}, "WordPad_WinSetAlwaysOnTop", "WordPad_WinSetAlwaysOnTop")
	WordPad_WinSetAlwaysOnTop_Created(obj) => WinSetAlwaysOnTop(1, obj.ID)	
		
		
#2: Show a tooltip containing the window information every time the Google Chrome window is activated/deactivated.

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

#3: Change the position/size of the Calculator window and display a tooltip showing the event parameters.
	
	Events.AddWindow({WinTitle:"Calculator", WinClass:"ApplicationFrameWindow", ProcessName:"ApplicationFrameHost.exe"}, "Calculator_WinMove", "Calculator_WinMove")

	Calculator_WinMove_Created(obj) {

		if WinWaitActive(obj.ID,, 2)
			WinMove 300, 300, 600, 400, obj.ID

		Tooltip(Events.Displayobj(obj), 0, 0), SetTimer(ToolTip, -8000)
	}

	Calculator_WinMove_Terminated(obj) {

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

	!2::Events.SetEvent(1, "WordPad_WinSetAlwaysOnTop")

## ProcessFinder
Returns an array containing objects with all existing processes that match the specified parameters. If there is no matching process, an empty array is returned.
        
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
Returns an array containing objects with all existing windows that match the specified parameters. If there is no matching window, an empty array is returned.
        
	WindowFinder(WinTitle, WinClass, ProcessName, ProcessPath, WinTitleMatchMode, WinActive, DetectHiddenWindows)

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
  > - **3:** A window's title must exactly match WinTitle to be a match.
  > - **RegEx:** Regular expression WinTitle matching.

* **DetectHiddenWindows**
  > Type: Integer
  > - **0:** Hidden windows are not detected. (Default)
  > - **1:** Hidden windows are detected
  
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
Create a folder named "Themes" in the root directory. Within that folder, create another folder and place 11 icons named "Main", "Exit", "Reload", "About", "Settings", "Edit Script", "Open Script Folder", "Select Profile", "Select", "Events", "Checkmark". To apply, select it from the dropdown menu in the GUI settings and press the "Save and Exit" or "Save" button.

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
