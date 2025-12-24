# Radify
## A radial menu launcher with multi-ring layouts, submenus and interactive items.

Inspired by [Radial menu v4](https://www.autohotkey.com/boards/viewtopic.php?f=6&t=12078) by *Learning one*.

---

![myImage](https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExa3E2ZTZqZW84eWVmdHhvMzdrODIwZzAzc2ljY2I2anZlY28xejA1eSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/WxY98hu8ecuirxzxrE/giphy.gif)

---

## Table of Contents

- [Requirements](#requirements)
- [Features](#features)
- [Built-in Menus](#built-in-menus)
- [Radify Skin Editor](#radify-skin-editor)
  - [Modify Default Settings](#modify-default-settings)
  - [Modify a Skin](#modify-a-skin)
  - [Set a Skin as Default](#set-a-skin-as-default)
  - [Skin Files](#skin-files)
  - [Set Media Directories](#set-media-directories)
- [How to Use](#how-to-use)
  - [As a Library in a Script](#as-a-library-in-a-script)
  - [Quick Start with Built-in Menus](#quick-start-with-built-in-menus)
  - [Default Actions and Shortcuts](#default-actions-and-shortcuts-in-radify-menusahk)
- [Item Object Properties](#item-object-properties)
- [Class Methods](#class-methods)
  - [CreateMenu()](#createmenu)
  - [Show()](#show)
  - [Close()](#close)
  - [SetImageDir()](#setimagedir)
  - [SetSoundDir()](#setsounddir)
- [Class Properties](#class-properties)
- [Options Object Properties](#options-object-properties)
  - [Skin & Images](#skin--images)
  - [Sounds](#sounds)
  - [Layout](#layout)
  - [Text Styling](#text-styling)
  - [Click Behavior](#click-behavior)
  - [Menu Actions](#menu-actions)
  - [Menu Closing Behavior](#menu-closing-behavior)
  - [Window & Interaction](#window--interaction)
  - [Tooltip & Effects](#tooltip--effects)
  - [Rendering](#rendering)
- [Media Directories Configuration](#media-directories-configuration)
- [Supported Image Formats](#supported-image-formats)
- [Supported Sound Formats](#supported-sound-formats)
- [Donate](#donate)
- [License](#license)
- [Credits](#credits)

---

## Requirements

- AutoHotkey v2
- GDI+ Library for AutoHotkey v2

---

## Features

- **Customizable Menu Options:** Configure images, text, tooltips, item size, skins, and more.
- **Custom Click Actions:** Assign various click actions to individual items and menus.
- **Hotkeys and Hotstrings:** Assign custom hotkeys and hotstrings to trigger specific item actions.
- **Multi-Level Submenus:** Create nested menus.
- **Interactive Effects:** Show tooltips and glow effects when hovering over items.
- **Sound Effects:** Add audio feedback for various menu interactions.
- **Skin Support:** Apply different skins. Compatible with [Radial menu v4 skins](https://www.autohotkey.com/boards/viewtopic.php?t=12078).
- **Built-In Menu Items:** 200+ items including emojis, symbols, websites, system settings, administrative tools, and power management options.

## Built-In Menus

- **Emojis Picker:** 60+ popular emojis.
- **Symbols Picker:** 50+ common symbols.
- **Websites:** 50+ frequently used websites.
- **Settings:** 15+ system settings (GUID and ms-settings: URI links).
- **Tools:** 15+ Windows system utilities and administrative tools.
- **Power Options:** Shutdown, Restart, Sleep, Advanced Startup, and Restart to Safe Mode.
- **Power Plans:** Set the active power plan.
- **System Cleanup:** Useful shortcuts for cleaning your system.

---

# Radify Skin Editor

Explore all customization options of the Radify class, configure settings, preview skins, and more.

---

![myImage](https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExeTc5dm9rOWJxbWc5NmxjdGdubGlvODk3MGl5bDRvZTl5cHAzaGNobSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/rDZgccNsMgxlQodUEi/giphy.gif)

---

## Features

- **Browse Skins:** Preview all available skins.
- **Configure Settings:** Configure default and individual skin settings.
- **Font and Color Selection:** Browse and preview system fonts and colors.
- **Sound Preview:** Browse and play all available sounds.

---

## Modify Default Settings

1. Open **Radify Skin Editor**
2. Select the **"Default"** skin (first in the list)
3. Configure the settings as needed
4. Click the **"Edit"** button
5. Click **"OK"** or **"Apply"**

---

## Modify a Skin

1. Open **Radify Skin Editor**
2. Select the skin you want to modify
3. Make your changes
4. Click the **"Edit"** button
5. Ensure all desired settings are checked
6. Click **"OK"** or **"Apply"**

---

## Set a Skin as Default

1. Open **Radify Skin Editor**
2. Choose your preferred skin
3. Click the floppy disk icon to save it as the default

---

## Skin Files

- `ItemGlow.png`
- `MenuOuterRim.png`
- `MenuBack.png`
- `ItemBack.png` *(required)*
- `CenterImage.png`
- `SubmenuIndicator.png`

**Note:**

- The Skins folder requires `.png` files for skin assets. Other image formats can be assigned programmatically or via **Radify Skin Editor**. See: [Supported Image Formats](#supported-image-formats).

***Radial menu v4 skins***

- All settings are loaded from `Preferences.json` instead of individual `skin definition.txt` files.

- To set the submenu indicator image, you can:
  - In **Radify Skin Editor**, set a default `SubmenuIndicatorImage`, or assign one per skin.
  - Add a `SubmenuIndicator.png` file to each skin folder.
  - Set `SubmenuIndicatorImage` programmatically.

---

## Set Media Directories

Image and sound files in the configured directories can be referenced by filename only. See [Media Directories Configuration](#media-directories-configuration)

---

## Radify Skin Editor Notes

- Reload any script using **Radify** after making changes for the changes to take effect.

---

# How to Use

- ## As a Library in a Script

Radify can be included as a library in any AutoHotkey v2 script to create menus.

**For example:**


    #Requires AutoHotkey v2.0
    #SingleInstance

    #Include <v2\GDIp\Gdip_All>
    #Include <v2\Radify\Radify>

    ;==============================================

    if (!pToken := Gdip_Startup())
        MsgBox('GDI+ failed to start. Please ensure you have GDI+ on your system.',, 'Iconx'), ExitApp()

    OnExit((*) => (Radify.DisposeResources(), Gdip_Shutdown(pToken)))

    HotIfWinExist('RadifyGui_0_0 ahk_class AutoHotkeyGUI')
    Hotkey('Esc', (*) => WinClose(WinExist()))
    HotIfWinExist()

    ;==============================================

    Radify.CreateMenu('myMenu', [
        [   ; ring 1
            {image: 'device-manager.png', click: (*) => Run('devmgmt.msc')},
            {image: 'disk-management.png', click: (*) => Run('diskmgmt.msc')},
            {image: 'computer-management.png', click: (*) => Run('compmgmt.msc')},
            {image: 'system-configuration.png', click: (*) => Run('msconfig.exe')},
            {image: 'system-information.png', click: (*) => Run('msinfo32.exe')},
            {image: 'task-scheduler.png', click: (*) => Run('taskschd.msc')},
        ],
        [   ; ring 2
            {image: 'services.png', click: (*) => Run('services.msc')},
            {image: 'registry-editor.png', click: (*) => Run('regedit.exe')},
            {image: 'optimize-drives.png', click: (*) => Run('dfrgui.exe')},
            {image: 'system-image.png', click: (*) => Run('sdclt.exe /BLBBACKUPWIZARD')},
            {image: 'event-viewer.png', click: (*) => Run('eventvwr.msc')},
            {image: 'windows-tools.png', click: (*) => Run('shell:::{D20EA4E1-3957-11D2-A40B-0C5020524153}')},
            {
                image: 'monitor.png',
                click: (*) => Run('resmon.exe'),
                text: 'Resmon',
                tooltip: 'Resource Monitor',
                itemImageScale: 0.35,
                itemImageYRatio: 0.25,
                textYRatio: 0.75,
            },
            {
                image: 'monitor.png',
                click: (*) => Run('perfmon.exe'),
                text: 'Perfmon',
                tooltip: 'Performance Monitor',
                itemImageScale: 0.35,
                itemImageYRatio: 0.25,
                textYRatio: 0.75,
            },
        ],
    ])

    ^1::Radify.Show('myMenu')
    ^2::Radify.Close('myMenu')

---

## Item Actions

- `Click`: Executes the item’s primary action.
- `Right-Click`: Executes an alternate action (if defined).
- `Ctrl + Click`: Executes the `CtrlClick` action if defined; otherwise, it executes the item’s `Click` action (if defined), without closing the menu.
- Actions can also be launched via `Shift + Click`, `Alt + Click`, `Hotkeys`, and `Hotstrings`.

---

- ## Quick Start with Built-in Menus

Run **Radify Menus.ahk** to access pre-built menus with 200+ items including emojis, symbols, websites, system settings, tools, and power options. You can create, customize, or modify items by editing the file.

---

## Default Actions and Shortcuts in ***Radify Menus.ahk***

## Open Menu

- `Middle mouse button`: Opens *mainMenu*
- `Tray icon clicks`:
  - `Click`: Opens *mainMenu*
  - `Double-Click`: Opens *appsMenu*
  - `Ctrl + Click`: Opens *websitesMenu*
  - `Shift + Click`: Opens *aiMenu*
  - `Alt + Click`: Opens *systemPowerMenu*

## Close Menu

- `Click` on the menu background.
- `Right-Click` on the menu background or the center.
- `Esc` key

## Move Menu

- `Click` and `Drag` the center to reposition the menu.

## Specific Item Actions (Same item, two actions)

**Items in the Emojis, Symbols, Websites, AI, and Shopping submenus**
- `Click`: Executes the primary action.
- `Right-Click`: Executes the primary action and keeps the menu open. By default, `Ctrl + Click` also executes the item’s `Click` action (if defined), without closing the menu.

**Apps submenu**
- `Right-Click` on submenu: Opens *Apps > Installed apps* in Windows Settings.

**Folders submenu**
- `Right-Click` on submenu: Opens *This PC*

**Settings submenu**
- `Right-Click` on submenu: Opens the *Windows Settings* app

**Power Plans submenu**
- `Right-Click` on submenu: Opens *Control Panel > Power Options*

**Cleanup submenu**
- `Click` on Recycle Bin item: Opens the Recycle Bin folder.
- `Right-Click` on Recycle Bin item: Empties the Recycle Bin.

---

### Notes

- All shortcuts and behaviors are customizable.

---

# Item Object Properties

Defines the characteristics and behavior of a menu item.

| Property     | Type   | Description
| ------------ | ------ | -------------------------------------
| `Image`      | string \| integer | Image displayed on the menu item. See:  [Supported Image Formats](#supported-image-formats).
| `Tooltip`    | string | Tooltip text shown on hover. See also: [`AutoTooltip`](#tooltip--effects).
| `Text`       | string | Text to display on the menu item.
| `Click`      | function object \| string | Action to execute when the item is clicked.
| `RightClick` | function object \| string | Action to execute when the item is right-clicked.
| `CtrlClick`  | function object \| string | Action to execute when the item is ctrl+clicked. If the `CtrlClick` action is not defined, `Ctrl + Click` executes the item’s `Click` action (if defined), without closing the menu.
| `ShiftClick` | function object \| string | Action to execute when the item is shift-clicked.
| `AltClick`   | function object \| string | Action to execute when the item is alt-clicked.
| `HotkeyClick`         | string | Hotkey that triggers the `Click` action.
| `HotkeyRightClick`    | string | Hotkey that triggers the `RightClick` action.
| `HotkeyCtrlClick`     | string | Hotkey that triggers the `CtrlClick` action.
| `HotkeyShiftClick`    | string | Hotkey that triggers the `ShiftClick` action.
| `HotkeyAltClick`      | string | Hotkey that triggers the `AltClick` action.
| `HotstringClick`      | string | Hotstring that triggers the `Click` action.
| `HotstringRightClick` | string | Hotstring that triggers the `RightClick` action.
| `HotstringCtrlClick`  | string | Hotstring that triggers the `CtrlClick` action.
| `HotstringShiftClick` | string | Hotstring that triggers the `ShiftClick` action.
| `HotstringAltClick`   | string | Hotstring that triggers the `AltClick` action.
| `Submenu`             | array  | The submenu structure: an array of one or more inner arrays (rings), each containing [`item objects`](#item-object-properties)
| `SubmenuOptions`      | object | Options specific to the submenu.

---

**Additional Properties:**

- `ItemBackgroundImage`, `ItemImageScale`, `ItemImageYRatio`, `SubmenuIndicatorImage`, `SubmenuIndicatorSize`, `SubmenuIndicatorYRatio`, `SoundOnSelect`, `CloseOnItemClick`, `CloseOnItemRightClick`, `MirrorClickToRightClick` and all [text styling](#text-styling) settings.

---

`Click`, `RightClick`, `CtrlClick`, `ShiftClick` and `AltClick` accept either a function object or a *predefined action*.

**Predefined Actions:**

- `Close`: Closes the entire menu tree.
- `CloseMenu`: Closes only the current menu.

---

**Special Interactions:**

- `Ctrl + Click`: If the `CtrlClick` action is not defined, `Ctrl + Click` executes the item’s `Click` action (if defined), without closing the menu.

---

**Empty Items:**

- An empty object `{}` inserts a blank space in the menu, useful for spacing or alignment.

---

# Class Methods

Methods of the Radify class:

## `CreateMenu(MenuID, MenuItems, Options)`

Creates a menu with the specified ID, structure, and configuration options.

| Parameter   | Type   | Description
| ----------- | ------ | -------------------------------------
| `MenuID`    | string | Unique identifier of the menu.
| `MenuItems` | array  | The menu structure: an array of one or more inner arrays (rings), each containing [item objects](#item-object-properties).
| [`Options`](#options-object-properties) | object | Configuration options for the menu.

---

## `Show(MenuID, AutoCenterMouse)`

Shows the menu.

| Parameter | Type   | Description
| --------- | ------ | -------------------------------------
| `MenuID`  | string | Unique identifier of the menu.
| `AutoCenterMouse` | boolean | Centers the mouse cursor when the menu is shown.

---

## `Close(MenuID, SuppressSound)`

Closes the entire menu tree of the specified menu.

| Parameter | Type   | Description
| --------- | ------ | -------------------------------------
| `MenuID`  | string | Unique identifier of the menu.
| `SuppressSound` | boolean | Suppresses the menu close sound.

---

## `SetImageDir(DirPath)`

Sets the directory for images, allowing image files to be referenced by filename only.

| Parameter | Type                | Description
| --------- | ------------------- | -------------------------------------
| `DirPath` | string \| undefined | The image directory path. If omitted, defaults to `rootDir\Images`. See: [Media Directories Configuration](#media-directories-configuration).

---

## `SetSoundDir(DirPath)`

Sets the directory for sounds, allowing sound files to be referenced by filename only.

| Parameter | Type                | Description
| --------- | ------------------- | -------------------------------------
| `DirPath` | string \| undefined | The sound directory path. If omitted, defaults to `rootDir\Sounds`. See: [Media Directories Configuration](#media-directories-configuration).

---

# Class Properties

Properties of the **Radify** class:

## `LastMenuOpenInfo`

Stores information about the last opened menu. Updated each time a menu is shown via the `Show` method.

| Property         | Type    | Description
|----------------- | ------- | ------------------------------------
| `mouseX`         | integer | X-coordinate when the menu was opened.
| `mouseY`         | integer | Y-coordinate when the menu was opened.
| `hwndUnderMouse` | integer | HWND of the window under the mouse when the menu was opened.

**Access example:**

    ; Toggles the always-on-top state of window
    ToggleWindowAlwaysOnTop() {
        info := Radify.lastMenuOpenInfo
        hwndUnderMouse := info.hwndUnderMouse

        try {
            winTitleUM := WinGetTitle('ahk_id ' hwndUnderMouse)
            winClassUM := WinGetClass('ahk_id ' hwndUnderMouse)
        } catch
            return

        if (!winTitleUM || winTitleUM = 'Program Manager' || winClassUM = 'Shell_TrayWnd')
            return

        WinSetAlwaysOnTop(-1, 'ahk_id ' hwndUnderMouse)
        exStyle := WinGetExStyle('ahk_id ' hwndUnderMouse)
        CoordMode('ToolTip', 'Screen')
        ToolTip(winTitleUM '`nAlways on Top "' (exStyle & 0x8 ? 'On' : 'Off') '"', info.mouseX, info.mouseY, 19)
        SetTimer((*) => ToolTip(,,,19), -2500)
    }

---

## `RootDir`

Stores the absolute path to the directory containing the script `Radify.ahk` or the compiled executable.

---

## `PicturesDir`

The Windows Pictures folder.

---

## `MusicDir`

The Windows Music folder.

---

## `DocumentsDir`

The Windows Documents folder.

---

# Options Object Properties

Configuration options for the menu.

Options apply only to the current menu and are not inherited by submenus, except for `skin` and its associated skin-defined options.
To set options for submenus, use the `submenuOptions` property.

Menu options are merged in the following order:

- User-defined options from the `CreateMenu` method or menu item `submenuOptions` properties.
- Skin-defined options.
- Global default options.

---

### Skin & Images

| Property                | Type              | Description
|------------------------ | ----------------- | -------------------------------------
| `Skin`                  | string            | Folder in `/Skins` containing skin assets. Open **Radify Skin Editor** to preview all available skins.
| `ItemGlowImage`         | string \| integer | Glow effect image displayed when hovering over a menu item. Requires `EnableGlow` to be `true`.
| `MenuOuterRimImage`     | string \| integer | Image for the outer rim of the menu.
| `MenuBackgroundImage`   | string \| integer | Background image of the menu.
| `ItemBackgroundImage`   | string \| integer | Background image for individual menu items. Requires `ItemBackgroundImageOnItems` to be `true`.
| `CenterBackgroundImage` | string \| integer | Background image for the center. Requires `ItemBackgroundImageOnCenter` to be `true`.
| `CenterImage`           | string \| integer | Image shown in the center of the menu.
| `SubmenuIndicatorImage` | string \| integer | Image indicating a submenu.

---

### Sounds

| Property          | Type   | Description
| ----------------- | ------ | -------------------------------------
| `SoundOnSelect`   | string | Sound played when an item is selected.
| `SoundOnShow`     | string | Sound played when the menu opens.
| `SoundOnClose`    | string | Sound played when the menu closes.
| `SoundOnSubShow`  | string | Sound played when a submenu opens.
| `SoundOnSubClose` | string | Sound played when a submenu closes.

---

### Layout

| Property                      | Type    | Description
| ----------------------------- | ------- | -------------------------------------
| `ItemSize`                    | integer | Size of menu items (25–250 px).
| `RadiusScale`                 | number  | Spacing between rings (0.5–2).
| `CenterSize`                  | integer | Size of center area (25–250 px).
| `CenterImageScale`            | number  | Scale of center image (0–1).
| `ItemImageScale`              | number  | Scale of item image (0–1).
| `ItemImageYRatio`             | number  | Y-position of item image (0 = top, 0.5 = center, 1 = bottom).
| `SubmenuIndicatorSize`        | integer | Size of submenu icon (5–50 px).
| `SubmenuIndicatorYRatio`      | number  | Y-position of submenu icon (0 = top, 0.5 = center, 1 = bottom).
| `OuterRingMargin`             | integer | Margin between the outermost ring and the edge of the menu (0–75 px).
| `OuterRimWidth`               | integer | Width of outer rim (0–25 px).
| `ItemBackgroundImageOnCenter` | boolean | Apply item background image to the center.
| `ItemBackgroundImageOnItems`  | boolean | Apply item background image to all menu items.

---

### Text Styling

| Property           | Type    | Description
| ------------------ | ------- | -------------------------------------
| `EnableItemText`   | boolean | Shows text labels on menu items.
| `TextFont`         | string  | Font name.
| `TextColor`        | string  | Font color in hex (e.g., `"FFFFFF"`).
| `TextSize`         | integer  | Font size (5–100 px).
| `TextFontOptions`  | string  | Font styles (`bold`, `italic`, `strikeout`, `underline`) (e.g., `"bold italic"`).
| `TextShadowColor`  | string  | Shadow color in hex (e.g., `"000000"`).
| `TextShadowOffset` | number  | Shadow offset (0–5 px).
| `TextBoxScale`     | number  | Text box scale (0.5–1).
| `TextYRatio`       | number  | Text Y-position (0 = top, 0.5 = center, 1 = bottom).
| `TextRendering`    | integer | Rendering quality for text:
|                    |         | - 0: Default
|                    |         | - 1: SingleBitPerPixelGridFit
|                    |         | - 2: SingleBitPerPixel
|                    |         | - 3: AntiAliasGridFit
|                    |         | - 4: AntiAlias
|                    |         | - 5: ClearTypeGridFit

---

### Click Behavior

| Property                  | Type    | Description
|-------------------------- | ------- | -------------------------------------
| `MirrorClickToRightClick` | boolean | Automatically assigns the `Click` action to `RightClick` for items that have a `Click` action but no `RightClick` action defined.
| `fillItemHitZone`         | boolean | Fills a transparent circular hit zone for items when no item background image is rendered, preventing mouse interaction from falling through transparent areas.
| `fillCenterHitZone`       | boolean | Fills a transparent circular hit zone for the center when no center background image is rendered, preventing mouse interaction from falling through transparent areas.

---

### Menu Actions

| Property           | Type                      | Description
|------------------- | ------------------------- | -------------------------------------
| `MenuClick`        | function object \| string | Action to execute when clicking the menu background.
| `MenuRightClick`   | function object \| string | Action to execute when right-clicking the menu background.
| `CenterClick`      | function object \| string | Action to execute when clicking the center area.
| `CenterRightClick` | function object \| string | Action to execute when right-clicking the center area.

These properties accept either a function object or a *predefined action*.

**Predefined Actions:**

- `Close`: Closes the entire menu tree.
- `CloseMenu`: Closes only the current menu.
- `Drag`: Makes the menu draggable. *Note: Dragging is only supported with left-click, not right-click.*

---

### Menu Closing Behavior

| Property                | Type    | Description
|------------------------ | ------- | -------------------------------------
| `CloseOnItemClick`      | boolean | Closes the entire menu tree when a menu item is clicked.
| `CloseOnItemRightClick` | boolean | Closes the entire menu tree when a menu item is right-clicked.
| `CloseMenuBlock`        | boolean | Prevents the menu from closing via the specific `HotIfWinExist(WinTitle)` example below. `Close(MenuID)` still works normally.
    HotIfWinExist('RadifyGui_0_0 ahk_class AutoHotkeyGUI')
    Hotkey('Esc', (*) => WinClose(WinExist()))
    HotIfWinExist()

---

### Window & Interaction

| Property          | Type    | Description
| ----------------- | ------- | -------------------------------------
| `AutoCenterMouse` | boolean | Centers the mouse cursor when the menu is shown.
| `AlwaysOnTop`     | boolean | Keeps the menu always on top.
| `ActivateOnShow`  | boolean | Activates menu window on show.

---

### Tooltip & Effects
| Property        | Type    | Description
| --------------- | ------- | -------------------------------------
| `AutoTooltip`   | boolean | Generates the tooltip text if `Tooltip` is not set, based on item text or image name.
| `EnableTooltip` | boolean | Enables tooltips for menu items.
| `EnableGlow`    | boolean | Enables glow effect on hover.

---

### Rendering

| Property            | Type    | Description
| ------------------- | ------- | -------------------------------------
| `GuiOptions`        | string  | AutoHotkey GUI options
| `SmoothingMode`     | integer | Shape rendering mode:
|                     |         | - 0: Default
|                     |         | - 1: High Speed
|                     |         | - 2: High Quality
|                     |         | - 3: None
|                     |         | - 4: AntiAlias
| `InterpolationMode` | integer | Image scaling quality:
|                     |         | - 0: Default
|                     |         | - 1: Low Quality
|                     |         | - 2: High Quality
|                     |         | - 3: Bilinear
|                     |         | - 4: Bicubic
|                     |         | - 5: Nearest Neighbor
|                     |         | - 6: High Quality Bilinear
|                     |         | - 7: High Quality Bicubic

---

# Media Directories Configuration

Image and sound files in the configured directories can be referenced by filename only, including the file extension (e.g., `downloads.png`, `tada.wav`).

- Directories can be configured in two ways:
  - Through the **Radify Skin Editor** interface
    1. Open **Radify Skin Editor**
    2. Click the folder icon
    3. Select a new directory for images or sounds
  - Programmatically using `SetImageDir(DirPath)` and `SetSoundDir(DirPath)` methods before creating menus.

- Available placeholders:
  - `RootDir`: the directory containing `Radify.ahk`.
  - `PicturesDir`: the Windows Pictures folder.
  - `MusicDir`: the Windows Music folder.
  - `DocumentsDir`: the Windows Documents folder.

---

# Supported Image Formats

- File path to a standard image (`ico, png, jpeg, jpg, gif, bmp, tif`).
- Filename with extension (e.g., `downloads.png`) - searches in the configured image directory.
- Image handles:
  - `hIcon`: Icon handle
  - `hBitmap`: GDI bitmap handle
  - `pBitmap`: GDI+ bitmap pointer
- Icons from resource libraries (`.exe`, `.dll`, `.cpl`). Use the format: `fullPath|iconN`, where `N` is the icon index. If `|iconN` is omitted, icon index 1 is used.
  - Examples:
    - `A_WinDir '\System32\imageres.dll|icon19'`
    - `A_ProgramFiles '\Everything\Everything.exe'`

---

# Supported Sound Formats

- Path to a `.wav` file.
- Filename with extension (e.g., `tada.wav`) - searches in both `C:\Windows\Media` and the configured sound directory.

---

# Donate

If you find my AHK code useful and would like to show your appreciation, any donation is greatly appreciated. Thank you!

[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/xmcqcx)

---

# License

- MIT License

---

# Credits

- [AutoHotkey](https://www.autohotkey.com) - Steve Gray, Chris Mallett, portions of the AutoIt Team, and various others.
- [Radial menu v4](https://www.autohotkey.com/boards/viewtopic.php?f=6&t=12078) by Learning one
- [GDI+](https://github.com/buliasz/AHKv2-Gdip/blob/master/Gdip_All.ahk)
  - tic - Created the original [Gdip.ahk](https://github.com/tariqporter/Gdip) library
  - Rseding91, mmikeww, buliasz, and various others.
- [JSON](https://github.com/thqby/ahk2_lib/blob/master/JSON.ahk) by thqby, HotKeyIt
- Icons and [emojis](https://github.com/microsoft/fluentui-emoji) © Microsoft.

---

**Radify**

- [GetFolderPath](https://www.autohotkey.com/boards/viewtopic.php?f=76&t=66133&start=20) by teadrinker
- [CalculatePopupWindowPosition](https://www.autohotkey.com/boards/viewtopic.php?t=103459) by lexikos
- [PlayWavConcurrent](https://www.autohotkey.com/boards/viewtopic.php?f=83&t=130425) by Faddix
- [ToolTipEx](https://github.com/nperovic/ToolTipEx) by nperovic

---

**Radify Skin Editor**

- [GuiCtrlTips](https://github.com/AHK-just-me/AHKv2_GuiCtrlTips) by just me
- [LVGridColor](https://www.autohotkey.com/boards/viewtopic.php?f=83&t=125259) by just me
- [GuiButtonIcon](https://www.autohotkey.com/boards/viewtopic.php?f=83&t=115871) by FanaticGuru
- [YACS - Yet Another Color Selector](https://github.com/tylerjcw/YACS) by Komrad Toast
- [ColorPicker](https://github.com/TheArkive/ColorPicker_ahk2) by Maestrith, TheArkive (v2 conversion)
- [GetFontNames](https://www.autohotkey.com/boards/viewtopic.php?t=66000) by teadrinker
- [MoveControls](https://github.com/Descolada/UIA-v2) by Descolada (from *UIATreeInspector.ahk*)
- Control_GetFont by SKAN, swagfag
  - [AHK Forum](https://www.autohotkey.com/board/topic/66235-retrieving-the-fontname-and-fontsize-of-a-gui-control)
  - [AHK Forum](https://www.autohotkey.com/boards/viewtopic.php?t=113540)
