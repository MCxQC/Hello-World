# Methods

## AddProcess
Adds a process event to monitor that match the specified parameters.
        
	Events.AddProcess(Process Properties, Function, Event Name [, Instance Mode])

### Parameters

* **Process Properties**

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

* **Instance Mode**
  >  Type: Integer
  > 
  >  - 1 = Call "Function_Created" and "Function_Terminated" for every instance of the process. (Default)
  >  - 2 = Call "Function_Created" only for the initial creation of the process. Call the "_Terminated" when the last instance of the process is terminated.

For example:

        Events.AddProcess({ProcessName:"notepad.exe"}, "Notepad_ProcessClose", "Notepad_ProcessClose")
        Notepad_ProcessClose_Created(obj) => ProcessClose(obj.PID)


include examples


## AddWindow
Adds a window event to monitor that match the specified parameters..

        Events.AddWindow(Window Properties, Function, Event Name [, Instance Mode, Created Mode, Terminated Mode, Delay])

### Parameters

* **Window Properties**
  > Type: Object
  >
  > - WinTitle
  > - WinTitleMatchMode   
  >    - **1:** A window's title must start with the specified WinTitle to be a match.
  >    - **2**: A window's title can contain WinTitle anywhere inside it to be a match. (Default)
  >    - **3:** A window's title must exactly match WinTitle to be a match.
  >    - **RegEx:** Regular expression WinTitle matching.
  >	
  > - WinClass
  > - ProcessName
  > - ProcessPath
  > - DetectHiddenWindows
  >    - **0:** Hidden windows are not detected. (Default)
  >    - **1:** Hidden windows are detected


* **Function**
  > Type: String
  > 
  > The name of the function to call when the event is created/terminated.

* **Instance Mode**
  > Type: Integer
  >    - **1:** Call "Function_Created" and "Function_Terminated" for every instance of the window matching the criteria. (Default)
  >    - **2:** Call "Function_Created" only for the initial instance of the window matching the criteria. Call the "Function_Terminated" when the last instance of the window matching the criteria is terminated.	
  >    - **3:** Call "Function_Created" and "Function_Terminated" when the window matching the criteria is activated/deactivated.

* **Created Mode**
  > Type: Integer
  > - **1:** Call "Function_Created" when the window matching the window criteria is detected. (Default)
  > - **2:** Call "Function_Created" only when a new window handle(ID) is detected.
  > - **3:** Call "Function_Created" 

* **Terminated Mode**
  > Type: Integer
  > - **1:** Call "Function_Terminated" when the window is not found anymore, the window handle(ID) can still exists. (Default)
  > - **2:** Call "Function_Terminated" only when the window handle(ID) is terminated.
  > - **3:** Call "Function_Terminated" when the window is not found anymore or the window handle(ID) is terminated.

For example:

        Events.AddWindow({WinTitle:"Calculator", WinClass:"ApplicationFrameWindow", ProcessName:"ApplicationFrameHost.exe"}, "Calculator_WinMove", "Calculator_WinMove")	

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

        !2::Events.SetEvent(1, "Notepad_ProcessClose")

## ProcessFinder
Returns an array containing objects with all existing processes that match the specified parameters. If there is no matching process, an empty array is returned.
        
	ProcessFinder(ProcessName, ProcessPath) 

* **ProcessName**
  > Type: String

* **ProcessPath**
  > Type: String    

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
  > - **2**: A window's title can contain WinTitle anywhere inside it to be a match. (Default)
  > - **3:** A window's title must exactly match WinTitle to be a match.
  > - **RegEx:** Regular expression WinTitle matching.

* **WinActive**
  > Type: Integer
  > - **0**
  > - **1**

* **DetectHiddenWindows**
  > Type: String
  > - **0:** Hidden windows are not detected. (Default)
  > - **1:** Hidden windows are detected

## DisplayObj
Converts an object to a string.

	DisplayObj(Object)

* **Object** 
  > Type: Object	

11 icons
"Main", "Exit", "Reload", "About", "Settings", "Edit Script", "Open Script Folder", "Select Profile", "Select", "Events", "Checkmark"
	
## Themes
Create a new folder in the "Themes" directory and put 11 icons named "On", "Off", "Events", "Select", "Checkmark", "Settings", "Exit", "Reload", "Edit Script", "Select Profile", "Open Script Folder" into the folder. To apply, select it from the dropdown menu in the GUI settings and press the "Save and Exit" or "Save" button.
	
## Tips
  - Adding a detection delay of about 1000ms can help avoid detection failures caused by the detection message triggering before the window is fully created.
  - If you have the choice, monitoring the window uses slightly fewer resources than monitoring the process.
  - ??? apres test p-e pas finalement. Avoid using Sleep, WinWait, ProcessWait etc... commands in events functions and opt for detection delays/Timers instead.

## Common mistakes
  - Event Function name not matching with associated function.
  - Error: Invalid property name in object literal. A comma is required at the end of each line when there are multiple line events.
  
  
## Known Issues
  
## Copyright and License
  - MIT License
  
## Donation (PayPal)
  - If you found this script useful and would like to donate. It would be greatly appreciated. Thank you! :smiley:
    https://www.paypal.com/paypalme/martinchartier  

## Credits
* **AutoHotkey**
  - Authors: Chris Mallett and Steve Gray (Lexikos), with portions by AutoIt Team and various AHK community members.
  - License: GNU General public license
  - Info and source code at: https://autohotkey.com/
  
* **GetCommandLine by teadrinker. (Based on Sean and SKAN v1 code)**
    https://www.autohotkey.com/boards/viewtopic.php?p=526409#p526409
  
* **Base64PNG_to_HICON by SKAN.**
    https://www.autohotkey.com/boards/viewtopic.php?p=168658#p168658
  
* **DisplayObj by FanaticGuru. (inspired by tidbit and Lexikos v1 code)**
    https://www.autohotkey.com/boards/viewtopic.php?p=507896#p507896
 
* **HasVal by jNizM.**
    https://www.autohotkey.com/boards/viewtopic.php?p=109617#p109617
