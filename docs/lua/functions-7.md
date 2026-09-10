## [:rewind: Lua Functions](functions.md)

---

[< prev](functions-6.md) | [1](functions.md) | [2](functions-2.md) | [3](functions-3.md) | [4](functions-4.md) | [5](functions-5.md) | [6](functions-6.md) | 7]


---
# functions from surface_collision.h

<br />


## find_wall_collisions

### Description
Detects wall collisions at a given position and adjusts the position based on the walls found.
Returns the number of wall collisions detected

### Lua Example
`local integerValue = find_wall_collisions(colData)`

### Parameters
| Field | Type |
| ----- | ---- |
| colData | [WallCollisionData](structs.md#WallCollisionData) |

### Returns
- `integer`

### C Prototype
`s32 find_wall_collisions(struct WallCollisionData *colData);`


## find_ceil

### Description
Finds the height of the highest ceiling above a given position (x, y, z) and return the corresponding ceil surface.
If no ceiling is found, returns the default height limit of `gLevelValues.cellHeightLimit`(20000 by default)

### Lua Example
`local numberValue, pceil = find_ceil(posX, posY, posZ)`

### Parameters
| Field | Type |
| ----- | ---- |
| posX | `number` |
| posY | `number` |
| posZ | `number` |

### Returns
- `number`
- [Surface](structs.md#Surface)

### C Prototype
`f32 find_ceil(f32 posX, f32 posY, f32 posZ, RET struct Surface **pceil);`


## find_ceil_height

### Description
Finds the height of the highest ceiling above a given position (x, y, z).
If no ceiling is found, returns the default height limit of `gLevelValues.cellHeightLimit`(20000 by default)

### Lua Example
`local numberValue = find_ceil_height(x, y, z)`

### Parameters
| Field | Type |
| ----- | ---- |
| x | `number` |
| y | `number` |
| z | `number` |

### Returns
- `number`

### C Prototype
`f32 find_ceil_height(f32 x, f32 y, f32 z);`


## find_floor_height

### Description
Finds the height of the highest floor below a given position (x, y, z).
If no floor is found, returns the default floor height of `gLevelValues.floorLowerLimit`(-11000 by default)

### Lua Example
`local numberValue = find_floor_height(x, y, z)`

### Parameters
| Field | Type |
| ----- | ---- |
| x | `number` |
| y | `number` |
| z | `number` |

### Returns
- `number`

### C Prototype
`f32 find_floor_height(f32 x, f32 y, f32 z);`


## find_floor

### Description
Finds the height of the highest floor below a given position (x, y, z) and return the corresponding floor surface.
If no floor is found, returns the default floor height of `gLevelValues.floorLowerLimit`(-11000 by default)

### Lua Example
`local numberValue, pfloor = find_floor(xPos, yPos, zPos)`

### Parameters
| Field | Type |
| ----- | ---- |
| xPos | `number` |
| yPos | `number` |
| zPos | `number` |

### Returns
- `number`
- [Surface](structs.md#Surface)

### C Prototype
`f32 find_floor(f32 xPos, f32 yPos, f32 zPos, RET struct Surface **pfloor);`


## find_water_level

### Description
Finds the height of water at a given position (x, z), if the position is within a water region.
If no water is found, returns the default height of `gLevelValues.floorLowerLimit`(-11000 by default)

### Lua Example
`local numberValue = find_water_level(x, z)`

### Parameters
| Field | Type |
| ----- | ---- |
| x | `number` |
| z | `number` |

### Returns
- `number`

### C Prototype
`f32 find_water_level(f32 x, f32 z);`


## find_poison_gas_level

### Description
Finds the height of the poison gas at a given position (x, z), if the position is within a gas region.
If no gas is found, returns the default height of `gLevelValues.floorLowerLimit`(-11000 by default)

### Lua Example
`local numberValue = find_poison_gas_level(x, z)`

### Parameters
| Field | Type |
| ----- | ---- |
| x | `number` |
| z | `number` |

### Returns
- `number`

### C Prototype
`f32 find_poison_gas_level(f32 x, f32 z);`


## set_find_wall_direction

### Description
Sets whether collision finding functions should check wall directions.

### Lua Example
`set_find_wall_direction(dir, active, airborne)`

### Parameters
| Field | Type |
| ----- | ---- |
| dir | [Vec3f](structs.md#Vec3f) |
| active | `boolean` |
| airborne | `boolean` |

### Returns
- None

### C Prototype
`void set_find_wall_direction(Vec3f dir, bool active, bool airborne);`


## closest_point_to_triangle

### Description
Gets the closest point of the triangle to `src` and returns it in `out`.

### Lua Example
`closest_point_to_triangle(surf, src, out)`

### Parameters
| Field | Type |
| ----- | ---- |
| surf | [Surface](structs.md#Surface) |
| src | [Vec3f](structs.md#Vec3f) |
| out | [Vec3f](structs.md#Vec3f) |

### Returns
- None

### C Prototype
`void closest_point_to_triangle(struct Surface* surf, Vec3f src, VEC_OUT Vec3f out);`


---
# functions from surface_load.h

<br />


## load_object_collision_model

### Description
Loads the object's collision data into dynamic collision.
You must run this every frame in your object's behavior loop for it to have collision

### Lua Example
`load_object_collision_model()`

### Parameters
- None

### Returns
- None

### C Prototype
`void load_object_collision_model(void);`


## load_static_object_collision

### Description
Loads the object's collision data into static collision.
You may run this only once to capture the object's collision at that frame.

### Lua Example
`local staticObjectCollisionValue = load_static_object_collision()`

### Parameters
- None

### Returns
- [StaticObjectCollision](structs.md#StaticObjectCollision)

### C Prototype
`struct StaticObjectCollision *load_static_object_collision();`


## toggle_static_object_collision

### Description
Toggles a collection of static object surfaces

### Lua Example
`toggle_static_object_collision(col, tangible)`

### Parameters
| Field | Type |
| ----- | ---- |
| col | [StaticObjectCollision](structs.md#StaticObjectCollision) |
| tangible | `boolean` |

### Returns
- None

### C Prototype
`void toggle_static_object_collision(struct StaticObjectCollision *col, bool tangible);`


## get_static_object_surface

### Description
Gets a surface corresponding to `index` from the static object collision

### Lua Example
`local surfaceValue = get_static_object_surface(col, index)`

### Parameters
| Field | Type |
| ----- | ---- |
| col | [StaticObjectCollision](structs.md#StaticObjectCollision) |
| index | `integer` |

### Returns
- [Surface](structs.md#Surface)

### C Prototype
`struct Surface *get_static_object_surface(struct StaticObjectCollision *col, u32 index);`


## remove_static_object_collision

### Description
Removes all surfaces belonging to a static object collision and reclaims the SOC metadata

### Lua Example
`remove_static_object_collision(col)`

### Parameters
| Field | Type |
| ----- | ---- |
| col | [StaticObjectCollision](structs.md#StaticObjectCollision) |

### Returns
- None

### C Prototype
`void remove_static_object_collision(struct StaticObjectCollision *col);`


## obj_get_surface_from_index

### Description
Gets a surface corresponding to `index` from the surface pool buffer

### Lua Example
`local surfaceValue = obj_get_surface_from_index(o, index)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| index | `integer` |

### Returns
- [Surface](structs.md#Surface)

### C Prototype
`struct Surface *obj_get_surface_from_index(struct Object *o, u32 index);`


## surface_has_force

### Description
Checks if a surface has force

### Lua Example
`local booleanValue = surface_has_force(surfaceType)`

### Parameters
| Field | Type |
| ----- | ---- |
| surfaceType | `integer` |

### Returns
- `boolean`

### C Prototype
`bool surface_has_force(s16 surfaceType);`


---
# functions from sync_object.h

<br />


## sync_object_get_random_seed

### Description
Retrieves the random seed of a sync object from its sync ID

### Lua Example
`local integerValue = sync_object_get_random_seed(syncId)`

### Parameters
| Field | Type |
| ----- | ---- |
| syncId | `integer` |

### Returns
- `integer`

### C Prototype
`u16 sync_object_get_random_seed(u32 syncId);`


## sync_object_get_object

### Description
Retrieves an object from a sync ID

### Lua Example
`local objectValue = sync_object_get_object(syncId)`

### Parameters
| Field | Type |
| ----- | ---- |
| syncId | `integer` |

### Returns
- [Object](structs.md#Object)

### C Prototype
`struct Object* sync_object_get_object(u32 syncId);`


## sync_object_is_initialized

### Description
Checks if a sync object is initialized using a `syncId`

### Lua Example
`local booleanValue = sync_object_is_initialized(syncId)`

### Parameters
| Field | Type |
| ----- | ---- |
| syncId | `integer` |

### Returns
- `boolean`

### C Prototype
`bool sync_object_is_initialized(u32 syncId);`


## sync_object_is_owned_locally

### Description
Checks if a sync object is owned locally using a `syncId`

### Lua Example
`local booleanValue = sync_object_is_owned_locally(syncId)`

### Parameters
| Field | Type |
| ----- | ---- |
| syncId | `integer` |

### Returns
- `boolean`

### C Prototype
`bool sync_object_is_owned_locally(u32 syncId);`


---

[< prev](functions-6.md) | [1](functions.md) | [2](functions-2.md) | [3](functions-3.md) | [4](functions-4.md) | [5](functions-5.md) | [6](functions-6.md) | 7]

