## [:rewind: Lua Functions](functions.md)

---

[< prev](functions-4.md) | [1](functions.md) | [2](functions-2.md) | [3](functions-3.md) | [4](functions-4.md) | 5 | [6](functions-6.md) | [7](functions-7.md) | [next >](functions-6.md)

---

# functions from mod_fs.h

## mod_fs_exists

### Description

Checks the existence of a modfs at path `modPath` or for the active mod if not provided. Checking for the existence of a private modfs will return false, even if it exists

### Lua Example

`local booleanValue, err = mod_fs_exists(modPath)`

### Parameters

| Field | Type |
| ----- | ---- |
| modPath | `string` |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_exists(OPTIONAL const char *modPath, RET enum ModFsErrorCode *err);`

## mod_fs_get

### Description

Gets the modfs object at path `modPath` or the active mod one if not provided. This function will return nil for a private modfs, even if it exists

### Lua Example

`local modFsValue, err = mod_fs_get(modPath)`

### Parameters

| Field | Type |
| ----- | ---- |
| modPath | `string` |

### Returns

- [ModFs](structs.md#ModFs)
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`struct ModFs *mod_fs_get(OPTIONAL const char *modPath, RET enum ModFsErrorCode *err);`

## mod_fs_reload

### Description

Reloads the modfs object at path `modPath`. This function will return nil for a private modfs, even if it exists

### Lua Example

`local modFsValue, err = mod_fs_reload(modPath)`

### Parameters

| Field | Type |
| ----- | ---- |
| modPath | `string` |

### Returns

- [ModFs](structs.md#ModFs)
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`struct ModFs *mod_fs_reload(OPTIONAL const char *modPath, RET enum ModFsErrorCode *err);`

## mod_fs_create

### Description

Creates a modfs object for the active mod if it doesn't exist. Returns the modfs object on success

### Lua Example

`local modFsValue, err = mod_fs_create()`

### Parameters

- None

### Returns

- [ModFs](structs.md#ModFs)
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`struct ModFs *mod_fs_create(RET enum ModFsErrorCode *err);`

## mod_fs_get_filename

### Description

Gets the filename at position `index` of the provided `modFs`

### Lua Example

`local stringValue, err = mod_fs_get_filename(modFs, index)`

### Parameters

| Field | Type |
| ----- | ---- |
| modFs | [ModFs](structs.md#ModFs) |
| index | `integer` |

### Returns

- `string`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`const char *mod_fs_get_filename(struct ModFs *modFs, u16 index, RET enum ModFsErrorCode *err);`

## mod_fs_get_file

### Description

Gets the file object at path `filepath` of the provided `modFs`. This function will return nil for a private modfs file, even if it exists

### Lua Example

`local modFsFileValue, err = mod_fs_get_file(modFs, filepath)`

### Parameters

| Field | Type |
| ----- | ---- |
| modFs | [ModFs](structs.md#ModFs) |
| filepath | `string` |

### Returns

- [ModFsFile](structs.md#ModFsFile)
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`struct ModFsFile *mod_fs_get_file(struct ModFs *modFs, const char *filepath, RET enum ModFsErrorCode *err);`

## mod_fs_create_file

### Description

Creates a new file at path `filepath` for the provided `modFs`. Set `text` to true to treat the file as a pure text file, not a binary file. Returns the created file on success

### Lua Example

`local modFsFileValue, err = mod_fs_create_file(modFs, filepath, text)`

### Parameters

| Field | Type |
| ----- | ---- |
| modFs | [ModFs](structs.md#ModFs) |
| filepath | `string` |
| text | `boolean` |

### Returns

- [ModFsFile](structs.md#ModFsFile)
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`struct ModFsFile *mod_fs_create_file(struct ModFs *modFs, const char *filepath, bool text, RET enum ModFsErrorCode *err);`

## mod_fs_move_file

### Description

Moves the file at path `oldpath` to `newpath` of the provided `modFs`. Set `overwriteExisting` to true to overwrite the file at path `newpath` if it exists. Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_move_file(modFs, oldpath, newpath, overwriteExisting)`

### Parameters

