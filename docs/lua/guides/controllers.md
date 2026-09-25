# Controllers

A [`Controller`](../structs.md#controller) is used to control the game (shocker). This guide will go over how to access a [`Controller`](../structs.md#controller), and read inputs from it.

## Accessing a Controller

### `gControllers`

`gControllers` is an array of `0` to `MAX_PLAYERS - 1` which has a [`Controller`](../structs.md#controller) struct for each player. This uses the local index, so `0` is always the local player. For more information, check out [the player index documentation](player-indexes.md).

```lua
local function update()
    -- if the user taps A, warp them back to CG
    if m.controller.buttonPressed & A_BUTTON ~= 0 then
        warp_to_level(LEVEL_CASTLE_GROUNDS, 1, 0)
    end
end

hook_event(HOOK_UPDATE, update)
```

### `MarioState`'s `controller`

If you have access to a `MarioState` you want to access the controller inputs of, use the `controller` field of that mario.

```lua
---@param m MarioState
local function before_mario_update(m)
    -- always have mario hit a
    m.controller.buttonPressed = m.controller.buttonPressed | A_BUTTON
end

hook_event(HOOK_BEFORE_MARIO_UPDATE, before_mario_update)
```

## Buttons

On a `Controller`, there are multiple fields to handle buttons:

| Field | Notes |
| ----- | ----- |
| `buttonPressed` | A button that has been pressed on the current frame |
| `buttonDown` | A button that is being held down. There is no minimum duration, so all buttons that go into `buttonPressed` also go into `buttonDown` |
| `buttonReleased` | A button that was released on the current frame |

There's quite a few buttons you have access to on a `Controller` as well:

- `A_BUTTON`
- `B_BUTTON`
- `X_BUTTON`
- `Y_BUTTON`
- `L_TRIG`
- `R_TRIG`
- `Z_TRIG`
- `START_BUTTON`
- `U_JPAD` (Up DPAD)
- `L_JPAD` (Left DPAD)
- `R_JPAD` (Right DPAD)
- `D_JPAD` (Down DPAD)
- `U_CBUTTONS` (Up C-Button)
- `L_CBUTTONS` (Left C-Button)
- `R_CBUTTONS` (Right C-Button)
- `D_CBUTTONS` (Down C-Button)

The `button*` fields are integers that use a bitmask. If you understand how those work, this will come intuitively, however we will go through each use case.

### Reading Button Inputs

Use the bitwise AND `&` operator with your button on the right and controller input on the left. If it's not `0`, then the button is being inputted, if it is `0`, then the button is not being inputted.

```lua
local controller = gControllers[0]

if controller.buttonPressed & B_BUTTON ~= 0 then
    -- we are pressing the B button
end
```

When reading multiple button inputs, you could do multiple `if` expressions, but no need! You can combine buttons into one large check by wrapping your buttons in parentheses, and in between each button adding the bitwise OR (`|`) operator.

```lua
local controller = gControllers[0]

if controller.buttonDown & (A_BUTTON | B_BUTTON) ~= 0 then
    -- we are holding down the A or B button
end
```

You can check if multiple buttons are being held by making sure the comparison for your button check is the same as itself:

```lua
local controller = gControllers[0]

if controller.buttonDown & (A_BUTTON | B_BUTTON) == (A_BUTTON | B_BUTTON) then
    -- we are holding down the A and B button
end
```

You could also take these button combos and store them in variables:

```lua
local controller = gControllers[0]
local reloadSaveStateInput = (L_TRIG | R_TRIG | Z_TRIG)

if controller.buttonDown & reloadSaveStateInput == reloadSaveStateInput then
    -- time to reload the save state!
end
```

### Writing Button Inputs

You can use the bitwise OR (`|`) operator to add button inputs to your current list of button inputs. To remove, combining the bitwise AND (`&`) and bitwise XOR (`~`) operator is the way to go.

```lua
local controller = gControllers[0]

-- make the controller press the A button only
controller.buttonPressed = A_BUTTON

-- make the controller press the A button along with any other inputs being held on the controller
controller.buttonPressed = controller.buttonPressed | A_BUTTON

-- make the controller hold down the X and Y button along with other inputs
controller.buttonDown = controller.buttonDown | X_BUTTON | Y_BUTTON

-- remove the A and X input from being held
controller.buttonDown = controller.buttonDown & ~A_BUTTON & ~X_BUTTON
```

## Joystick

As a general summarization:

| Fields | Stick Location | Notes |
| ------ | -------------- | ----- |
| `rawStickX` and `rawStickY` | Left Stick | The raw stick values, from `-127` (Left/Down) to `127` (Right/Up) |
| `extStickX` and `extStickY` | Right Stick | The raw stick values for the right stick, from `-127` (Left/Down) to `127` (Right/Up) |
| `stickX` and `stickY` | Left Stick | The adjusted stick value, derived from the raw stick values. Has a range of `-64` (Left/Down) to `64` (Right/Up). This is the stick value used for Mario |

### The Left Joystick

`rawStickX` and `rawStickY` are the raw stick value, which goes from `-127` to `127`. This is the easiest, most convenient, and most precise to use, however it isn't the value used for Mario.

`stickX` and `stickY` is used for calculating anything related to Mario, like Mario's `intendedYaw`. The values it uses are... quite arbitrary, but to break it down:

- The stick value is offset by `6` in each direction, so a raw stick value of `36` would end up as a stick value of `30`, and one of `-36` would be `-30`
- When the raw stick input is less than `9` (or greater than `-9` depending on the direction) the value is ignored, so the stick value remains at `0`. This sort of acts as a builtin deadzone
- The stick value is capped to `64`

This is the value that is used for Mario when calculating things like the `intendedYaw` and `faceAngle.y`.

### The Right Joystick

`extStick` is what stores the information for your right joystick if you are on a modern controller. It uses a range of `0` to `127`.

This value isn't used by the vanilla game. When using this, account for the fact users may use keyboard and mouse, or that users may use an original N64 controller, which only has one joystick.
