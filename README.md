# Radify
## A radial menu launcher with multi-ring layouts, submenus and interactive items.

Inspired by [Radial menu v4](https://www.autohotkey.com/boards/viewtopic.php?f=6&t=12078) by *Learning one*.

---

![myImage](https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExNmtmdXU4a2U3OXlsbW1yeGc0NmRsanR6MnA5NmZvZWNxZjAzOTc4biZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/qN1VceBgbaBeHW4wL9/giphy.gif)

---

## 📦 Requirements

- AutoHotkey v2
- GDI+ Library for AutoHotkey v2

---

## ✨ Features

- **Customizable Menu Options:** Configure images, text, tooltips, item size, skins, and more.
- **Custom Click Actions:** Assign various click actions to menus and individual items.
- **Hotkeys and Hotstrings:** Assign custom hotkeys and hotstrings to trigger specific item actions.
- **Multi-Level Submenus:** Create nested menus with unlimited depth.
- **Interactive Effects:** Show tooltips and glow effects when hovering over items.
- **Sound Effects:** Add audio feedback for various menu interactions.
- **Skin Support:** Apply different skins. Compatible with [Radial menu v4 skins](https://www.autohotkey.com/boards/viewtopic.php?t=12078).

## ✨ Built-In Submenus

- **Emojis Picker:** 50+ popular emojis.
- **Characters Picker:** 40+ common special characters.
- **Websites:** 25+ frequently used websites.
- **Settings:** 20+ system settings (GUID and ms-settings: URI links).
- **Tools:** 15+ Windows system utilities and administrative tools.
- **Power Options:** Shutdown, Restart, Sleep, Advanced Startup, and Restart to Safe Mode.
- **Power Plans:** Set the active power plan.
- **System Cleanup:** Utilities for cleaning disks and temporary files.

---

# 🎨 Radify Skin Editor

Explore all customization options of the Radify class, configure settings, preview skins, and more.

---

## ✨ Skin Editor Features

- **Browse Skins:** Preview all available skins.
- **Configure Settings:** Configure default and individual skin settings.
- **Font and Color Selection:** Browse and preview system fonts and colors.
- **Sound Preview:** Browse and play all available sounds.

---

## 🔧 Modify Default Settings

1. Open the **Radify Skin Editor**
2. Select the **"Default"** skin (first in the list)
3. Configure the settings as needed
4. Click the **"Edit"** button
5. Confirm with **"OK"** or **"Apply"**

---

## 🎨 Modify a Skin

1. Open the **Radify Skin Editor**
2. Select the skin you want to modify
3. Make your changes
4. Click the **"Edit"** button
5. Ensure all desired settings are checked
6. Click **"OK"** or **"Apply"**

---

## 🌟 Set a Skin as Default

1. Open the **Radify Skin Editor**
2. Choose your preferred skin
3. Click the floppy disk icon to save it as the default

---

## 🖼️ Skin Files

- `ItemGlow.png`
- `MenuOuterRim.png`
- `MenuBack.png`
- `ItemBack.png` *(required)*
- `CenterImage.png`
- `SubmenuIndicator.png`

**Note:**

- The Skins folder supports `.png` files only. Other image formats can be assigned programmatically or via **Radify Skin Editor**. See:  [Supported Image Formats](#supported-image-formats) .

***Radial menu v4 skins***

- All settings are loaded from `Preferences.json` rather than from `skin definition.txt` files.

- To set the submenu indicator image, you can:
  - In **Radify Skin Editor**, set a default `SubmenuIndicatorImage`, or assign one per skin.
  - Add a `SubmenuIndicator.png` file to each skin folder.
  - Assign it programmatically via the `CreateMenu` options parameter.

---

## 📁 Set Media Directory

Files in those folders can be referenced by filename only. The application looks for files in two specific folders: `/Images` and `/Sounds`.

- For **images**, include the file extension. (e.g., `downloads.png`)
- For **sounds**, omit the `.wav` extension. (e.g., `tada`)

Steps:

1. Open the **Radify Skin Editor**
2. Click the folder icon
3. Choose a new directory

---

## 🗒️ Radify Skin Editor Notes

- Reload any script using **Radify** after making changes.

---

# 📖 How to Use

- Run `Radify Menus.ahk`

- Create menus and add or remove items by editing `Radify Menus.ahk`

## Launch Item Action

- `Click`: Executes the item’s primary action.
- `Right-Click`: Executes an alternate action (if assigned).
- `Ctrl + Click`: Executes the `CtrlClick` action if defined; otherwise, it executes the item’s` Click` action (if defined), without closing the menu.
- Actions can also be launched via `Shift + Click`, `Alt + Click`, `Hotkey`, and `Hotstring`.

---

# 🖱️ Default Shortcuts in ***Radify Menus.ahk***

## Open Menu

- `Middle mouse button`: Opens *mainMenu* with the cursor centered on the menu.
- `Tray icon clicks`:
  - `Click`: Opens *mainMenu*
  - `Double-click`: Opens *websitesMenu*
  - `Ctrl + Click`: Opens *foldersMenu*
  - `Shift + Click`: Opens *appsMenu*
  - `Alt + Click`: Opens *settingsMenu*

## Close Menu

- `Click` anywhere on the menu—except on an item or the center.
- `Right-click` on the center of the menu.
- `Esc` key

## Move Menu

- `Click` and `drag` the center to reposition the menu.

## Specific Item Actions (Same item, two actions)

**Items in the Symbols, Emojis, Websites, and Shopping submenus**
- `Click`: Executes the primary action.
- `Right-click`: Executes the primary action and keeps the menu open. By default, `Ctrl + Click` also executes the item’s `Click` action (if defined), without closing the menu.

**Apps submenu**
- `Right-click` on submenu: Opens *Apps > Installed apps* in Windows Settings.

**Folders submenu**
- `Right-click` on submenu: Opens *This PC*

**Settings submenu**
- `Right-click` on submenu: Opens the *Windows Settings* app

**Cleanup submenu**
- `Click` on Recycle Bin item: Opens the Recycle Bin folder.
- `Right-click` on Recycle Bin item: Empties the Recycle Bin.

---

## 🗒️ Notes

1. All shortcuts and behaviors are customizable.

2. **Radify** can be included as a library in other AutoHotkey scripts. Make sure to include the required libraries and initialize GDI+ with `Gdip_Startup()`. Then, on exit, call `Radify.DisposeResources()` and `Gdip_Shutdown()` to properly shut down resources, as shown below:


    #Include <v2\GDIp\Gdip_All>
    #Include <v2\Radify\Radify>

    if (!pToken := Gdip_Startup())
        MsgBox('Gdiplus failed to start. Please ensure you have gdiplus on your system.',, 'Iconx'), ExitApp()

    OnExit(*) => (Radify.DisposeResources(), Gdip_Shutdown(pToken))

---

# 🔧 Class Methods

Available methods for the **Radify** class:

## 🔧 Show(MenuID, AutoCenterMouse)

Shows the menu at the current mouse position.

| Parameter | Type   | Description
| --------- | ------ | -------------------------------------
| `MenuID`  | string | Unique identifier of the menu.
| `AutoCenterMouse` | boolean | Center mouse cursor when showing menu.

---

## 🔧 Close(MenuID)

Closes the entire menu tree of the specified menu.

| Parameter | Type   | Description
| --------- | ------ | -------------------------------------
| `MenuID`  | string | Unique identifier of the menu.
| `SuppressSounds` | boolean | Suppresses the menu close sound.

---

## 🔧 CreateMenu(MenuID, MenuItems, Options)

Creates a menu with the specified ID, structure, and configuration options.

| Parameter   | Type   | Description
| ----------- | ------ | -------------------------------------
| `MenuID`    | string | Unique identifier of the menu.
| `MenuItems` | array  | The menu structure: an array of one or more inner arrays (rings), each containing [`item objects`](#item-object-properties).
| [`Options`](#options-object-properties)   | object | Configuration options for the menu.

**Example**

    Radify.CreateMenu('toolsMenu', [
    	[   ; Ring 1
            {image: 'device-manager.png', click: () => Run('devmgmt.msc')},
    		{image: 'disk-management.png', click: () => Run('diskmgmt.msc')},
    		{image: 'computer-management.png', click: () => Run('mmc.exe compmgmt.msc')},
            {}, ; empty space
    	],
    	[   ; Ring 2
    		{image: 'services.png', click: () => Run('services.msc')},
    		{image: 'registry-editor.png', click: () => Run('regedit.exe')},
    		{image: 'optimize-drives.png', click: () => Run('dfrgui.exe')},
        ]
    ], {skin:"rustic"})

    ^1::Radify.Show('toolsMenu')
    ^2::Radify.Close('toolsMenu')

---

### ⚙️ Options Object Properties

Configuration options for the menu.

**Note:**
Options apply only to the current menu and are not inherited by submenus, except for `skin`.
To pass other options to submenus, use the `submenuOptions` key on individual menu items.

Each menu's options are merged in the following order:
- User-defined options passed to the `CreateMenu` method.
- Skin-defined options. (if any)
- Global default options.

---

### 🎨 Skin & Images

| Property                 | Type   | Description
| ------------------------ | ------ | -------------------------------------
| `Skin`                   | string | Folder in `/Skins` containing skin assets.
| `ItemGlowImage`          | string | Glow effect image on hover. Requires `EnableGlow` to be `true`.
| `MenuOuterRimImage`      | string | Image for the outer rim of the menu.
| `MenuBackgroundImage`    | string | Background image of the menu.
| `ItemBackgroundImage`    | string | Background image for individual menu items. Requires `ItemBackgroundImageOnItems` to be `true`.
| `CenterBackgroundImage`  | string | Background image for the center. Requires `ItemBackgroundImageOnCenter` to be `true`.
| `CenterImage`            | string | Image shown in the center of the menu.
| `SubmenuIndicatorImage`  | string | Icon indicating a submenu.

---

### 🔊 Sounds

| Property         | Type   | Description
| ---------------- | ------ | -------------------------------------
| `SoundOnSelect`  | string | Sound played when an item is selected.
| `SoundOnShow`    | string | Sound played when the menu opens.
| `SoundOnClose`   | string | Sound played when the menu closes.
| `SoundOnSubShow` | string | Sound played when a submenu opens.
| `SoundOnSubClose`| string | Sound played when a submenu closes.

**Supported Sound Formats:**

- Path to a `.wav` file.
- Filename from `C:\Windows\Media` or `\Sounds` folder. Omit the `.wav` extension. (e.g., `tada`)

---

### 📐 Layout

| Property                     | Type    | Description
| ---------------------------- | ------- | -------------------------------------
| `ItemSize`                   | number  | Size of menu items (25–250 px).
| `RadiusScale`                | number  | Spacing between rings (0.5–2).
| `CenterSize`                 | number  | Size of center area (25–250 px).
| `CenterImageScale`           | number  | Scale of center image (0–1).
| `ItemImageScale`             | number  | Scale for item image (0–1).
| `ItemImageYRatio`            | number  | Y-position of item image (0 = top, 0.5 = center, 1 = bottom).
| `SubmenuIndicatorSize`       | number  | Size of submenu icon (5–50 px).
| `SubmenuIndicatorYRatio`     | number  | Y-position of submenu icon (0 = top, 0.5 = center, 1 = bottom).
| `OuterRingMargin`            | number  | Margin between the outermost ring and the edge of the menu (0–75 px).
| `OuterRimWidth`              | number  | Width of outer rim (0–25 px).
| `ItemBackgroundImageOnCenter`| boolean | Apply item background image to the center.
| `ItemBackgroundImageOnItems` | boolean | Apply item background image to all menu items.

---

### 📝 Text Styling

| Property           | Type   | Description
| ------------------ | ------ | -------------------------------------
| `TextFont`         | string | Font name.
| `TextColor`        | string | Font color in hex (e.g., `"FFFFFF"`).
| `TextSize`         | number | Font size (5–100).
| `TextFontOptions`  | string | Font styles (`bold`, `italic`, `strikeout`, `underline`) (e.g., `"Bold Italic"`).
| `TextShadowColor`  | string | Shadow color in hex (e.g., `"000000"`).
| `TextShadowOffset` | number | Shadow offset (0–5 px).
| `TextBoxScale`     | number | Text box scale (0.5–1).
| `TextYRatio`       | number | Text Y-position (0 = top, 0.5 = center, 1 = bottom).
| `TextRendering`    | number | Rendering quality for text:
|                    |        | - 0: Default
|                    |        | - 1: SingleBitPerPixelGridFit
|                    |        | - 2: SingleBitPerPixel
|                    |        | - 3: AntiAliasGridFit
|                    |        | - 4: AntiAlias
|                    |        | - 5: ClearTypeGridFit


---

### 🖱️ Click Behavior

| Property                  | Type    | Description
|---------------------------| ------- | -------------------------------------
| `MirrorClickToRightClick` | boolean | Automatically assigns the `Click` function to `RightClick` for items that have a `Click` action but no `RightClick` action defined.

---

### 🖱️ Menu Actions

| Property           | Type                      | Description
|------------------- | ------------------------- | -------------------------------------
| `MenuClick`        | function object or string | Action to execute when clicking the menu background.
| `MenuRightClick`   | function object or string | Action to execute when right-clicking the menu background.
| `CenterClick`      | function object or string | Action to execute when clicking the center area.
| `CenterRightClick` | function object or string | Action to execute when right-clicking the center area.

These properties accept either a function object or a *predefined action*.

**Predefined Actions:**

- `Close`: Closes the entire menu tree.
- `CloseMenu`: Closes only the current menu.
- `Drag`: Makes the menu draggable. *Note: Dragging is only supported with left-click, not right-click.*

---

### ⚙️ Menu Closing Behavior

| Property                | Type    | Description
|------------------------ |-------- | -------------------------------------
| `CloseOnItemClick`      | boolean | Closes the entire menu tree when a menu item is clicked.
| `CloseOnItemRightClick` | boolean | Closes the entire menu tree when a menu item is right-clicked.
| `CloseMenuBlock`        | boolean | Prevents the menu from closing via the specific `HotIfWinExist(WinTitle)` example below. Close(MenuID) still works normally.
    HotIfWinExist('RadifyGui_0_0 ahk_class AutoHotkeyGUI')
    Hotkey('Esc', (*) => WinClose(WinExist()))
    HotIfWinExist()

---

### 🪟 Window & Interaction

| Property          | Type    | Description
| ----------------- | ------- | -------------------------------------
| `AutoCenterMouse` | boolean | Center mouse cursor when showing menu.
| `AlwaysOnTop`     | boolean | Keeps the menu always on top.
| `ActivateOnShow`  | boolean | Activates menu window on show.

---

### 💬 Tooltip & Effects
| Property         | Type    | Description
| ---------------- | ------- | -------------------------------------
| `AutoTooltip`    | boolean | Generates the tooltip text if `Tooltip` is not set, based on item text or image name.
| `EnableTooltip`  | boolean | Enables tooltips for menu items.
| `EnableGlow`     | boolean | Enables glow effect on hover.
| `EnableItemText` | boolean | Shows text labels on menu items.

---

### 🧮 Rendering

| Property            | Type   | Description
| -----------------   | ------ | -------------------------------------
| `GuiOptions`        | string | Custom AHK GUI options.
| `SmoothingMode`     | number | Shape rendering mode:
|                     |        | - 0: Default
|                     |        | - 1: High Speed
|                     |        | - 2: High Quality
|                     |        | - 3: None
|                     |        | - 4: AntiAlias
| `InterpolationMode` | number | Image scaling quality:
|                     |        | - 0: Default
|                     |        | - 1: Low Quality
|                     |        | - 2: High Quality
|                     |        | - 3: Bilinear
|                     |        | - 4: Bicubic
|                     |        | - 5: Nearest Neighbor
|                     |        | - 6: High Quality Bilinear
|                     |        | - 7: High Quality Bicubic

---

### 🧩 Item Object Properties

Defines the characteristics and behavior of a menu item.

Each item object may include:

| Property      | Type   | Description
| ------------- | ------ | -------------------------------------
| `Image`       | string | Image displayed on the menu item. See:  [Supported Image Formats](#supported-image-formats).
| `Tooltip`     | string | Tooltip text shown on hover. See also: [`AutoTooltip`](#tooltip--effects).
| `Text`        | string | Text to display on the menu item.
| `Click`       | function object or string | Action to execute when the item is clicked.
| `RightClick`  | function object or string | Action to execute when the item is right-clicked.
| `ShiftClick`  | function object or string | Action to execute when the item is shift-clicked.
| `AltClick`    | function object or string | Action to execute when the item is alt-clicked.
| `CtrlClick`   | function object or string | Action to execute when the item is ctrl+clicked. If the `CtrlClick` action is not defined, `Ctrl + Click` executes the item’s `Click` action (if defined), without closing the menu.
| `HotkeyClick`         | string | Hotkey that triggers the `Click` action.
| `HotkeyRightClick`    | string | Hotkey that triggers the `RightClick` action.
| `HotkeyShiftClick`    | string | Hotkey that triggers the `ShiftClick` action.
| `HotkeyAltClick`      | string | Hotkey that triggers the `AltClick` action.
| `HotkeyCtrlClick`     | string | Hotkey that triggers the `CtrlClick` action.
| `HotstringClick`      | string | Hotstring that triggers the `Click` action.
| `HotstringRightClick` | string | Hotstring that triggers the `RightClick` action.
| `HotstringShiftClick` | string | Hotstring that triggers the `ShiftClick` action.
| `HotstringAltClick`   | string | Hotstring that triggers the `AltClick` action.
| `HotstringCtrlClick`  | string | Hotstring that triggers the `CtrlClick` action.
| `SubMenu`             | array  | Array of rings. Each ring is an array of item objects.                      |
| `SubmenuOptions`      | object | Options specific to the submenu.

---

**Additional Properties:**

- `ItemBackgroundImage`, `ItemImageScale`, `ItemImageYRatio`, `SubmenuIndicatorImage`, `SubmenuIndicatorSize`, `SubmenuIndicatorYRatio`, `SoundOnSelect`, `CloseOnItemClick`, `CloseOnItemRightClick`, `MirrorClickToRightClick` and All [Text Styling](#text-styling) settings.

---

`Click`, `RightClick`, `ShiftClick`, `AltClick` and `CtrlClick` accept either a function object or a *predefined action*.

**Predefined Actions:**

- `Close`: Closes the entire menu tree.
- `CloseMenu`: Closes only the current menu.

---

**Special Interactions:**

- `Ctrl + Click`: If the `CtrlClick` action is not defined, `Ctrl + Click` executes the item’s `Click` action (if defined), without closing the menu.

**Empty Items:**

- An empty object `{}` inserts a blank space in the menu, useful for spacing or alignment.

---

### Supported Image Formats 🖼️

- File path to a standard image. (`png, jpeg, jpg, ico, gif, bmp, tif`)
- Filename located in the `/Images` folder (include the file extension, e.g., `downloads.png`).
- Image handle (`hIcon`, `hBitmap`).
- Icons from resource libraries (`.exe`, `.dll`, `.cpl`). Use the format: `full_path|iconN`, where `N` is the icon index. If `|iconN` is omitted, icon index 1 is used by default.
  - Examples:
    - `A_WinDir '\System32\imageres.dll|icon19'`
    - `A_ProgramFiles '\Everything\Everything.exe'`

---

# ☕ Donate

If you find my AHK code helpful and want to show your appreciation, a donation would be greatly appreciated. Thank you!

[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/xmcqcx)

---

# 🎖️ Credits

- [AutoHotkey](https://www.autohotkey.com) – Steve Gray, Chris Mallett, portions of the AutoIt Team, and various others.
- [Radial menu v4](https://www.autohotkey.com/boards/viewtopic.php?f=6&t=12078) by Learning one
- [GDI+](https://github.com/buliasz/AHKv2-Gdip/blob/master/Gdip_All.ahk)
  - tic – Created the original [Gdip.ahk](https://github.com/tariqporter/Gdip) library
  - Rseding91, mmikeww, buliasz
- [JSON](https://github.com/thqby/ahk2_lib/blob/master/JSON.ahk) by thqby, HotKeyIt
- Icons and [emojis](https://github.com/microsoft/fluentui-emoji) © Microsoft.

---

**Radify**
- [CalculatePopupWindowPosition](https://www.autohotkey.com/boards/viewtopic.php?t=103459) by lexikos
- [PlayWavConcurrent](https://www.autohotkey.com/boards/viewtopic.php?f=83&t=130425) by Faddix
- [ToolTipEx](https://github.com/nperovic/ToolTipEx) by nperovic

---

**Radify Skin Editor**

- [GuiCtrlTips](https://github.com/AHK-just-me/AHKv2_GuiCtrlTips) by just me
- [LVGridColor](https://www.autohotkey.com/boards/viewtopic.php?f=83&t=125259) by just me
- [GuiButtonIcon](https://www.autohotkey.com/boards/viewtopic.php?f=83&t=115871) by FanaticGuru
- [YACS – Yet Another Color Selector](https://github.com/tylerjcw/YACS) by Komrad Toast
- [ColorPicker](https://github.com/TheArkive/ColorPicker_ahk2) by Maestrith, TheArkive (v2 conversion)
- [GetFontNames](https://www.autohotkey.com/boards/viewtopic.php?t=66000) by teadrinker
- [MoveControls](https://github.com/Descolada/UIA-v2) by Descolada (from *UIATreeInspector.ahk*)
- **Control_GetFont** by SKAN, swagfag
  - [AHK Forum](https://www.autohotkey.com/board/topic/66235-retrieving-the-fontname-and-fontsize-of-a-gui-control)
  - [AHK Forum](https://www.autohotkey.com/boards/viewtopic.php?t=113540)

---

### 📄 License

- MIT License
