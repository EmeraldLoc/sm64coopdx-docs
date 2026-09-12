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
    -- Don't process any mario that isn't the local mario
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
-- rotate mario's yaw against his will by 50 units per frame
m.faceAngle.y = m.faceAngle.y + 50
```

### `intendedYaw`

Mario's `intendedYaw` is a `float` that usually is Mario's currently held rotation on the joystick. It's the target yaw for Mario.

```lua
-- if mario is diving, allow for free rotation of the face angle
if m.action == ACT_DIVING then
    m.faceAngle.y = m.intendedYaw
end
```

### `forwardVel`, `vel`, `angleVel`, `slideVelX`, and `slideVelZ`

TODO

### `action`, `actionState`, `actionArg`, `actionTimer`, and `prevAction`

TODO

### `flags`

TODO

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

### `controller`

TODO

### `input`

TODO

### `peakHeight`

TODO

### `wall`, `floor`, and `ceiling`

TODO

### `floorHeight` and `ceilHeight`

TODO

### `waterLevel`

TODO

### `marioBodyState`

TODO

### `heldObj`, `heldByObj`, `interactObj`, `riddenObj`, and `usedObj`

TODO