| Field | Type |
| ----- | ---- |
| modFs | [ModFs](structs.md#ModFs) |
| oldpath | `string` |
| newpath | `string` |
| overwriteExisting | `boolean` |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_move_file(struct ModFs *modFs, const char *oldpath, const char *newpath, bool overwriteExisting, RET enum ModFsErrorCode *err);`

## mod_fs_copy_file

### Description

Copies the file at path `srcpath` to `dstpath` of the provided `modFs`. Set `overwriteExisting` to true to overwrite the file at path `dstpath` if it exists. Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_copy_file(modFs, srcpath, dstpath, overwriteExisting)`

### Parameters

| Field | Type |
| ----- | ---- |
| modFs | [ModFs](structs.md#ModFs) |
| srcpath | `string` |
| dstpath | `string` |
| overwriteExisting | `boolean` |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_copy_file(struct ModFs *modFs, const char *srcpath, const char *dstpath, bool overwriteExisting, RET enum ModFsErrorCode *err);`

## mod_fs_delete_file

### Description

Deletes the file at path `filepath` of the provided `modFs`. Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_delete_file(modFs, filepath)`

### Parameters

| Field | Type |
| ----- | ---- |
| modFs | [ModFs](structs.md#ModFs) |
| filepath | `string` |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_delete_file(struct ModFs *modFs, const char *filepath, RET enum ModFsErrorCode *err);`

## mod_fs_clear

### Description

Deletes all files of the provided `modFs`. Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_clear(modFs)`

### Parameters

| Field | Type |
| ----- | ---- |
| modFs | [ModFs](structs.md#ModFs) |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_clear(struct ModFs *modFs, RET enum ModFsErrorCode *err);`

## mod_fs_save

### Description

Saves the provided `modFs` to persistent storage. Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_save(modFs)`

### Parameters

| Field | Type |
| ----- | ---- |
| modFs | [ModFs](structs.md#ModFs) |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_save(struct ModFs *modFs, RET enum ModFsErrorCode *err);`

## mod_fs_delete

### Description

Removes the provided `modFs` from persistent storage and deletes its object. Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_delete(modFs)`

### Parameters

| Field | Type |
| ----- | ---- |
| modFs | [ModFs](structs.md#ModFs) |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_delete(struct ModFs *modFs, RET enum ModFsErrorCode *err);`

## mod_fs_set_public

### Description

Marks the provided `modFs` as public (i.e. readable by other mods). Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_set_public(modFs, pub)`

### Parameters

| Field | Type |
| ----- | ---- |
| modFs | [ModFs](structs.md#ModFs) |
| pub | `boolean` |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_set_public(struct ModFs *modFs, bool pub, RET enum ModFsErrorCode *err);`

## mod_fs_file_read_bool

### Description

Reads a boolean from a binary modfs `file`

### Lua Example

`local booleanValue, err = mod_fs_file_read_bool(file)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_file_read_bool(struct ModFsFile *file, RET enum ModFsErrorCode *err);`

## mod_fs_file_read_integer

### Description

Reads an integer from a binary modfs `file`. `intType` must be one of the `INT_TYPE_*` constants

### Lua Example

`local integerValue, err = mod_fs_file_read_integer(file, intType)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |
| intType | [enum ModFsFileIntType](constants.md#enum-ModFsFileIntType) |

### Returns

- `integer`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`lua_Integer mod_fs_file_read_integer(struct ModFsFile *file, enum ModFsFileIntType intType, RET enum ModFsErrorCode *err);`

## mod_fs_file_read_number

### Description

Reads an floating-point number from a binary modfs `file`. `floatType` must be one of the `FLOAT_TYPE_*` constants

### Lua Example

`local numberValue, err = mod_fs_file_read_number(file, floatType)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |
| floatType | [enum ModFsFileFloatType](constants.md#enum-ModFsFileFloatType) |

### Returns

- `number`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`lua_Number mod_fs_file_read_number(struct ModFsFile *file, enum ModFsFileFloatType floatType, RET enum ModFsErrorCode *err);`

## mod_fs_file_read_bytes

### Description

Reads a bytestring of `length` bytes from a binary modfs `file`

### Lua Example

`local stringValue, err = mod_fs_file_read_bytes(file, length)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |
| length | `integer` |

### Returns

- `string`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`ByteString mod_fs_file_read_bytes(struct ModFsFile *file, u32 length, RET enum ModFsErrorCode *err);`

## mod_fs_file_read_string

### Description

Reads a string from a binary modfs `file`, or read the whole content of a text modfs `file`

### Lua Example

`local stringValue, err = mod_fs_file_read_string(file)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |

### Returns

- `string`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`const char *mod_fs_file_read_string(struct ModFsFile *file, RET enum ModFsErrorCode *err);`

## mod_fs_file_read_line

### Description

Reads a line from a text modfs `file`

### Lua Example

`local stringValue, err = mod_fs_file_read_line(file)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |

### Returns

- `string`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`const char *mod_fs_file_read_line(struct ModFsFile *file, RET enum ModFsErrorCode *err);`

## mod_fs_file_write_bool

### Description

Writes a boolean to a binary modfs `file`. Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_file_write_bool(file, value)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |
| value | `boolean` |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_file_write_bool(struct ModFsFile *file, bool value, RET enum ModFsErrorCode *err);`

## mod_fs_file_write_integer

### Description

Writes an integer to a binary modfs `file`. `intType` must be one of the `INT_TYPE_*` constants. Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_file_write_integer(file, value, intType)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |
| value | `integer` |
| intType | [enum ModFsFileIntType](constants.md#enum-ModFsFileIntType) |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_file_write_integer(struct ModFsFile *file, lua_Integer value, enum ModFsFileIntType intType, RET enum ModFsErrorCode *err);`

## mod_fs_file_write_number

### Description

Writes an floating-point number to a binary modfs `file`. `floatType` must be one of the `FLOAT_TYPE_*` constants. Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_file_write_number(file, value, floatType)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |
| value | `number` |
| floatType | [enum ModFsFileFloatType](constants.md#enum-ModFsFileFloatType) |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_file_write_number(struct ModFsFile *file, lua_Number value, enum ModFsFileFloatType floatType, RET enum ModFsErrorCode *err);`

## mod_fs_file_write_bytes

### Description

Writes a bytestring to a modfs `file`. Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_file_write_bytes(file, bytestring)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |
| bytestring | `string` |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_file_write_bytes(struct ModFsFile *file, ByteString bytestring, RET enum ModFsErrorCode *err);`

## mod_fs_file_write_string

### Description

Writes a string to a modfs `file`. Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_file_write_string(file, str)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |
| str | `string` |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_file_write_string(struct ModFsFile *file, const char *str, RET enum ModFsErrorCode *err);`

## mod_fs_file_write_line

### Description

Writes a line to a text modfs `file`. Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_file_write_line(file, str)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |
| str | `string` |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_file_write_line(struct ModFsFile *file, const char *str, RET enum ModFsErrorCode *err);`

## mod_fs_file_seek

### Description

Sets the current position of a modfs `file`.
If `origin` is `FILE_SEEK_SET`, file position is set to `offset`.
If `origin` is `FILE_SEEK_CUR`, `offset` is added to file current position.
If `origin` is `FILE_SEEK_END`, file position is set to `end of file + offset`.
Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_file_seek(file, offset, origin)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |
| offset | `integer` |
| origin | [enum ModFsFileSeek](constants.md#enum-ModFsFileSeek) |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_file_seek(struct ModFsFile *file, s32 offset, enum ModFsFileSeek origin, RET enum ModFsErrorCode *err);`

## mod_fs_file_rewind

### Description

Sets the current position of a modfs `file` to its beginning.
Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_file_rewind(file)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_file_rewind(struct ModFsFile *file, RET enum ModFsErrorCode *err);`

## mod_fs_file_is_eof

### Description

Returns true if the provided modfs `file` has reached its end of file

### Lua Example

`local booleanValue, err = mod_fs_file_is_eof(file)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_file_is_eof(struct ModFsFile *file, RET enum ModFsErrorCode *err);`

## mod_fs_file_fill

### Description

Fills a modfs `file` with `byte` repeated `length` times. Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_file_fill(file, byte, length)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |
| byte | `integer` |
| length | `integer` |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_file_fill(struct ModFsFile *file, u8 byte, u32 length, RET enum ModFsErrorCode *err);`

## mod_fs_file_erase

### Description

Erases `length` bytes or characters from a modfs `file`. Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_file_erase(file, length)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |
| length | `integer` |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_file_erase(struct ModFsFile *file, u32 length, RET enum ModFsErrorCode *err);`

## mod_fs_file_set_text_mode

### Description

Marks the provided modfs `file` as text. Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_file_set_text_mode(file, text)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |
| text | `boolean` |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_file_set_text_mode(struct ModFsFile *file, bool text, RET enum ModFsErrorCode *err);`

## mod_fs_file_set_public

### Description

Marks the provided modfs `file` as public (i.e. readable by other mods). Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_file_set_public(file, pub)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |
| pub | `boolean` |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_file_set_public(struct ModFsFile *file, bool pub, RET enum ModFsErrorCode *err);`

## mod_fs_file_set_compression

### Description

Sets the compression level of the provided modfs `file`. Must be between 0 (no compression) and 9 (most compression). Returns true on success

### Lua Example

`local booleanValue, err = mod_fs_file_set_compression(file, level)`

### Parameters

| Field | Type |
| ----- | ---- |
| file | [ModFsFile](structs.md#ModFsFile) |
| level | `integer` |

### Returns

- `boolean`
- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`bool mod_fs_file_set_compression(struct ModFsFile *file, s32 level, RET enum ModFsErrorCode *err);`

## mod_fs_hide_errors

### Description

Hides script errors raised by `mod_fs` functions. Errors messages are still generated and can be retrieved with `mod_fs_get_last_error()`

### Lua Example

`mod_fs_hide_errors(hide)`

### Parameters

| Field | Type |
| ----- | ---- |
| hide | `boolean` |

### Returns

- None

### C Prototype

`void mod_fs_hide_errors(bool hide);`

## mod_fs_get_last_error_code

### Description

Returns the last error code raised by `mod_fs` functions

### Lua Example

`local enumValue = mod_fs_get_last_error_code()`

### Parameters

- None

### Returns

- [enum ModFsErrorCode](constants.md#enum-ModFsErrorCode)

### C Prototype

`enum ModFsErrorCode mod_fs_get_last_error_code();`

## mod_fs_get_last_error

### Description

Returns the last error message generated by `mod_fs` functions or nil if no error occurred

### Lua Example

`local stringValue = mod_fs_get_last_error()`

### Parameters

- None

### Returns

- `string`

### C Prototype

`const char *mod_fs_get_last_error();`

---

# functions from mod_storage.h

## mod_storage_save

### Description

Saves a `key` corresponding to a string `value` to mod storage

### Lua Example

`local booleanValue = mod_storage_save(key, value)`

### Parameters

| Field | Type |
| ----- | ---- |
| key | `string` |
| value | `string` |

### Returns

- `boolean`

### C Prototype

`bool mod_storage_save(const char* key, const char* value);`

## mod_storage_save_integer

### Description

Saves a `key` corresponding to an integer `value` to mod storage

### Lua Example

`local booleanValue = mod_storage_save_integer(key, value)`

### Parameters

| Field | Type |
| ----- | ---- |
| key | `string` |
| value | `integer` |

### Returns

- `boolean`

### C Prototype

`bool mod_storage_save_integer(const char* key, lua_Integer value);`

## mod_storage_save_number

### Description

Saves a `key` corresponding to a number `value` to mod storage

### Lua Example

`local booleanValue = mod_storage_save_number(key, value)`

### Parameters

| Field | Type |
| ----- | ---- |
| key | `string` |
| value | `number` |

### Returns

- `boolean`

### C Prototype

`bool mod_storage_save_number(const char* key, lua_Number value);`

## mod_storage_save_bool

### Description

Saves a `key` corresponding to a bool `value` to mod storage

### Lua Example

`local booleanValue = mod_storage_save_bool(key, value)`

### Parameters

| Field | Type |
| ----- | ---- |
| key | `string` |
| value | `boolean` |

### Returns

- `boolean`

### C Prototype

`bool mod_storage_save_bool(const char* key, bool value);`

## mod_storage_load

### Description

Loads a string `value` from a `key` in mod storage. If the `key` is not found, returns `defaultValue` or `nil`

### Lua Example

`local stringValue = mod_storage_load(key, defaultValue)`

### Parameters

| Field | Type |
| ----- | ---- |
| key | `string` |
| defaultValue | `string` |

### Returns

- `string`

### C Prototype

`const char *mod_storage_load(const char* key, OPTIONAL const char* defaultValue);`

## mod_storage_load_integer

### Description

Loads an integer `value` from a `key` in mod storage. If the `key` is not found, returns `defaultValue` or `0`

### Lua Example

`local integerValue = mod_storage_load_integer(key, defaultValue)`

### Parameters

| Field | Type |
| ----- | ---- |
| key | `string` |
| defaultValue | `integer` |

### Returns

- `integer`

### C Prototype

`lua_Integer mod_storage_load_integer(const char* key, OPTIONAL lua_Integer defaultValue);`

## mod_storage_load_number

### Description

Loads a number `value` from a `key` in mod storage. If the `key` is not found, returns `defaultValue` or `0`

### Lua Example

`local numberValue = mod_storage_load_number(key, defaultValue)`

### Parameters

| Field | Type |
| ----- | ---- |
| key | `string` |
| defaultValue | `number` |

### Returns

- `number`

### C Prototype

`lua_Number mod_storage_load_number(const char* key, OPTIONAL lua_Number defaultValue);`

## mod_storage_load_bool

### Description

Loads a bool `value` from a `key` in mod storage. If the `key` is not found, returns `defaultValue` or `false`

### Lua Example

`local booleanValue = mod_storage_load_bool(key, defaultValue)`

### Parameters

| Field | Type |
| ----- | ---- |
| key | `string` |
| defaultValue | `boolean` |

### Returns

- `boolean`

### C Prototype

`bool mod_storage_load_bool(const char* key, OPTIONAL bool defaultValue);`

## mod_storage_load_all

### Description

Loads all keys and values in mod storage as strings and returns them as a table

### Lua Example

`local tableValue = mod_storage_load_all()`

### Parameters

- None

### Returns

- `table`

### C Prototype

`LuaTable mod_storage_load_all(void);`

## mod_storage_exists

### Description

Checks if a `key` is in mod storage

### Lua Example

`local booleanValue = mod_storage_exists(key)`

### Parameters

| Field | Type |
| ----- | ---- |
| key | `string` |

### Returns

- `boolean`

### C Prototype

`bool mod_storage_exists(const char* key);`

## mod_storage_remove

### Description

Removes a `key` from mod storage

### Lua Example

`local booleanValue = mod_storage_remove(key)`

### Parameters

| Field | Type |
| ----- | ---- |
| key | `string` |

### Returns

- `boolean`

### C Prototype

`bool mod_storage_remove(const char* key);`

## mod_storage_clear

### Description

Clears the mod's data from mod storage

### Lua Example

`local booleanValue = mod_storage_clear()`

### Parameters

- None

### Returns

- `boolean`

### C Prototype

`bool mod_storage_clear(void);`

---

# functions from network_player.h

## network_player_connected_count

### Description

Gets the amount of players connected

### Lua Example

`local integerValue = network_player_connected_count()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`u8 network_player_connected_count(void);`

## network_player_set_description

### Description

Sets the description field of `np`

### Lua Example

`network_player_set_description(np, description, r, g, b, a)`

### Parameters

| Field | Type |
| ----- | ---- |
| np | [NetworkPlayer](structs.md#NetworkPlayer) |
| description | `string` |
| r | `integer` |
| g | `integer` |
| b | `integer` |
| a | `integer` |

### Returns

- None

### C Prototype

`void network_player_set_description(struct NetworkPlayer* np, const char* description, u8 r, u8 g, u8 b, u8 a);`

## network_player_set_override_location

### Description

Overrides the location of `np`

### Lua Example

`network_player_set_override_location(np, location)`

### Parameters

| Field | Type |
| ----- | ---- |
| np | [NetworkPlayer](structs.md#NetworkPlayer) |
| location | `string` |

### Returns

- None

### C Prototype

`void network_player_set_override_location(struct NetworkPlayer *np, const char *location);`

## network_player_from_global_index

### Description

Gets a network player from `globalIndex`

### Lua Example

`local networkPlayerValue = network_player_from_global_index(globalIndex)`

### Parameters

| Field | Type |
| ----- | ---- |
| globalIndex | `integer` |

### Returns

- [NetworkPlayer](structs.md#NetworkPlayer)

### C Prototype

`struct NetworkPlayer* network_player_from_global_index(u8 globalIndex);`

## get_network_player_from_level

### Description

Gets the first network player whose information matches `courseNum`, `actNum`, and `levelNum`

### Lua Example

`local networkPlayerValue = get_network_player_from_level(courseNum, actNum, levelNum)`

### Parameters

| Field | Type |
| ----- | ---- |
| courseNum | `integer` |
| actNum | `integer` |
| levelNum | `integer` |

### Returns

- [NetworkPlayer](structs.md#NetworkPlayer)

### C Prototype

`struct NetworkPlayer* get_network_player_from_level(s16 courseNum, s16 actNum, s16 levelNum);`

## get_network_player_from_area

### Description

Gets the first network player whose information matches `courseNum`, `actNum`, `levelNum`, and `areaIndex`

### Lua Example

`local networkPlayerValue = get_network_player_from_area(courseNum, actNum, levelNum, areaIndex)`

### Parameters

| Field | Type |
| ----- | ---- |
| courseNum | `integer` |
| actNum | `integer` |
| levelNum | `integer` |
| areaIndex | `integer` |

### Returns

- [NetworkPlayer](structs.md#NetworkPlayer)

### C Prototype

`struct NetworkPlayer* get_network_player_from_area(s16 courseNum, s16 actNum, s16 levelNum, s16 areaIndex);`

## get_network_player_smallest_global

### Description

Gets the active network player with the smallest global index. Useful for assigning one player to "own" some kind of functionality or object

### Lua Example

`local networkPlayerValue = get_network_player_smallest_global()`

### Parameters

- None

### Returns

- [NetworkPlayer](structs.md#NetworkPlayer)

### C Prototype

`struct NetworkPlayer* get_network_player_smallest_global(void);`

## network_player_set_override_palette_color

### Description

Sets the `part in `np`'s override color palette`

### Lua Example

`network_player_set_override_palette_color(np, part, color)`

### Parameters

| Field | Type |
| ----- | ---- |
| np | [NetworkPlayer](structs.md#NetworkPlayer) |
| part | [enum PlayerPart](constants.md#enum-PlayerPart) |
| color | [Color](structs.md#Color) |

### Returns

- None

### C Prototype

`void network_player_set_override_palette_color(struct NetworkPlayer *np, enum PlayerPart part, Color color);`

## network_player_reset_override_palette

### Description

Resets `np`'s override color palette

### Lua Example

`network_player_reset_override_palette(np)`

### Parameters

| Field | Type |
| ----- | ---- |
| np | [NetworkPlayer](structs.md#NetworkPlayer) |

### Returns

- None

### C Prototype

`void network_player_reset_override_palette(struct NetworkPlayer *np);`

## network_player_is_override_palette_same

### Description

Checks if `np`'s override color palette is identical to the regular color palette

### Lua Example

`local booleanValue = network_player_is_override_palette_same(np)`

### Parameters

| Field | Type |
| ----- | ---- |
| np | [NetworkPlayer](structs.md#NetworkPlayer) |

### Returns

- `boolean`

### C Prototype

`bool network_player_is_override_palette_same(struct NetworkPlayer *np);`

---

# functions from network_utils.h

## network_global_index_from_local

### Description

Gets a player's global index from their local index

### Lua Example

`local integerValue = network_global_index_from_local(localIndex)`

### Parameters

| Field | Type |
| ----- | ---- |
| localIndex | `integer` |

### Returns

- `integer`

### C Prototype

`u8 network_global_index_from_local(u8 localIndex);`

## network_local_index_from_global

### Description

Gets a player's local index from their global index

### Lua Example

`local integerValue = network_local_index_from_global(globalIndex)`

### Parameters

| Field | Type |
| ----- | ---- |
| globalIndex | `integer` |

### Returns

- `integer`

### C Prototype

`u8 network_local_index_from_global(u8 globalIndex);`

## network_is_server

### Description

Checks if you are hosting the current lobby, this value doesn't change

### Lua Example

`local booleanValue = network_is_server()`

### Parameters

- None

### Returns

- `boolean`

### C Prototype

`bool network_is_server(void);`

## network_is_moderator

### Description

Checks if you are a moderator in the current lobby

### Lua Example

`local booleanValue = network_is_moderator()`

### Parameters

- None

### Returns

- `boolean`

### C Prototype

`bool network_is_moderator(void);`

## network_get_player_text_color_string

### Description

Gets the DJUI hex color code string for the player corresponding to `localIndex`'s cap color

### Lua Example

`local stringValue = network_get_player_text_color_string(localIndex)`

### Parameters

| Field | Type |
| ----- | ---- |
| localIndex | `integer` |

### Returns

- `string`

### C Prototype

`const char* network_get_player_text_color_string(u8 localIndex);`

## network_check_singleplayer_pause

### Description

Checks if the game can currently be paused in singleplayer

### Lua Example

`local booleanValue = network_check_singleplayer_pause()`

### Parameters

- None

### Returns

- `boolean`

### C Prototype

`bool network_check_singleplayer_pause(void);`

## network_discord_id_from_local_index

### Description

Gets a Discord ID corresponding to the network player with `localIndex`

### Lua Example

`local stringValue = network_discord_id_from_local_index(localIndex)`

### Parameters

| Field | Type |
| ----- | ---- |
| localIndex | `integer` |

### Returns

- `string`

### C Prototype

`const char* network_discord_id_from_local_index(u8 localIndex);`

---

# functions from obj_behaviors.c

## set_yoshi_as_not_dead

### Description

Marks Yoshi as alive

### Lua Example

`set_yoshi_as_not_dead()`

### Parameters

- None

### Returns

- None

### C Prototype

`void set_yoshi_as_not_dead(void);`

## obj_find_wall

### Description

Finds any wall collisions, applies them, and turns away from the surface

### Lua Example

`local integerValue = obj_find_wall(objNewX, objY, objNewZ, objVelX, objVelZ)`

### Parameters

| Field | Type |
| ----- | ---- |
| objNewX | `number` |
| objY | `number` |
| objNewZ | `number` |
| objVelX | `number` |
| objVelZ | `number` |

### Returns

- `integer`

### C Prototype

`s8 obj_find_wall(f32 objNewX, f32 objY, f32 objNewZ, f32 objVelX, f32 objVelZ);`

## turn_obj_away_from_steep_floor

### Description

Turns an object away from steep floors, similarly to walls

### Lua Example

`local integerValue = turn_obj_away_from_steep_floor(objFloor, floorY, objVelX, objVelZ)`

### Parameters

| Field | Type |
| ----- | ---- |
| objFloor | [Surface](structs.md#Surface) |
| floorY | `number` |
| objVelX | `number` |
| objVelZ | `number` |

### Returns

- `integer`

### C Prototype

`s8 turn_obj_away_from_steep_floor(struct Surface *objFloor, f32 floorY, f32 objVelX, f32 objVelZ);`

## obj_orient_graph

### Description

Orients an object with the given normals, typically the surface under the object

### Lua Example

`obj_orient_graph(obj, normalX, normalY, normalZ)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| normalX | `number` |
| normalY | `number` |
| normalZ | `number` |

### Returns

- None

### C Prototype

`void obj_orient_graph(struct Object *obj, f32 normalX, f32 normalY, f32 normalZ);`

## calc_obj_friction

### Description

Determines an object's forward speed multiplier

### Lua Example

`local objFriction = calc_obj_friction(floor_nY)`

### Parameters

| Field | Type |
| ----- | ---- |
| floor_nY | `number` |

### Returns

- `number`

### C Prototype

`void calc_obj_friction(RET f32 *objFriction, f32 floor_nY);`

## calc_new_obj_vel_and_pos_y

### Description

Updates an objects speed for gravity and updates Y position

### Lua Example

`calc_new_obj_vel_and_pos_y(objFloor, objFloorY, objVelX, objVelZ)`

### Parameters

| Field | Type |
| ----- | ---- |
| objFloor | [Surface](structs.md#Surface) |
| objFloorY | `number` |
| objVelX | `number` |
| objVelZ | `number` |

### Returns

- None

### C Prototype

`void calc_new_obj_vel_and_pos_y(struct Surface *objFloor, f32 objFloorY, f32 objVelX, f32 objVelZ);`

## calc_new_obj_vel_and_pos_y_underwater

### Description

Adjusts the current object's veloicty and y position for being underwater

### Lua Example

`calc_new_obj_vel_and_pos_y_underwater(objFloor, floorY, objVelX, objVelZ, waterY)`

### Parameters

| Field | Type |
| ----- | ---- |
| objFloor | [Surface](structs.md#Surface) |
| floorY | `number` |
| objVelX | `number` |
| objVelZ | `number` |
| waterY | `number` |

### Returns

- None

### C Prototype

`void calc_new_obj_vel_and_pos_y_underwater(struct Surface *objFloor, f32 floorY, f32 objVelX, f32 objVelZ, f32 waterY);`

## obj_update_pos_vel_xz

### Description

Updates an objects position from forward velocity and move angle yaw

### Lua Example

`obj_update_pos_vel_xz()`

### Parameters

- None

### Returns

- None

### C Prototype

`void obj_update_pos_vel_xz(void);`

## obj_splash

### Description

Generates splashes if at surface of water, entering water, or bubbles if underwater

### Lua Example

`obj_splash(waterY, objY)`

### Parameters

| Field | Type |
| ----- | ---- |
| waterY | `integer` |
| objY | `integer` |

### Returns

- None

### C Prototype

`void obj_splash(s32 waterY, s32 objY);`

## object_step

### Description

Generic object move function. Handles walls, water, floors, and gravity.
Returns flags for certain interactions

### Lua Example

`local integerValue = object_step()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s16 object_step(void);`

## object_step_without_floor_orient

### Description

Takes an object step but does not orient with the object's floor.
Used for boulders, falling pillars, and the rolling snowman body

### Lua Example

`local integerValue = object_step_without_floor_orient()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s16 object_step_without_floor_orient(void);`

## obj_move_xyz_using_fvel_and_yaw

### Description

Updates the object `obj` horizontal velocity using its forward velocity and move angle yaw, then moves it

### Lua Example

`obj_move_xyz_using_fvel_and_yaw(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_move_xyz_using_fvel_and_yaw(struct Object *obj);`

## is_point_within_radius_of_mario

### Description

Checks if a point is within distance from any active Mario visible to objects' graphical position

### Lua Example

`local integerValue = is_point_within_radius_of_mario(x, y, z, dist)`

### Parameters

| Field | Type |
| ----- | ---- |
| x | `number` |
| y | `number` |
| z | `number` |
| dist | `integer` |

### Returns

- `integer`

### C Prototype

`s8 is_point_within_radius_of_mario(f32 x, f32 y, f32 z, s32 dist);`

## is_point_within_radius_of_any_player

### Description

Checks if a point is within distance from any active Mario's graphical position

### Lua Example

`local integerValue = is_point_within_radius_of_any_player(x, y, z, dist)`

### Parameters

| Field | Type |
| ----- | ---- |
| x | `number` |
| y | `number` |
| z | `number` |
| dist | `integer` |

### Returns

- `integer`

### C Prototype

`s8 is_point_within_radius_of_any_player(f32 x, f32 y, f32 z, s32 dist);`

## is_player_active

### Description

Checks if `m` is in the current course/act/level/area and isn't bubbled

### Lua Example

`local integerValue = is_player_active(m)`

### Parameters

| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |

### Returns

- `integer`

### C Prototype

`u8 is_player_active(struct MarioState* m);`

## is_other_player_active

### Description

Checks if any player besides the local player is in the current course/act/level/area

### Lua Example

`local integerValue = is_other_player_active()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`u8 is_other_player_active(void);`

## is_player_in_local_area

### Description

Checks if `m` is in the current course/act/level/area

### Lua Example

`local integerValue = is_player_in_local_area(m)`

### Parameters

| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |

### Returns

- `integer`

### C Prototype

`u8 is_player_in_local_area(struct MarioState* m);`

## nearest_mario_state_to_object

### Description

Gets the nearest active Mario who isn't bubbled to `obj`

### Lua Example

`local marioStateValue = nearest_mario_state_to_object(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- [MarioState](structs.md#MarioState)

### C Prototype

`struct MarioState* nearest_mario_state_to_object(struct Object *obj);`

## nearest_possible_mario_state_to_object

### Description

Gets the nearest possible Mario to `obj` despite anything like bubbled state or enemy visibility

### Lua Example

`local marioStateValue = nearest_possible_mario_state_to_object(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- [MarioState](structs.md#MarioState)

### C Prototype

`struct MarioState* nearest_possible_mario_state_to_object(struct Object *obj);`

## nearest_player_to_object

### Description

Gets the nearest player (Mario Object) to `obj`

### Lua Example

`local objectValue = nearest_player_to_object(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- [Object](structs.md#Object)

### C Prototype

`struct Object* nearest_player_to_object(struct Object *obj);`

## nearest_interacting_mario_state_to_object

### Description

Gets the nearest interacting Mario to `obj`

### Lua Example

`local marioStateValue = nearest_interacting_mario_state_to_object(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- [MarioState](structs.md#MarioState)

### C Prototype

`struct MarioState *nearest_interacting_mario_state_to_object(struct Object *obj);`

## nearest_interacting_player_to_object

### Description

Gets the nearest interacting player (Mario Object) to `obj`

### Lua Example

`local objectValue = nearest_interacting_player_to_object(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- [Object](structs.md#Object)

### C Prototype

`struct Object *nearest_interacting_player_to_object(struct Object *obj);`

## is_nearest_mario_state_to_object

### Description

Checks if `m` is the nearest Mario to `obj`

### Lua Example

`local integerValue = is_nearest_mario_state_to_object(m, obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |
| obj | [Object](structs.md#Object) |

### Returns

- `integer`

### C Prototype

`u8 is_nearest_mario_state_to_object(struct MarioState *m, struct Object *obj);`

## is_nearest_player_to_object

### Description

Checks if `m` is the nearest player (Mario Object) to `obj`

### Lua Example

`local integerValue = is_nearest_player_to_object(m, obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| m | [Object](structs.md#Object) |
| obj | [Object](structs.md#Object) |

### Returns

- `integer`

### C Prototype

`u8 is_nearest_player_to_object(struct Object *m, struct Object *obj);`

## is_point_close_to_object

### Description

Checks if a point is within `dist` of `obj`

### Lua Example

`local integerValue = is_point_close_to_object(obj, x, y, z, dist)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| x | `number` |
| y | `number` |
| z | `number` |
| dist | `integer` |

### Returns

- `integer`

### C Prototype

`s8 is_point_close_to_object(struct Object *obj, f32 x, f32 y, f32 z, s32 dist);`

## set_object_visibility

### Description

Sets an object as visible if within a certain distance of Mario's graphical position

### Lua Example

`set_object_visibility(obj, dist)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| dist | `integer` |

### Returns

- None

### C Prototype

`void set_object_visibility(struct Object *obj, s32 dist);`

## obj_return_home_if_safe

### Description

Turns an object towards home if Mario is not near to it

### Lua Example

`local integerValue = obj_return_home_if_safe(obj, homeX, y, homeZ, dist)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| homeX | `number` |
| y | `number` |
| homeZ | `number` |
| dist | `integer` |

### Returns

- `integer`

### C Prototype

`s8 obj_return_home_if_safe(struct Object *obj, f32 homeX, f32 y, f32 homeZ, s32 dist);`

## obj_return_and_displace_home

### Description

Randomly displaces an objects home if RNG says to, and turns the object towards its home

### Lua Example

`obj_return_and_displace_home(obj, homeX, homeY, homeZ, baseDisp)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| homeX | `number` |
| homeY | `number` |
| homeZ | `number` |
| baseDisp | `integer` |

### Returns

- None

### C Prototype

`void obj_return_and_displace_home(struct Object *obj, f32 homeX, UNUSED f32 homeY, f32 homeZ, s32 baseDisp);`

## obj_check_if_facing_toward_angle

### Description

A series of checks using sin and cos to see if a given angle is facing in the same direction
of a given angle, within a certain range

### Lua Example

`local integerValue = obj_check_if_facing_toward_angle(base, goal, range)`

### Parameters

| Field | Type |
| ----- | ---- |
| base | `integer` |
| goal | `integer` |
| range | `integer` |

### Returns

- `integer`

### C Prototype

`s8 obj_check_if_facing_toward_angle(u32 base, u32 goal, s16 range);`

## obj_find_wall_displacement

### Description

Finds any wall collisions and returns what the displacement vector would be

### Lua Example

`local integerValue = obj_find_wall_displacement(dist, x, y, z, radius)`

### Parameters

| Field | Type |
| ----- | ---- |
| dist | [Vec3f](structs.md#Vec3f) |
| x | `number` |
| y | `number` |
| z | `number` |
| radius | `number` |

### Returns

- `integer`

### C Prototype

`s8 obj_find_wall_displacement(VEC_OUT Vec3f dist, f32 x, f32 y, f32 z, f32 radius);`

## obj_spawn_yellow_coins

### Description

Spawns a number of coins at the location of an object with a random forward velocity, y velocity, and direction

### Lua Example

`obj_spawn_yellow_coins(obj, nCoins)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| nCoins | `integer` |

### Returns

- None

### C Prototype

`void obj_spawn_yellow_coins(struct Object *obj, s8 nCoins);`

## obj_flicker_and_disappear

### Description

Controls whether certain objects should flicker/when to despawn

### Lua Example

`local integerValue = obj_flicker_and_disappear(obj, lifeSpan)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| lifeSpan | `integer` |

### Returns

- `integer`

### C Prototype

`s8 obj_flicker_and_disappear(struct Object *obj, s16 lifeSpan);`

## current_mario_room_check

### Description

Checks if a given room is Mario's current room, even if on an object

### Lua Example

`local integerValue = current_mario_room_check(room)`

### Parameters

| Field | Type |
| ----- | ---- |
| room | `integer` |

### Returns

- `integer`

### C Prototype

`s8 current_mario_room_check(s16 room);`

## obj_check_floor_death

### Description

Checks if `floor`'s type is burning or death plane and if so change the
current object's action accordingly

### Lua Example

`obj_check_floor_death(collisionFlags, floor)`

### Parameters

| Field | Type |
| ----- | ---- |
| collisionFlags | `integer` |
| floor | [Surface](structs.md#Surface) |

### Returns

- None

### C Prototype

`void obj_check_floor_death(s16 collisionFlags, struct Surface *floor);`

## obj_lava_death

### Description

Controls an object dying in lava by creating smoke, sinking the object, playing
audio, and eventually despawning it. Returns TRUE when the obj is dead

### Lua Example

`local integerValue = obj_lava_death()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s8 obj_lava_death(void);`

## spawn_orange_number

### Description

Spawns an orange number object relatively, such as those that count up for secrets

### Lua Example

`spawn_orange_number(behParam, relX, relY, relZ)`

### Parameters

| Field | Type |
| ----- | ---- |
| behParam | `integer` |
| relX | `integer` |
| relY | `integer` |
| relZ | `integer` |

### Returns

- None

### C Prototype

`void spawn_orange_number(s8 behParam, s16 relX, s16 relY, s16 relZ);`

---

# functions from obj_behaviors_2.c

## obj_is_rendering_enabled

### Description

Checks if the current object's rendering is enabled

### Lua Example

`local integerValue = obj_is_rendering_enabled()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s32 obj_is_rendering_enabled(void);`

## obj_get_pitch_from_vel

### Description

Calculates the current object's theoretical pitch from forward velocity and vertical velocity

### Lua Example

`local integerValue = obj_get_pitch_from_vel()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s16 obj_get_pitch_from_vel(void);`

## obj_set_dist_from_home

### Description

Sets the current object's position to the home with an additional forward vector multiplied by `distFromHome`

### Lua Example

`obj_set_dist_from_home(distFromHome)`

### Parameters

| Field | Type |
| ----- | ---- |
| distFromHome | `number` |

### Returns

- None

### C Prototype

`void obj_set_dist_from_home(f32 distFromHome);`

## obj_is_near_to_and_facing_mario

### Description

Checks if the current object is in `maxDist` to `m` and the angle difference is less than `maxAngleDiff`

### Lua Example

`local integerValue = obj_is_near_to_and_facing_mario(m, maxDist, maxAngleDiff)`

### Parameters

| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |
| maxDist | `number` |
| maxAngleDiff | `integer` |

### Returns

- `integer`

### C Prototype

`s32 obj_is_near_to_and_facing_mario(struct MarioState* m, f32 maxDist, s16 maxAngleDiff);`

## platform_on_track_update_pos_or_spawn_ball

### Description

Handles the platform on track's trajectory marker ball spawning

### Lua Example

`platform_on_track_update_pos_or_spawn_ball(ballIndex, x, y, z)`

### Parameters

| Field | Type |
| ----- | ---- |
| ballIndex | `integer` |
| x | `number` |
| y | `number` |
| z | `number` |

### Returns

- None

### C Prototype

`void platform_on_track_update_pos_or_spawn_ball(s32 ballIndex, f32 x, f32 y, f32 z);`

## cur_obj_spin_all_dimensions

### Description

Spins an object in every direction with `pitchSpeed` and `rollSpeed`

### Lua Example

`cur_obj_spin_all_dimensions(pitchSpeed, rollSpeed)`

### Parameters

| Field | Type |
| ----- | ---- |
| pitchSpeed | `number` |
| rollSpeed | `number` |

### Returns

- None

### C Prototype

`void cur_obj_spin_all_dimensions(f32 pitchSpeed, f32 rollSpeed);`

## obj_rotate_yaw_and_bounce_off_walls

### Description

Approaches the current object's yaw to `targetYaw` by `turnAmount`

### Lua Example

`obj_rotate_yaw_and_bounce_off_walls(targetYaw, turnAmount)`

### Parameters

| Field | Type |
| ----- | ---- |
| targetYaw | `integer` |
| turnAmount | `integer` |

### Returns

- None

### C Prototype

`void obj_rotate_yaw_and_bounce_off_walls(s16 targetYaw, s16 turnAmount);`

## obj_get_pitch_to_home

### Description

Gets the current object's theoretical pitch to the home with the lateral distance from it

### Lua Example

`local integerValue = obj_get_pitch_to_home(latDistToHome)`

### Parameters

| Field | Type |
| ----- | ---- |
| latDistToHome | `number` |

### Returns

- `integer`

### C Prototype

`s16 obj_get_pitch_to_home(f32 latDistToHome);`

## obj_compute_vel_from_move_pitch

### Description

Computes the current object's forward vel and vertical velocity with the move angle pitch

### Lua Example

`obj_compute_vel_from_move_pitch(speed)`

### Parameters

| Field | Type |
| ----- | ---- |
| speed | `number` |

### Returns

- None

### C Prototype

`void obj_compute_vel_from_move_pitch(f32 speed);`

## cur_obj_init_anim_extend

### Description

Initializes an animation for the current object and loops back around if the animation ends

### Lua Example

`cur_obj_init_anim_extend(animIndex)`

### Parameters

| Field | Type |
| ----- | ---- |
| animIndex | `integer` |

### Returns

- None

### C Prototype

`void cur_obj_init_anim_extend(s32 animIndex);`

## cur_obj_init_anim_and_check_if_end

### Description

Initializes an animation for the current object and returns if the animation has ended

### Lua Example

`local integerValue = cur_obj_init_anim_and_check_if_end(animIndex)`

### Parameters

| Field | Type |
| ----- | ---- |
| animIndex | `integer` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_init_anim_and_check_if_end(s32 animIndex);`

## cur_obj_init_anim_check_frame

### Description

Initializes an animation for the current object and checks if the animation frame is a specific frame

### Lua Example

`local integerValue = cur_obj_init_anim_check_frame(animIndex, animFrame)`

### Parameters

| Field | Type |
| ----- | ---- |
| animIndex | `integer` |
| animFrame | `integer` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_init_anim_check_frame(s32 animIndex, s32 animFrame);`

## cur_obj_set_anim_if_at_end

### Description

Sets the current object's animation to a new animation if the current animation has ended

### Lua Example

`local integerValue = cur_obj_set_anim_if_at_end(animIndex)`

### Parameters

| Field | Type |
| ----- | ---- |
| animIndex | `integer` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_set_anim_if_at_end(s32 animIndex);`

## cur_obj_play_sound_at_anim_range

### Description

Plays a sound when the animation frame is in a range

### Lua Example

`local integerValue = cur_obj_play_sound_at_anim_range(startFrame, endFrame, sound)`

### Parameters

| Field | Type |
| ----- | ---- |
| startFrame | `integer` |
| endFrame | `integer` |
| sound | `integer` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_play_sound_at_anim_range(s8 startFrame, s8 endFrame, u32 sound);`

## obj_turn_pitch_toward_mario

### Description

Turns the current object towards `m` by `turnAmount` and subtracts and adds `targetOffsetY` to the Y position, effectively cancelling any effect out

### Lua Example

`local integerValue = obj_turn_pitch_toward_mario(m, targetOffsetY, turnAmount)`

### Parameters

| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |
| targetOffsetY | `number` |
| turnAmount | `integer` |

### Returns

- `integer`

### C Prototype

`s16 obj_turn_pitch_toward_mario(struct MarioState* m, f32 targetOffsetY, s16 turnAmount);`

## approach_f32_ptr

### Description

Approaches a `target` for `px` using `delta`. Returns TRUE if `px` reaches `target`

### Lua Example

`local integerValue, px = approach_f32_ptr(px, target, delta)`

### Parameters

| Field | Type |
| ----- | ---- |
| px | `number` |
| target | `number` |
| delta | `number` |

### Returns

- `integer`
- `number`

### C Prototype

`s32 approach_f32_ptr(INOUT f32 *px, f32 target, f32 delta);`

## obj_forward_vel_approach

### Description

Approaches a `target` value with the current object's forward velocity using `delta`

### Lua Example

`local integerValue = obj_forward_vel_approach(target, delta)`

### Parameters

| Field | Type |
| ----- | ---- |
| target | `number` |
| delta | `number` |

### Returns

- `integer`

### C Prototype

`s32 obj_forward_vel_approach(f32 target, f32 delta);`

## obj_y_vel_approach

### Description

Approaches a `target` value with the current object's vertical velocity using `delta`

### Lua Example

`local integerValue = obj_y_vel_approach(target, delta)`

### Parameters

| Field | Type |
| ----- | ---- |
| target | `number` |
| delta | `number` |

### Returns

- `integer`

### C Prototype

`s32 obj_y_vel_approach(f32 target, f32 delta);`

## obj_move_pitch_approach

### Description

Approaches a `target` value with the current object's move pitch using `delta`

### Lua Example

`local integerValue = obj_move_pitch_approach(target, delta)`

### Parameters

| Field | Type |
| ----- | ---- |
| target | `integer` |
| delta | `integer` |

### Returns

- `integer`

### C Prototype

`s32 obj_move_pitch_approach(s16 target, s16 delta);`

## obj_face_pitch_approach

### Description

Approaches a `target` value with the current object's facing pitch using `delta`

### Lua Example

`local integerValue = obj_face_pitch_approach(targetPitch, deltaPitch)`

### Parameters

| Field | Type |
| ----- | ---- |
| targetPitch | `integer` |
| deltaPitch | `integer` |

### Returns

- `integer`

### C Prototype

`s32 obj_face_pitch_approach(s16 targetPitch, s16 deltaPitch);`

## obj_face_yaw_approach

### Description

Approaches a `target` value with the current object's facing yaw using `delta`

### Lua Example

`local integerValue = obj_face_yaw_approach(targetYaw, deltaYaw)`

### Parameters

| Field | Type |
| ----- | ---- |
| targetYaw | `integer` |
| deltaYaw | `integer` |

### Returns

- `integer`

### C Prototype

`s32 obj_face_yaw_approach(s16 targetYaw, s16 deltaYaw);`

## obj_face_roll_approach

### Description

Approaches a `target` value with the current object's facing roll using `delta`

### Lua Example

`local integerValue = obj_face_roll_approach(targetRoll, deltaRoll)`

### Parameters

| Field | Type |
| ----- | ---- |
| targetRoll | `integer` |
| deltaRoll | `integer` |

### Returns

- `integer`

### C Prototype

`s32 obj_face_roll_approach(s16 targetRoll, s16 deltaRoll);`

## obj_smooth_turn

### Description

Smoothly turns `angle` and adjust `angleVel` using parameters. Returns TRUE if `angle` reaches `targetAngle`

### Lua Example

`local integerValue, angleVel, angle = obj_smooth_turn(angleVel, angle, targetAngle, targetSpeedProportion, accel, minSpeed, maxSpeed)`

### Parameters

| Field | Type |
| ----- | ---- |
| angleVel | `integer` |
| angle | `integer` |
| targetAngle | `integer` |
| targetSpeedProportion | `number` |
| accel | `integer` |
| minSpeed | `integer` |
| maxSpeed | `integer` |

### Returns

- `integer`
- `integer`
- `integer`

### C Prototype

`s32 obj_smooth_turn(INOUT s16 *angleVel, INOUT s32 *angle, s16 targetAngle, f32 targetSpeedProportion, s16 accel, s16 minSpeed, s16 maxSpeed);`

## obj_roll_to_match_yaw_turn

### Description

Rolls the current object to the move angle subtracted by `targetYaw`, clamping between negative and positive `maxRoll` and using `rollSpeed`

### Lua Example

`obj_roll_to_match_yaw_turn(targetYaw, maxRoll, rollSpeed)`

### Parameters

| Field | Type |
| ----- | ---- |
| targetYaw | `integer` |
| maxRoll | `integer` |
| rollSpeed | `integer` |

### Returns

- None

### C Prototype

`void obj_roll_to_match_yaw_turn(s16 targetYaw, s16 maxRoll, s16 rollSpeed);`

## random_linear_offset

### Description

Generates a random offset with a base and range of `base` to `range`

### Lua Example

`local integerValue = random_linear_offset(base, range)`

### Parameters

| Field | Type |
| ----- | ---- |
| base | `integer` |
| range | `integer` |

### Returns

- `integer`

### C Prototype

`s16 random_linear_offset(s16 base, s16 range);`

## random_mod_offset

### Description

Generates a random offset using step multiplied a value between 0 and `mod` (the random function goes to 65535 but wraps around to 0 at `mod`)

### Lua Example

`local integerValue = random_mod_offset(base, step, mod)`

### Parameters

| Field | Type |
| ----- | ---- |
| base | `integer` |
| step | `integer` |
| mod | `integer` |

### Returns

- `integer`

### C Prototype

`s16 random_mod_offset(s16 base, s16 step, s16 mod);`

## obj_random_fixed_turn

### Description

Rotates the current object's move angle yaw using `delta` in either a randomly decided positive or negative direction

### Lua Example

`local integerValue = obj_random_fixed_turn(delta)`

### Parameters

| Field | Type |
| ----- | ---- |
| delta | `integer` |

### Returns

- `integer`

### C Prototype

`s16 obj_random_fixed_turn(s16 delta);`

## obj_grow_then_shrink

### Description

Begin by increasing the current object's scale by `scaleVel`, and slowly decreasing `scaleVel`.
Once the object starts to shrink, wait a bit, and then begin to scale the object toward `endScale`.
The first time it reaches below `shootFireScale` during this time, return 1.
Return -1 once it's reached endScale

### Lua Example

`local integerValue, scaleVel = obj_grow_then_shrink(scaleVel, shootFireScale, endScale)`

### Parameters

| Field | Type |
| ----- | ---- |
| scaleVel | `number` |
| shootFireScale | `number` |
| endScale | `number` |

### Returns

- `integer`
- `number`

### C Prototype

`s32 obj_grow_then_shrink(INOUT f32 *scaleVel, f32 shootFireScale, f32 endScale);`

## oscillate_toward

### Description

Oscillates `value` towards `target`. Returns TRUE when `value` reaches `target`

### Lua Example

`local integerValue, value, vel = oscillate_toward(value, vel, target, velCloseToZero, accel, slowdown)`

### Parameters

| Field | Type |
| ----- | ---- |
| value | `integer` |
| vel | `number` |
| target | `integer` |
| velCloseToZero | `number` |
| accel | `number` |
| slowdown | `number` |

### Returns

- `integer`
- `integer`
- `number`

### C Prototype

`s32 oscillate_toward(INOUT s32 *value, INOUT f32 *vel, s32 target, f32 velCloseToZero, f32 accel, f32 slowdown);`

## obj_update_blinking

### Description

Update the current object's blinking through `oAnimState`

### Lua Example

`local blinkTimer = obj_update_blinking(blinkTimer, baseCycleLength, cycleLengthRange, blinkLength)`

### Parameters

| Field | Type |
| ----- | ---- |
| blinkTimer | `integer` |
| baseCycleLength | `integer` |
| cycleLengthRange | `integer` |
| blinkLength | `integer` |

### Returns

- `integer`

### C Prototype

`void obj_update_blinking(INOUT s32 *blinkTimer, s16 baseCycleLength, s16 cycleLengthRange, s16 blinkLength);`

## obj_resolve_object_collisions

### Description

Resolves "collisions" with the current object and other objects by offsetting the current object's position. Returns TRUE and the target yaw if there is collision

### Lua Example

`local integerValue, targetYaw = obj_resolve_object_collisions()`

### Parameters

- None

### Returns

- `integer`
- `integer`

### C Prototype

`s32 obj_resolve_object_collisions(RET s32 *targetYaw);`

## obj_bounce_off_walls_edges_objects

### Description

Bounces the current object off of walls, edges, and objects. Returns TRUE and the target yaw if there is collision

### Lua Example

`local integerValue, targetYaw = obj_bounce_off_walls_edges_objects()`

### Parameters

- None

### Returns

- `integer`
- `integer`

### C Prototype

`s32 obj_bounce_off_walls_edges_objects(RET s32 *targetYaw);`

## obj_resolve_collisions_and_turn

### Description

Resolves collisions and turns the current object towards `targetYaw` using `turnSpeed`

### Lua Example

`local integerValue = obj_resolve_collisions_and_turn(targetYaw, turnSpeed)`

### Parameters

| Field | Type |
| ----- | ---- |
| targetYaw | `integer` |
| turnSpeed | `integer` |

### Returns

- `integer`

### C Prototype

`s32 obj_resolve_collisions_and_turn(s16 targetYaw, s16 turnSpeed);`

## obj_die_if_health_non_positive

### Description

Spawns mist particles, plays a sound (`oDeathSound`,) spawns coins (`oNumLootCoins`,) and hides the object if the health is less than 0 or deletes the object if the health is 0 or higher

### Lua Example

`obj_die_if_health_non_positive()`

### Parameters

- None

### Returns

- None

### C Prototype

`void obj_die_if_health_non_positive(void);`

## obj_unused_die

### Description

Sets the current object's health to 0 and runs `obj_die_if_health_non_positive()`

### Lua Example

`obj_unused_die()`

### Parameters

- None

### Returns

- None

### C Prototype

`void obj_unused_die(void);`

## obj_set_knockback_action

### Description

Sets the current object's action, forward velocity, and vertical velocity to preset values (`OBJ_ACT_*`)

### Lua Example

`obj_set_knockback_action(attackType)`

### Parameters

| Field | Type |
| ----- | ---- |
| attackType | `integer` |

### Returns

- None

### C Prototype

`void obj_set_knockback_action(s32 attackType);`

## obj_set_squished_action

### Description

Plays `SOUND_OBJ_STOMPED` and sets the current object's action to `OBJ_ACT_SQUISHED`

### Lua Example

`obj_set_squished_action()`

### Parameters

- None

### Returns

- None

### C Prototype

`void obj_set_squished_action(void);`

## obj_die_if_above_lava_and_health_non_positive

### Description

Checks if the object is above lava and has non-positive health. Kills the object if true and returns `TRUE` if above lava

### Lua Example

`local integerValue = obj_die_if_above_lava_and_health_non_positive()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s32 obj_die_if_above_lava_and_health_non_positive(void);`

## obj_handle_attacks

### Description

Sets the object's hitbox, handles attack interactions by calling appropriate attack handlers, and returns the attack type or 0

### Lua Example

`local integerValue = obj_handle_attacks(hitbox, attackedMarioAction, attackHandlers)`

### Parameters

| Field | Type |
| ----- | ---- |
| hitbox | [ObjectHitbox](structs.md#ObjectHitbox) |
| attackedMarioAction | `integer` |
| attackHandlers | `Pointer` <`integer`> |

### Returns

- `integer`

### C Prototype

`s32 obj_handle_attacks(struct ObjectHitbox *hitbox, s32 attackedMarioAction, u8 *attackHandlers);`

## obj_act_knockback

### Description

Handles the knockback action by updating floor/walls, extending animation, checking lava, and moving the object

### Lua Example

`obj_act_knockback(baseScale)`

### Parameters

| Field | Type |
| ----- | ---- |
| baseScale | `number` |

### Returns

- None

### C Prototype

`void obj_act_knockback(UNUSED f32 baseScale);`

## obj_act_squished

### Description

Handles the squished action by scaling the object vertically and horizontally while checking if it's time to die

### Lua Example

`obj_act_squished(baseScale)`

### Parameters

| Field | Type |
| ----- | ---- |
| baseScale | `number` |

### Returns

- None

### C Prototype

`void obj_act_squished(f32 baseScale);`

## obj_update_standard_actions

### Description

Updates standard object actions like knockback and squished. Returns TRUE if action is less than 100, `FALSE` otherwise

### Lua Example

`local integerValue = obj_update_standard_actions(scale)`

### Parameters

| Field | Type |
| ----- | ---- |
| scale | `number` |

### Returns

- `integer`

### C Prototype

`s32 obj_update_standard_actions(f32 scale);`

## obj_check_attacks

### Description

Checks the current object's interaction status and sets action to `attackedMarioAction` if Mario has been attacked and runs `obj_die_if_health_non_positive()` if the object is attacked by Mario. Sets the hitbox parameters and resets interaction status to 0

### Lua Example

`local integerValue = obj_check_attacks(hitbox, attackedMarioAction)`

### Parameters

| Field | Type |
| ----- | ---- |
| hitbox | [ObjectHitbox](structs.md#ObjectHitbox) |
| attackedMarioAction | `integer` |

### Returns

- `integer`

### C Prototype

`s32 obj_check_attacks(struct ObjectHitbox *hitbox, s32 attackedMarioAction);`

## obj_move_for_one_second

### Description

Moves the current object for specifically one second (`oTimer` < 30)

### Lua Example

`local integerValue = obj_move_for_one_second(endAction)`

### Parameters

| Field | Type |
| ----- | ---- |
| endAction | `integer` |

### Returns

- `integer`

### C Prototype

`s32 obj_move_for_one_second(s32 endAction);`

## treat_far_home_as_mario

### Description

Treats far home as Mario. Returns the distance and angle to the nearest player

### Lua Example

`local distanceToPlayer, angleToPlayer = treat_far_home_as_mario(threshold)`

### Parameters

| Field | Type |
| ----- | ---- |
| threshold | `number` |

### Returns

- `integer`
- `integer`

### C Prototype

`void treat_far_home_as_mario(f32 threshold, RET s32* distanceToPlayer, RET s32* angleToPlayer);`

## obj_spit_fire

### Description

Spawns a small piranha flame object with the given parameters. Used by Bowser, Fly Guy, Piranha Plant, and Fire Spitters

### Lua Example

`local objectValue = obj_spit_fire(relativePosX, relativePosY, relativePosZ, scale, model, startSpeed, endSpeed, movePitch)`

### Parameters

| Field | Type |
| ----- | ---- |
| relativePosX | `integer` |
| relativePosY | `integer` |
| relativePosZ | `integer` |
| scale | `number` |
| model | `integer` |
| startSpeed | `number` |
| endSpeed | `number` |
| movePitch | `integer` |

### Returns

- [Object](structs.md#Object)

### C Prototype

`struct Object* obj_spit_fire(s16 relativePosX, s16 relativePosY, s16 relativePosZ, f32 scale, s32 model, f32 startSpeed, f32 endSpeed, s16 movePitch);`

---

# functions from object_helpers.c

## clear_move_flag

### Description

Clears the `flag` from the `bitSet`

### Lua Example

`local integerValue, bitSet = clear_move_flag(bitSet, flag)`

### Parameters

| Field | Type |
| ----- | ---- |
| bitSet | `integer` |
| flag | `integer` |

### Returns

- `integer`
- `integer`

### C Prototype

`s32 clear_move_flag(INOUT u32 *bitSet, s32 flag);`

## set_room_override

### Description

Overrides the current room Mario is in. Set to -1 to reset override

### Lua Example

`set_room_override(room)`

### Parameters

| Field | Type |
| ----- | ---- |
| room | `integer` |

### Returns

- None

### C Prototype

`void set_room_override(s16 room);`

## obj_update_pos_from_parent_transformation

### Description

Updates an object's position based on a parent transformation matrix

### Lua Example

`obj_update_pos_from_parent_transformation(mtx, obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| mtx | [Mat4](structs.md#Mat4) |
| obj | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_update_pos_from_parent_transformation(Mat4 mtx, struct Object *obj);`

## obj_apply_scale_to_matrix

### Description

Applies an object's scale to a transformation matrix

### Lua Example

`obj_apply_scale_to_matrix(obj, dst, src)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| dst | [Mat4](structs.md#Mat4) |
| src | [Mat4](structs.md#Mat4) |

### Returns

- None

### C Prototype

`void obj_apply_scale_to_matrix(struct Object *obj, VEC_OUT Mat4 dst, Mat4 src);`

## create_transformation_from_matrices

### Description

Combines two transformation matrices into a single result matrix

### Lua Example

`create_transformation_from_matrices(dest, src1, src2)`

### Parameters

| Field | Type |
| ----- | ---- |
| dest | [Mat4](structs.md#Mat4) |
| src1 | [Mat4](structs.md#Mat4) |
| src2 | [Mat4](structs.md#Mat4) |

### Returns

- None

### C Prototype

`void create_transformation_from_matrices(VEC_OUT Mat4 dest, Mat4 src1, Mat4 src2);`

## obj_set_held_state

### Description

Sets an object's held state based on the behavior script it will perform

### Lua Example

`obj_set_held_state(obj, heldBehavior)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| heldBehavior | `Pointer` <`BehaviorScript`> |

### Returns

- None

### C Prototype

`void obj_set_held_state(struct Object *obj, const BehaviorScript *heldBehavior);`

## lateral_dist_between_objects

### Description

Calculates the lateral (XZ) distance between two objects

### Lua Example

`local numberValue = lateral_dist_between_objects(obj1, obj2)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj1 | [Object](structs.md#Object) |
| obj2 | [Object](structs.md#Object) |

### Returns

- `number`

### C Prototype

`f32 lateral_dist_between_objects(struct Object *obj1, struct Object *obj2);`

## dist_between_objects

### Description

Calculates the 3D distance between two objects

### Lua Example

`local numberValue = dist_between_objects(obj1, obj2)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj1 | [Object](structs.md#Object) |
| obj2 | [Object](structs.md#Object) |

### Returns

- `number`

### C Prototype

`f32 dist_between_objects(struct Object *obj1, struct Object *obj2);`

## dist_between_object_and_point

### Description

Calculates the 3D distance between an object and a point

### Lua Example

`local numberValue = dist_between_object_and_point(obj, pointX, pointY, pointZ)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| pointX | `number` |
| pointY | `number` |
| pointZ | `number` |

### Returns

- `number`

### C Prototype

`f32 dist_between_object_and_point(struct Object *obj, f32 pointX, f32 pointY, f32 pointZ);`

## cur_obj_forward_vel_approach_upward

### Description

Increases the current object's forward velocity toward target by increment

### Lua Example

`cur_obj_forward_vel_approach_upward(target, increment)`

### Parameters

| Field | Type |
| ----- | ---- |
| target | `number` |
| increment | `number` |

### Returns

- None

### C Prototype

`void cur_obj_forward_vel_approach_upward(f32 target, f32 increment);`

## approach_f32_signed

### Description

Approaches a value toward a target using signed increments. Returns `TRUE` when target is reached

### Lua Example

`local integerValue, value = approach_f32_signed(value, target, increment)`

### Parameters

| Field | Type |
| ----- | ---- |
| value | `number` |
| target | `number` |
| increment | `number` |

### Returns

- `integer`
- `number`

### C Prototype

`s32 approach_f32_signed(INOUT f32 *value, f32 target, f32 increment);`

## approach_f32_symmetric

### Description

Approaches a value toward a target using symmetric increments

### Lua Example

`local numberValue = approach_f32_symmetric(value, target, increment)`

### Parameters

| Field | Type |
| ----- | ---- |
| value | `number` |
| target | `number` |
| increment | `number` |

### Returns

- `number`

### C Prototype

`f32 approach_f32_symmetric(f32 value, f32 target, f32 increment);`

## approach_s16_symmetric

### Description

Approaches a 16-bit value toward a target using symmetric increments

### Lua Example

`local integerValue = approach_s16_symmetric(value, target, increment)`

### Parameters

| Field | Type |
| ----- | ---- |
| value | `integer` |
| target | `integer` |
| increment | `integer` |

### Returns

- `integer`

### C Prototype

`s16 approach_s16_symmetric(s16 value, s16 target, s16 increment);`

## cur_obj_rotate_yaw_toward

### Description

Rotates the current object's yaw angle toward a target. Returns `TRUE` when target is reached

### Lua Example

`local integerValue = cur_obj_rotate_yaw_toward(target, increment)`

### Parameters

| Field | Type |
| ----- | ---- |
| target | `integer` |
| increment | `integer` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_rotate_yaw_toward(s16 target, s16 increment);`

## obj_angle_to_object

### Description

Calculates the angle from one object to another in yaw

### Lua Example

`local integerValue = obj_angle_to_object(obj1, obj2)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj1 | [Object](structs.md#Object) |
| obj2 | [Object](structs.md#Object) |

### Returns

- `integer`

### C Prototype

`s16 obj_angle_to_object(struct Object *obj1, struct Object *obj2);`

## obj_pitch_to_object

### Description

Calculates the pitch angle from one object to another

### Lua Example

`local integerValue = obj_pitch_to_object(obj, target)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| target | [Object](structs.md#Object) |

### Returns

- `integer`

### C Prototype

`s16 obj_pitch_to_object(struct Object* obj, struct Object* target);`

## obj_angle_to_point

### Description

Calculates the yaw angle from an object to a point

### Lua Example

`local integerValue = obj_angle_to_point(obj, pointX, pointZ)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| pointX | `number` |
| pointZ | `number` |

### Returns

- `integer`

### C Prototype

`s16 obj_angle_to_point(struct Object *obj, f32 pointX, f32 pointZ);`

## obj_turn_toward_object

### Description

Rotates an object's specified angle toward another object by `turnAmount`

### Lua Example

`local integerValue = obj_turn_toward_object(obj, target, angleIndex, turnAmount)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| target | [Object](structs.md#Object) |
| angleIndex | `integer` |
| turnAmount | `integer` |

### Returns

- `integer`

### C Prototype

`s16 obj_turn_toward_object(struct Object *obj, struct Object *target, s16 angleIndex, s16 turnAmount);`

## obj_set_parent_relative_pos

### Description

Sets an object's position relative to its parent

### Lua Example

`obj_set_parent_relative_pos(obj, relX, relY, relZ)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| relX | `integer` |
| relY | `integer` |
| relZ | `integer` |

### Returns

- None

### C Prototype

`void obj_set_parent_relative_pos(struct Object *obj, s16 relX, s16 relY, s16 relZ);`

## obj_set_pos

### Description

Sets an object's position in 3D space

### Lua Example

`obj_set_pos(obj, x, y, z)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| x | `integer` |
| y | `integer` |
| z | `integer` |

### Returns

- None

### C Prototype

`void obj_set_pos(struct Object *obj, s16 x, s16 y, s16 z);`

## obj_set_angle

### Description

Sets an object's face and move angles to the same pitch, yaw, and roll

### Lua Example

`obj_set_angle(obj, pitch, yaw, roll)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| pitch | `integer` |
| yaw | `integer` |
| roll | `integer` |

### Returns

- None

### C Prototype

`void obj_set_angle(struct Object *obj, s16 pitch, s16 yaw, s16 roll);`

## obj_set_move_angle

### Description

Sets an object's movement angle (pitch, yaw, roll)

### Lua Example

`obj_set_move_angle(obj, pitch, yaw, roll)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| pitch | `integer` |
| yaw | `integer` |
| roll | `integer` |

### Returns

- None

### C Prototype

`void obj_set_move_angle(struct Object *obj, s16 pitch, s16 yaw, s16 roll);`

## obj_set_face_angle

### Description

Sets an object's face angle (pitch, yaw, roll)

### Lua Example

`obj_set_face_angle(obj, pitch, yaw, roll)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| pitch | `integer` |
| yaw | `integer` |
| roll | `integer` |

### Returns

- None

### C Prototype

`void obj_set_face_angle(struct Object *obj, s16 pitch, s16 yaw, s16 roll);`

## obj_set_gfx_angle

### Description

Sets the graphics angle for an object (pitch, yaw, roll)

### Lua Example

`obj_set_gfx_angle(obj, pitch, yaw, roll)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| pitch | `integer` |
| yaw | `integer` |
| roll | `integer` |

### Returns

- None

### C Prototype

`void obj_set_gfx_angle(struct Object *obj, s16 pitch, s16 yaw, s16 roll);`

## obj_set_gfx_pos

### Description

Sets the graphics position for an object in 3D space

### Lua Example

`obj_set_gfx_pos(obj, x, y, z)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| x | `number` |
| y | `number` |
| z | `number` |

### Returns

- None

### C Prototype

`void obj_set_gfx_pos(struct Object *obj, f32 x, f32 y, f32 z);`

## obj_set_gfx_scale

### Description

Sets the graphics scale for an object in X, Y, Z dimensions

### Lua Example

`obj_set_gfx_scale(obj, x, y, z)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| x | `number` |
| y | `number` |
| z | `number` |

### Returns

- None

### C Prototype

`void obj_set_gfx_scale(struct Object *obj, f32 x, f32 y, f32 z);`

## spawn_water_droplet

### Description

Spawns a water droplet object with the specified parameters

### Lua Example

`local objectValue = spawn_water_droplet(parent, params)`

### Parameters

| Field | Type |
| ----- | ---- |
| parent | [Object](structs.md#Object) |
| params | [WaterDropletParams](structs.md#WaterDropletParams) |

### Returns

- [Object](structs.md#Object)

### C Prototype

`struct Object *spawn_water_droplet(struct Object *parent, struct WaterDropletParams *params);`

## obj_build_relative_transform

### Description

Builds a relative transformation matrix for an object based on parent-relative position and face angle

### Lua Example

`obj_build_relative_transform(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_build_relative_transform(struct Object *obj);`

## cur_obj_move_using_vel

### Description

Moves the current object using its velocity vector

### Lua Example

`cur_obj_move_using_vel()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_move_using_vel(void);`

## obj_copy_graph_y_offset

### Description

Copies the graph Y offset from one object to another

### Lua Example

`obj_copy_graph_y_offset(dst, src)`

### Parameters

| Field | Type |
| ----- | ---- |
| dst | [Object](structs.md#Object) |
| src | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_copy_graph_y_offset(struct Object *dst, struct Object *src);`

## obj_copy_pos_and_angle

### Description

Copies both position and angles from one object to another

### Lua Example

`obj_copy_pos_and_angle(dst, src)`

### Parameters

| Field | Type |
| ----- | ---- |
| dst | [Object](structs.md#Object) |
| src | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_copy_pos_and_angle(struct Object *dst, struct Object *src);`

## obj_copy_pos

### Description

Copies position from one object to another

### Lua Example

`obj_copy_pos(dst, src)`

### Parameters

| Field | Type |
| ----- | ---- |
| dst | [Object](structs.md#Object) |
| src | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_copy_pos(struct Object *dst, struct Object *src);`

## obj_copy_angle

### Description

Copies move and face angles from one object to another

### Lua Example

`obj_copy_angle(dst, src)`

### Parameters

| Field | Type |
| ----- | ---- |
| dst | [Object](structs.md#Object) |
| src | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_copy_angle(struct Object *dst, struct Object *src);`

## obj_set_gfx_pos_from_pos

### Description

Synchronizes an object's graphics position with its physical position

### Lua Example

`obj_set_gfx_pos_from_pos(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_set_gfx_pos_from_pos(struct Object *obj);`

## obj_init_animation

### Description

Initializes an animation for an object by index

### Lua Example

`obj_init_animation(obj, animIndex)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| animIndex | `integer` |

### Returns

- None

### C Prototype

`void obj_init_animation(struct Object *obj, s32 animIndex);`

## linear_mtxf_mul_vec3f

### Description

Multiplies a vector by a matrix of the form:
`| ? ? ? 0 |`
`| ? ? ? 0 |`
`| ? ? ? 0 |`
`| 0 0 0 1 |`
i.e. a matrix representing a linear transformation over 3 space

### Lua Example

`linear_mtxf_mul_vec3f(m, dst, v)`

### Parameters

| Field | Type |
| ----- | ---- |
| m | [Mat4](structs.md#Mat4) |
| dst | [Vec3f](structs.md#Vec3f) |
| v | [Vec3f](structs.md#Vec3f) |

### Returns

- None

### C Prototype

`void linear_mtxf_mul_vec3f(Mat4 m, VEC_OUT Vec3f dst, Vec3f v);`

## linear_mtxf_transpose_mul_vec3f

### Description

Multiplies a vector by the transpose of a matrix of the form:
`| ? ? ? 0 |`
`| ? ? ? 0 |`
`| ? ? ? 0 |`
`| 0 0 0 1 |`
i.e. a matrix representing a linear transformation over 3 space

### Lua Example

`linear_mtxf_transpose_mul_vec3f(m, dst, v)`

### Parameters

| Field | Type |
| ----- | ---- |
| m | [Mat4](structs.md#Mat4) |
| dst | [Vec3f](structs.md#Vec3f) |
| v | [Vec3f](structs.md#Vec3f) |

### Returns

- None

### C Prototype

`void linear_mtxf_transpose_mul_vec3f(Mat4 m, VEC_OUT Vec3f dst, Vec3f v);`

## obj_apply_scale_to_transform

### Description

Applies an object's scale to its transformation matrix

### Lua Example

`obj_apply_scale_to_transform(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_apply_scale_to_transform(struct Object *obj);`

## obj_copy_scale

### Description

Copies the scale from one object to another

### Lua Example

`obj_copy_scale(dst, src)`

### Parameters

| Field | Type |
| ----- | ---- |
| dst | [Object](structs.md#Object) |
| src | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_copy_scale(struct Object *dst, struct Object *src);`

## obj_scale_xyz

### Description

Sets an object's scale independently for X, Y, Z dimensions

### Lua Example

`obj_scale_xyz(obj, xScale, yScale, zScale)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| xScale | `number` |
| yScale | `number` |
| zScale | `number` |

### Returns

- None

### C Prototype

`void obj_scale_xyz(struct Object *obj, f32 xScale, f32 yScale, f32 zScale);`

## obj_scale

### Description

Sets an object's uniform scale for all dimensions

### Lua Example

`obj_scale(obj, scale)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| scale | `number` |

### Returns

- None

### C Prototype

`void obj_scale(struct Object *obj, f32 scale);`

## cur_obj_scale

### Description

Sets the current object's uniform scale for all dimensions

### Lua Example

`cur_obj_scale(scale)`

### Parameters

| Field | Type |
| ----- | ---- |
| scale | `number` |

### Returns

- None

### C Prototype

`void cur_obj_scale(f32 scale);`

## cur_obj_init_animation

### Description

Initializes an animation for the current object by index

### Lua Example

`cur_obj_init_animation(animIndex)`

### Parameters

| Field | Type |
| ----- | ---- |
| animIndex | `integer` |

### Returns

- None

### C Prototype

`void cur_obj_init_animation(s32 animIndex);`

## cur_obj_init_animation_with_sound

### Description

Initializes an animation for the current object and sets sound state

### Lua Example

`cur_obj_init_animation_with_sound(animIndex)`

### Parameters

| Field | Type |
| ----- | ---- |
| animIndex | `integer` |

### Returns

- None

### C Prototype

`void cur_obj_init_animation_with_sound(s32 animIndex);`

## obj_init_animation_with_accel_and_sound

### Description

Initializes an animation with acceleration and sound state for an object

### Lua Example

`obj_init_animation_with_accel_and_sound(obj, animIndex, accel)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| animIndex | `integer` |
| accel | `number` |

### Returns

- None

### C Prototype

`void obj_init_animation_with_accel_and_sound(struct Object *obj, s32 animIndex, f32 accel);`

## cur_obj_init_animation_with_accel_and_sound

### Description

Initializes an animation with acceleration and sound state for the current object

### Lua Example

`cur_obj_init_animation_with_accel_and_sound(animIndex, accel)`

### Parameters

| Field | Type |
| ----- | ---- |
| animIndex | `integer` |
| accel | `number` |

### Returns

- None

### C Prototype

`void cur_obj_init_animation_with_accel_and_sound(s32 animIndex, f32 accel);`

## cur_obj_enable_rendering_and_become_tangible

### Description

Enables rendering and tangibility for an object

### Lua Example

`cur_obj_enable_rendering_and_become_tangible(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void cur_obj_enable_rendering_and_become_tangible(struct Object *obj);`

## cur_obj_enable_rendering

### Description

Enables rendering for the current object

### Lua Example

`cur_obj_enable_rendering()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_enable_rendering(void);`

## cur_obj_disable_rendering_and_become_intangible

### Description

Disables rendering and makes an object intangible

### Lua Example

`cur_obj_disable_rendering_and_become_intangible(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void cur_obj_disable_rendering_and_become_intangible(struct Object *obj);`

## cur_obj_disable_rendering

### Description

Disables rendering for the current object

### Lua Example

`cur_obj_disable_rendering()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_disable_rendering(void);`

## cur_obj_unhide

### Description

Makes the current object visible by removing the invisible flag

### Lua Example

`cur_obj_unhide()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_unhide(void);`

## cur_obj_hide

### Description

Hides the current object by setting the invisible flag

### Lua Example

`cur_obj_hide()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_hide(void);`

## cur_obj_set_pos_relative

### Description

Sets the current object's position relative to another object's facing direction

### Lua Example

`cur_obj_set_pos_relative(other, dleft, dy, dforward)`

### Parameters

| Field | Type |
| ----- | ---- |
| other | [Object](structs.md#Object) |
| dleft | `number` |
| dy | `number` |
| dforward | `number` |

### Returns

- None

### C Prototype

`void cur_obj_set_pos_relative(struct Object *other, f32 dleft, f32 dy, f32 dforward);`

## cur_obj_set_pos_relative_to_parent

### Description

Sets the current object's position relative to its parent's facing direction

### Lua Example

`cur_obj_set_pos_relative_to_parent(dleft, dy, dforward)`

### Parameters

| Field | Type |
| ----- | ---- |
| dleft | `number` |
| dy | `number` |
| dforward | `number` |

### Returns

- None

### C Prototype

`void cur_obj_set_pos_relative_to_parent(f32 dleft, f32 dy, f32 dforward);`

## cur_obj_unused_init_on_floor

### Description

Unused function that initializes the current object on the floor

### Lua Example

`cur_obj_unused_init_on_floor()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_unused_init_on_floor(void);`

## obj_set_face_angle_to_move_angle

### Description

Synchronizes an object's face angle with its move angle

### Lua Example

`obj_set_face_angle_to_move_angle(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_set_face_angle_to_move_angle(struct Object *obj);`

## get_object_list_from_behavior

### Description

Retrieves the object list type that a behavior script belongs to

### Lua Example

`local integerValue = get_object_list_from_behavior(behavior)`

### Parameters

| Field | Type |
| ----- | ---- |
| behavior | `Pointer` <`BehaviorScript`> |

### Returns

- `integer`

### C Prototype

`u32 get_object_list_from_behavior(const BehaviorScript *behavior);`

## cur_obj_nearest_object_with_behavior

### Description

Finds the nearest object with the specified behavior to the current object

### Lua Example

`local objectValue = cur_obj_nearest_object_with_behavior(behavior)`

### Parameters

| Field | Type |
| ----- | ---- |
| behavior | `Pointer` <`BehaviorScript`> |

### Returns

- [Object](structs.md#Object)

### C Prototype

`struct Object *cur_obj_nearest_object_with_behavior(const BehaviorScript *behavior);`

## cur_obj_dist_to_nearest_object_with_behavior

### Description

Calculates the distance from the current object to the nearest object with specified behavior

### Lua Example

`local numberValue = cur_obj_dist_to_nearest_object_with_behavior(behavior)`

### Parameters

| Field | Type |
| ----- | ---- |
| behavior | `Pointer` <`BehaviorScript`> |

### Returns

- `number`

### C Prototype

`f32 cur_obj_dist_to_nearest_object_with_behavior(const BehaviorScript *behavior);`

## cur_obj_find_nearest_pole

### Description

Finds the nearest pole-like object to the current object

### Lua Example

`local objectValue = cur_obj_find_nearest_pole()`

### Parameters

- None

### Returns

- [Object](structs.md#Object)

### C Prototype

`struct Object* cur_obj_find_nearest_pole(void);`

## cur_obj_find_nearest_object_with_behavior

### Description

Finds the nearest object with specified behavior and returns distance via pointer

### Lua Example

`local objectValue, dist = cur_obj_find_nearest_object_with_behavior(behavior)`

### Parameters

| Field | Type |
| ----- | ---- |
| behavior | `Pointer` <`BehaviorScript`> |

### Returns

- [Object](structs.md#Object)
- `number`

### C Prototype

`struct Object *cur_obj_find_nearest_object_with_behavior(const BehaviorScript *behavior, RET f32 *dist);`

## cur_obj_count_objects_with_behavior

### Description

Counts objects with specified behavior within distance of current object

### Lua Example

`local integerValue = cur_obj_count_objects_with_behavior(behavior, dist)`

### Parameters

| Field | Type |
| ----- | ---- |
| behavior | `Pointer` <`BehaviorScript`> |
| dist | `number` |

### Returns

- `integer`

### C Prototype

`u16 cur_obj_count_objects_with_behavior(const BehaviorScript* behavior, f32 dist);`

## find_unimportant_object

### Description

Finds an unimportant object from the unimportant object list

### Lua Example

`local objectValue = find_unimportant_object()`

### Parameters

- None

### Returns

- [Object](structs.md#Object)

### C Prototype

`struct Object *find_unimportant_object(void);`

## count_unimportant_objects

### Description

Counts the number of unimportant objects in the unimportant object list

### Lua Example

`local integerValue = count_unimportant_objects()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s32 count_unimportant_objects(void);`

## count_objects_with_behavior

### Description

Counts the number of objects with the specified behavior

### Lua Example

`local integerValue = count_objects_with_behavior(behavior)`

### Parameters

| Field | Type |
| ----- | ---- |
| behavior | `Pointer` <`BehaviorScript`> |

### Returns

- `integer`

### C Prototype

`s32 count_objects_with_behavior(const BehaviorScript *behavior);`

## delete_all_objects_with_behavior

### Description

Deletes all objects with the specified behavior

### Lua Example

`delete_all_objects_with_behavior(behavior)`

### Parameters

| Field | Type |
| ----- | ---- |
| behavior | `Pointer` <`BehaviorScript`> |

### Returns

- None

### C Prototype

`void delete_all_objects_with_behavior(const BehaviorScript *behavior);`

## find_object_with_behavior

### Description

Finds any object with the specified behavior

### Lua Example

`local objectValue = find_object_with_behavior(behavior)`

### Parameters

| Field | Type |
| ----- | ---- |
| behavior | `Pointer` <`BehaviorScript`> |

### Returns

- [Object](structs.md#Object)

### C Prototype

`struct Object *find_object_with_behavior(const BehaviorScript *behavior);`

## cur_obj_find_nearby_held_actor

### Description

Finds an object with specified behavior within `maxDist` that is being held by a player

### Lua Example

`local objectValue = cur_obj_find_nearby_held_actor(behavior, maxDist)`

### Parameters

| Field | Type |
| ----- | ---- |
| behavior | `Pointer` <`BehaviorScript`> |
| maxDist | `number` |

### Returns

- [Object](structs.md#Object)

### C Prototype

`struct Object *cur_obj_find_nearby_held_actor(const BehaviorScript *behavior, f32 maxDist);`

## cur_obj_reset_timer_and_subaction

### Description

Resets the current object's timer and sub-action to 0

### Lua Example

`cur_obj_reset_timer_and_subaction()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_reset_timer_and_subaction(void);`

## cur_obj_change_action

### Description

Changes the current object's action and resets timer and subaction

### Lua Example

`cur_obj_change_action(action)`

### Parameters

| Field | Type |
| ----- | ---- |
| action | `integer` |

### Returns

- None

### C Prototype

`void cur_obj_change_action(s32 action);`

## cur_obj_set_vel_from_mario_vel

### Description

Sets the current object's forward velocity based on Mario's velocity with scaling

### Lua Example

`cur_obj_set_vel_from_mario_vel(m, f12, f14)`

### Parameters

| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |
| f12 | `number` |
| f14 | `number` |

### Returns

- None

### C Prototype

`void cur_obj_set_vel_from_mario_vel(struct MarioState* m, f32 f12, f32 f14);`

## cur_obj_reverse_animation

### Description

Decreases the current object's animation frame by one

### Lua Example

`cur_obj_reverse_animation()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_reverse_animation(void);`

## cur_obj_extend_animation_if_at_end

### Description

Extends the current object's animation frame if at loop end

### Lua Example

`cur_obj_extend_animation_if_at_end()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_extend_animation_if_at_end(void);`

## cur_obj_check_if_near_animation_end

### Description

Checks if the current object's animation is near the end

### Lua Example

`local integerValue = cur_obj_check_if_near_animation_end()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s32 cur_obj_check_if_near_animation_end(void);`

## cur_obj_check_if_at_animation_end

### Description

Checks if the current object's animation is at the end

### Lua Example

`local integerValue = cur_obj_check_if_at_animation_end()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s32 cur_obj_check_if_at_animation_end(void);`

## cur_obj_check_anim_frame

### Description

Checks if the current object's animation is at a specific frame

### Lua Example

`local integerValue = cur_obj_check_anim_frame(frame)`

### Parameters

| Field | Type |
| ----- | ---- |
| frame | `integer` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_check_anim_frame(s32 frame);`

## cur_obj_check_anim_frame_in_range

### Description

Checks if the current object's animation frame is within a range

### Lua Example

`local integerValue = cur_obj_check_anim_frame_in_range(startFrame, rangeLength)`

### Parameters

| Field | Type |
| ----- | ---- |
| startFrame | `integer` |
| rangeLength | `integer` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_check_anim_frame_in_range(s32 startFrame, s32 rangeLength);`

## mario_is_in_air_action

### Description

Checks if Mario is in an air action

### Lua Example

`local integerValue = mario_is_in_air_action(m)`

### Parameters

| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |

### Returns

- `integer`

### C Prototype

`s32 mario_is_in_air_action(struct MarioState* m);`

## mario_is_dive_sliding

### Description

Checks if Mario is performing a dive slide action

### Lua Example

`local integerValue = mario_is_dive_sliding(m)`

### Parameters

| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |

### Returns

- `integer`

### C Prototype

`s32 mario_is_dive_sliding(struct MarioState* m);`

## cur_obj_set_y_vel_and_animation

### Description

Sets the current object's vertical velocity and initializes an animation

### Lua Example

`cur_obj_set_y_vel_and_animation(velY, animIndex)`

### Parameters

| Field | Type |
| ----- | ---- |
| velY | `number` |
| animIndex | `integer` |

### Returns

- None

### C Prototype

`void cur_obj_set_y_vel_and_animation(f32 velY, s32 animIndex);`

## cur_obj_unrender_and_reset_state

### Description

Disables rendering, makes intangible, and resets animation and action

### Lua Example

`cur_obj_unrender_and_reset_state(animIndex, action)`

### Parameters

| Field | Type |
| ----- | ---- |
| animIndex | `integer` |
| action | `integer` |

### Returns

- None

### C Prototype

`void cur_obj_unrender_and_reset_state(s32 animIndex, s32 action);`

## cur_obj_move_after_thrown_or_dropped

### Description

Moves an object after being thrown or dropped with gravity applied

### Lua Example

`cur_obj_move_after_thrown_or_dropped(forwardVel, velY)`

### Parameters

| Field | Type |
| ----- | ---- |
| forwardVel | `number` |
| velY | `number` |

### Returns

- None

### C Prototype

`void cur_obj_move_after_thrown_or_dropped(f32 forwardVel, f32 velY);`

## cur_obj_get_thrown_or_placed

### Description

Handles object state when it's been thrown or placed by a player

### Lua Example

`cur_obj_get_thrown_or_placed(forwardVel, velY, thrownAction)`

### Parameters

| Field | Type |
| ----- | ---- |
| forwardVel | `number` |
| velY | `number` |
| thrownAction | `integer` |

### Returns

- None

### C Prototype

`void cur_obj_get_thrown_or_placed(f32 forwardVel, f32 velY, s32 thrownAction);`

## cur_obj_get_dropped

### Description

Handles object state when it's been dropped by a player

### Lua Example

`cur_obj_get_dropped()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_get_dropped(void);`

## mario_set_flag

### Description

Sets a flag on Mario's state

### Lua Example

`mario_set_flag(flag)`

### Parameters

| Field | Type |
| ----- | ---- |
| flag | `integer` |

### Returns

- None

### C Prototype

`void mario_set_flag(s32 flag);`

## cur_obj_clear_interact_status_flag

### Description

Clears a flag from the current object's interaction status

### Lua Example

`local integerValue = cur_obj_clear_interact_status_flag(flag)`

### Parameters

| Field | Type |
| ----- | ---- |
| flag | `integer` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_clear_interact_status_flag(s32 flag);`

## obj_mark_for_deletion

### Description

Marks an object to be unloaded at the end of the frame

### Lua Example

`obj_mark_for_deletion(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_mark_for_deletion(struct Object *obj);`

## cur_obj_disable

### Description

Disables the current object by hiding, disabling rendering, and making intangible

### Lua Example

`cur_obj_disable()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_disable(void);`

## cur_obj_become_intangible

### Description

Makes the current object intangible

### Lua Example

`cur_obj_become_intangible()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_become_intangible(void);`

## cur_obj_become_tangible

### Description

Makes the current object tangible

### Lua Example

`cur_obj_become_tangible()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_become_tangible(void);`

## obj_become_tangible

### Description

Makes an object tangible

### Lua Example

`obj_become_tangible(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_become_tangible(struct Object *obj);`

## cur_obj_update_floor_height

### Description

Updates the current object's floor height based on its position

### Lua Example

`cur_obj_update_floor_height()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_update_floor_height(void);`

## cur_obj_update_floor_height_and_get_floor

### Description

Updates the current object's floor height and returns the floor surface under it

### Lua Example

`local surfaceValue = cur_obj_update_floor_height_and_get_floor()`

### Parameters

- None

### Returns

- [Surface](structs.md#Surface)

### C Prototype

`struct Surface *cur_obj_update_floor_height_and_get_floor(void);`

## apply_drag_to_value

### Description

Applies nonlinear drag to a value pointer based on drag strength

### Lua Example

`local value = apply_drag_to_value(value, dragStrength)`

### Parameters

| Field | Type |
| ----- | ---- |
| value | `number` |
| dragStrength | `number` |

### Returns

- `number`

### C Prototype

`void apply_drag_to_value(INOUT f32 *value, f32 dragStrength);`

## cur_obj_apply_drag_xz

### Description

Applies drag to the current object's horizontal velocity components

### Lua Example

`cur_obj_apply_drag_xz(dragStrength)`

### Parameters

| Field | Type |
| ----- | ---- |
| dragStrength | `number` |

### Returns

- None

### C Prototype

`void cur_obj_apply_drag_xz(f32 dragStrength);`

## cur_obj_move_xz

### Description

Attempts to move the current object in XZ, handling floor slope, edges, and room boundaries

### Lua Example

`local integerValue = cur_obj_move_xz(steepSlopeNormalY, careAboutEdgesAndSteepSlopes)`

### Parameters

| Field | Type |
| ----- | ---- |
| steepSlopeNormalY | `number` |
| careAboutEdgesAndSteepSlopes | `integer` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_move_xz(f32 steepSlopeNormalY, s32 careAboutEdgesAndSteepSlopes);`

## cur_obj_move_update_underwater_flags

### Description

Updates underwater movement flags and vertical damping while submerged

### Lua Example

`cur_obj_move_update_underwater_flags()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_move_update_underwater_flags(void);`

## cur_obj_move_update_ground_air_flags

### Description

Updates ground and air movement flags after a vertical move

### Lua Example

`cur_obj_move_update_ground_air_flags(gravity, bounciness)`

### Parameters

| Field | Type |
| ----- | ---- |
| gravity | `number` |
| bounciness | `number` |

### Returns

- None

### C Prototype

`void cur_obj_move_update_ground_air_flags(UNUSED f32 gravity, f32 bounciness);`

## cur_obj_move_y_and_get_water_level

### Description

Applies gravity and buoyancy to vertical velocity and returns the water level at the current XZ position

### Lua Example

`local numberValue = cur_obj_move_y_and_get_water_level(gravity, buoyancy)`

### Parameters

| Field | Type |
| ----- | ---- |
| gravity | `number` |
| buoyancy | `number` |

### Returns

- `number`

### C Prototype

`f32 cur_obj_move_y_and_get_water_level(f32 gravity, f32 buoyancy);`

## cur_obj_move_y

### Description

Moves the current object vertically while handling ground, water surface, and underwater states

### Lua Example

`cur_obj_move_y(gravity, bounciness, buoyancy)`

### Parameters

| Field | Type |
| ----- | ---- |
| gravity | `number` |
| bounciness | `number` |
| buoyancy | `number` |

### Returns

- None

### C Prototype

`void cur_obj_move_y(f32 gravity, f32 bounciness, f32 buoyancy);`

## cur_obj_unused_resolve_wall_collisions

### Description

Performs a wall collision sweep for the current object if the radius is positive

### Lua Example

`cur_obj_unused_resolve_wall_collisions(offsetY, radius)`

### Parameters

| Field | Type |
| ----- | ---- |
| offsetY | `number` |
| radius | `number` |

### Returns

- None

### C Prototype

`void cur_obj_unused_resolve_wall_collisions(f32 offsetY, f32 radius);`

## abs_angle_diff

### Description

Returns the absolute difference between two 16-bit angles

### Lua Example

`local integerValue = abs_angle_diff(x0, x1)`

### Parameters

| Field | Type |
| ----- | ---- |
| x0 | `integer` |
| x1 | `integer` |

### Returns

- `integer`

### C Prototype

`s16 abs_angle_diff(s16 x0, s16 x1);`

## cur_obj_move_xz_using_fvel_and_yaw

### Description

Sets the current object's horizontal velocity from forward speed and yaw, then moves it in XZ

### Lua Example

`cur_obj_move_xz_using_fvel_and_yaw()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_move_xz_using_fvel_and_yaw(void);`

## cur_obj_move_y_with_terminal_vel

### Description

Moves the current object vertically and caps downward speed at terminal velocity

### Lua Example

`cur_obj_move_y_with_terminal_vel()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_move_y_with_terminal_vel(void);`

## cur_obj_compute_vel_xz

### Description

Computes the current object's horizontal velocity from forward speed and yaw

### Lua Example

`cur_obj_compute_vel_xz()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_compute_vel_xz(void);`

## increment_velocity_toward_range

### Description

Returns a signed velocity increment that moves a value toward a target range around center

### Lua Example

`local numberValue = increment_velocity_toward_range(value, center, zeroThreshold, increment)`

### Parameters

| Field | Type |
| ----- | ---- |
| value | `number` |
| center | `number` |
| zeroThreshold | `number` |
| increment | `number` |

### Returns

- `number`

### C Prototype

`f32 increment_velocity_toward_range(f32 value, f32 center, f32 zeroThreshold, f32 increment);`

## obj_check_if_collided_with_object

### Description

Checks whether obj1's collided object list contains obj2

### Lua Example

`local integerValue = obj_check_if_collided_with_object(obj1, obj2)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj1 | [Object](structs.md#Object) |
| obj2 | [Object](structs.md#Object) |

### Returns

- `integer`

### C Prototype

`s32 obj_check_if_collided_with_object(struct Object *obj1, struct Object *obj2);`

## cur_obj_set_behavior

### Description

Sets the current object's behavior script

### Lua Example

`cur_obj_set_behavior(behavior)`

### Parameters

| Field | Type |
| ----- | ---- |
| behavior | `Pointer` <`BehaviorScript`> |

### Returns

- None

### C Prototype

`void cur_obj_set_behavior(const BehaviorScript *behavior);`

## obj_set_behavior

### Description

Sets the specified object's behavior script

### Lua Example

`obj_set_behavior(obj, behavior)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| behavior | `Pointer` <`BehaviorScript`> |

### Returns

- None

### C Prototype

`void obj_set_behavior(struct Object *obj, const BehaviorScript *behavior);`

## cur_obj_has_behavior

### Description

Checks whether the current object has the specified behavior

### Lua Example

`local integerValue = cur_obj_has_behavior(behavior)`

### Parameters

| Field | Type |
| ----- | ---- |
| behavior | `Pointer` <`BehaviorScript`> |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_has_behavior(const BehaviorScript *behavior);`

## obj_has_behavior

### Description

Checks whether an object has the specified behavior

### Lua Example

`local integerValue = obj_has_behavior(obj, behavior)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| behavior | `Pointer` <`BehaviorScript`> |

### Returns

- `integer`

### C Prototype

`s32 obj_has_behavior(struct Object *obj, const BehaviorScript *behavior);`

## cur_obj_lateral_dist_from_obj_to_home

### Description

Calculates the lateral distance from another object to the current object's home position

### Lua Example

`local numberValue = cur_obj_lateral_dist_from_obj_to_home(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- `number`

### C Prototype

`f32 cur_obj_lateral_dist_from_obj_to_home(struct Object *obj);`

## cur_obj_lateral_dist_from_mario_to_home

### Description

Calculates Mario's lateral distance to the current object's home position

### Lua Example

`local numberValue = cur_obj_lateral_dist_from_mario_to_home()`

### Parameters

- None

### Returns

- `number`

### C Prototype

`f32 cur_obj_lateral_dist_from_mario_to_home(void);`

## cur_obj_lateral_dist_to_home

### Description

Calculates the current object's lateral distance to its home position

### Lua Example

`local numberValue = cur_obj_lateral_dist_to_home()`

### Parameters

- None

### Returns

- `number`

### C Prototype

`f32 cur_obj_lateral_dist_to_home(void);`

## cur_obj_outside_home_square

### Description

Checks whether the current object is outside a square centered on its home position

### Lua Example

`local integerValue = cur_obj_outside_home_square(halfLength)`

### Parameters

| Field | Type |
| ----- | ---- |
| halfLength | `number` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_outside_home_square(f32 halfLength);`

## cur_obj_outside_home_rectangle

### Description

Checks whether the current object is outside a rectangle centered on its home position

### Lua Example

`local integerValue = cur_obj_outside_home_rectangle(minX, maxX, minZ, maxZ)`

### Parameters

| Field | Type |
| ----- | ---- |
| minX | `number` |
| maxX | `number` |
| minZ | `number` |
| maxZ | `number` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_outside_home_rectangle(f32 minX, f32 maxX, f32 minZ, f32 maxZ);`

## cur_obj_set_pos_to_home

### Description

Teleports the current object to its home position

### Lua Example

`cur_obj_set_pos_to_home()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_set_pos_to_home(void);`

## cur_obj_set_pos_to_home_and_stop

### Description

Teleports the current object to its home position and stops its motion

### Lua Example

`cur_obj_set_pos_to_home_and_stop()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_set_pos_to_home_and_stop(void);`

## cur_obj_shake_y

### Description

Shakes the current object vertically by alternating upward and downward offsets

### Lua Example

`cur_obj_shake_y(amount)`

### Parameters

| Field | Type |
| ----- | ---- |
| amount | `number` |

### Returns

- None

### C Prototype

`void cur_obj_shake_y(f32 amount);`

## cur_obj_start_cam_event

### Description

Starts a camera event and makes the current object the secondary camera focus

### Lua Example

`cur_obj_start_cam_event(obj, cameraEvent)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| cameraEvent | `integer` |

### Returns

- None

### C Prototype

`void cur_obj_start_cam_event(UNUSED struct Object *obj, s32 cameraEvent);`

## set_mario_interact_hoot_if_in_range

### Description

Sets Mario's interact status to hoot-grabbed if Mario is within range `maxDistanceToMario`

### Lua Example

`set_mario_interact_hoot_if_in_range(unused1, unused2, maxDistanceToMario)`

### Parameters

| Field | Type |
| ----- | ---- |
| unused1 | `integer` |
| unused2 | `integer` |
| maxDistanceToMario | `number` |

### Returns

- None

### C Prototype

`void set_mario_interact_hoot_if_in_range(UNUSED s32 unused1, UNUSED s32 unused2, f32 maxDistanceToMario);`

## obj_set_billboard

### Description

Enables billboard rendering for an object

### Lua Example

`obj_set_billboard(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_set_billboard(struct Object *obj);`

## obj_set_cylboard

### Description

Enables cylindrical billboard rendering for an object

### Lua Example

`obj_set_cylboard(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_set_cylboard(struct Object *obj);`

## cur_obj_set_billboard_if_vanilla_cam

### Description

Chooses the appropriate billboard type for the current object based on camera mode

### Lua Example

`cur_obj_set_billboard_if_vanilla_cam()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_set_billboard_if_vanilla_cam(void);`

## obj_set_hitbox_radius_and_height

### Description

Sets an object's hitbox radius and height

### Lua Example

`obj_set_hitbox_radius_and_height(obj, radius, height)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| radius | `number` |
| height | `number` |

### Returns

- None

### C Prototype

`void obj_set_hitbox_radius_and_height(struct Object *obj, f32 radius, f32 height);`

## obj_set_hurtbox_radius_and_height

### Description

Sets an object's hurtbox radius and height

### Lua Example

`obj_set_hurtbox_radius_and_height(obj, radius, height)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| radius | `number` |
| height | `number` |

### Returns

- None

### C Prototype

`void obj_set_hurtbox_radius_and_height(struct Object *obj, f32 radius, f32 height);`

## cur_obj_set_hitbox_radius_and_height

### Description

Sets the current object's hitbox radius and height

### Lua Example

`cur_obj_set_hitbox_radius_and_height(radius, height)`

### Parameters

| Field | Type |
| ----- | ---- |
| radius | `number` |
| height | `number` |

### Returns

- None

### C Prototype

`void cur_obj_set_hitbox_radius_and_height(f32 radius, f32 height);`

## cur_obj_set_hurtbox_radius_and_height

### Description

Sets the current object's hurtbox radius and height

### Lua Example

`cur_obj_set_hurtbox_radius_and_height(radius, height)`

### Parameters

| Field | Type |
| ----- | ---- |
| radius | `number` |
| height | `number` |

### Returns

- None

### C Prototype

`void cur_obj_set_hurtbox_radius_and_height(f32 radius, f32 height);`

## obj_spawn_loot_coins

### Description

Spawns loot coins from an object using the specified behavior, jitter, and model

### Lua Example

`obj_spawn_loot_coins(obj, numCoins, baseYVel, coinBehavior, posJitter, model)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| numCoins | `integer` |
| baseYVel | `number` |
| coinBehavior | `Pointer` <`BehaviorScript`> |
| posJitter | `integer` |
| model | `integer` |

### Returns

- None

### C Prototype

`void obj_spawn_loot_coins(struct Object *obj, s32 numCoins, f32 baseYVel, const BehaviorScript *coinBehavior, s16 posJitter, s16 model);`

## obj_spawn_loot_blue_coins

### Description

Spawns blue loot coins from an object

### Lua Example

`obj_spawn_loot_blue_coins(obj, numCoins, baseYVel, posJitter)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| numCoins | `integer` |
| baseYVel | `number` |
| posJitter | `integer` |

### Returns

- None

### C Prototype

`void obj_spawn_loot_blue_coins(struct Object *obj, s32 numCoins, f32 baseYVel, s16 posJitter);`

## obj_spawn_loot_yellow_coins

### Description

Spawns yellow loot coins from an object

### Lua Example

`obj_spawn_loot_yellow_coins(obj, numCoins, baseYVel)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| numCoins | `integer` |
| baseYVel | `number` |

### Returns

- None

### C Prototype

`void obj_spawn_loot_yellow_coins(struct Object *obj, s32 numCoins, f32 baseYVel);`

## cur_obj_spawn_loot_coin_at_mario_pos

### Description

Spawns a yellow coin at Mario's position and decrements the current object's loot count

### Lua Example

`cur_obj_spawn_loot_coin_at_mario_pos(m)`

### Parameters

| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |

### Returns

- None

### C Prototype

`void cur_obj_spawn_loot_coin_at_mario_pos(struct MarioState* m);`

## cur_obj_abs_y_dist_to_home

### Description

Returns the absolute vertical distance from the object to its home position

### Lua Example

`local numberValue = cur_obj_abs_y_dist_to_home()`

### Parameters

- None

### Returns

- `number`

### C Prototype

`f32 cur_obj_abs_y_dist_to_home(void);`

## cur_obj_advance_looping_anim

### Description

Advances the current object animation frame and returns the normalized frame progress

### Lua Example

`local integerValue = cur_obj_advance_looping_anim()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s32 cur_obj_advance_looping_anim(void);`

## cur_obj_detect_steep_floor

### Description

Checks whether the object is moving into a steep floor or death plane and returns a collision code

### Lua Example

`local integerValue = cur_obj_detect_steep_floor(steepAngleDegrees)`

### Parameters

| Field | Type |
| ----- | ---- |
| steepAngleDegrees | `integer` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_detect_steep_floor(s16 steepAngleDegrees);`

## cur_obj_resolve_wall_collisions

### Description

Resolves wall collisions for the current object and returns `TRUE` if it hit a steep wall

### Lua Example

`local integerValue = cur_obj_resolve_wall_collisions()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s32 cur_obj_resolve_wall_collisions(void);`

## cur_obj_update_floor

### Description

Updates the current object's floor pointer, floor type, and floor room based on the surface below it

### Lua Example

`cur_obj_update_floor()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_update_floor(void);`

## cur_obj_update_floor_and_resolve_wall_collisions

### Description

Updates the floor and resolves walls for the current object, setting move flags accordingly

### Lua Example

`cur_obj_update_floor_and_resolve_wall_collisions(steepSlopeDegrees)`

### Parameters

| Field | Type |
| ----- | ---- |
| steepSlopeDegrees | `integer` |

### Returns

- None

### C Prototype

`void cur_obj_update_floor_and_resolve_wall_collisions(s16 steepSlopeDegrees);`

## cur_obj_update_floor_and_walls

### Description

Updates the current object floor and wall state using a default steep slope threshold

### Lua Example

`cur_obj_update_floor_and_walls()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_update_floor_and_walls(void);`

## cur_obj_move_standard

### Description

Updates the current object velocity and position using standard gravity, drag, and slope behavior

### Lua Example

`cur_obj_move_standard(steepSlopeAngleDegrees)`

### Parameters

| Field | Type |
| ----- | ---- |
| steepSlopeAngleDegrees | `integer` |

### Returns

- None

### C Prototype

`void cur_obj_move_standard(s16 steepSlopeAngleDegrees);`

## cur_obj_within_12k_bounds

### Description

Checks whether the current object is within a 12,000-unit world bound on all axes

### Lua Example

`local integerValue = cur_obj_within_12k_bounds()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s32 cur_obj_within_12k_bounds(void);`

## cur_obj_move_using_vel_and_gravity

### Description

Applies object velocity and gravity directly to the object's position with no terminal velocity

### Lua Example

`cur_obj_move_using_vel_and_gravity()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_move_using_vel_and_gravity(void);`

## cur_obj_move_using_fvel_and_gravity

### Description

Computes the object's XZ velocity from forward velocity then applies gravity-based movement

### Lua Example

`cur_obj_move_using_fvel_and_gravity()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_move_using_fvel_and_gravity(void);`

## obj_set_pos_relative

### Description

Sets an object position relative to another object using local left, up, and forward offsets

### Lua Example

`obj_set_pos_relative(obj, other, dleft, dy, dforward)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| other | [Object](structs.md#Object) |
| dleft | `number` |
| dy | `number` |
| dforward | `number` |

### Returns

- None

### C Prototype

`void obj_set_pos_relative(struct Object *obj, struct Object *other, f32 dleft, f32 dy, f32 dforward);`

## cur_obj_angle_to_home

### Description

Returns the yaw angle from the current object toward its home position

### Lua Example

`local integerValue = cur_obj_angle_to_home()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s16 cur_obj_angle_to_home(void);`

## obj_set_gfx_pos_at_obj_pos

### Description

Copies an object's world position and orientation into another object's graphics node

### Lua Example

`obj_set_gfx_pos_at_obj_pos(obj1, obj2)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj1 | [Object](structs.md#Object) |
| obj2 | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_set_gfx_pos_at_obj_pos(struct Object *obj1, struct Object *obj2);`

## obj_translate_local

### Description

Transforms the vector at `localTranslateIndex` into the object's local coordinates, and then adds it to the vector at `posIndex`

### Lua Example

`obj_translate_local(obj, posIndex, localTranslateIndex)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| posIndex | `integer` |
| localTranslateIndex | `integer` |

### Returns

- None

### C Prototype

`void obj_translate_local(struct Object *obj, s16 posIndex, s16 localTranslateIndex);`

## obj_build_transform_from_pos_and_angle

### Description

Copies an object's position and rotation into its transform matrix using the specified field indices

### Lua Example

`obj_build_transform_from_pos_and_angle(obj, posIndex, angleIndex)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| posIndex | `integer` |
| angleIndex | `integer` |

### Returns

- None

### C Prototype

`void obj_build_transform_from_pos_and_angle(struct Object *obj, s16 posIndex, s16 angleIndex);`

## obj_set_throw_matrix_from_transform

### Description

Sets the object's graphics throw matrix from its transform and applies object scale if needed

### Lua Example

`obj_set_throw_matrix_from_transform(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_set_throw_matrix_from_transform(struct Object *obj);`

## obj_build_transform_relative_to_parent

### Description

Builds the object's world transform relative to its parent and updates its world position

### Lua Example

`obj_build_transform_relative_to_parent(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_build_transform_relative_to_parent(struct Object *obj);`

## obj_create_transform_from_self

### Description

Initializes the object's own transform matrix from its current world position

### Lua Example

`obj_create_transform_from_self(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_create_transform_from_self(struct Object *obj);`

## cur_obj_rotate_move_angle_using_vel

### Description

Rotates the current object's move angles by its angular velocity components

### Lua Example

`cur_obj_rotate_move_angle_using_vel()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_rotate_move_angle_using_vel(void);`

## cur_obj_rotate_face_angle_using_vel

### Description

Rotates the current object's face angles by its angular velocity components

### Lua Example

`cur_obj_rotate_face_angle_using_vel()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_rotate_face_angle_using_vel(void);`

## cur_obj_set_face_angle_to_move_angle

### Description

Copies the current object's move angles into its face angles

### Lua Example

`cur_obj_set_face_angle_to_move_angle()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_set_face_angle_to_move_angle(void);`

## cur_obj_follow_path

### Description

Advances path-following state and returns whether a waypoint or path end was reached

### Lua Example

`local integerValue = cur_obj_follow_path(unusedArg)`

### Parameters

| Field | Type |
| ----- | ---- |
| unusedArg | `integer` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_follow_path(UNUSED s32 unusedArg);`

## chain_segment_init

### Description

Initializes a chain segment's position and orientation to identity values

### Lua Example

`chain_segment_init(segment)`

### Parameters

| Field | Type |
| ----- | ---- |
| segment | [ChainSegment](structs.md#ChainSegment) |

### Returns

- None

### C Prototype

`void chain_segment_init(struct ChainSegment *segment);`

## random_f32_around_zero

### Description

Returns a random floating-point value within +/- diameter/2

### Lua Example

`local numberValue = random_f32_around_zero(diameter)`

### Parameters

| Field | Type |
| ----- | ---- |
| diameter | `number` |

### Returns

- `number`

### C Prototype

`f32 random_f32_around_zero(f32 diameter);`

## obj_scale_random

### Description

Randomly scales an object within a range and applies a minimum scale

### Lua Example

`obj_scale_random(obj, rangeLength, minScale)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| rangeLength | `number` |
| minScale | `number` |

### Returns

- None

### C Prototype

`void obj_scale_random(struct Object *obj, f32 rangeLength, f32 minScale);`

## obj_translate_xyz_random

### Description

Applies a random translation to an object on all three axes

### Lua Example

`obj_translate_xyz_random(obj, rangeLength)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| rangeLength | `number` |

### Returns

- None

### C Prototype

`void obj_translate_xyz_random(struct Object *obj, f32 rangeLength);`

## obj_translate_xz_random

### Description

Applies a random translation to an object on the X and Z axes

### Lua Example

`obj_translate_xz_random(obj, rangeLength)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| rangeLength | `number` |

### Returns

- None

### C Prototype

`void obj_translate_xz_random(struct Object *obj, f32 rangeLength);`

## obj_build_vel_from_transform

### Description

Builds the object's world velocity from its transform basis vectors

### Lua Example

`obj_build_vel_from_transform(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_build_vel_from_transform(struct Object *obj);`

## cur_obj_set_pos_via_transform

### Description

Moves the current object using its transform-derived velocity

### Lua Example

`cur_obj_set_pos_via_transform()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_set_pos_via_transform(void);`

## cur_obj_reflect_move_angle_off_wall

### Description

Reflects the current object's move angle across its wall normal

### Lua Example

`local integerValue = cur_obj_reflect_move_angle_off_wall()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s16 cur_obj_reflect_move_angle_off_wall(void);`

## cur_obj_spawn_particles

### Description

Spawns particles based on information in a SpawnParticlesInfo structure

### Lua Example

`cur_obj_spawn_particles(info)`

### Parameters

| Field | Type |
| ----- | ---- |
| info | [SpawnParticlesInfo](structs.md#SpawnParticlesInfo) |

### Returns

- None

### C Prototype

`void cur_obj_spawn_particles(struct SpawnParticlesInfo *info);`

## obj_set_hitbox

### Description

Sets an object's hitbox and hurtbox quantities then makes it tangible

### Lua Example

`obj_set_hitbox(obj, hitbox)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| hitbox | [ObjectHitbox](structs.md#ObjectHitbox) |

### Returns

- None

### C Prototype

`void obj_set_hitbox(struct Object *obj, struct ObjectHitbox *hitbox);`

## signum_positive

### Description

Returns 1 for non-negative values and -1 for negative values

### Lua Example

`local integerValue = signum_positive(x)`

### Parameters

| Field | Type |
| ----- | ---- |
| x | `integer` |

### Returns

- `integer`

### C Prototype

`s32 signum_positive(s32 x);`

## cur_obj_wait_then_blink

### Description

Makes the current object blink after a delay and returns `TRUE` when blinking is complete

### Lua Example

`local integerValue = cur_obj_wait_then_blink(timeUntilBlinking, numBlinks)`

### Parameters

| Field | Type |
| ----- | ---- |
| timeUntilBlinking | `integer` |
| numBlinks | `integer` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_wait_then_blink(s32 timeUntilBlinking, s32 numBlinks);`

## cur_obj_is_mario_ground_pounding_platform

### Description

Returns `TRUE` if any active player is ground-pounding the current platform object

### Lua Example

`local integerValue = cur_obj_is_mario_ground_pounding_platform()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s32 cur_obj_is_mario_ground_pounding_platform(void);`

## obj_is_mario_ground_pounding_platform

### Description

Checks whether a MarioState is ground-pounding the specified platform object

### Lua Example

`local integerValue = obj_is_mario_ground_pounding_platform(m, obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |
| obj | [Object](structs.md#Object) |

### Returns

- `integer`

### C Prototype

`s32 obj_is_mario_ground_pounding_platform(struct MarioState *m, struct Object *obj);`

## spawn_mist_particles

### Description

Spawns mist particles at the current object without playing sound

### Lua Example

`spawn_mist_particles()`

### Parameters

- None

### Returns

- None

### C Prototype

`void spawn_mist_particles(void);`

## spawn_mist_particles_with_sound

### Description

Spawns mist particles at the current object and plays the specified sound

### Lua Example

`spawn_mist_particles_with_sound(sp18)`

### Parameters

| Field | Type |
| ----- | ---- |
| sp18 | `integer` |

### Returns

- None

### C Prototype

`void spawn_mist_particles_with_sound(u32 sp18);`

## cur_obj_push_mario_away

### Description

Pushes any player within a radius away from the current object on the XZ plane

### Lua Example

`cur_obj_push_mario_away(radius)`

### Parameters

| Field | Type |
| ----- | ---- |
| radius | `number` |

### Returns

- None

### C Prototype

`void cur_obj_push_mario_away(f32 radius);`

## cur_obj_push_mario_away_from_cylinder

### Description

Pushes any player within a vertical cylinder away from the current object

### Lua Example

`cur_obj_push_mario_away_from_cylinder(radius, extentY)`

### Parameters

| Field | Type |
| ----- | ---- |
| radius | `number` |
| extentY | `number` |

### Returns

- None

### C Prototype

`void cur_obj_push_mario_away_from_cylinder(f32 radius, f32 extentY);`

## bhv_dust_smoke_loop

### Description

Behavior loop function for dust smoke

### Lua Example

`bhv_dust_smoke_loop()`

### Parameters

- None

### Returns

- None

### C Prototype

`void bhv_dust_smoke_loop(void);`

## cur_obj_scale_over_time

### Description

Smoothly scales between `minScale` and `maxScale` the current object over a `duration` using enabled `axes` (1 = x, 2 = y, 4 = z, can be combined)

### Lua Example

`cur_obj_scale_over_time(axes, duration, minScale, maxScale)`

### Parameters

| Field | Type |
| ----- | ---- |
| axes | `integer` |
| duration | `integer` |
| minScale | `number` |
| maxScale | `number` |

### Returns

- None

### C Prototype

`void cur_obj_scale_over_time(s32 axes, s32 duration, f32 minScale, f32 maxScale);`

## cur_obj_set_pos_to_home_with_debug

### Description

Moves an object to its home position while applying debug position offsets

### Lua Example

`cur_obj_set_pos_to_home_with_debug()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_set_pos_to_home_with_debug(void);`

## cur_obj_is_mario_on_platform

### Description

Returns `TRUE` if Mario is currently standing on the current platform object

### Lua Example

`local integerValue = cur_obj_is_mario_on_platform()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s32 cur_obj_is_mario_on_platform(void);`

## cur_obj_is_any_player_on_platform

### Description

Returns `TRUE` if any player is standing on the current platform object

### Lua Example

`local integerValue = cur_obj_is_any_player_on_platform()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s32 cur_obj_is_any_player_on_platform(void);`

## cur_obj_shake_y_until

### Description

Oscillates the current object vertically until a specified number of cycles passes

### Lua Example

`local integerValue = cur_obj_shake_y_until(cycles, amount)`

### Parameters

| Field | Type |
| ----- | ---- |
| cycles | `integer` |
| amount | `integer` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_shake_y_until(s32 cycles, s32 amount);`

## cur_obj_move_up_and_down

### Description

Moves the current object up and down along a preset displacement table

### Lua Example

`local integerValue = cur_obj_move_up_and_down(index)`

### Parameters

| Field | Type |
| ----- | ---- |
| index | `integer` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_move_up_and_down(s32 index);`

## spawn_star_with_no_lvl_exit

### Description

Spawns a star object without triggering level exit behavior

### Lua Example

`local objectValue = spawn_star_with_no_lvl_exit(setHomeToMario, unused)`

### Parameters

| Field | Type |
| ----- | ---- |
| setHomeToMario | `integer` |
| unused | `integer` |

### Returns

- [Object](structs.md#Object)

### C Prototype

`struct Object *spawn_star_with_no_lvl_exit(s32 setHomeToMario, s32 unused);`

## spawn_base_star_with_no_lvl_exit

### Description

Spawns a base star with default parameters and no level exit behavior

### Lua Example

`spawn_base_star_with_no_lvl_exit()`

### Parameters

- None

### Returns

- None

### C Prototype

`void spawn_base_star_with_no_lvl_exit(void);`

## cur_obj_mario_far_away

### Description

Returns `TRUE` if the current object is farther than 2000 units from every active Mario

### Lua Example

`local integerValue = cur_obj_mario_far_away()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s32 cur_obj_mario_far_away(void);`

## is_mario_moving_fast_or_in_air

### Description

Returns `TRUE` if the current Mario is moving faster than threshold or is airborne

### Lua Example

`local integerValue = is_mario_moving_fast_or_in_air(speedThreshold)`

### Parameters

| Field | Type |
| ----- | ---- |
| speedThreshold | `integer` |

### Returns

- `integer`

### C Prototype

`s32 is_mario_moving_fast_or_in_air(s32 speedThreshold);`

## is_item_in_array

### Description

Checks whether a signed item appears in a terminated array

### Lua Example

`local integerValue = is_item_in_array(item, array)`

### Parameters

| Field | Type |
| ----- | ---- |
| item | `integer` |
| array | `Pointer` <`integer`> |

### Returns

- `integer`

### C Prototype

`s32 is_item_in_array(s8 item, s8 *array);`

## bhv_init_room

### Description

Sets the current object's room based on the floor surface underneath it

### Lua Example

`bhv_init_room()`

### Parameters

- None

### Returns

- None

### C Prototype

`void bhv_init_room(void);`

## cur_obj_enable_rendering_if_mario_in_room

### Description

Enables rendering for the current object if any active player is in a connected room

### Lua Example

`cur_obj_enable_rendering_if_mario_in_room()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_enable_rendering_if_mario_in_room(void);`

## cur_obj_set_hitbox_and_die_if_attacked

### Description

Gives the current object a hitbox and kills it if attacked, with optional loot suppression

### Lua Example

`local integerValue = cur_obj_set_hitbox_and_die_if_attacked(hitbox, deathSound, noLootCoins)`

### Parameters

| Field | Type |
| ----- | ---- |
| hitbox | [ObjectHitbox](structs.md#ObjectHitbox) |
| deathSound | `integer` |
| noLootCoins | `integer` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_set_hitbox_and_die_if_attacked(struct ObjectHitbox *hitbox, s32 deathSound, s32 noLootCoins);`

## obj_explode_and_spawn_coins

### Description

Explodes the current object, spawns particles, and optionally spawns coins

### Lua Example

`obj_explode_and_spawn_coins(mistSize, coinType)`

### Parameters

| Field | Type |
| ----- | ---- |
| mistSize | `number` |
| coinType | [enum CoinType](constants.md#enum-CoinType) |

### Returns

- None

### C Prototype

`void obj_explode_and_spawn_coins(f32 mistSize, enum CoinType coinType);`

## cur_obj_if_hit_wall_bounce_away

### Description

Sets the current object to bounce away if it hit a wall

### Lua Example

`cur_obj_if_hit_wall_bounce_away()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_if_hit_wall_bounce_away(void);`

## cur_obj_hide_if_mario_far_away_y

### Description

Hides the current object if Mario is too far above or below it, otherwise ensures it is visible

### Lua Example

`local integerValue = cur_obj_hide_if_mario_far_away_y(distY)`

### Parameters

| Field | Type |
| ----- | ---- |
| distY | `number` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_hide_if_mario_far_away_y(f32 distY);`

## obj_is_hidden

### Description

Returns `TRUE` if the given object is currently hidden from rendering

### Lua Example

`local integerValue = obj_is_hidden(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- `integer`

### C Prototype

`s32 obj_is_hidden(struct Object *obj);`

## enable_time_stop

### Description

Enables global time stop state

### Lua Example

`enable_time_stop()`

### Parameters

- None

### Returns

- None

### C Prototype

`void enable_time_stop(void);`

## enable_time_stop_if_alone

### Description

Enables time stop only when the local player is alone

### Lua Example

`enable_time_stop_if_alone()`

### Parameters

- None

### Returns

- None

### C Prototype

`void enable_time_stop_if_alone(void);`

## disable_time_stop

### Description

Disables global time stop state

### Lua Example

`disable_time_stop()`

### Parameters

- None

### Returns

- None

### C Prototype

`void disable_time_stop(void);`

## set_time_stop_flags

### Description

Sets global time stop flags

### Lua Example

`set_time_stop_flags(flags)`

### Parameters

| Field | Type |
| ----- | ---- |
| flags | `integer` |

### Returns

- None

### C Prototype

`void set_time_stop_flags(s32 flags);`

## set_time_stop_flags_if_alone

### Description

Sets time stop flags only if the local player is alone

### Lua Example

`set_time_stop_flags_if_alone(flags)`

### Parameters

| Field | Type |
| ----- | ---- |
| flags | `integer` |

### Returns

- None

### C Prototype

`void set_time_stop_flags_if_alone(s32 flags);`

## clear_time_stop_flags

### Description

Clears selected global time stop flags

### Lua Example

`clear_time_stop_flags(flags)`

### Parameters

| Field | Type |
| ----- | ---- |
| flags | `integer` |

### Returns

- None

### C Prototype

`void clear_time_stop_flags(s32 flags);`

## cur_obj_can_mario_activate_textbox

### Description

Checks whether Mario can activate the current object's textbox within a vertical and horizontal range

### Lua Example

`local integerValue = cur_obj_can_mario_activate_textbox(m, radius, height, unused)`

### Parameters

| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |
| radius | `number` |
| height | `number` |
| unused | `integer` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_can_mario_activate_textbox(struct MarioState* m, f32 radius, f32 height, OPTIONAL UNUSED s32 unused);`

## cur_obj_end_dialog

### Description

Ends dialog state for the current object and records Mario's response

### Lua Example

`cur_obj_end_dialog(m, dialogFlags, dialogResult)`

### Parameters

| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |
| dialogFlags | `integer` |
| dialogResult | `integer` |

### Returns

- None

### C Prototype

`void cur_obj_end_dialog(struct MarioState* m, s32 dialogFlags, s32 dialogResult);`

## cur_obj_has_model

### Description

Checks whether the current object uses the specified model geometry

### Lua Example

`local integerValue = cur_obj_has_model(modelID)`

### Parameters

| Field | Type |
| ----- | ---- |
| modelID | `integer` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_has_model(u16 modelID);`

## cur_obj_align_gfx_with_floor

### Description

Aligns the current object's graphics with the floor normal at its position

### Lua Example

`cur_obj_align_gfx_with_floor()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_align_gfx_with_floor(void);`

## mario_is_within_rectangle

### Description

Returns `TRUE` if Mario's position lies within a 2D rectangle on the XZ plane

### Lua Example

`local integerValue = mario_is_within_rectangle(minX, maxX, minZ, maxZ)`

### Parameters

| Field | Type |
| ----- | ---- |
| minX | `integer` |
| maxX | `integer` |
| minZ | `integer` |
| maxZ | `integer` |

### Returns

- `integer`

### C Prototype

`s32 mario_is_within_rectangle(s16 minX, s16 maxX, s16 minZ, s16 maxZ);`

## cur_obj_shake_screen

### Description

Shakes the camera around the current object with a given intensity

### Lua Example

`cur_obj_shake_screen(shake)`

### Parameters

| Field | Type |
| ----- | ---- |
| shake | `integer` |

### Returns

- None

### C Prototype

`void cur_obj_shake_screen(s32 shake);`

## obj_attack_collided_from_other_object

### Description

Marks another object as attacked by the current object and returns whether it collided

### Lua Example

`local integerValue = obj_attack_collided_from_other_object(obj)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns

- `integer`

### C Prototype

`s32 obj_attack_collided_from_other_object(struct Object *obj);`

## cur_obj_was_attacked_or_ground_pounded

### Description

Returns `TRUE` if the current object was attacked or ground-pounded and clears interact status

### Lua Example

`local integerValue = cur_obj_was_attacked_or_ground_pounded()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s32 cur_obj_was_attacked_or_ground_pounded(void);`

## obj_copy_behavior_params

### Description

Copies behavior parameters from one object to another

### Lua Example

`obj_copy_behavior_params(dst, src)`

### Parameters

| Field | Type |
| ----- | ---- |
| dst | [Object](structs.md#Object) |
| src | [Object](structs.md#Object) |

### Returns

- None

### C Prototype

`void obj_copy_behavior_params(struct Object *dst, struct Object *src);`

## cur_obj_init_animation_and_anim_frame

### Description

Initializes the current object's animation and sets a specific frame

### Lua Example

`cur_obj_init_animation_and_anim_frame(animIndex, animFrame)`

### Parameters

| Field | Type |
| ----- | ---- |
| animIndex | `integer` |
| animFrame | `integer` |

### Returns

- None

### C Prototype

`void cur_obj_init_animation_and_anim_frame(s32 animIndex, s32 animFrame);`

## cur_obj_init_animation_and_check_if_near_end

### Description

Initializes the current object's animation and checks if it is near the end

### Lua Example

`local integerValue = cur_obj_init_animation_and_check_if_near_end(animIndex)`

### Parameters

| Field | Type |
| ----- | ---- |
| animIndex | `integer` |

### Returns

- `integer`

### C Prototype

`s32 cur_obj_init_animation_and_check_if_near_end(s32 animIndex);`

## cur_obj_init_animation_and_extend_if_at_end

### Description

Initializes the current object's animation and extends it if the animation has ended

### Lua Example

`cur_obj_init_animation_and_extend_if_at_end(animIndex)`

### Parameters

| Field | Type |
| ----- | ---- |
| animIndex | `integer` |

### Returns

- None

### C Prototype

`void cur_obj_init_animation_and_extend_if_at_end(s32 animIndex);`

## cur_obj_check_grabbed_mario

### Description

Checks whether the current object has grabbed Mario and becomes intangible if so

### Lua Example

`local integerValue = cur_obj_check_grabbed_mario()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s32 cur_obj_check_grabbed_mario(void);`

## player_performed_grab_escape_action

### Description

Returns `TRUE` if the player performed an escape action during a grab

### Lua Example

`local integerValue = player_performed_grab_escape_action()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s32 player_performed_grab_escape_action(void);`

## cur_obj_unused_play_footstep_sound

### Description

Plays a footstep sound when the current animation reaches one of two frames

### Lua Example

`cur_obj_unused_play_footstep_sound(animFrame1, animFrame2, sound)`

### Parameters

| Field | Type |
| ----- | ---- |
| animFrame1 | `integer` |
| animFrame2 | `integer` |
| sound | `integer` |

### Returns

- None

### C Prototype

`void cur_obj_unused_play_footstep_sound(s32 animFrame1, s32 animFrame2, s32 sound);`

## enable_time_stop_including_mario

### Description

Enables time stop for the world and Mario/doors

### Lua Example

`enable_time_stop_including_mario()`

### Parameters

- None

### Returns

- None

### C Prototype

`void enable_time_stop_including_mario(void);`

## disable_time_stop_including_mario

### Description

Disables time stop for the world and Mario/doors

### Lua Example

`disable_time_stop_including_mario()`

### Parameters

- None

### Returns

- None

### C Prototype

`void disable_time_stop_including_mario(void);`

## cur_obj_check_interacted

### Description

Returns `TRUE` if the current object has been interacted with and clears the status

### Lua Example

`local integerValue = cur_obj_check_interacted()`

### Parameters

- None

### Returns

- `integer`

### C Prototype

`s32 cur_obj_check_interacted(void);`

## cur_obj_spawn_loot_blue_coin

### Description

Spawns a blue coin from the current object when sufficient loot coins are available

### Lua Example

`cur_obj_spawn_loot_blue_coin()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_spawn_loot_blue_coin(void);`

## cur_obj_spawn_star_at_y_offset

### Description

Temporarily shifts the current object's Y position and spawns a star

### Lua Example

`cur_obj_spawn_star_at_y_offset(targetX, targetY, targetZ, offsetY)`

### Parameters

| Field | Type |
| ----- | ---- |
| targetX | `number` |
| targetY | `number` |
| targetZ | `number` |
| offsetY | `number` |

### Returns

- None

### C Prototype

`void cur_obj_spawn_star_at_y_offset(f32 targetX, f32 targetY, f32 targetZ, f32 offsetY);`

## cur_obj_set_home_once

### Description

Sets the current object's home position once and marks it as initialized

### Lua Example

`cur_obj_set_home_once()`

### Parameters

- None

### Returns

- None

### C Prototype

`void cur_obj_set_home_once(void);`

## get_trajectory_length

### Description

Gets the number of steps in a trajectory until the end marker

### Lua Example

`local integerValue = get_trajectory_length(trajectory)`

### Parameters

| Field | Type |
| ----- | ---- |
| trajectory | `Pointer` <`Trajectory`> |

### Returns

- `integer`

### C Prototype

`s32 get_trajectory_length(Trajectory* trajectory);`

---

# functions from object_list_processor.h

## set_object_respawn_info_bits

### Description

Runs an OR operator on the `obj`'s respawn info with `bits` << 8. If `bits` is 0xFF, this prevents the object from respawning after leaving and re-entering the area

### Lua Example

`set_object_respawn_info_bits(obj, bits)`

### Parameters

| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| bits | `integer` |

### Returns

- None

### C Prototype

`void set_object_respawn_info_bits(struct Object *obj, u8 bits);`

---

[< prev](functions-4.md) | [1](functions.md) | [2](functions-2.md) | [3](functions-3.md) | [4](functions-4.md) | 5 | [6](functions-6.md) | [7](functions-7.md) | [next >](functions-6.md)
