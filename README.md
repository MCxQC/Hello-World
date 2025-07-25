

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

### [🪟] Interaction

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
| `GuiOptions`        | string | AutoHotkey GUI options
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
| `Tooltip`     | string | Tooltip text shown on hover. See also: [`AutoTooltip`](#tooltip-effects).
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
| `SubMenu`             | array  | The submenu structure: an array of one or more inner arrays (rings), each containing [`item objects`](#item-object-properties).
| `SubmenuOptions`      | object | Options specific to the submenu.

---
