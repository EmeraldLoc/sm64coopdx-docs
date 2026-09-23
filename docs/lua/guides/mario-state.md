## [:rewind: Modding](../modding.md)

# `MarioState`

A [`MarioState`](../structs.md#mariostate) is a Mario "object" that contains all information about Mario. Mario's position, facing angle, speed, health, inputs, etc. are all stored in a `MarioState`.

This guide through `MarioState` will be split into multiple sections:

- [Accessing a `MarioState`](#accessing-a-mariostate)
- [Basic `MarioState` Properties](#basic-mariostate-properties)

## Accessing a `MarioState`

There are a few ways to access a `MarioState`:

### Direct Access

You can directly access a `MarioState` at any time via `gMarioStates`.

`gMarioStates` is an array of `MarioState`'s of size `MAX_PLAYERS`. It's based on the local index (see TODO for more information), so `gMarioStates[0]` is always the local `MarioState`.

```lua
---@type MarioState
local m = gMarioStates[0]
```

### Access From a [Hook Event](hook-events.md)

Many [hook events](hook-events.md) pass in a `MarioState` as a parameter. `HOOK_MARIO_UPDATE`, `HOOK_BEFORE_PHYS_STEP`, `HOOK_ON_PVP_ATTACK`, that's just a few instances. There are **tons** of hooks in which a `MarioState` is passed in.

```lua
---@param m MarioState
local function mario_update(m)
    -- HOOK_MARIO_UPDATE runs through every single mario, but we only want to edit
    -- the local mario, so bail if player index is not 0
    -- More information on indexes can be found in the TODO
    if m.playerIndex ~= 0 then return end

    -- disable fall damage by making the check used for it always be the mario's
    -- current height
    m.peakHeight = m.pos.y
end

hook_event(HOOK_MARIO_UPDATE, mario_update)
```

Consult the [hook event documentation](hook-events.md) to see what index you can expect for the `MarioState` when coming from a hook event. Some pass in the local mario only, others pass in any mario.

## Basic `MarioState` Properties

A `MarioState` is a **very** large class with a bunch of properties. We'll be going over the most important ones, but we won't be going over every single one. For a complete look, please take a look at the [`MarioState` struct](../structs.md#mariostate).

### `playerIndex`

Mario's `playerIndex` is the local index that owns that `MarioState` (for more info on networked indexes, see TODO). It's also the key for `gMarioStates`. So `gMarioStates[m.playerIndex] == m`.

```lua
---@param m MarioState
local function mario_update(m)
    -- don't process any mario that isn't the local mario
    if m.playerIndex ~= 0 then return end

    -- do stuff
end

hook_event(HOOK_MARIO_UPDATE, mario_update)
```

### `pos`

Mario's `pos` is a [`Vec3f`](../structs.md#vec3f) which contains Mario's current position, or location. A single unit is roughly a centimeter in real life.

```lua
-- if Mario taps the X button, send him to a diagonal PU!
if m.controller.buttonPressed & X_BUTTON ~= 0 then
    -- 65536 is the number in which the floor collision calculation completely loops
    m.pos.x = m.pos.x + 65536
    m.pos.z = m.pos.z + 65536
end
```

### `faceAngle`

Mario's `faceAngle` is a [`Vec3s`](../structs.md#vec3s). It's a 16-bit angle, which means the angle ranges from `-32768` to `32767`. This is Mario's current facing angle.

Note that this is **not** Mario's *graphical* rotation, that would be on Mario's [`object`](../structs.md#object), accessed via the `marioObj` field, stored in the `header`, then `gfx`, and finally the `angle`.

```lua
-- rotate mario's yaw against his will by 90 degrees
m.faceAngle.y = m.faceAngle.y + 0x4000 -- 16,384 is 0x4000
```

### `intendedYaw`

Mario's `intendedYaw` is a `float` that usually is Mario's currently held rotation on the joystick. It's the target yaw for Mario.

```lua
-- if mario is diving, allow for free rotation of the face angle
if m.action == ACT_DIVING then
    m.faceAngle.y = m.intendedYaw
end
```

### `forwardVel`, `vel`, `slideVelX`, and `slideVelZ`

Mario has quite a few velocity components. Mario's `forwardVel` is the most straightforward. It's the velocity Mario is going forward.

The exact usage and what this value lines up with depends on the action. For most actions, what represents "forwards" is the direction mario is facing.

`m.forwardVel` is the easiest, most straightforward velocity to modify.

`vel`, for most actions, is derived from Mario's `forwardVel` using Mario's yaw (`faceAngle.y`). That's for **most** actions. There's a couple exceptions to this rule, most notably for moving along a surface like Quicksand. For mutating velocity, in many instances manipulating `vel` is better for smoother speed acceleration or deceleration. For mutation the hook used also matters.

Mario's `y` `vel` (`vel.y`) is fully independent from the standard calculation used from the `forwardVel`. That operates independently, and is the sole decider of Mario's vertical velocity.

Assuming Mario is sliding, Mario's sliding velocity (`m.slideVelX` and `m.slideVelZ`) is not based around Mario's `forwardVel`, in fact, Mario's `forwardVel` is set depending on the slide velocity. The slide velocity is calculated from the controller's joystick as well as the angle of the slope Mario is sliding down.

Assuming Mario is not sliding, Mario's slide velocity **mostly** is set to the same as Mario's `vel`.

```lua
---@param m MarioState
local function before_phys_step(m)
    -- the actions here are unstable! They will constantly compound acceleration,
    -- causing obnoxiously high speeds
    if  m.action ~= ACT_BACKWARD_AIR_KB
    and m.action ~= ACT_FORWARD_AIR_KB
    and m.action ~= ACT_HARD_BACKWARD_AIR_KB
    and m.action ~= ACT_HARD_FORWARD_AIR_KB
    and m.action ~= ACT_BACKWARD_AIR_KB
    and m.action ~= ACT_SOFT_BONK
    and m.action ~= ACT_WATER_JUMP then
        -- speed up by a multiplier of 1.3
        m.vel.x = m.vel.x * 1.3
        m.vel.z = m.vel.z * 1.3
    end

    hook_event(HOOK_BEFORE_PHYS_STEP, before_phys_step)
end
```

### `action`, `actionState`, `actionArg`, `actionTimer`, and `prevAction`

Mario's `action` is his current state. It's whatever he is doing right now. You can be walking (`ACT_WALK`), diving (`ACT_DIVE`), etc. and it is all represented with an action. A list of actions may be found (TODO: Allow macro definitions to be converted to enums in Autogen for easier linking in documentation).

Mario's `action` should never be set or mutated directly. Instead, use [`set_mario_action`](../functions-4.md#set_mario_action). Failure to do so may leave `actionState`, `actionArg`, and `actionTimer` variables with whatever they were before.

Mario's `prevAction` is the action he had the previous time `set_mario_action` was called.

- Mario's `actionTimer` is the amount of time in frames Mario has been in that action for
- Mario's `actionState` is like a sub-action in an action. It's used a variable for internal tracking in an action
- Mario's `actionArg` is the argument passed in `set_mario_action`. It's an argument for the setter of the action, and isn't really meant to be changed by the action itself

For information on how to create a action, and code examples for actions, please see (TODO: Write documentation on custom Mario actions)

### `controller`

Mario's `controller` is one of the access points for a `Controller`. For more information on how those works, view the [Controller documentation](controllers.md).

### `flags`

Mario's `flags` are a set of, well, flags that Mario has. There are many flags. Here's a list, but not all of these are documented (yet), however we will document the more important ones:

```lua
MARIO_NORMAL_CAP
MARIO_VANISH_CAP
MARIO_METAL_CAP
MARIO_WING_CAP
MARIO_CAP_ON_HEAD
MARIO_CAP_IN_HAND
MARIO_METAL_SHOCK
MARIO_TELEPORTING
MARIO_UNKNOWN_08
MARIO_UNKNOWN_13
MARIO_ACTION_SOUND_PLAYED
MARIO_MARIO_SOUND_PLAYED
MARIO_UNKNOWN_18
MARIO_PUNCHING
MARIO_KICKING
MARIO_TRIPPING
MARIO_UNKNOWN_25
MARIO_UNKNOWN_30
MARIO_UNKNOWN_31

MARIO_SPECIAL_CAPS (MARIO_VANISH_CAP | MARIO_METAL_CAP | MARIO_WING_CAP)
MARIO_CAPS (MARIO_NORMAL_CAP | MARIO_SPECIAL_CAPS)
```

`m.flags` uses bitwise operations. Just as a quick guideline:

- `&` is used to check if a flag is active. `m.flags & MARIO_X ~= 0` returns non-zero if the flag is set
- `|` combines multiple flags together or enables a new flag on `m.flags`
- `~` inverts bits. Combined with `&` (as `m.flags & ~MARIO_X`), it clears a specific flag

To better showcase this, here is a list of unorganized code examples:

```lua
-- check if mario has any cap
if m.flags & MARIO_SPECIAL_CAPS ~= 0 then
    -- do something
end

-- don't let mario have a wing cap!
m.flags = m.flags & ~MARIO_WING_CAP

-- check if mario is teleporting
if m.flags & MARIO_TELEPORTING ~= 0 then
    -- steal mario's vanish cap if mario is teleporting
    m.flags = m.flags & ~MARIO_VANISH_CAP
end

-- you can also check if mario has multiple caps
if m.flags & (MARIO_VANISH_CAP | MARIO_METAL_CAP) ~= 0 then
    -- do something
end

-- check if mario has no cap on
if m.flags & MARIO_CAP_ON_HEAD == 0 then
    -- mario has no cap! put a cap back on his head
    -- note: this code is inefficient, better to not do the if check
    -- but this works for the code example
    m.flags = m.flags | MARIO_CAP_ON_HEAD
end
```

The flags shown in the first list is decently self-explanatory (except for the flags that are just "unknown" :D ).

### `health`, `hurtCounter`, and `healCounter`

Mario's `health` is the current health of Mario. Mario's `health` is not actually split into individual slices, that's simply what it is visually. Under the hood, Mario's `health` is a number that ranges between `0x0` (`0`) to `0x880` (`2176`).

The 8th slice has a buffer of `0x80` (`128`), so `0x800` (`2048`) will render mario at full health (but internally Mario will not be at full health). This is to pad out effects like toxic gas, burning, drowning, etc.

Here's a table for the slice values for health:

| Health Range | Health Hex Range | Slice Count |
| ------------ | ---------------- | ----------- |
| 000 - 255 | 0x00 - 0xFF | 0 Slices |
| 256 - 511 | 0x100 - 0x1FF | 1 Slice |
| 512 - 767 | 0x200 - 0x2FF | 2 Slices |
| 768 - 1023 | 0x300 - 0x3FF | 3 Slices |
| 1024 - 1279 | 0x400 - 0x4FF | 4 Slices |
| 1280 - 1535 | 0x500 - 0x5FF | 5 Slices |
| 1536 - 1791 | 0x600 - 0x6FF | 6 Slices |
| 1792 - 2047 | 0x700 - 0x7FF | 7 Slices |
| 2048 - 2176 | 0x800 - 0x880 | 8 Slices |

```lua
hook_chat_command("set-marios-health", "Sets Mario's health in slices", function(msg)
    local health = tonumber(msg)
    if health == nil or health < 0 or health > 8 then
        command_message_create("Failed to set health, please enter a number between 0-8!", CONSOLE_MESSAGE_ERROR)
        return true
    end

    m.health = health * 0x100

    -- alternatively, doing a bitshift left by `8` will do this perfectly as well

    --m.health = health << 8

    -- Note: These methods will NOT get mario's health up to the absolute maximum (0x880)
    -- To do that, you can do

    -- m.health = health * 0x110

    -- or the bitwise equivalent

    -- m.health = health << 8 | 0x80

    -- or you can hardcode health 8 to equal 0x880

    -- if health == 8 then m.health = 0x880 end

    command_message_create("Set mario's health to " .. health)
    return true
end)
```

- When Mario is inhaling toxic gas fumes and is NOT metal, he loses `4` health per frame
- If Mario is freezing in water, and Mario is tangible, he loses `3` health per frame
- If Mario is underwater, tangible, and is NOT freezing, he loses `1` health per frame
- If Mario is poking his head above the water, is NOT freezing, and IS tangible, he gains `0x1A` (`26`) health per frame

You can check if Mario is in toxic gas or is freezing via the input `INPUT_IN_POISON_GAS`. You can also check if Mario is wearing a metal cap by checking Mario's `flags` and checking for `MARIO_METAL_CAP`

You can also check if Mario is swimming by checking if mario is swimming via `ACT_FLAG_SWIMMING`. You can check if Mario is tangible via `ACT_FLAG_INTANGIBLE`. You can check the terrain type, and if Mario will freeze in water, via `m.area.terrainType`

```lua
terrainIsSnow = m.area.terrainType & TERRAIN_MASK == TERRAIN_SNOW;
```

In all of these instances, Mario's health does *not* update if `healCounter` or `hurtCounter` is not equal to `0`.

Here's a code example showing every single one of these healing and hurting measures being countered:

```lua
---@param m MarioState
local function mario_update(m)
    if m.playerIndex ~= 0 then return end -- only run for local player

    -- when mario is healing or hurting, mario's health is not adjusted
    if m.healCounter ~= 0 or m.hurtCounter ~= 0 then return end

    -- if we are in poisonous gas and don't have metal cap, increase mario's health by 4 to counter health decrease
    if m.input & INPUT_IN_POISON_GAS ~= 0 and m.flags & MARIO_METAL_CAP == 0 then
        m.health = m.health + 4
    end

    -- make sure we are swimming and tangible
    if m.action & ACT_FLAG_SWIMMING ~= 0 and m.action & ACT_FLAG_INTANGIBLE == 0 then
        -- get if we are currently in snow or not
        local terrainIsSnow = m.area.terrainType & TERRAIN_MASK == TERRAIN_SNOW;

        if (m.pos.y >= m.waterLevel - 140 and not terrainIsSnow) then
            -- mario is healing! Counter by subtracting mario's health by 0x1A (26)
            m.health = m.health - 0x1A
        else
            -- mario is hurting! Depending on whether `terrainIsSnow`, increment health by 3 or 1
            m.health = m.health + (terrainIsSnow and 3 or 1)
        end
    end
end

hook_event(HOOK_MARIO_UPDATE, mario_update)
```

Mario's `healCounter` is the amount of health to gain and `hurtCounter` is the amount of health to lose per frame by units of `0x40`. They are `integers`, which means they cannot hold decimals. Doing so will cause "integer truncation."

In this unit space, `30.015625` is equivalent to the maximum health assuming the maximum is `0x880`. Assuming a unit range where max health is `0x800`, which is the maximum health by the slice, `32` is the equivalent to the maximum health. It takes `4` frames to change Mario's health by 1 slice, so that means the `healCounter`/`hurtCounter` must be `4` to drop by a single slice.

```lua
-- if we hit the A button, drop mario's health by 1 slice
if m.controller.buttonPressed & A_BUTTON ~= 0 then
    m.hurtCounter = 4 -- 4 in a hurt counter = 1 slice
end
```

Healing and hurting both cancel eachother out. That means that if `m.hurtCounter` is `4` and `m.healCounter` is `4`, that will be equivalent to both being `0`.

Both counters are `u8`'s, which means that if the value goes below `0` or above `255`, it wraps to the other side. A value `256` will internally be set to `0`, and a value of `-1` will internally be set to 255``.

### `peakHeight`

Mario's `peakHeight` is used to track just that, Mario's peak height. This value:

- Checks if Mario should take fall damage
- Checks if Mario should play the far fall sound (`CHAR_SOUND_WAAAOOOW`)
- Checks if Mario should get stuck in the ground when falling into snow
- Checks if Mario should go "HAHA" (`CHAR_SOUND_HAHA_2`) if he fell from a high enough height

```lua
-- disable fall damage by setting mario's peakHeight to mario's height each frame

---@param m MarioState
local function mario_update(m)
    m.peakHeight = m.pos.y
end

hook_event(HOOK_MARIO_UPDATE, mario_update)
```

### `wall`, `floor`, and `ceil`

Mario's `wall`, `floor`, and `ceil` are all of type [Surface](../structs.md#surface).

- The `floor` is the floor Mario is currently above
- The `ceil` is the ceiling Mario is currently below
- The `wall` is the wall Mario is currently touching

These values can be `nil`:

- If Mario is not above a floor, `floor` will be `nil`
- If Mario is not below a ceiling, `ceil` will be `nil`
- If Mario is not touching a wall, `wall` will be `nil`

```lua
-- if mario is touching a wall, climb up it
if m.wall then
    -- freefall gives mario air control and allows him to dive and such
    set_mario_action(m, ACT_FREEFALL, 0)
    m.vel.y = 10

    -- if mario hits A, let him wallkick
    if m.controller.buttonPressed & A_BUTTON ~= 0 then
        m.faceAngle.y = m.faceAngle.y + 0x8000;

        set_mario_action(m, ACT_WALL_KICK_AIR, 0);
    end
end
```

### `floorHeight` and `ceilHeight`

Mario's `floorHeight` is the `y` position of the floor Mario is above. Mario does not need to be standing for this height to be active.

Mario's `ceilHeight` is the `y` position of the ceiling Mario is below. Mario does not need to be hanging from a ceiling or touching a ceiling for this to be active.

In the event Mario goes out of bounds, the `floorHeight` will be calculated from Mario's last valid position rather than Mario's current position.

For the `ceilHeight`, in the event Mario is not under a ceiling, it will be set `gLevelValues.cellHeightLimit`.

The lowest the `floorHeight` will go is `gLevelValues.floorLowerLimit`. The highest a ceiling will go is `gLevelValues.cellHeightLimit`.

```lua
-- give mario a speed boost if he is touching the floor, with a hard-cap of 48
if m.pos.y == m.floorHeight then
    m.forwardVel = math.min(m.forwardVel + 5, 48)
end
```

### `waterLevel`

Mario's `waterLevel` is the `y` coordinate of water under Mario. In the event there is no water under Mario, `waterLevel` will be set to `gLevelValues.floorLowerLimit`.

If Mario's `pos.y` is within 480 units of the `waterLevel`, that means Mario is swimming near the surface.

Different actions check at different offsets for the water level. For instance, when entering a level, to decide when to enter the swimming action, the it checks if `m.pos.y` is less than `m.waterLevel - 100`. However in other instances, notably for checking if mario should transition from swimming to walking, it checks if `m.pos.y` is less than `m.waterLevel - 80`.

Generally, the consensus is if Mario's `m.pos.y` is less than `m.waterLevel - 100`, then Mario is inside water. This is what the check is for all air actions, bubbles, most cutscenes, etc. Just know that this isn't what it is all the time.

```lua
-- give mario the vanish cap if he is underwater
if m.pos.y < m.waterLevel - 100 then
    m.flags = m.flags | MARIO_VANISH_CAP
end
```

### `marioBodyState`

Mario's [`marioBodyState`](../structs.md#mariobodystate) contains a lot of information about the visual state of Mario's player model. Mario's lighting, shading, the held object's last position (HOLP), eye state, hand state, head angle, head pos, and a heck of a lot more.

Take a look at the [`MarioBodyState`](../structs.md#mariobodystate) struct to get a better idea of all the things to look at. Don't be afraid to experiment, that's the best way to learn what the stuff here does!

There's constants for most of these values, most being intuitive, but as a general map:

| Field | Enum or Constant Prefix |
| ----- | ----------------------- |
| `capState` | [`MarioCapGSCId`](../constants.md#enum-mariocapgscid) |
| `eyeState` | [`MarioEyesGSCId`](../constants.md#enum-marioeyesgscid) |
| `handState` | [`MarioHandGSCId`](../constants.md#enum-mariohandgscid) |
| `modelState` | `MODEL_STATE_*` |
| `grabPos` | [`MarioGrabPosGSCId`](../constants.md#enum-mariograbposgscid) |

```lua
-- have mario shout-out world peace
m.marioBodyState.handState = MARIO_HAND_PEACE_SIGN

-- shade mario red
m.marioBodyState.shadeR = 255
```

### `marioObj`

`marioObj` is Mario's self object. It's the object Mario is. Anything you can do with an object you can manipulate using `marioObj`.

Mario's object includes many things you'd find in any object, the gfx data in `m.marioObj.header.gfx`, position, rotation, and scale data, and more.

```lua
-- set mario to be double his normal size
cur_obj_set_scale(m.marioObj, 2)
```

### `heldObj`, `heldByObj`, `interactObj`, `riddenObj`, and `usedObj`

Each of these fields are [`Object`s](../structs.md#object) related to Mario in whatever way is described. All these objects can be `nil`. These fields may point to the same object.

- `interactObj` is the most broad. If Mario is interacting with an object, it'll appear here! It specifically is for *interacting*. Things like poles, the Big Boo's Haunt cage entrance, and more are not included
- `usedObj` is the object Mario is "using." It covers a lot of the same ground as `interactObj`, but includes some things it misses like BBH's cage entrance and poles. It's missing it's fair share of things, such as some `interact_x` function not setting `usedObj`
- `heldObj` is the object Mario is currently holding
- `heldByObj` is the object Mario is being held by, such as King Bob-omb or Chuckya
- `riddenObj` is the object Mario is currently riding. In vanilla, this is only used for the Koopa Shell

There are nuance to these, so experiment if necessary to see which one fits your use case.

```lua
-- send any object mario holds 200 units above him
if m.heldObj then
    local o = m.heldObj
    -- drop_and_set_mario_action sends the object to the holp, which is never set in
    -- this situation, so we need to hardcode oPosX and oPosZ to be set to mario's position
    drop_and_set_mario_action(m, ACT_IDLE, 0)
    o.oPosX = m.pos.x
    o.oPosY = o.oPosY + 300
    o.oPosZ = m.pos.z
end
```
