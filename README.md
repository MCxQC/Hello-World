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
- [Methods](#methods)
	- [SetProfile](#setprofile)
	- [SetEvent](#setevent)
  	- [SetPeriodWMI](#setperiodwmi)
	- [ProcessFinder](#processfinder)
	- [WindowFinder](#windowfinder)
	- [DeviceFinder](#devicefinder)
	- [Notify](#notify)
	- [CustomGUI](#customgui)
	- [Sound](#sound)
- [Donation](#donation)
- [Credits](#credits)

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

* Edit an Event
  - Click the "Edit" button, double-click on it in the list or right-click and choose "Edit Event".
  
* Write a function associated with the event.
  - In the file "WinExeCommander.ahk", create a function to be called when the event is created or terminated. Append "_Created" or "_Terminated" to the event function name.

For example:
 
When the Calculator app is opened, set the window to be always on top.

Function Name: Calculator_AlwaysOnTop

 	Calculator_AlwaysOnTop_Created(mEvent) {
	    
	    if WinExist('ahk_id ' mEvent['id'])
	        WinSetAlwaysOnTop(1, 'ahk_id ' mEvent['id'])
	    else
	        WinExeCmd.Notify('WinExeCommander', 'Calculator does not exist.', A_WinDir '\system32\user32.dll|Icon4')    
	}

When the Notepad app is opened, changes the position and/or size of Notepad.

Function Name: Notepad

	Notepad_Created(mEvent) {
	    
	    if WinExist('ahk_id ' mEvent['id'])
		    WinMove(900, 200, 500, 500, 'ahk_id ' mEvent['id'])
	    else
	        WinExeCmd.CustomGui('Notepad does not exist.',, A_WinDir '\system32\user32.dll|Icon4')
	}

When the 'mspaint.exe' process is created, change its priority level to 'High'.

Function Name: MSPaint_ProcessSetPriority
	
 	MSPaint_ProcessSetPriority_Created(mEvent) {
	
	    if ProcessExist(mEvent['pid'])
	        ProcessSetPriority('High', mEvent['pid'])
	    else
	        WinExeCmd.CustomGui('mspaint.exe does not exist.',, A_WinDir '\system32\user32.dll|Icon4')
	}

* To identify a device
  - Open the "Event Manager"
  - Click "Add Event"
  - In the device section, check if the device is listed.
  - Alternatively, run "DeviceInfoFinder.ahk", found in the "Tools" tray menu, menubar, and the device section.
  
* Loading Profiles
  - The profile contains the Events information, period WMI and the windows events. By default, when loading a profile, the existing events will remain the same, and only the event states are loaded. In the Profile Manager, you can choose whether to load the period WMI and windows events or not. Enabling "Replace All Events" will replace all existing events with those from the profile.

* Applying Changes
  - To apply modifications, make sure to click the "Apply" button after creating or modifying an event, changing the WMI period, loading a profile etc...

* Themes Creation
  - Create a "Themes" folder in the root directory.
  - Within that folder, create another folder and place 13 icons named: "about", "checkmark", "edit", "events", "exit", "folder", "loading", "main", "profile", "reload", "select", "settings", "tools".
  - To apply, select it from the dropdown menu in the settings. 

* Adding notification sounds
 - Create a "Sounds" folder in the root directory and place WAV files within that folder.
 
* Start with Windows
  - To automatically run this script on startup, add its shortcut to the Startup folder.  
 
## Event Parameters
  > - **Event Name**
  >
  > - **Function**
  >    - The name of the function to call upon event creation or termination. To call the function, append "_Created" or "_Terminated" to the function name.
  >
  > - **Critical**
  >    - The function's thread is critical or not critical.
  >
  > - **Status**
  >    - Display GUI with the Event status in the bottom right corner.
  >  
  > - **Info**
  >    - Display GUI with the Event information in the top left corner.
  >  
  > - **Log Info**
  >    - Log Event information to "EventsLog.txt"
  >   
  > - **Sound**
  >    - Notification Sounds.


### Window Parameters
  > - **WinTitle**:
  >    - Case-sensitive, except when using the i) modifier in a RegEx pattern.
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
  >    - **Uncheck:** Hidden windows are not detected. (Default)
  >    - **Check:** Hidden windows are detected.
  > 
  > - **WinActive**   
  >    - **Uncheck:** Not monitoring for active window. (Default)
  >    - **Check:** Monitoring for active window.
  > 
  > - **WinMinMax** 
  >    - **Null:** Not monitoring WinMinMax
  >    - **0:** The window is neither minimized nor maximized.
  >    - **1:** The window is maximized.
  >    - **-1:** The window is minimized.
  >    - **Limitation:** Only one window per Event can be monitored.
  >   
  > - **Monitoring** 
  >    - **WinEvent**
  >        - SetWinEventHook. Sets an event hook function for a range of Windows Events. (Default)
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
  >    *Some programs generate various windows, some of which can be visible or hidden. This has the potential to cause confusion when the mode is set to 1, as the event function will execute multiple times. The default mode is 2 to eliminate this potential confusion. 
  >   
  > - **Period/Delay**
  >    - Period: The interval (in milliseconds) to check for the window's existence.
  >    - Delay (WinEvent): The approximate delay (in milliseconds) for checking the existence of the window after a window event message is fired by the SetWinEventHook function.


### Process Parameters
  > - **Process Name**
  > - **Process Path**
  >
  > - **Monitoring** 
  >    - **WMI**
  >    		- Check for the existence of the process at a specified time interval using WMI Provider Host process. (Default)
  >    - **Timer**
  >        - Check for the existence of the process at a specified time interval.
  >
  > - **Period**
  >    - Period: The interval (in milliseconds) to check for the presence of the process.
  >
  > - **Mode**
  >    - **1:** Call "Function_Created" for every process ID created. Call "Function_Terminated" for every process ID terminated.
  >    - **2:** Call "Function_Created" only for the initial process ID created. Call "Function_Terminated" only when the last process ID is terminated. (Default)
  >    - **3:** Call "Function_Created" for every process ID created. Call "Function_Terminated" only when the last process ID is terminated.
  > 
  >    * Some programs generate various processes with the same name. This has the potential to cause confusion when the mode is set to 1, as the event function will execute multiple times. The default mode is 2 to eliminate this potential confusion.
  
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
  >        - Check for the existence of the device at a specified time interval.
  > 
  > - **Period/Delay**
  >    - Period: The interval (in milliseconds) to check for the device's existence.
  >    - Delay (DeviceChange): The approximate delay (in milliseconds) for checking the existence of the device after a device event message is fired by the DeviceChange function.
  >  
  > - **Mode**
  >    - **1:** Call "Function_Created" for every device connected. Call "Function_Terminated" for every device disconnected. (Default)
  >    - **2:** Call "Function_Created" only for the initial device connected. Call "Function_Terminated" only when the last device is disconnected.
  >    - **3:** Call "Function_Created" for every device connected. Call "Function_Terminated" only when the last device is disconnected.
  

# Methods


## SetProfile

	SetProfile(Profile Name)
  
  > - **Profile Name**	
  >    - Type: String
  
For example:

	^7::WinExeCmd.SetProfile('All Events Disable')


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


## SetPeriodWMI
	SetPeriodWMI(Period)

  > - **Period**
  >    - Integer or String
  
 For example:
  
	^6::WinExeCmd.SetPeriodWMI(3000)


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
    aObjProcessFinder := WinExeCmd.ProcessFinder('notepad.exe') 
    WinExeCmd.Notify(, WinExeCmd.Displayobj(aObjProcessFinder),,, 'topCenter')
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
    aObjWindowFinder := WinExeCmd.WindowFinder(, 'WordPadClass', 'wordpad.exe')
    WinExeCmd.Notify(, WinExeCmd.Displayobj(aObjWindowFinder),,, 'topCenter')
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
  		aObjDeviceFinder := WinExeCmd.DeviceFinder('Kingston DataTraveler 3.0 USB Device')
  		WinExeCmd.Notify(, WinExeCmd.Displayobj(aObjDeviceFinder),,, 'topCenter')
	}
  

Check if device is connected:  
 	
 	^1::
	{
	    if WinExeCmd.DeviceFinder(,'USBSTOR\DISK&VEN_KINGSTON&PROD_DATATRAVELER_3.0&REV_\E0D55EA573DCF450E97C104C&0').Length
        	WinExeCmd.CustomGui('The device is connected',, 'iconi')
	}
  

## Notify
Display Notifications.
        
	Notify(hdTxt, bdTxt, Icon, options, position, duration, callback, sound, iconSize, hdFontSize, hdFontColor, hdFont, bdtxtWidth, bdFontSize, bdFontColor, bdFont, bgColor, style)

> - **hdTxt**
>    - Type: String
>    - Header text
>
> - **bdTxt**
>    - Type: String
>    - Body text
>
> - **icon**
>    - Type: String
>    - Picture controls -https://www.autohotkey.com/docs/v2/lib/GuiControls.htm#Picture
>    - "icon!" , "icon?", "iconx", "iconi"
>    - Icon from dll: A_WinDir '\system32\user32.dll|Icon4'
>    - Loads picture from file: 'HICON:*' LoadPicture(A_WinDir '\System32\imageres.dll', 'Icon4 w48', &imageType)     
>  
> - **options**
>    - Type: String
>    - Default: "+Owner -Caption +AlwaysOnTop"
>
> - **position**
>    - Type: String
>    - "bottomRight" or "bottomCenter" or "bottomLeft" or "topLeft" or "topCenter" or "topRight". Default: "bottomRight"
>
> - **duration**
>    - Type: Integer
>    - The display duration (in milliseconds) for the notification before it disappears. Set it to 0 to keep it on the screen until left-clicking on the GUI. Default: "6000" ms
>
> - **callback**
>    - Type: Function Object
>    - A function object to call when left-clicking on the GUI.
>
> - **sound**
>    - Type: String
>    - The path of the .wav file to be played. -https://www.autohotkey.com/docs/v2/lib/SoundPlay.htm
>
> - **iconSize**
>    - Type: Integer
>
> - **hdFontSize**
>    - Type: Integer
>
> - **hdFontColor**
>    - Type: String
>
> - **hdFont**
>    - Type: String
>
> - **bdtxtWidth**
>    - Type: Integer
>
> - **bdFontSize**
>    - Type: Integer
>
> - **bdFontColor**
>    - Type: String
>
> - **bdFont**
>    - Type: String
>
> - **bgColor**
>    - Type: String
>
> - **style**
>    - Type: String
>    - "round" or "square". Default: "round"

For example:

	^l:: WinExeCmd.Notify('The header text', 'The body text', A_WinDir '\system32\user32.dll|Icon4')


## CustomGUI
Display Custom GUI.

	CustomGUI(text, title, icon, options, owner, winSetAoT, posXY, sound, objBtn, iconSize, fontSize, textWidth, textHeight, btnWidth, btnHeight)

> - **text**
>    - Type: String
>    - The text to display inside the GUI.
>
> - **title**
>    - Type: String
>    - The title of the GUI. Default: A_ScriptName
>
> - **icon**
>    - Type: String
>    - Picture controls -https://www.autohotkey.com/docs/v2/lib/GuiControls.htm#Picture
>    - "icon!" , "icon?", "iconx", "iconi"
>    - Icon from dll: A_WinDir '\system32\user32.dll|Icon4'
>    - Loads picture from file: 'HICON:*' LoadPicture(A_WinDir '\System32\imageres.dll', 'Icon4 w48', &imageType)     
>                
> - **options**
>    - Type: String
>    - Sets various options and styles for the appearance and behavior of the window. Default: "-MinimizeBox -MaximizeBox" -https://www.autohotkey.com/docs/v2/lib/Gui.htm#Opt
>
> - **owner**
>    - Type: GUI object
>    - To make the window owned by another.
>
> - **winSetAoT**
>    - Type: Integer
>    - WinSetAlwaysOnTop. 0 or 1. Default: 0
>
> - **posXY**
>    - Type: String
>
> - **sound**
>    - Type: String
>    - The path of the .wav file to be played. -https://www.autohotkey.com/docs/v2/lib/SoundPlay.htm
>
> - **objBtn**
>    - Type: Object
>    - The button(s) of the GUI. Default: {1:{name:'*OK', callback:'this.CustomGUI_Destroy'}}
>
> - **iconSize**
>    - Type: Integer
> 
> - **fontSize**
>    - Type: Integer
> 
> - **textWidth**
>    - Type: Integer
> 
> - **textHeight**
>    - Type: Integer
> 
> - **btnWidth**
>    - Type: Integer
> 
> - **btnHeight**
>    - Type: Integer

For example:

	!d:: WinExeCmd.CustomGUI('The script file failed to open.', 'Error', A_WinDir '\system32\user32.dll|Icon4',,,,,, {1: {name:'*OK', callback:'this.gCustomGUI_Destroy'}})


## Sound
Plays a sound.

	Sound(sound)

> - **sound**
>    - Type: String
>    - SoundPlay. -https://www.autohotkey.com/docs/v2/lib/SoundPlay.htm
>    - "soundx" , "soundi"

For example:

	!q:: WinExeCmd.Sound('soundx')


## Donation
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

* **GuiCtrlTips by just me.**
  - https://github.com/AHK-just-me/AHKv2_GuiCtrlTips

* **MoveControls by Descolada. (from UIATreeInspector.ahk)**
  - https://github.com/Descolada/UIA-v2

* **FrameShadow by Klark92**
  - https://www.autohotkey.com/boards/viewtopic.php?f=6&t=29117&hilit=FrameShadow

* **Notify is inspired by NotifyV2 (from the-Automator.com)**
  - https://www.the-automator.com/downloads/maestrith-notify-class-v2/ 
