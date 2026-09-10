## [:rewind: Lua Functions](functions.md)

---

[< prev](functions-5.md) | [1](functions.md) | [2](functions-2.md) | [3](functions-3.md) | [4](functions-4.md) | [5](functions-5.md) | 6 | [7](functions-7.md) | [next >](functions-7.md)]


---
# functions from rumble_init.h

<br />


## queue_rumble_data

### Description
Queues rumble data with `time` and `level`

### Lua Example
`queue_rumble_data(time, level)`

### Parameters
| Field | Type |
| ----- | ---- |
| time | `integer` |
| level | `integer` |

### Returns
- None

### C Prototype
`void queue_rumble_data(s16 time, s16 level);`


## queue_rumble_data_object

### Description
Queues rumble data for object with `time` and `level`, factoring in its distance from Mario

### Lua Example
`queue_rumble_data_object(object, time, level)`

### Parameters
| Field | Type |
| ----- | ---- |
| object | [Object](structs.md#Object) |
| time | `integer` |
| level | `integer` |

### Returns
- None

### C Prototype
`void queue_rumble_data_object(struct Object* object, s16 time, s16 level);`


## queue_rumble_data_mario

### Description
Queues rumble data with `time` and `level` only if `m` is the local Mario

### Lua Example
`queue_rumble_data_mario(m, time, level)`

### Parameters
| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |
| time | `integer` |
| level | `integer` |

### Returns
- None

### C Prototype
`void queue_rumble_data_mario(struct MarioState* m, s16 time, s16 level);`


## queue_rumble_decay

### Description
Queues rumble `decay`

### Lua Example
`queue_rumble_decay(decay)`

### Parameters
| Field | Type |
| ----- | ---- |
| decay | `integer` |

### Returns
- None

### C Prototype
`void queue_rumble_decay(s16 decay);`


## is_rumble_finished_and_queue_empty

### Description
Checks if rumble is finished and there is no rumble queued

### Lua Example
`local integerValue = is_rumble_finished_and_queue_empty()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u8 is_rumble_finished_and_queue_empty(void);`


## reset_rumble_timers

### Description
Resets rumble timers only if `m` is the local Mario

### Lua Example
`reset_rumble_timers(m)`

### Parameters
| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |

### Returns
- None

### C Prototype
`void reset_rumble_timers(struct MarioState* m);`


## reset_rumble_timers_vibrate

### Description
Resets rumble timers and sets vibrate based on `level`

### Lua Example
`reset_rumble_timers_vibrate(m, level)`

### Parameters
| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |
| level | `integer` |

### Returns
- None

### C Prototype
`void reset_rumble_timers_vibrate(struct MarioState* m, s32 level);`


## queue_rumble_submerged

### Description
Queues rumble data for submerged actions

### Lua Example
`queue_rumble_submerged()`

### Parameters
- None

### Returns
- None

### C Prototype
`void queue_rumble_submerged(void);`


## cancel_rumble

### Description
Cancels all currently queued rumble data

### Lua Example
`cancel_rumble()`

### Parameters
- None

### Returns
- None

### C Prototype
`void cancel_rumble(void);`


---
# functions from save_file.h

<br />


## get_level_num_from_course_num

### Description
Gets the course number's corresponding level number

### Lua Example
`local integerValue = get_level_num_from_course_num(courseNum)`

### Parameters
| Field | Type |
| ----- | ---- |
| courseNum | `integer` |

### Returns
- `integer`

### C Prototype
`s8 get_level_num_from_course_num(s16 courseNum);`


## get_level_course_num

### Description
Gets the level number's corresponding course number

### Lua Example
`local integerValue = get_level_course_num(levelNum)`

### Parameters
| Field | Type |
| ----- | ---- |
| levelNum | `integer` |

### Returns
- `integer`

### C Prototype
`s8 get_level_course_num(s16 levelNum);`


## touch_coin_score_age

### Description
Marks the coin score for a specific course as the newest among all save files. Adjusts the age of other scores to reflect the update.
Useful for leaderboard tracking or displaying recent progress

### Lua Example
`touch_coin_score_age(fileIndex, courseIndex)`

### Parameters
| Field | Type |
| ----- | ---- |
| fileIndex | `integer` |
| courseIndex | `integer` |

### Returns
- None

### C Prototype
`void touch_coin_score_age(s32 fileIndex, s32 courseIndex);`


## save_file_do_save

### Description
Saves the current state of the game into a specified save file. Includes data verification and backup management.
Useful for maintaining game progress during play or when saving manually

### Lua Example
`save_file_do_save(fileIndex, forceSave)`

### Parameters
| Field | Type |
| ----- | ---- |
| fileIndex | `integer` |
| forceSave | `integer` |

### Returns
- None

### C Prototype
`void save_file_do_save(s32 fileIndex, s8 forceSave);`


## save_file_erase

### Description
Erases all data in a specified save file, including backup slots. Marks the save file as modified and performs a save to apply the changes.
Useful for resetting a save file to its default state

### Lua Example
`save_file_erase(fileIndex)`

### Parameters
| Field | Type |
| ----- | ---- |
| fileIndex | `integer` |

### Returns
- None

### C Prototype
`void save_file_erase(s32 fileIndex);`


## save_file_erase_current_backup_save

### Description
Erases the backup data for the current save file without affecting the primary save data. Reloads the save file afterward

### Lua Example
`save_file_erase_current_backup_save()`

### Parameters
- None

### Returns
- None

### C Prototype
`void save_file_erase_current_backup_save(void);`


## save_file_reload

### Description
Reloads the save file data into memory, optionally resetting all save files. Marks the save file as modified.
Useful for reloading state after data corruption or during development debugging

### Lua Example
`save_file_reload(load_all)`

### Parameters
| Field | Type |
| ----- | ---- |
| load_all | `integer` |

### Returns
- None

### C Prototype
`void save_file_reload(u8 load_all);`


## save_file_get_max_coin_score

### Description
Determines the maximum coin score for a course across all save files. Returns the score along with the file index of the save containing it.
Useful for leaderboard-style comparisons and overall progress tracking

### Lua Example
`local integerValue = save_file_get_max_coin_score(courseIndex)`

### Parameters
| Field | Type |
| ----- | ---- |
| courseIndex | `integer` |

### Returns
- `integer`

### C Prototype
`u32 save_file_get_max_coin_score(s32 courseIndex);`


## save_file_get_course_star_count

### Description
Calculates the total number of stars collected in a specific course for a given save file.
Useful for determining completion status of individual levels

### Lua Example
`local integerValue = save_file_get_course_star_count(fileIndex, courseIndex)`

### Parameters
| Field | Type |
| ----- | ---- |
| fileIndex | `integer` |
| courseIndex | `integer` |

### Returns
- `integer`

### C Prototype
`s32 save_file_get_course_star_count(s32 fileIndex, s32 courseIndex);`


## save_file_get_total_star_count

### Description
Calculates the total number of stars collected across multiple courses within a specified range.
Useful for determining the overall progress toward game completion

### Lua Example
`local integerValue = save_file_get_total_star_count(fileIndex, minCourse, maxCourse)`

### Parameters
| Field | Type |
| ----- | ---- |
| fileIndex | `integer` |
| minCourse | `integer` |
| maxCourse | `integer` |

### Returns
- `integer`

### C Prototype
`s32 save_file_get_total_star_count(s32 fileIndex, s32 minCourse, s32 maxCourse);`


## save_file_set_flags

### Description
Adds new flags to the save file's flag bitmask.
Useful for updating progress or triggering new gameplay features

### Lua Example
`save_file_set_flags(flags)`

### Parameters
| Field | Type |
| ----- | ---- |
| flags | `integer` |

### Returns
- None

### C Prototype
`void save_file_set_flags(u32 flags);`


## save_file_clear_flags

### Description
Clears specific flags in the current save file. The flags are specified as a bitmask in the `flags` parameter. Ensures that the save file remains valid after clearing.
Useful for removing specific game states, such as collected items or completed objectives, without resetting the entire save

### Lua Example
`save_file_clear_flags(flags)`

### Parameters
| Field | Type |
| ----- | ---- |
| flags | `integer` |

### Returns
- None

### C Prototype
`void save_file_clear_flags(u32 flags);`


## save_file_get_flags

### Description
Retrieves the bitmask of flags representing the current state of the save file. Flags indicate collected items, completed objectives, and other game states.
Useful for checking specific game progress details

### Lua Example
`local integerValue = save_file_get_flags()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u32 save_file_get_flags(void);`


## save_file_get_star_flags

### Description
Retrieves the bitmask of stars collected in a specific course or castle secret stars (-1).
Useful for evaluating level progress and completion

### Lua Example
`local integerValue = save_file_get_star_flags(fileIndex, courseIndex)`

### Parameters
| Field | Type |
| ----- | ---- |
| fileIndex | `integer` |
| courseIndex | `integer` |

### Returns
- `integer`

### C Prototype
`u32 save_file_get_star_flags(s32 fileIndex, s32 courseIndex);`


## save_file_set_star_flags

### Description
Adds specific star flags to the save file, indicating collected stars for a course or castle secret stars. Updates the save file flags as necessary.
Useful for recording progress after star collection

### Lua Example
`save_file_set_star_flags(fileIndex, courseIndex, starFlags)`

### Parameters
| Field | Type |
| ----- | ---- |
| fileIndex | `integer` |
| courseIndex | `integer` |
| starFlags | `integer` |

### Returns
- None

### C Prototype
`void save_file_set_star_flags(s32 fileIndex, s32 courseIndex, u32 starFlags);`


## save_file_remove_star_flags

### Description
Removes specific star flags from the save file. This modifies the bitmask representing collected stars for a course or castle secret stars.
Useful for undoing progress or debugging collected stars

### Lua Example
`save_file_remove_star_flags(fileIndex, courseIndex, starFlagsToRemove)`

### Parameters
| Field | Type |
| ----- | ---- |
| fileIndex | `integer` |
| courseIndex | `integer` |
| starFlagsToRemove | `integer` |

### Returns
- None

### C Prototype
`void save_file_remove_star_flags(s32 fileIndex, s32 courseIndex, u32 starFlagsToRemove);`


## save_file_get_course_coin_score

### Description
Returns the highest coin score for a specified course in the save file. Performs checks to ensure the coin score is valid.
Useful for tracking player achievements and high scores

### Lua Example
`local integerValue = save_file_get_course_coin_score(fileIndex, courseIndex)`

### Parameters
| Field | Type |
| ----- | ---- |
| fileIndex | `integer` |
| courseIndex | `integer` |

### Returns
- `integer`

### C Prototype
`s32 save_file_get_course_coin_score(s32 fileIndex, s32 courseIndex);`


## save_file_set_course_coin_score

### Description
Updates the coin score for a specific course in the save file. The new score is provided in the `coinScore` parameter.
Useful for manually setting achievements such as high coin counts in individual levels

### Lua Example
`save_file_set_course_coin_score(fileIndex, courseIndex, coinScore)`

### Parameters
| Field | Type |
| ----- | ---- |
| fileIndex | `integer` |
| courseIndex | `integer` |
| coinScore | `integer` |

### Returns
- None

### C Prototype
`void save_file_set_course_coin_score(s32 fileIndex, s32 courseIndex, u8 coinScore);`


## save_file_is_cannon_unlocked

### Description
Checks whether the cannon in the specified course is unlocked. Returns true if the cannon is unlocked, otherwise false.
Useful for tracking course-specific progress and enabling shortcuts

### Lua Example
`local integerValue = save_file_is_cannon_unlocked(fileIndex, courseIndex)`

### Parameters
| Field | Type |
| ----- | ---- |
| fileIndex | `integer` |
| courseIndex | `integer` |

### Returns
- `integer`

### C Prototype
`s32 save_file_is_cannon_unlocked(s32 fileIndex, s32 courseIndex);`


## save_file_set_cannon_unlocked

### Description
Unlocks the cannon in the current course

### Lua Example
`save_file_set_cannon_unlocked()`

### Parameters
- None

### Returns
- None

### C Prototype
`void save_file_set_cannon_unlocked(void);`


## save_file_get_cap_pos

### Description
Retrieves the current position of Mario's cap, if it is on the ground in the current level and area. The position is stored in the provided `capPos` parameter.
Useful for tracking the cap's location after it has been dropped or lost

### Lua Example
`local integerValue = save_file_get_cap_pos(capPos)`

### Parameters
| Field | Type |
| ----- | ---- |
| capPos | [Vec3s](structs.md#Vec3s) |

### Returns
- `integer`

### C Prototype
`s32 save_file_get_cap_pos(VEC_OUT Vec3s capPos);`


## save_file_get_sound_mode

### Description
Returns the current sound mode (e.g., stereo, mono) stored in the save file.
Useful for checking the audio output preferences when loading a save

### Lua Example
`local integerValue = save_file_get_sound_mode()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u16 save_file_get_sound_mode(void);`


---
# functions from seqplayer.h

<br />


## sequence_player_get_tempo

### Description
Gets the `tempo` of `player`

### Lua Example
`local integerValue = sequence_player_get_tempo(player)`

### Parameters
| Field | Type |
| ----- | ---- |
| player | `integer` |

### Returns
- `integer`

### C Prototype
`u16 sequence_player_get_tempo(u8 player);`


## sequence_player_set_tempo

### Description
Sets the `tempo` of `player`. Resets when another sequence is played

### Lua Example
`sequence_player_set_tempo(player, tempo)`

### Parameters
| Field | Type |
| ----- | ---- |
| player | `integer` |
| tempo | `integer` |

### Returns
- None

### C Prototype
`void sequence_player_set_tempo(u8 player, u16 tempo);`


## sequence_player_get_tempo_acc

### Description
Gets the `tempoAcc` (tempo accumulation) of `player`

### Lua Example
`local integerValue = sequence_player_get_tempo_acc(player)`

### Parameters
| Field | Type |
| ----- | ---- |
| player | `integer` |

### Returns
- `integer`

### C Prototype
`u16 sequence_player_get_tempo_acc(u8 player);`


## sequence_player_set_tempo_acc

### Description
Sets the `tempoAcc` (tempo accumulation) of `player`. Resets when another sequence is played

### Lua Example
`sequence_player_set_tempo_acc(player, tempoAcc)`

### Parameters
| Field | Type |
| ----- | ---- |
| player | `integer` |
| tempoAcc | `integer` |

### Returns
- None

### C Prototype
`void sequence_player_set_tempo_acc(u8 player, u16 tempoAcc);`


## sequence_player_get_transposition

### Description
Gets the `transposition` (pitch) of `player`

### Lua Example
`local integerValue = sequence_player_get_transposition(player)`

### Parameters
| Field | Type |
| ----- | ---- |
| player | `integer` |

### Returns
- `integer`

### C Prototype
`u16 sequence_player_get_transposition(u8 player);`


## sequence_player_set_transposition

### Description
Sets the `transposition` (pitch) of `player`. Resets when another sequence is played

### Lua Example
`sequence_player_set_transposition(player, transposition)`

### Parameters
| Field | Type |
| ----- | ---- |
| player | `integer` |
| transposition | `integer` |

### Returns
- None

### C Prototype
`void sequence_player_set_transposition(u8 player, u16 transposition);`


## sequence_player_get_volume

### Description
Gets the volume of `player`

### Lua Example
`local numberValue = sequence_player_get_volume(player)`

### Parameters
| Field | Type |
| ----- | ---- |
| player | `integer` |

### Returns
- `number`

### C Prototype
`f32 sequence_player_get_volume(u8 player);`


## sequence_player_get_fade_volume

### Description
Gets the fade volume of `player`

### Lua Example
`local numberValue = sequence_player_get_fade_volume(player)`

### Parameters
| Field | Type |
| ----- | ---- |
| player | `integer` |

### Returns
- `number`

### C Prototype
`f32 sequence_player_get_fade_volume(u8 player);`


## sequence_player_set_fade_volume

### Description
Sets the fade volume of `player`

### Lua Example
`sequence_player_set_fade_volume(player, volume)`

### Parameters
| Field | Type |
| ----- | ---- |
| player | `integer` |
| volume | `number` |

### Returns
- None

### C Prototype
`void sequence_player_set_fade_volume(u8 player, f32 volume);`


## sequence_player_get_mute_volume_scale

### Description
Gets the mute volume scale of `player`

### Lua Example
`local numberValue = sequence_player_get_mute_volume_scale(player)`

### Parameters
| Field | Type |
| ----- | ---- |
| player | `integer` |

### Returns
- `number`

### C Prototype
`f32 sequence_player_get_mute_volume_scale(u8 player);`


---
# functions from smlua_anim_utils.h

<br />


## get_mario_vanilla_animation

### Description
Gets a vanilla mario Animation with `index`

### Lua Example
`local animationValue = get_mario_vanilla_animation(index)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |

### Returns
- [Animation](structs.md#Animation)

### C Prototype
`struct Animation *get_mario_vanilla_animation(u16 index);`


## smlua_anim_util_set_animation

### Description
Sets the animation of `obj` to the animation `name` corresponds to

### Lua Example
`smlua_anim_util_set_animation(obj, name)`

### Parameters
| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |
| name | `string` |

### Returns
- None

### C Prototype
`void smlua_anim_util_set_animation(struct Object *obj, const char *name);`


## smlua_anim_util_get_current_animation_name

### Description
Gets the name of the current animation playing on `obj`, returns `nil` if there's no name

### Lua Example
`local stringValue = smlua_anim_util_get_current_animation_name(obj)`

### Parameters
| Field | Type |
| ----- | ---- |
| obj | [Object](structs.md#Object) |

### Returns
- `string`

### C Prototype
`const char *smlua_anim_util_get_current_animation_name(struct Object *obj);`


---
# functions from smlua_audio_utils.h

<br />


## smlua_audio_utils_reset_all

### Description
Resets all custom sequences back to vanilla

### Lua Example
`smlua_audio_utils_reset_all()`

### Parameters
- None

### Returns
- None

### C Prototype
`void smlua_audio_utils_reset_all(void);`


## smlua_audio_utils_replace_sequence

### Description
Replaces the sequence corresponding to `sequenceId` with one called `m64Name`.m64 with `bankId` and `defaultVolume`

### Lua Example
`smlua_audio_utils_replace_sequence(sequenceId, bankId, defaultVolume, m64Name)`

### Parameters
| Field | Type |
| ----- | ---- |
| sequenceId | `integer` |
| bankId | `integer` |
| defaultVolume | `integer` |
| m64Name | `string` |

### Returns
- None

### C Prototype
`void smlua_audio_utils_replace_sequence(u8 sequenceId, u8 bankId, u8 defaultVolume, const char* m64Name);`


## smlua_audio_utils_allocate_sequence

### Description
Allocates a new sequence ID

### Lua Example
`local integerValue = smlua_audio_utils_allocate_sequence()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u8 smlua_audio_utils_allocate_sequence(void);`


## audio_load

### Description
Loads an `audio` by `filename` (with extension)

### Lua Example
`local modAudioValue = audio_load(filename, type)`

### Parameters
| Field | Type |
| ----- | ---- |
| filename | `string` |
| type | [enum ModAudioType](constants.md#enum-ModAudioType) |

### Returns
- [ModAudio](structs.md#ModAudio)

### C Prototype
`struct ModAudio* audio_load(const char* filename, OPTIONAL enum ModAudioType type);`


## audio_play

### Description
Plays an `audio` stream with `volume`. `restart` sets the elapsed time back to 0.

### Lua Example
`audio_play(audio, restart, volume)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |
| restart | `boolean` |
| volume | `number` |

### Returns
- None

### C Prototype
`void audio_stream_play(struct ModAudio* audio, bool restart, f32 volume);`


## audio_play

### Description
Plays an `audio` sample at `position` with `volume`

### Lua Example
`local modAudioValue = audio_play(audio, position, volume)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |
| position | [Vec3f](structs.md#Vec3f) |
| volume | `number` |

### Returns
- [ModAudio](structs.md#ModAudio)

### C Prototype
`struct ModAudio* audio_sample_play(struct ModAudio* audio, Vec3f position, f32 volume);`


## audio_play

### Description
Plays an `audio`

### Lua Example
`audio_play(audio)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |

### Returns
- None

### C Prototype
`void audio_play(struct ModAudio* audio);`


## audio_pause

### Description
Pauses an `audio`

### Lua Example
`audio_pause(audio)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |

### Returns
- None

### C Prototype
`void audio_pause(struct ModAudio* audio);`


## audio_stop

### Description
Stops an `audio`

### Lua Example
`audio_stop(audio)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |

### Returns
- None

### C Prototype
`void audio_stop(struct ModAudio* audio);`


## audio_destroy

### Description
Destroys an `audio`

### Lua Example
`audio_destroy(audio)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |

### Returns
- None

### C Prototype
`void audio_destroy(struct ModAudio* audio);`


## audio_reload

### Description
Reloads a destroyed `audio`

### Lua Example
`audio_reload(audio)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |

### Returns
- None

### C Prototype
`void audio_reload(struct ModAudio* audio);`


## audio_copy

### Description
Copies an `audio`

### Lua Example
`local modAudioValue = audio_copy(audio)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |

### Returns
- [ModAudio](structs.md#ModAudio)

### C Prototype
`struct ModAudio* audio_copy(struct ModAudio* audio);`


## audio_get_volume

### Description
Gets the volume of an `audio`

### Lua Example
`local numberValue = audio_get_volume(audio)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |

### Returns
- `number`

### C Prototype
`f32 audio_get_volume(struct ModAudio* audio);`


## audio_set_volume

### Description
Sets the volume of an `audio`

### Lua Example
`audio_set_volume(audio, volume)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |
| volume | `number` |

### Returns
- None

### C Prototype
`void audio_set_volume(struct ModAudio* audio, f32 volume);`


## audio_get_pan

### Description
Gets the pan of an `audio`

### Lua Example
`local numberValue = audio_get_pan(audio)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |

### Returns
- `number`

### C Prototype
`f32 audio_get_pan(struct ModAudio* audio);`


## audio_set_pan

### Description
Sets the pan of an `audio`

### Lua Example
`audio_set_pan(audio, pan)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |
| pan | `number` |

### Returns
- None

### C Prototype
`void audio_set_pan(struct ModAudio* audio, f32 pan);`


## audio_get_length

### Description
Gets the length of an `audio` in seconds

### Lua Example
`local length = audio_get_length(audio)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |

### Returns
- `number`

### C Prototype
`void audio_get_length(struct ModAudio* audio, RET f32 *length);`


## audio_get_position

### Description
Gets the position of an `audio` in seconds

### Lua Example
`local position = audio_get_position(audio)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |

### Returns
- `number`

### C Prototype
`void audio_get_position(struct ModAudio* audio, RET f32 *position);`


## audio_set_position

### Description
Sets the position of an `audio` in seconds

### Lua Example
`audio_set_position(audio, pos)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |
| pos | `number` |

### Returns
- None

### C Prototype
`void audio_set_position(struct ModAudio* audio, f32 pos);`


## audio_get_looping

### Description
Gets if an `audio` is looping or not

### Lua Example
`local booleanValue = audio_get_looping(audio)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |

### Returns
- `boolean`

### C Prototype
`bool audio_get_looping(struct ModAudio* audio);`


## audio_set_looping

### Description
Sets if an `audio` is looping or not

### Lua Example
`audio_set_looping(audio, looping)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |
| looping | `boolean` |

### Returns
- None

### C Prototype
`void audio_set_looping(struct ModAudio* audio, bool looping);`


## audio_get_playing

### Description
Gets if an `audio` is playing

### Lua Example
`local booleanValue = audio_get_playing(audio)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |

### Returns
- `boolean`

### C Prototype
`bool audio_get_playing(struct ModAudio* audio);`


## audio_set_playing

### Description
Sets if an `audio` is playing

### Lua Example
`audio_set_playing(audio, playing)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |
| playing | `boolean` |

### Returns
- None

### C Prototype
`void audio_set_playing(struct ModAudio* audio, bool playing);`


## audio_get_loop_points

### Description
Gets an `audio`'s loop points in samples

### Lua Example
`local loopStart, loopEnd = audio_get_loop_points(audio)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |

### Returns
- `integer`
- `integer`

### C Prototype
`void audio_get_loop_points(struct ModAudio* audio, RET u64 *loopStart, RET u64 *loopEnd);`


## audio_set_loop_points

### Description
Sets an `audio`'s loop points in samples

### Lua Example
`audio_set_loop_points(audio, loopStart, loopEnd)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |
| loopStart | `integer` |
| loopEnd | `integer` |

### Returns
- None

### C Prototype
`void audio_set_loop_points(struct ModAudio* audio, s64 loopStart, OPTIONAL s64 loopEnd);`


## audio_get_frequency

### Description
Gets the frequency of an `audio`

### Lua Example
`local numberValue = audio_get_frequency(audio)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |

### Returns
- `number`

### C Prototype
`f32 audio_get_frequency(struct ModAudio* audio);`


## audio_set_frequency

### Description
Sets the frequency of an `audio`

### Lua Example
`audio_set_frequency(audio, freq)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |
| freq | `number` |

### Returns
- None

### C Prototype
`void audio_set_frequency(struct ModAudio* audio, f32 freq);`


## audio_get_volume_channel

### Description
Gets the volume channel of an `audio`

### Lua Example
`local integerValue = audio_get_volume_channel(audio)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |

### Returns
- `integer`

### C Prototype
`u8 audio_get_volume_channel(struct ModAudio *audio);`


## audio_set_volume_channel

### Description
Sets the volume channel of an `audio`

### Lua Example
`audio_set_volume_channel(audio, channel)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |
| channel | `integer` |

### Returns
- None

### C Prototype
`void audio_set_volume_channel(struct ModAudio *audio, u8 channel);`


## audio_get_sample_rate

### Description
Gets the sample rate of an `audio`

### Lua Example
`local integerValue = audio_get_sample_rate(audio)`

### Parameters
| Field | Type |
| ----- | ---- |
| audio | [ModAudio](structs.md#ModAudio) |

### Returns
- `integer`

### C Prototype
`u32 audio_get_sample_rate(struct ModAudio* audio);`


---
# functions from smlua_camera_utils.h

<br />


## camera_reset_overrides

### Description
Resets camera config overrides

### Lua Example
`camera_reset_overrides()`

### Parameters
- None

### Returns
- None

### C Prototype
`void camera_reset_overrides(void);`


## camera_freeze

### Description
Freezes the camera by not updating it

### Lua Example
`camera_freeze()`

### Parameters
- None

### Returns
- None

### C Prototype
`void camera_freeze(void);`


## camera_unfreeze

### Description
Unfreezes the camera

### Lua Example
`camera_unfreeze()`

### Parameters
- None

### Returns
- None

### C Prototype
`void camera_unfreeze(void);`


## camera_is_frozen

### Description
Checks if the camera is frozen

### Lua Example
`local booleanValue = camera_is_frozen()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool camera_is_frozen(void);`


## camera_romhack_allow_only_mods

### Description
Sets if only mods are allowed to modify the camera (Enabling prevents the player from modifying the camera through the settings)

### Lua Example
`camera_romhack_allow_only_mods(allow)`

### Parameters
| Field | Type |
| ----- | ---- |
| allow | `integer` |

### Returns
- None

### C Prototype
`void camera_romhack_allow_only_mods(u8 allow);`


## camera_set_romhack_override

### Description
Sets the romhack camera override status

### Lua Example
`camera_set_romhack_override(rco)`

### Parameters
| Field | Type |
| ----- | ---- |
| rco | [enum RomhackCameraOverride](constants.md#enum-RomhackCameraOverride) |

### Returns
- None

### C Prototype
`void camera_set_romhack_override(enum RomhackCameraOverride rco);`


## camera_romhack_allow_switchable

### Description
Sets if the romhack camera should allow water/flying switching, triggered with the L button

### Lua Example
`camera_romhack_allow_switchable(allow)`

### Parameters
| Field | Type |
| ----- | ---- |
| allow | `integer` |

### Returns
- None

### C Prototype
`void camera_romhack_allow_switchable(u8 allow);`


## camera_allow_toxic_gas_camera

### Description
Sets if the romhack camera should fly above poison gas

### Lua Example
`camera_allow_toxic_gas_camera(allow)`

### Parameters
| Field | Type |
| ----- | ---- |
| allow | `integer` |

### Returns
- None

### C Prototype
`void camera_allow_toxic_gas_camera(u8 allow);`


## camera_romhack_allow_dpad_usage

### Description
Sets if the romhack camera should allow D-Pad movement

### Lua Example
`camera_romhack_allow_dpad_usage(allow)`

### Parameters
| Field | Type |
| ----- | ---- |
| allow | `integer` |

### Returns
- None

### C Prototype
`void camera_romhack_allow_dpad_usage(u8 allow);`


## camera_romhack_set_collisions

### Description
Toggles collision settings for the ROM hack camera.
This enables or disables specific collision behaviors in modded levels

### Lua Example
`camera_romhack_set_collisions(enable)`

### Parameters
| Field | Type |
| ----- | ---- |
| enable | `integer` |

### Returns
- None

### C Prototype
`void camera_romhack_set_collisions(u8 enable);`


## camera_romhack_set_zoomed_in_dist

### Description
Sets the romhack camera's zoomed in distance (Default: 900)

### Lua Example
`camera_romhack_set_zoomed_in_dist(val)`

### Parameters
| Field | Type |
| ----- | ---- |
| val | `integer` |

### Returns
- None

### C Prototype
`void camera_romhack_set_zoomed_in_dist(u32 val);`


## camera_romhack_set_zoomed_out_dist

### Description
Sets the romhack camera's zoomed out additional distance (Default: 500)

### Lua Example
`camera_romhack_set_zoomed_out_dist(val)`

### Parameters
| Field | Type |
| ----- | ---- |
| val | `integer` |

### Returns
- None

### C Prototype
`void camera_romhack_set_zoomed_out_dist(u32 val);`


## camera_romhack_set_zoomed_in_height

### Description
Sets the romhack camera's zoomed in height (Default: 300)

### Lua Example
`camera_romhack_set_zoomed_in_height(val)`

### Parameters
| Field | Type |
| ----- | ---- |
| val | `integer` |

### Returns
- None

### C Prototype
`void camera_romhack_set_zoomed_in_height(u32 val);`


## camera_romhack_set_zoomed_out_height

### Description
Sets the romhack camera's zoomed out additional height (Default: 150)

### Lua Example
`camera_romhack_set_zoomed_out_height(val)`

### Parameters
| Field | Type |
| ----- | ---- |
| val | `integer` |

### Returns
- None

### C Prototype
`void camera_romhack_set_zoomed_out_height(u32 val);`


## camera_romhack_get_zoomed_in_dist

### Description
Gets the romhack camera's zoomed in distance

### Lua Example
`local integerValue = camera_romhack_get_zoomed_in_dist()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u32 camera_romhack_get_zoomed_in_dist(void);`


## camera_romhack_get_zoomed_out_dist

### Description
Gets the romhack camera's additional zoomed out distance

### Lua Example
`local integerValue = camera_romhack_get_zoomed_out_dist()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u32 camera_romhack_get_zoomed_out_dist(void);`


## camera_romhack_get_zoomed_in_height

### Description
Gets the romhack camera's zoomed in height

### Lua Example
`local integerValue = camera_romhack_get_zoomed_in_height()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u32 camera_romhack_get_zoomed_in_height(void);`


## camera_romhack_get_zoomed_out_height

### Description
Gets the romhack camera's additional zoomed out height

### Lua Example
`local integerValue = camera_romhack_get_zoomed_out_height()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u32 camera_romhack_get_zoomed_out_height(void);`


## camera_get_romhack_override

### Description
Gets the current romhack camera override status

### Lua Example
`local enumValue = camera_get_romhack_override()`

### Parameters
- None

### Returns
- [enum RomhackCameraOverride](constants.md#enum-RomhackCameraOverride)

### C Prototype
`enum RomhackCameraOverride camera_get_romhack_override(void);`


## camera_romhack_get_allow_switchable

### Description
Gets if the romhack camera should allow water/flying switching

### Lua Example
`local integerValue = camera_romhack_get_allow_switchable()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u8 camera_romhack_get_allow_switchable(void);`


## camera_get_allow_toxic_gas_camera

### Description
Gets if the romhack camera should fly above poison gas

### Lua Example
`local integerValue = camera_get_allow_toxic_gas_camera()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u8 camera_get_allow_toxic_gas_camera(void);`


## camera_romhack_get_allow_dpad_usage

### Description
Gets if the romhack camera should allow D-Pad movement

### Lua Example
`local integerValue = camera_romhack_get_allow_dpad_usage()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u8 camera_romhack_get_allow_dpad_usage(void);`


## camera_romhack_get_collisions

### Description
Gets if the romhack camera has surface collisions

### Lua Example
`local integerValue = camera_romhack_get_collisions()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u8 camera_romhack_get_collisions(void);`


## camera_config_is_free_cam_enabled

### Description
Checks if Free Camera is enabled

### Lua Example
`local booleanValue = camera_config_is_free_cam_enabled()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool camera_config_is_free_cam_enabled(void);`


## camera_config_is_analog_cam_enabled

### Description
Checks if Analog Camera is enabled

### Lua Example
`local booleanValue = camera_config_is_analog_cam_enabled()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool camera_config_is_analog_cam_enabled(void);`


## camera_config_is_dpad_enabled

### Description
Checks if Freecam DPad Behavior is enabled

### Lua Example
`local booleanValue = camera_config_is_dpad_enabled()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool camera_config_is_dpad_enabled(void);`


## camera_config_is_collision_enabled

### Description
Checks if Camera Collision is enabled

### Lua Example
`local booleanValue = camera_config_is_collision_enabled()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool camera_config_is_collision_enabled(void);`


## camera_config_is_mouse_look_enabled

### Description
Checks if Mouse Look is enabled

### Lua Example
`local booleanValue = camera_config_is_mouse_look_enabled()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool camera_config_is_mouse_look_enabled(void);`


## camera_config_is_x_inverted

### Description
Checks if camera X is inverted

### Lua Example
`local booleanValue = camera_config_is_x_inverted()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool camera_config_is_x_inverted(void);`


## camera_config_is_y_inverted

### Description
Checks if camera Y is inverted

### Lua Example
`local booleanValue = camera_config_is_y_inverted()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool camera_config_is_y_inverted(void);`


## camera_config_get_x_sensitivity

### Description
Gets camera X sensitivity

### Lua Example
`local integerValue = camera_config_get_x_sensitivity()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u32 camera_config_get_x_sensitivity(void);`


## camera_config_get_y_sensitivity

### Description
Gets camera Y sensitivity

### Lua Example
`local integerValue = camera_config_get_y_sensitivity()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u32 camera_config_get_y_sensitivity(void);`


## camera_config_get_aggression

### Description
Gets camera aggression

### Lua Example
`local integerValue = camera_config_get_aggression()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u32 camera_config_get_aggression(void);`


## camera_config_get_pan_level

### Description
Gets camera pan level

### Lua Example
`local integerValue = camera_config_get_pan_level()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u32 camera_config_get_pan_level(void);`


## camera_config_get_deceleration

### Description
Gets camera deceleration

### Lua Example
`local integerValue = camera_config_get_deceleration()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u32 camera_config_get_deceleration(void);`


## camera_config_get_centering

### Description
Gets if the L button will center the camera

### Lua Example
`local booleanValue = camera_config_get_centering()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool camera_config_get_centering(void);`


## camera_config_enable_free_cam

### Description
Overrides if Free Camera is enabled

### Lua Example
`camera_config_enable_free_cam(enable)`

### Parameters
| Field | Type |
| ----- | ---- |
| enable | `boolean` |

### Returns
- None

### C Prototype
`void camera_config_enable_free_cam(bool enable);`


## camera_config_enable_analog_cam

### Description
Overrides if Analog Camera is enabled

### Lua Example
`camera_config_enable_analog_cam(enable)`

### Parameters
| Field | Type |
| ----- | ---- |
| enable | `boolean` |

### Returns
- None

### C Prototype
`void camera_config_enable_analog_cam(bool enable);`


## camera_config_enable_centering

### Description
Overrides if the L button will center the camera

### Lua Example
`camera_config_enable_centering(enable)`

### Parameters
| Field | Type |
| ----- | ---- |
| enable | `boolean` |

### Returns
- None

### C Prototype
`void camera_config_enable_centering(bool enable);`


## camera_config_enable_dpad

### Description
Overrides if Freecam DPad Behavior is enabled

### Lua Example
`camera_config_enable_dpad(enable)`

### Parameters
| Field | Type |
| ----- | ---- |
| enable | `boolean` |

### Returns
- None

### C Prototype
`void camera_config_enable_dpad(bool enable);`


## camera_config_enable_collisions

### Description
Overrides if Camera Collision is enabled

### Lua Example
`camera_config_enable_collisions(enable)`

### Parameters
| Field | Type |
| ----- | ---- |
| enable | `boolean` |

### Returns
- None

### C Prototype
`void camera_config_enable_collisions(bool enable);`


## camera_config_enable_mouse_look

### Description
Overrides if camera mouse look is enabled

### Lua Example
`camera_config_enable_mouse_look(enable)`

### Parameters
| Field | Type |
| ----- | ---- |
| enable | `boolean` |

### Returns
- None

### C Prototype
`void camera_config_enable_mouse_look(bool enable);`


## camera_config_invert_x

### Description
Overrides if camera X is inverted

### Lua Example
`camera_config_invert_x(invert)`

### Parameters
| Field | Type |
| ----- | ---- |
| invert | `boolean` |

### Returns
- None

### C Prototype
`void camera_config_invert_x(bool invert);`


## camera_config_invert_y

### Description
Overrides if camera Y is inverted

### Lua Example
`camera_config_invert_y(invert)`

### Parameters
| Field | Type |
| ----- | ---- |
| invert | `boolean` |

### Returns
- None

### C Prototype
`void camera_config_invert_y(bool invert);`


## camera_config_set_x_sensitivity

### Description
Overrides camera X sensitivity

### Lua Example
`camera_config_set_x_sensitivity(value)`

### Parameters
| Field | Type |
| ----- | ---- |
| value | `integer` |

### Returns
- None

### C Prototype
`void camera_config_set_x_sensitivity(u32 value);`


## camera_config_set_y_sensitivity

### Description
Overrides camera Y sensitivity

### Lua Example
`camera_config_set_y_sensitivity(value)`

### Parameters
| Field | Type |
| ----- | ---- |
| value | `integer` |

### Returns
- None

### C Prototype
`void camera_config_set_y_sensitivity(u32 value);`


## camera_config_set_aggression

### Description
Overrides camera aggression

### Lua Example
`camera_config_set_aggression(value)`

### Parameters
| Field | Type |
| ----- | ---- |
| value | `integer` |

### Returns
- None

### C Prototype
`void camera_config_set_aggression(u32 value);`


## camera_config_set_pan_level

### Description
Overrides camera pan level

### Lua Example
`camera_config_set_pan_level(value)`

### Parameters
| Field | Type |
| ----- | ---- |
| value | `integer` |

### Returns
- None

### C Prototype
`void camera_config_set_pan_level(u32 value);`


## camera_config_set_deceleration

### Description
Overrides camera deceleration

### Lua Example
`camera_config_set_deceleration(value)`

### Parameters
| Field | Type |
| ----- | ---- |
| value | `integer` |

### Returns
- None

### C Prototype
`void camera_config_set_deceleration(u32 value);`


## camera_get_checking_surfaces

### Description
Checks if the camera should account for surfaces

### Lua Example
`local booleanValue = camera_get_checking_surfaces()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool camera_get_checking_surfaces(void);`


## camera_set_checking_surfaces

### Description
Sets if the camera should account for surfaces

### Lua Example
`camera_set_checking_surfaces(value)`

### Parameters
| Field | Type |
| ----- | ---- |
| value | `boolean` |

### Returns
- None

### C Prototype
`void camera_set_checking_surfaces(bool value);`


## center_free_camera

### Description
Centers the free camera.
This function is designed for rotating the camera to face Mario's facing angle when Free Camera is enabled

### Lua Example
`center_free_camera()`

### Parameters
- None

### Returns
- None

### C Prototype
`void center_free_camera(void);`


---
# functions from smlua_collision_utils.h

<br />


## collision_find_floor

### Description
Finds a potential floor at the given `x`, `y`, and `z` values

### Lua Example
`local surfaceValue = collision_find_floor(x, y, z)`

### Parameters
| Field | Type |
| ----- | ---- |
| x | `number` |
| y | `number` |
| z | `number` |

### Returns
- [Surface](structs.md#Surface)

### C Prototype
`struct Surface* collision_find_floor(f32 x, f32 y, f32 z);`


## collision_find_ceil

### Description
Finds a potential ceiling at the given `x`, `y`, and `z` values

### Lua Example
`local surfaceValue = collision_find_ceil(x, y, z)`

### Parameters
| Field | Type |
| ----- | ---- |
| x | `number` |
| y | `number` |
| z | `number` |

### Returns
- [Surface](structs.md#Surface)

### C Prototype
`struct Surface* collision_find_ceil(f32 x, f32 y, f32 z);`


## get_water_surface_pseudo_floor

### Description
Gets the generated water floor surface used when riding a shell

### Lua Example
`local surfaceValue = get_water_surface_pseudo_floor()`

### Parameters
- None

### Returns
- [Surface](structs.md#Surface)

### C Prototype
`struct Surface* get_water_surface_pseudo_floor(void);`


## smlua_collision_util_get

### Description
Gets the `Collision` with `name`

### Lua Example
`local pointerValue = smlua_collision_util_get(name)`

### Parameters
| Field | Type |
| ----- | ---- |
| name | `string` |

### Returns
- `Pointer` <`Collision`>

### C Prototype
`Collision* smlua_collision_util_get(const char* name);`


## collision_get_temp_wall_collision_data

### Description
Returns a temporary wall collision data pointer

### Lua Example
`local wallCollisionDataValue = collision_get_temp_wall_collision_data()`

### Parameters
- None

### Returns
- [WallCollisionData](structs.md#WallCollisionData)

### C Prototype
`struct WallCollisionData* collision_get_temp_wall_collision_data(void);`


## get_surface_from_wcd_index

### Description
Gets the surface corresponding to `index` from `wcd`

### Lua Example
`local surfaceValue = get_surface_from_wcd_index(wcd, index)`

### Parameters
| Field | Type |
| ----- | ---- |
| wcd | [WallCollisionData](structs.md#WallCollisionData) |
| index | `integer` |

### Returns
- [Surface](structs.md#Surface)

### C Prototype
`struct Surface* get_surface_from_wcd_index(struct WallCollisionData* wcd, s8 index);`


## smlua_collision_util_get_current_terrain_collision

### Description
Gets the current level terrain collision

### Lua Example
`local pointerValue = smlua_collision_util_get_current_terrain_collision()`

### Parameters
- None

### Returns
- `Pointer` <`Collision`>

### C Prototype
`Collision* smlua_collision_util_get_current_terrain_collision(void);`


## smlua_collision_util_get_level_collision

### Description
Gets the `level` terrain collision from `area`

### Lua Example
`local pointerValue = smlua_collision_util_get_level_collision(level, area)`

### Parameters
| Field | Type |
| ----- | ---- |
| level | `integer` |
| area | `integer` |

### Returns
- `Pointer` <`Collision`>

### C Prototype
`Collision *smlua_collision_util_get_level_collision(u32 level, u16 area);`


## smlua_collision_util_find_surface_types

### Description
Gets a table of the surface types from `data`

### Lua Example
`smlua_collision_util_find_surface_types(data)`

### Parameters
| Field | Type |
| ----- | ---- |
| data | `Pointer` <`Collision`> |

### Returns
- None

### C Prototype
`void smlua_collision_util_find_surface_types(Collision* data);`


## smlua_collision_add_surface

### Description
Allocates a new collision surface with the given vertices, computes the surface normal and other fields, and inserts it into the spatial partition.
Returns the new surface, or `nil` if the triangle is degenerate (zero area).
Set `dynamic` to `true` for surfaces that are cleared each frame, or `false` for persistent static surfaces

### Lua Example
`local surfaceValue = smlua_collision_add_surface(dynamic, surfaceType, vertex1, vertex2, vertex3)`

### Parameters
| Field | Type |
| ----- | ---- |
| dynamic | `boolean` |
| surfaceType | `integer` |
| vertex1 | [Vec3s](structs.md#Vec3s) |
| vertex2 | [Vec3s](structs.md#Vec3s) |
| vertex3 | [Vec3s](structs.md#Vec3s) |

### Returns
- [Surface](structs.md#Surface)

### C Prototype
`struct Surface* smlua_collision_add_surface(bool dynamic, s16 surfaceType, Vec3s vertex1, Vec3s vertex2, Vec3s vertex3);`


## smlua_collision_move_surface

### Description
Moves an existing collision surface to new vertex positions.
Recalculates the surface normal, origin offset, and Y bounds, removes the surface from its old spatial partition cells, and re-adds it to the correct cells.
The previous vertices are preserved for interpolation

### Lua Example
`smlua_collision_move_surface(surface, vertex1, vertex2, vertex3)`

### Parameters
| Field | Type |
| ----- | ---- |
| surface | [Surface](structs.md#Surface) |
| vertex1 | [Vec3s](structs.md#Vec3s) |
| vertex2 | [Vec3s](structs.md#Vec3s) |
| vertex3 | [Vec3s](structs.md#Vec3s) |

### Returns
- None

### C Prototype
`void smlua_collision_move_surface(struct Surface *surface, Vec3s vertex1, Vec3s vertex2, Vec3s vertex3);`


## smlua_collision_delete_surface

### Description
Fully deletes a collision surface: removes it from the spatial partitions and frees its pool slot.

### Lua Example
`smlua_collision_delete_surface(surface)`

### Parameters
| Field | Type |
| ----- | ---- |
| surface | [Surface](structs.md#Surface) |

### Returns
- None

### C Prototype
`void smlua_collision_delete_surface(struct Surface *surface);`


## surface_is_quicksand

### Description
Checks if the surface is quicksand

### Lua Example
`local booleanValue = surface_is_quicksand(surf)`

### Parameters
| Field | Type |
| ----- | ---- |
| surf | [Surface](structs.md#Surface) |

### Returns
- `boolean`

### C Prototype
`bool surface_is_quicksand(struct Surface* surf);`


## surface_is_not_hard

### Description
Checks if the surface is not a hard surface

### Lua Example
`local booleanValue = surface_is_not_hard(surf)`

### Parameters
| Field | Type |
| ----- | ---- |
| surf | [Surface](structs.md#Surface) |

### Returns
- `boolean`

### C Prototype
`bool surface_is_not_hard(struct Surface* surf);`


## surface_is_painting_warp

### Description
Checks if the surface is a painting warp

### Lua Example
`local booleanValue = surface_is_painting_warp(surf)`

### Parameters
| Field | Type |
| ----- | ---- |
| surf | [Surface](structs.md#Surface) |

### Returns
- `boolean`

### C Prototype
`bool surface_is_painting_warp(struct Surface* surf);`


---
# functions from smlua_gfx_utils.h

<br />


## get_shader_flag_enabled

### Description
Gets if a custom shader flag (`SHADER_FLAG_*`) is enabled or not

### Lua Example
`local booleanValue = get_shader_flag_enabled(flag)`

### Parameters
| Field | Type |
| ----- | ---- |
| flag | [enum ShaderFlag](constants.md#enum-ShaderFlag) |

### Returns
- `boolean`

### C Prototype
`bool get_shader_flag_enabled(enum ShaderFlag flag);`


## set_shader_flag_enabled

### Description
Enables a custom shader flag (`SHADER_FLAG_*`) for the renderer

### Lua Example
`set_shader_flag_enabled(flag, enabled)`

### Parameters
| Field | Type |
| ----- | ---- |
| flag | [enum ShaderFlag](constants.md#enum-ShaderFlag) |
| enabled | `boolean` |

### Returns
- None

### C Prototype
`void set_shader_flag_enabled(enum ShaderFlag flag, bool enabled);`


## get_shader_flag_value

### Description
Gets a value for one of the custom shader flags (`SHADER_FLAG_*`)

### Lua Example
`local numberValue = get_shader_flag_value(flag)`

### Parameters
| Field | Type |
| ----- | ---- |
| flag | [enum ShaderFlag](constants.md#enum-ShaderFlag) |

### Returns
- `number`

### C Prototype
`f32 get_shader_flag_value(enum ShaderFlag flag);`


## set_shader_flag_value

### Description
Sets a value for one of the custom shader flags (`SHADER_FLAG_*`) for the renderer

### Lua Example
`set_shader_flag_value(flag, value)`

### Parameters
| Field | Type |
| ----- | ---- |
| flag | [enum ShaderFlag](constants.md#enum-ShaderFlag) |
| value | `number` |

### Returns
- None

### C Prototype
`void set_shader_flag_value(enum ShaderFlag flag, f32 value);`


## get_global_shader_flags_enabled

### Description
Gets if custom shader flags are enabled globally

### Lua Example
`local booleanValue = get_global_shader_flags_enabled()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool get_global_shader_flags_enabled(void);`


## set_global_shader_flags_enabled

### Description
Enables custom shader flags as a global toggle, useful for disabling without manually going through every effect

### Lua Example
`set_global_shader_flags_enabled(enabled)`

### Parameters
| Field | Type |
| ----- | ---- |
| enabled | `boolean` |

### Returns
- None

### C Prototype
`void set_global_shader_flags_enabled(bool enabled);`


## clear_all_shader_flags

### Description
Clears all custom shader flags (`SHADER_FLAG_*`) for the renderer

### Lua Example
`clear_all_shader_flags()`

### Parameters
- None

### Returns
- None

### C Prototype
`void clear_all_shader_flags(void);`


## get_shading_fullbright_enabled

### Description
Gets if fullbright mode is enabled for shaded materials (`G_LIGHTING`)

### Lua Example
`local booleanValue = get_shading_fullbright_enabled()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool get_shading_fullbright_enabled(void);`


## set_shading_fullbright_enabled

### Description
Enables fullbright mode for shaded materials (`G_LIGHTING`.)
If a light color is completely black, the rendered color will default to the shade color.
This is for already fullbright materials that set their shade color to something and their light color to black.
This visually corrects rendering on materials such as Mario's emblem.
Useful for using the lighting engine and having entirely your own shading without the game's own systems
and compatibility with most models, not having to used specialized env/prim color approaches for example

### Lua Example
`set_shading_fullbright_enabled(enabled)`

### Parameters
| Field | Type |
| ----- | ---- |
| enabled | `boolean` |

### Returns
- None

### C Prototype
`void set_shading_fullbright_enabled(bool enabled);`


## set_override_fov

### Description
Sets the override FOV

### Lua Example
`set_override_fov(fov)`

### Parameters
| Field | Type |
| ----- | ---- |
| fov | `number` |

### Returns
- None

### C Prototype
`void set_override_fov(f32 fov);`


## set_override_near

### Description
Sets the override near plane

### Lua Example
`set_override_near(near)`

### Parameters
| Field | Type |
| ----- | ---- |
| near | `number` |

### Returns
- None

### C Prototype
`void set_override_near(f32 near);`


## set_override_far

### Description
Sets the override far plane

### Lua Example
`set_override_far(far)`

### Parameters
| Field | Type |
| ----- | ---- |
| far | `number` |

### Returns
- None

### C Prototype
`void set_override_far(f32 far);`


## get_lighting_dir

### Description
Gets a value of the global lighting direction

### Lua Example
`local numberValue = get_lighting_dir(index)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |

### Returns
- `number`

### C Prototype
`f32 get_lighting_dir(u8 index);`


## set_lighting_dir

### Description
Sets a value of the global lighting direction

### Lua Example
`set_lighting_dir(index, value)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |
| value | `number` |

### Returns
- None

### C Prototype
`void set_lighting_dir(u8 index, f32 value);`


## get_lighting_color

### Description
Gets a value of the global lighting color

### Lua Example
`local integerValue = get_lighting_color(index)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |

### Returns
- `integer`

### C Prototype
`u8 get_lighting_color(u8 index);`


## get_lighting_color_ambient

### Description
Gets a value of the global ambient lighting color

### Lua Example
`local integerValue = get_lighting_color_ambient(index)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |

### Returns
- `integer`

### C Prototype
`u8 get_lighting_color_ambient(u8 index);`


## set_lighting_color

### Description
Sets a value of the global lighting color

### Lua Example
`set_lighting_color(index, value)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |
| value | `integer` |

### Returns
- None

### C Prototype
`void set_lighting_color(u8 index, u8 value);`


## set_lighting_color_ambient

### Description
Sets a value of the global lighting color (run this after `set_lighting_color` for the ambient color to not be overriden)

### Lua Example
`set_lighting_color_ambient(index, value)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |
| value | `integer` |

### Returns
- None

### C Prototype
`void set_lighting_color_ambient(u8 index, u8 value);`


## get_vertex_color

### Description
Gets a value of the global vertex shading color

### Lua Example
`local integerValue = get_vertex_color(index)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |

### Returns
- `integer`

### C Prototype
`u8 get_vertex_color(u8 index);`


## set_vertex_color

### Description
Sets a value of the global vertex shading color

### Lua Example
`set_vertex_color(index, value)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |
| value | `integer` |

### Returns
- None

### C Prototype
`void set_vertex_color(u8 index, u8 value);`


## get_fog_color

### Description
Gets a value of the global fog color

### Lua Example
`local integerValue = get_fog_color(index)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |

### Returns
- `integer`

### C Prototype
`u8 get_fog_color(u8 index);`


## set_fog_color

### Description
Sets a value of the global fog color

### Lua Example
`set_fog_color(index, value)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |
| value | `integer` |

### Returns
- None

### C Prototype
`void set_fog_color(u8 index, u8 value);`


## get_fog_intensity

### Description
Gets the intensity of the fog

### Lua Example
`local numberValue = get_fog_intensity()`

### Parameters
- None

### Returns
- `number`

### C Prototype
`f32 get_fog_intensity(void);`


## set_fog_intensity

### Description
Sets the intensity of the fog (this value scales very quickly, 1.0 to 1.1 is a desirable range)

### Lua Example
`set_fog_intensity(intensity)`

### Parameters
| Field | Type |
| ----- | ---- |
| intensity | `number` |

### Returns
- None

### C Prototype
`void set_fog_intensity(f32 intensity);`


## get_skybox

### Description
Gets the current skybox

### Lua Example
`local integerValue = get_skybox()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`s8 get_skybox(void);`


## set_override_skybox

### Description
Sets the override skybox

### Lua Example
`set_override_skybox(background)`

### Parameters
| Field | Type |
| ----- | ---- |
| background | `integer` |

### Returns
- None

### C Prototype
`void set_override_skybox(s8 background);`


## get_skybox_color

### Description
Gets a value of the global skybox color

### Lua Example
`local integerValue = get_skybox_color(index)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |

### Returns
- `integer`

### C Prototype
`u8 get_skybox_color(u8 index);`


## set_skybox_color

### Description
Sets a value of the global skybox color

### Lua Example
`set_skybox_color(index, value)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |
| value | `integer` |

### Returns
- None

### C Prototype
`void set_skybox_color(u8 index, u8 value);`


## gfx_parse

### Description
Traverses a display list. Takes a Lua function as a parameter, which is called back for each command in the display list with the parameters `cmd` (display list pointer), and `op`

### Lua Example
`gfx_parse(cmd, func)`

### Parameters
| Field | Type |
| ----- | ---- |
| cmd | `Pointer` <`Gfx`> |
| func | `Lua Function` () |

### Returns
- None

### C Prototype
`void gfx_parse(Gfx *cmd, LuaFunction func);`


## gfx_get_op

### Description
Gets the op of the display list command

### Lua Example
`local integerValue = gfx_get_op(cmd)`

### Parameters
| Field | Type |
| ----- | ---- |
| cmd | `Pointer` <`Gfx`> |

### Returns
- `integer`

### C Prototype
`u32 gfx_get_op(Gfx *cmd);`


## gfx_get_display_list

### Description
Gets the display list from a display list command if it has the op `G_DL`

### Lua Example
`local pointerValue = gfx_get_display_list(cmd)`

### Parameters
| Field | Type |
| ----- | ---- |
| cmd | `Pointer` <`Gfx`> |

### Returns
- `Pointer` <`Gfx`>

### C Prototype
`Gfx *gfx_get_display_list(Gfx *cmd);`


## gfx_get_vertex_buffer

### Description
Gets the vertex buffer from a display list command if it has the op `G_VTX`

### Lua Example
`local pointerValue = gfx_get_vertex_buffer(cmd)`

### Parameters
| Field | Type |
| ----- | ---- |
| cmd | `Pointer` <`Gfx`> |

### Returns
- `Pointer` <`Vtx`>

### C Prototype
`Vtx *gfx_get_vertex_buffer(Gfx *cmd);`


## gfx_get_vertex_count

### Description
Gets the number of vertices from a display list command if it has the op `G_VTX`

### Lua Example
`local integerValue = gfx_get_vertex_count(cmd)`

### Parameters
| Field | Type |
| ----- | ---- |
| cmd | `Pointer` <`Gfx`> |

### Returns
- `integer`

### C Prototype
`u16 gfx_get_vertex_count(Gfx *cmd);`


## gfx_get_texture

### Description
Gets the texture from a display list command if it has an image related op

### Lua Example
`local pointerValue = gfx_get_texture(cmd)`

### Parameters
| Field | Type |
| ----- | ---- |
| cmd | `Pointer` <`Gfx`> |

### Returns
- `Pointer` <`Texture`>

### C Prototype
`Texture *gfx_get_texture(Gfx *cmd);`


## gfx_get_from_name

### Description
Gets a display list of the current mod from its name.
Returns a pointer to the display list and its length

### Lua Example
`local pointerValue, length = gfx_get_from_name(name)`

### Parameters
| Field | Type |
| ----- | ---- |
| name | `string` |

### Returns
- `Pointer` <`Gfx`>
- `integer`

### C Prototype
`Gfx *gfx_get_from_name(const char *name, RET u32 *length);`


## gfx_get_name

### Description
Gets the name of a display list

### Lua Example
`local stringValue = gfx_get_name(gfx)`

### Parameters
| Field | Type |
| ----- | ---- |
| gfx | `Pointer` <`Gfx`> |

### Returns
- `string`

### C Prototype
`const char *gfx_get_name(Gfx *gfx);`


## gfx_get_length

### Description
Gets the max length of a display list

### Lua Example
`local integerValue = gfx_get_length(gfx)`

### Parameters
| Field | Type |
| ----- | ---- |
| gfx | `Pointer` <`Gfx`> |

### Returns
- `integer`

### C Prototype
`u32 gfx_get_length(Gfx *gfx);`


## gfx_get_command

### Description
Gets a command of a display list at position `offset`

### Lua Example
`local pointerValue = gfx_get_command(gfx, offset)`

### Parameters
| Field | Type |
| ----- | ---- |
| gfx | `Pointer` <`Gfx`> |
| offset | `integer` |

### Returns
- `Pointer` <`Gfx`>

### C Prototype
`Gfx *gfx_get_command(Gfx *gfx, u32 offset);`


## gfx_get_next_command

### Description
Gets the next command of a given display list pointer. Intended to use in a for loop

### Lua Example
`local pointerValue = gfx_get_next_command(gfx)`

### Parameters
| Field | Type |
| ----- | ---- |
| gfx | `Pointer` <`Gfx`> |

### Returns
- `Pointer` <`Gfx`>

### C Prototype
`Gfx *gfx_get_next_command(Gfx *gfx);`


## gfx_copy

### Description
Copies `length` commands from display list `src` to display list `dest`

### Lua Example
`gfx_copy(dest, src, length)`

### Parameters
| Field | Type |
| ----- | ---- |
| dest | `Pointer` <`Gfx`> |
| src | `Pointer` <`Gfx`> |
| length | `integer` |

### Returns
- None

### C Prototype
`void gfx_copy(Gfx *dest, Gfx *src, u32 length);`


## gfx_create

### Description
Creates a new named display list of `length` commands

### Lua Example
`local pointerValue = gfx_create(name, length)`

### Parameters
| Field | Type |
| ----- | ---- |
| name | `string` |
| length | `integer` |

### Returns
- `Pointer` <`Gfx`>

### C Prototype
`Gfx *gfx_create(const char *name, u32 length);`


## gfx_resize

### Description
Resizes a display list created by `gfx_create`

### Lua Example
`gfx_resize(gfx, newLength)`

### Parameters
| Field | Type |
| ----- | ---- |
| gfx | `Pointer` <`Gfx`> |
| newLength | `integer` |

### Returns
- None

### C Prototype
`void gfx_resize(Gfx *gfx, u32 newLength);`


## gfx_delete

### Description
Deletes a display list created by `gfx_create`

### Lua Example
`gfx_delete(gfx)`

### Parameters
| Field | Type |
| ----- | ---- |
| gfx | `Pointer` <`Gfx`> |

### Returns
- None

### C Prototype
`void gfx_delete(Gfx *gfx);`


## gfx_delete_all

### Description
Deletes all display lists created by `gfx_create`

### Lua Example
`gfx_delete_all()`

### Parameters
- None

### Returns
- None

### C Prototype
`void gfx_delete_all();`


## vtx_get_from_name

### Description
Gets a vertex buffer of the current mod from its name.
Returns a pointer to the vertex buffer and its vertex count

### Lua Example
`local pointerValue, count = vtx_get_from_name(name)`

### Parameters
| Field | Type |
| ----- | ---- |
| name | `string` |

### Returns
- `Pointer` <`Vtx`>
- `integer`

### C Prototype
`Vtx *vtx_get_from_name(const char *name, RET u32 *count);`


## vtx_get_name

### Description
Gets the name of a vertex buffer

### Lua Example
`local stringValue = vtx_get_name(vtx)`

### Parameters
| Field | Type |
| ----- | ---- |
| vtx | `Pointer` <`Vtx`> |

### Returns
- `string`

### C Prototype
`const char *vtx_get_name(Vtx *vtx);`


## vtx_get_count

### Description
Gets the max count of vertices of a vertex buffer

### Lua Example
`local integerValue = vtx_get_count(vtx)`

### Parameters
| Field | Type |
| ----- | ---- |
| vtx | `Pointer` <`Vtx`> |

### Returns
- `integer`

### C Prototype
`u32 vtx_get_count(Vtx *vtx);`


## vtx_get_vertex

### Description
Gets a vertex of a vertex buffer at position `offset`

### Lua Example
`local pointerValue = vtx_get_vertex(vtx, offset)`

### Parameters
| Field | Type |
| ----- | ---- |
| vtx | `Pointer` <`Vtx`> |
| offset | `integer` |

### Returns
- `Pointer` <`Vtx`>

### C Prototype
`Vtx *vtx_get_vertex(Vtx *vtx, u32 offset);`


## vtx_get_next_vertex

### Description
Gets the next vertex of a given vertex pointer. Intended to use in a for loop

### Lua Example
`local pointerValue = vtx_get_next_vertex(vtx)`

### Parameters
| Field | Type |
| ----- | ---- |
| vtx | `Pointer` <`Vtx`> |

### Returns
- `Pointer` <`Vtx`>

### C Prototype
`Vtx *vtx_get_next_vertex(Vtx *vtx);`


## vtx_copy

### Description
Copies `count` vertices from vertex buffer `src` to vertex buffer `dest`

### Lua Example
`vtx_copy(dest, src, count)`

### Parameters
| Field | Type |
| ----- | ---- |
| dest | `Pointer` <`Vtx`> |
| src | `Pointer` <`Vtx`> |
| count | `integer` |

### Returns
- None

### C Prototype
`void vtx_copy(Vtx *dest, Vtx *src, u32 count);`


## vtx_create

### Description
Creates a new named vertex buffer of `count` vertices

### Lua Example
`local pointerValue = vtx_create(name, count)`

### Parameters
| Field | Type |
| ----- | ---- |
| name | `string` |
| count | `integer` |

### Returns
- `Pointer` <`Vtx`>

### C Prototype
`Vtx *vtx_create(const char *name, u32 count);`


## vtx_resize

### Description
Resizes a vertex buffer created by `vtx_create`

### Lua Example
`vtx_resize(vtx, newCount)`

### Parameters
| Field | Type |
| ----- | ---- |
| vtx | `Pointer` <`Vtx`> |
| newCount | `integer` |

### Returns
- None

### C Prototype
`void vtx_resize(Vtx *vtx, u32 newCount);`


## vtx_delete

### Description
Deletes a vertex buffer created by `vtx_create`

### Lua Example
`vtx_delete(vtx)`

### Parameters
| Field | Type |
| ----- | ---- |
| vtx | `Pointer` <`Vtx`> |

### Returns
- None

### C Prototype
`void vtx_delete(Vtx *vtx);`


## vtx_delete_all

### Description
Deletes all vertex buffers created by `vtx_create`

### Lua Example
`vtx_delete_all()`

### Parameters
- None

### Returns
- None

### C Prototype
`void vtx_delete_all();`


---
# functions from smlua_level_utils.h

<br />


## smlua_level_util_change_area

### Description
Instantly changes the current area to `areaIndex`

### Lua Example
`smlua_level_util_change_area(areaIndex)`

### Parameters
| Field | Type |
| ----- | ---- |
| areaIndex | `integer` |

### Returns
- None

### C Prototype
`void smlua_level_util_change_area(s32 areaIndex);`


## smlua_level_util_get_info

### Description
Gets information on a custom level from `levelNum`

### Lua Example
`local customLevelInfoValue = smlua_level_util_get_info(levelNum)`

### Parameters
| Field | Type |
| ----- | ---- |
| levelNum | `integer` |

### Returns
- [CustomLevelInfo](structs.md#CustomLevelInfo)

### C Prototype
`struct CustomLevelInfo* smlua_level_util_get_info(s16 levelNum);`


## smlua_level_util_get_info_from_short_name

### Description
Gets information on a custom level from `shortName`

### Lua Example
`local customLevelInfoValue = smlua_level_util_get_info_from_short_name(shortName)`

### Parameters
| Field | Type |
| ----- | ---- |
| shortName | `string` |

### Returns
- [CustomLevelInfo](structs.md#CustomLevelInfo)

### C Prototype
`struct CustomLevelInfo* smlua_level_util_get_info_from_short_name(const char* shortName);`


## smlua_level_util_get_info_from_course_num

### Description
Gets information on a custom level from `courseNum`

### Lua Example
`local customLevelInfoValue = smlua_level_util_get_info_from_course_num(courseNum)`

### Parameters
| Field | Type |
| ----- | ---- |
| courseNum | `integer` |

### Returns
- [CustomLevelInfo](structs.md#CustomLevelInfo)

### C Prototype
`struct CustomLevelInfo* smlua_level_util_get_info_from_course_num(u8 courseNum);`


## level_register

### Description
Registers a fully custom level. Level ID begins at 50

### Lua Example
`local integerValue = level_register(scriptEntryName, courseNum, fullName, shortName, acousticReach, echoLevel1, echoLevel2, echoLevel3)`

### Parameters
| Field | Type |
| ----- | ---- |
| scriptEntryName | `string` |
| courseNum | `integer` |
| fullName | `string` |
| shortName | `string` |
| acousticReach | `integer` |
| echoLevel1 | `integer` |
| echoLevel2 | `integer` |
| echoLevel3 | `integer` |

### Returns
- `integer`

### C Prototype
`s16 level_register(const char* scriptEntryName, s16 courseNum, const char* fullName, const char* shortName, u32 acousticReach, u32 echoLevel1, u32 echoLevel2, u32 echoLevel3);`


## level_is_vanilla_level

### Description
Checks if `levelNum` is a vanilla level

### Lua Example
`local booleanValue = level_is_vanilla_level(levelNum)`

### Parameters
| Field | Type |
| ----- | ---- |
| levelNum | `integer` |

### Returns
- `boolean`

### C Prototype
`bool level_is_vanilla_level(s16 levelNum);`


## warp_to_warpnode

### Description
Warps to `aWarpId` of `aArea` in `aLevel` during `aAct`

### Lua Example
`local booleanValue = warp_to_warpnode(aLevel, aArea, aAct, aWarpId)`

### Parameters
| Field | Type |
| ----- | ---- |
| aLevel | `integer` |
| aArea | `integer` |
| aAct | `integer` |
| aWarpId | `integer` |

### Returns
- `boolean`

### C Prototype
`bool warp_to_warpnode(s32 aLevel, s32 aArea, s32 aAct, s32 aWarpId);`


## warp_to_level

### Description
Warps to `aArea` of `aLevel` in `aAct`

### Lua Example
`local booleanValue = warp_to_level(aLevel, aArea, aAct)`

### Parameters
| Field | Type |
| ----- | ---- |
| aLevel | `integer` |
| aArea | `integer` |
| aAct | `integer` |

### Returns
- `boolean`

### C Prototype
`bool warp_to_level(s32 aLevel, s32 aArea, s32 aAct);`


## warp_restart_level

### Description
Restarts the current level

### Lua Example
`local booleanValue = warp_restart_level()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool warp_restart_level(void);`


## warp_to_start_level

### Description
Warps to the start level (Castle Grounds by default)

### Lua Example
`local booleanValue = warp_to_start_level()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool warp_to_start_level(void);`


## warp_exit_level

### Description
Exits the current level after `aDelay`

### Lua Example
`local booleanValue = warp_exit_level(aDelay)`

### Parameters
| Field | Type |
| ----- | ---- |
| aDelay | `integer` |

### Returns
- `boolean`

### C Prototype
`bool warp_exit_level(s32 aDelay);`


## warp_to_castle

### Description
Warps back to the castle from `aLevel`

### Lua Example
`local booleanValue = warp_to_castle(aLevel)`

### Parameters
| Field | Type |
| ----- | ---- |
| aLevel | `integer` |

### Returns
- `boolean`

### C Prototype
`bool warp_to_castle(s32 aLevel);`


## level_create_warp_node

### Description
Creates a warp node in level `levelNum` and area `areaIndex` with id `id` to the warp node `destNode` in level `destLevel` and area `destArea`.
If `checkpoint` is true, Mario will warp directly to this node if he enters the level again (after a death for example).
`marioSpawnType` indicates which kind of action Mario should perform when exiting this node. Its value must be one of the `MARIO_SPAWN_` constants.

### Lua Example
`local customWarpNodeValue = level_create_warp_node(levelNum, areaIndex, id, marioSpawnType, destLevel, destArea, destNode, checkpoint)`

### Parameters
| Field | Type |
| ----- | ---- |
| levelNum | `integer` |
| areaIndex | `integer` |
| id | `integer` |
| marioSpawnType | [enum MarioSpawnType](constants.md#enum-MarioSpawnType) |
| destLevel | `integer` |
| destArea | `integer` |
| destNode | `integer` |
| checkpoint | `boolean` |

### Returns
- [CustomWarpNode](structs.md#CustomWarpNode)

### C Prototype
`struct CustomWarpNode *level_create_warp_node(u8 levelNum, u8 areaIndex, u8 id, enum MarioSpawnType marioSpawnType, u8 destLevel, u8 destArea, u8 destNode, bool checkpoint);`


## level_create_warp_node_with_object

### Description
Creates a warp node in level `levelNum` and area `areaIndex` with id `id` to the warp node `destNode` in level `destLevel` and area `destArea`, and associates it an object described by `pos`, `angle`, `modelId`, `behaviorId` and `behParams`. Note that the object must have the `INTERACT_WARP` interaction type for the warp to work properly.
If `checkpoint` is true, Mario will warp directly to this node if he enters the level again (after a death for example).
`marioSpawnType` indicates which kind of action Mario should perform when exiting this node. Its value must be one of the `MARIO_SPAWN_` constants.

### Lua Example
`local customWarpNodeValue = level_create_warp_node_with_object(levelNum, areaIndex, id, marioSpawnType, destLevel, destArea, destNode, checkpoint, pos, angle, modelId, behaviorId, behParams)`

### Parameters
| Field | Type |
| ----- | ---- |
| levelNum | `integer` |
| areaIndex | `integer` |
| id | `integer` |
| marioSpawnType | [enum MarioSpawnType](constants.md#enum-MarioSpawnType) |
| destLevel | `integer` |
| destArea | `integer` |
| destNode | `integer` |
| checkpoint | `boolean` |
| pos | [Vec3f](structs.md#Vec3f) |
| angle | [Vec3s](structs.md#Vec3s) |
| modelId | [enum ModelExtendedId](constants.md#enum-ModelExtendedId) |
| behaviorId | [enum BehaviorId](constants.md#enum-BehaviorId) |
| behParams | `integer` |

### Returns
- [CustomWarpNode](structs.md#CustomWarpNode)

### C Prototype
`struct CustomWarpNode *level_create_warp_node_with_object(u8 levelNum, u8 areaIndex, u8 id, enum MarioSpawnType marioSpawnType, u8 destLevel, u8 destArea, u8 destNode, bool checkpoint, Vec3f pos, Vec3s angle, enum ModelExtendedId modelId, enum BehaviorId behaviorId, u32 behParams);`


## level_get_warp_node

### Description
Gets the warp node in level `levelNum` and area `areaIndex` with id `id`.
Only the warp nodes created by `level_create_warp_node` or `level_create_warp_node_with_object` can be returned by this function.

### Lua Example
`local customWarpNodeValue = level_get_warp_node(levelNum, areaIndex, id)`

### Parameters
| Field | Type |
| ----- | ---- |
| levelNum | `integer` |
| areaIndex | `integer` |
| id | `integer` |

### Returns
- [CustomWarpNode](structs.md#CustomWarpNode)

### C Prototype
`struct CustomWarpNode *level_get_warp_node(u8 levelNum, u8 areaIndex, u8 id);`


## level_delete_warp_node

### Description
Deletes the warp node in level `levelNum` and area `areaIndex` with id `id`.
Only the warp nodes created by `level_create_warp_node` or `level_create_warp_node_with_object` can be deleted by this function.

### Lua Example
`level_delete_warp_node(levelNum, areaIndex, id)`

### Parameters
| Field | Type |
| ----- | ---- |
| levelNum | `integer` |
| areaIndex | `integer` |
| id | `integer` |

### Returns
- None

### C Prototype
`void level_delete_warp_node(u8 levelNum, u8 areaIndex, u8 id);`


## level_clear_warp_nodes

### Description
Deletes all the warp nodes in level `levelNum`.
Only the warp nodes created by `level_create_warp_node` or `level_create_warp_node_with_object` can be deleted by this function.

### Lua Example
`level_clear_warp_nodes(levelNum)`

### Parameters
| Field | Type |
| ----- | ---- |
| levelNum | `integer` |

### Returns
- None

### C Prototype
`void level_clear_warp_nodes(u8 levelNum);`


---
# functions from smlua_misc_utils.h

<br />


## get_network_area_timer

### Description
Gets the current area's networked timer

### Lua Example
`local integerValue = get_network_area_timer()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u32 get_network_area_timer(void);`


## get_network_area_random_seed

### Description
Gets the current area's networked random seed

### Lua Example
`local integerValue = get_network_area_random_seed()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u32 get_network_area_random_seed(void);`


## get_area_update_counter

### Description
Gets the area update counter incremented when objects are updated

### Lua Example
`local integerValue = get_area_update_counter()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u16 get_area_update_counter(void);`


## get_temp_s32_pointer

### Description
Returns a temporary signed 32-bit integer pointer with its value set to `initialValue`

### Lua Example
`local pointerValue = get_temp_s32_pointer(initialValue)`

### Parameters
| Field | Type |
| ----- | ---- |
| initialValue | `integer` |

### Returns
- `Pointer` <`integer`>

### C Prototype
`s32* get_temp_s32_pointer(s32 initialValue);`


## deref_s32_pointer

### Description
Gets the signed 32-bit integer value from `pointer`

### Lua Example
`local integerValue = deref_s32_pointer(pointer)`

### Parameters
| Field | Type |
| ----- | ---- |
| pointer | `Pointer` <`integer`> |

### Returns
- `integer`

### C Prototype
`s32 deref_s32_pointer(s32* pointer);`


## djui_popup_create_global

### Description
Creates a DJUI popup that is broadcasted to every client

### Lua Example
`djui_popup_create_global(message, lines)`

### Parameters
| Field | Type |
| ----- | ---- |
| message | `string` |
| lines | `integer` |

### Returns
- None

### C Prototype
`void djui_popup_create_global(const char* message, int lines);`


## djui_is_popup_disabled

### Description
Returns if popups are disabled

### Lua Example
`local booleanValue = djui_is_popup_disabled()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool djui_is_popup_disabled(void);`


## djui_set_popup_disabled_override

### Description
Sets if popups are disabled

### Lua Example
`djui_set_popup_disabled_override(value)`

### Parameters
| Field | Type |
| ----- | ---- |
| value | `boolean` |

### Returns
- None

### C Prototype
`void djui_set_popup_disabled_override(bool value);`


## djui_reset_popup_disabled_override

### Description
Resets if popups are disabled

### Lua Example
`djui_reset_popup_disabled_override()`

### Parameters
- None

### Returns
- None

### C Prototype
`void djui_reset_popup_disabled_override(void);`


## djui_is_playerlist_open

### Description
Checks if the DJUI playerlist is open

### Lua Example
`local booleanValue = djui_is_playerlist_open()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool djui_is_playerlist_open(void);`


## djui_attempting_to_open_playerlist

### Description
Checks if the DJUI playerlist is attempting to be opened

### Lua Example
`local booleanValue = djui_attempting_to_open_playerlist()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool djui_attempting_to_open_playerlist(void);`


## djui_get_playerlist_page_index

### Description
Gets the DJUI playerlist's page index

### Lua Example
`local integerValue = djui_get_playerlist_page_index()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u8 djui_get_playerlist_page_index(void);`


## djui_is_chatbox_open

### Description
Checks if the DJUI chatbox is open

### Lua Example
`local booleanValue = djui_is_chatbox_open()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool djui_is_chatbox_open(void);`


## djui_menu_get_font

### Description
Gets the DJUI menu font

### Lua Example
`local enumValue = djui_menu_get_font()`

### Parameters
- None

### Returns
- [enum DjuiFontType](constants.md#enum-DjuiFontType)

### C Prototype
`enum DjuiFontType djui_menu_get_font(void);`


## djui_menu_get_theme

### Description
Gets the DJUI menu theme

### Lua Example
`local djuiThemeValue = djui_menu_get_theme()`

### Parameters
- None

### Returns
- [DjuiTheme](structs.md#DjuiTheme)

### C Prototype
`struct DjuiTheme* djui_menu_get_theme(void);`


## djui_is_playerlist_ping_visible

### Description
Checks if the DJUI playerlist ping icon is visible

### Lua Example
`local booleanValue = djui_is_playerlist_ping_visible()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool djui_is_playerlist_ping_visible(void);`


## get_dialog_box_state

### Description
Gets the current state of the dialog box

### Lua Example
`local integerValue = get_dialog_box_state()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`s8 get_dialog_box_state(void);`


## get_dialog_id

### Description
Gets the current dialog box ID

### Lua Example
`local integerValue = get_dialog_id()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`s32 get_dialog_id(void);`


## get_last_star_or_key

### Description
Gets if the last objective collected was a star (0) or a key (1)

### Lua Example
`local integerValue = get_last_star_or_key()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u8 get_last_star_or_key(void);`


## set_last_star_or_key

### Description
Sets if the last objective collected was a star (0) or a key (1)

### Lua Example
`set_last_star_or_key(value)`

### Parameters
| Field | Type |
| ----- | ---- |
| value | `integer` |

### Returns
- None

### C Prototype
`void set_last_star_or_key(u8 value);`


## get_last_completed_course_num

### Description
Gets the last course a star or key was collected in

### Lua Example
`local integerValue = get_last_completed_course_num()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u8 get_last_completed_course_num(void);`


## set_last_completed_course_num

### Description
Sets the last course a star or key was collected in

### Lua Example
`set_last_completed_course_num(courseNum)`

### Parameters
| Field | Type |
| ----- | ---- |
| courseNum | `integer` |

### Returns
- None

### C Prototype
`void set_last_completed_course_num(u8 courseNum);`


## get_last_completed_star_num

### Description
Gets the last collected star's number (1-7)

### Lua Example
`local integerValue = get_last_completed_star_num()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u8 get_last_completed_star_num(void);`


## set_last_completed_star_num

### Description
Sets the last collected star's number (1-7)

### Lua Example
`set_last_completed_star_num(starNum)`

### Parameters
| Field | Type |
| ----- | ---- |
| starNum | `integer` |

### Returns
- None

### C Prototype
`void set_last_completed_star_num(u8 starNum);`


## get_got_file_coin_hi_score

### Description
Checks if the save file's coin "HI SCORE" was obtained with the last star or key collection

### Lua Example
`local booleanValue = get_got_file_coin_hi_score()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool get_got_file_coin_hi_score(void);`


## set_got_file_coin_hi_score

### Description
Sets if the save file's coin "HI SCORE" was obtained with the last star or key collection

### Lua Example
`set_got_file_coin_hi_score(value)`

### Parameters
| Field | Type |
| ----- | ---- |
| value | `boolean` |

### Returns
- None

### C Prototype
`void set_got_file_coin_hi_score(bool value);`


## get_save_file_modified

### Description
Checks if the save file has been modified without saving

### Lua Example
`local booleanValue = get_save_file_modified()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool get_save_file_modified(void);`


## set_save_file_modified

### Description
Sets if the save file has been modified without saving

### Lua Example
`set_save_file_modified(value)`

### Parameters
| Field | Type |
| ----- | ---- |
| value | `boolean` |

### Returns
- None

### C Prototype
`void set_save_file_modified(bool value);`


## hud_hide

### Description
Hides the HUD

### Lua Example
`hud_hide()`

### Parameters
- None

### Returns
- None

### C Prototype
`void hud_hide(void);`


## hud_show

### Description
Shows the HUD

### Lua Example
`hud_show()`

### Parameters
- None

### Returns
- None

### C Prototype
`void hud_show(void);`


## hud_is_hidden

### Description
Checks if the HUD is hidden

### Lua Example
`local booleanValue = hud_is_hidden()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool hud_is_hidden(void);`


## hud_get_value

### Description
Gets a HUD display value

### Lua Example
`local integerValue = hud_get_value(type)`

### Parameters
| Field | Type |
| ----- | ---- |
| type | [enum HudDisplayValue](constants.md#enum-HudDisplayValue) |

### Returns
- `integer`

### C Prototype
`s32 hud_get_value(enum HudDisplayValue type);`


## hud_set_value

### Description
Sets a HUD display value

### Lua Example
`hud_set_value(type, value)`

### Parameters
| Field | Type |
| ----- | ---- |
| type | [enum HudDisplayValue](constants.md#enum-HudDisplayValue) |
| value | `integer` |

### Returns
- None

### C Prototype
`void hud_set_value(enum HudDisplayValue type, s32 value);`


## hud_render_power_meter

### Description
Renders a power meter on the HUD

### Lua Example
`hud_render_power_meter(health, x, y, width, height)`

### Parameters
| Field | Type |
| ----- | ---- |
| health | `integer` |
| x | `number` |
| y | `number` |
| width | `number` |
| height | `number` |

### Returns
- None

### C Prototype
`void hud_render_power_meter(s32 health, f32 x, f32 y, f32 width, f32 height);`


## hud_render_power_meter_interpolated

### Description
Renders an interpolated power meter on the HUD

### Lua Example
`hud_render_power_meter_interpolated(health, prevX, prevY, prevWidth, prevHeight, x, y, width, height)`

### Parameters
| Field | Type |
| ----- | ---- |
| health | `integer` |
| prevX | `number` |
| prevY | `number` |
| prevWidth | `number` |
| prevHeight | `number` |
| x | `number` |
| y | `number` |
| width | `number` |
| height | `number` |

### Returns
- None

### C Prototype
`void hud_render_power_meter_interpolated(s32 health, f32 prevX, f32 prevY, f32 prevWidth, f32 prevHeight, f32 x, f32 y, f32 width, f32 height);`


## hud_get_flash

### Description
Gets if the star counter on the HUD should flash

### Lua Example
`local integerValue = hud_get_flash()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`s8 hud_get_flash(void);`


## hud_set_flash

### Description
Sets if the star counter on the HUD should flash

### Lua Example
`hud_set_flash(value)`

### Parameters
| Field | Type |
| ----- | ---- |
| value | `integer` |

### Returns
- None

### C Prototype
`void hud_set_flash(s8 value);`


## act_select_hud_hide

### Description
Hides part of the Act Select HUD

### Lua Example
`act_select_hud_hide(part)`

### Parameters
| Field | Type |
| ----- | ---- |
| part | [enum ActSelectHudPart](constants.md#enum-ActSelectHudPart) |

### Returns
- None

### C Prototype
`void act_select_hud_hide(enum ActSelectHudPart part);`


## act_select_hud_show

### Description
Shows part of the Act Select HUD

### Lua Example
`act_select_hud_show(part)`

### Parameters
| Field | Type |
| ----- | ---- |
| part | [enum ActSelectHudPart](constants.md#enum-ActSelectHudPart) |

### Returns
- None

### C Prototype
`void act_select_hud_show(enum ActSelectHudPart part);`


## act_select_hud_is_hidden

### Description
Checks if part of the Act Select HUD is hidden

### Lua Example
`local booleanValue = act_select_hud_is_hidden(part)`

### Parameters
| Field | Type |
| ----- | ---- |
| part | [enum ActSelectHudPart](constants.md#enum-ActSelectHudPart) |

### Returns
- `boolean`

### C Prototype
`bool act_select_hud_is_hidden(enum ActSelectHudPart part);`


## is_game_paused

### Description
Checks if the game is paused

### Lua Example
`local booleanValue = is_game_paused()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool is_game_paused(void);`


## is_pause_menu_hidden

### Description
Gets if the pause menu elements are hidden, useful for creating custom pause menus

### Lua Example
`local booleanValue = is_pause_menu_hidden()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool is_pause_menu_hidden(void);`


## set_pause_menu_hidden

### Description
Sets if the pause menu elements are hidden, useful for creating custom pause menus

### Lua Example
`set_pause_menu_hidden(hidden)`

### Parameters
| Field | Type |
| ----- | ---- |
| hidden | `boolean` |

### Returns
- None

### C Prototype
`void set_pause_menu_hidden(bool hidden);`


## game_pause

### Description
Pauses the game

### Lua Example
`game_pause()`

### Parameters
- None

### Returns
- None

### C Prototype
`void game_pause(void);`


## game_unpause

### Description
Unpauses the game

### Lua Example
`game_unpause()`

### Parameters
- None

### Returns
- None

### C Prototype
`void game_unpause(void);`


## is_transition_playing

### Description
Checks if a screen transition is playing

### Lua Example
`local booleanValue = is_transition_playing()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool is_transition_playing(void);`


## get_current_play_mode

### Description
Gets the current play mode (`PLAY_MODE_*`)

### Lua Example
`local integerValue = get_current_play_mode()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`s16 get_current_play_mode(void);`


## get_delayed_warp_op

### Description
Gets the delayed warp operation type (`WARP_OP_*`)

### Lua Example
`local integerValue = get_delayed_warp_op()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`s16 get_delayed_warp_op(void);`


## allocate_mario_action

### Description
Allocates an action ID with bitwise flags

### Lua Example
`local integerValue = allocate_mario_action(actFlags)`

### Parameters
| Field | Type |
| ----- | ---- |
| actFlags | `integer` |

### Returns
- `integer`

### C Prototype
`u32 allocate_mario_action(u32 actFlags);`


## get_hand_foot_pos_x

### Description
Gets the X coordinate of Mario's hand (0-1) or foot (2-3)
but it is important to note that the positions are not updated off-screen

### Lua Example
`local numberValue = get_hand_foot_pos_x(m, index)`

### Parameters
| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |
| index | `integer` |

### Returns
- `number`

### C Prototype
`f32 get_hand_foot_pos_x(struct MarioState* m, u8 index);`


## get_hand_foot_pos_y

### Description
Gets the Y coordinate of Mario's hand (0-1) or foot (2-3)
but It is important to note that the positions are not updated off-screen

### Lua Example
`local numberValue = get_hand_foot_pos_y(m, index)`

### Parameters
| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |
| index | `integer` |

### Returns
- `number`

### C Prototype
`f32 get_hand_foot_pos_y(struct MarioState* m, u8 index);`


## get_hand_foot_pos_z

### Description
Gets the Z coordinate of Mario's hand (0-1) or foot (2-3)
but it is important to note that the positions are not updated off-screen

### Lua Example
`local numberValue = get_hand_foot_pos_z(m, index)`

### Parameters
| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |
| index | `integer` |

### Returns
- `number`

### C Prototype
`f32 get_hand_foot_pos_z(struct MarioState* m, u8 index);`


## get_mario_anim_part_pos

### Description
Retrieves the animated part position associated to `animPart` from the MarioState `m` and stores it into `pos`. Returns `true` on success or `false` on failure

### Lua Example
`local booleanValue = get_mario_anim_part_pos(m, animPart, pos)`

### Parameters
| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |
| animPart | `integer` |
| pos | [Vec3f](structs.md#Vec3f) |

### Returns
- `boolean`

### C Prototype
`bool get_mario_anim_part_pos(struct MarioState *m, u32 animPart, VEC_OUT Vec3f pos);`


## get_mario_anim_part_rot

### Description
Retrieves the animated part rotation associated to `animPart` from the MarioState `m` and stores it into `rot`. Returns `true` on success or `false` on failure

### Lua Example
`local booleanValue = get_mario_anim_part_rot(m, animPart, rot)`

### Parameters
| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |
| animPart | `integer` |
| rot | [Vec3s](structs.md#Vec3s) |

### Returns
- `boolean`

### C Prototype
`bool get_mario_anim_part_rot(struct MarioState *m, u32 animPart, VEC_OUT Vec3s rot);`


## get_mario_anim_part_mtx

### Description
Retrieves the animated part matrix associated to `animPart` from the MarioState `m` and stores it into `mtx`. Returns `true` on success or `false` on failure

### Lua Example
`local booleanValue = get_mario_anim_part_mtx(m, animPart, mtx)`

### Parameters
| Field | Type |
| ----- | ---- |
| m | [MarioState](structs.md#MarioState) |
| animPart | `integer` |
| mtx | [Mat4](structs.md#Mat4) |

### Returns
- `boolean`

### C Prototype
`bool get_mario_anim_part_mtx(struct MarioState *m, u32 animPart, VEC_OUT Mat4 mtx);`


## get_current_save_file_num

### Description
Gets the current save file number (1-indexed)

### Lua Example
`local integerValue = get_current_save_file_num()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`s16 get_current_save_file_num(void);`


## save_file_get_using_backup_slot

### Description
Checks if the save file is using its backup slot

### Lua Example
`local booleanValue = save_file_get_using_backup_slot()`

### Parameters
- None

### Returns
- `boolean`

### C Prototype
`bool save_file_get_using_backup_slot(void);`


## save_file_set_using_backup_slot

### Description
Sets if the save file should use its backup slot

### Lua Example
`save_file_set_using_backup_slot(usingBackupSlot)`

### Parameters
| Field | Type |
| ----- | ---- |
| usingBackupSlot | `boolean` |

### Returns
- None

### C Prototype
`void save_file_set_using_backup_slot(bool usingBackupSlot);`


## movtexqc_register

### Description
Registers a custom moving texture entry (used for vanilla water boxes)

### Lua Example
`movtexqc_register(name, level, area, type)`

### Parameters
| Field | Type |
| ----- | ---- |
| name | `string` |
| level | `integer` |
| area | `integer` |
| type | `integer` |

### Returns
- None

### C Prototype
`void movtexqc_register(const char* name, s16 level, s16 area, s16 type);`


## get_water_level

### Description
Gets the water level in an area corresponding to `index` (0-indexed)

### Lua Example
`local integerValue = get_water_level(index)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |

### Returns
- `integer`

### C Prototype
`s16 get_water_level(u8 index);`


## set_water_level

### Description
Sets the water level in an area corresponding to `index` (0-indexed)

### Lua Example
`set_water_level(index, height, sync)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |
| height | `integer` |
| sync | `boolean` |

### Returns
- None

### C Prototype
`void set_water_level(u8 index, s16 height, bool sync);`


## course_is_main_course

### Description
Checks if a course is a main course and not the castle or secret levels

### Lua Example
`local booleanValue = course_is_main_course(courseNum)`

### Parameters
| Field | Type |
| ----- | ---- |
| courseNum | `integer` |

### Returns
- `boolean`

### C Prototype
`bool course_is_main_course(u16 courseNum);`


## get_ttc_speed_setting

### Description
Gets TTC's speed setting

### Lua Example
`local integerValue = get_ttc_speed_setting()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`s16 get_ttc_speed_setting(void);`


## set_ttc_speed_setting

### Description
Sets TTC's speed setting (TTC_SPEED_*)

### Lua Example
`set_ttc_speed_setting(speed)`

### Parameters
| Field | Type |
| ----- | ---- |
| speed | `integer` |

### Returns
- None

### C Prototype
`void set_ttc_speed_setting(s16 speed);`


## get_time

### Description
Gets the Unix Timestamp

### Lua Example
`local integerValue = get_time()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`s64 get_time(void);`


## get_date_and_time

### Description
Gets the system clock's date and time

### Lua Example
`local dateTimeValue = get_date_and_time()`

### Parameters
- None

### Returns
- [DateTime](structs.md#DateTime)

### C Prototype
`struct DateTime* get_date_and_time(void);`


## get_envfx

### Description
Gets the non overridden environment effect (e.g. snow)

### Lua Example
`local integerValue = get_envfx()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u16 get_envfx(void);`


## set_override_envfx

### Description
Sets the override environment effect (e.g. snow)

### Lua Example
`set_override_envfx(envfx)`

### Parameters
| Field | Type |
| ----- | ---- |
| envfx | `integer` |

### Returns
- None

### C Prototype
`void set_override_envfx(s32 envfx);`


## get_global_timer

### Description
Gets the global timer that has been ticking at 30 frames per second since game boot

### Lua Example
`local integerValue = get_global_timer()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u32 get_global_timer(void);`


## get_dialog_response

### Description
Gets the choice selected inside of a dialog box (0-1)

### Lua Example
`local integerValue = get_dialog_response()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`s32 get_dialog_response(void);`


## get_time_stop_flags

### Description
Gets the active time stop flags, used to freeze specific objects during cutscenes

### Lua Example
`local integerValue = get_time_stop_flags()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u32 get_time_stop_flags(void);`


## get_local_discord_id

### Description
Gets the local discord ID if it isn't disabled, otherwise "0" is returned

### Lua Example
`local stringValue = get_local_discord_id()`

### Parameters
- None

### Returns
- `string`

### C Prototype
`const char* get_local_discord_id(void);`


## get_coopnet_id

### Description
Gets the CoopNet ID of a player with `localIndex` if CoopNet is being used and the player is connected, otherwise "-1" is returned

### Lua Example
`local stringValue = get_coopnet_id(localIndex)`

### Parameters
| Field | Type |
| ----- | ---- |
| localIndex | `integer` |

### Returns
- `string`

### C Prototype
`const char* get_coopnet_id(s8 localIndex);`


## get_volume_master

### Description
Gets the master volume level

### Lua Example
`local integerValue = get_volume_master()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u8 get_volume_master(void);`


## get_volume_level

### Description
Gets the volume level of music

### Lua Example
`local integerValue = get_volume_level()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u8 get_volume_level(void);`


## get_volume_sfx

### Description
Gets the volume level of sound effects

### Lua Example
`local integerValue = get_volume_sfx()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u8 get_volume_sfx(void);`


## get_volume_env

### Description
Gets the volume level of environment sounds effects

### Lua Example
`local integerValue = get_volume_env()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`u8 get_volume_env(void);`


## set_volume_master

### Description
Sets the master volume level

### Lua Example
`set_volume_master(volume)`

### Parameters
| Field | Type |
| ----- | ---- |
| volume | `integer` |

### Returns
- None

### C Prototype
`void set_volume_master(u8 volume);`


## set_volume_level

### Description
Sets the volume level of music

### Lua Example
`set_volume_level(volume)`

### Parameters
| Field | Type |
| ----- | ---- |
| volume | `integer` |

### Returns
- None

### C Prototype
`void set_volume_level(u8 volume);`


## set_volume_sfx

### Description
Sets the volume level of sound effects

### Lua Example
`set_volume_sfx(volume)`

### Parameters
| Field | Type |
| ----- | ---- |
| volume | `integer` |

### Returns
- None

### C Prototype
`void set_volume_sfx(u8 volume);`


## set_volume_env

### Description
Sets the volume level of environment sounds effects

### Lua Example
`set_volume_env(volume)`

### Parameters
| Field | Type |
| ----- | ---- |
| volume | `integer` |

### Returns
- None

### C Prototype
`void set_volume_env(u8 volume);`


## get_environment_region

### Description
Gets an environment region (gas/water boxes) height value

### Lua Example
`local integerValue = get_environment_region(index)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |

### Returns
- `integer`

### C Prototype
`s16 get_environment_region(u8 index);`


## set_environment_region

### Description
Sets an environment region (gas/water boxes) height value

### Lua Example
`set_environment_region(index, value)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |
| value | `integer` |

### Returns
- None

### C Prototype
`void set_environment_region(u8 index, s16 value);`


## mod_file_exists

### Description
Checks if a file exists inside of a mod

### Lua Example
`local booleanValue = mod_file_exists(filename)`

### Parameters
| Field | Type |
| ----- | ---- |
| filename | `string` |

### Returns
- `boolean`

### C Prototype
`bool mod_file_exists(const char* filename);`


## get_active_mod

### Description
Gets the mod currently being processed

### Lua Example
`local modValue = get_active_mod()`

### Parameters
- None

### Returns
- [Mod](structs.md#Mod)

### C Prototype
`struct Mod* get_active_mod(void);`


## get_mod_files

### Description
Gets all files a mod contains

### Lua Example
`local tableValue = get_mod_files(mod, subDirectory)`

### Parameters
| Field | Type |
| ----- | ---- |
| mod | [Mod](structs.md#Mod) |
| subDirectory | `string` |

### Returns
- `table`

### C Prototype
`LuaTable get_mod_files(struct Mod* mod, OPTIONAL const char* subDirectory);`


## set_window_title

### Description
Sets the window title to a custom title

### Lua Example
`set_window_title(title)`

### Parameters
| Field | Type |
| ----- | ---- |
| title | `string` |

### Returns
- None

### C Prototype
`void set_window_title(const char* title);`


## reset_window_title

### Description
Resets the window title

### Lua Example
`reset_window_title()`

### Parameters
- None

### Returns
- None

### C Prototype
`void reset_window_title(void);`


## get_os_name

### Description
Gets the name of the operating system the game is running on

### Lua Example
`local stringValue = get_os_name()`

### Parameters
- None

### Returns
- `string`

### C Prototype
`const char* get_os_name(void);`


## geo_get_current_root

### Description
Gets the current root node being processed

### Lua Example
`local graphNodeRootValue = geo_get_current_root()`

### Parameters
- None

### Returns
- [GraphNodeRoot](structs.md#GraphNodeRoot)

### C Prototype
`struct GraphNodeRoot* geo_get_current_root(void);`


## geo_get_current_master_list

### Description
Gets the current master list node being processed

### Lua Example
`local graphNodeMasterListValue = geo_get_current_master_list()`

### Parameters
- None

### Returns
- [GraphNodeMasterList](structs.md#GraphNodeMasterList)

### C Prototype
`struct GraphNodeMasterList* geo_get_current_master_list(void);`


## geo_get_current_perspective

### Description
Gets the current perspective node being processed

### Lua Example
`local graphNodePerspectiveValue = geo_get_current_perspective()`

### Parameters
- None

### Returns
- [GraphNodePerspective](structs.md#GraphNodePerspective)

### C Prototype
`struct GraphNodePerspective* geo_get_current_perspective(void);`


## geo_get_current_camera

### Description
Gets the current camera node being processed

### Lua Example
`local graphNodeCameraValue = geo_get_current_camera()`

### Parameters
- None

### Returns
- [GraphNodeCamera](structs.md#GraphNodeCamera)

### C Prototype
`struct GraphNodeCamera* geo_get_current_camera(void);`


## geo_get_current_held_object

### Description
Gets the current held object node being processed

### Lua Example
`local graphNodeHeldObjectValue = geo_get_current_held_object()`

### Parameters
- None

### Returns
- [GraphNodeHeldObject](structs.md#GraphNodeHeldObject)

### C Prototype
`struct GraphNodeHeldObject* geo_get_current_held_object(void);`


## geo_skip_interpolation

### Description
Skips graph node interpolation for a frame

### Lua Example
`geo_skip_interpolation(node, obj)`

### Parameters
| Field | Type |
| ----- | ---- |
| node | [GraphNode](structs.md#GraphNode) |
| obj | [GraphNodeObject](structs.md#GraphNodeObject) |

### Returns
- None

### C Prototype
`void geo_skip_interpolation(struct GraphNode *node, struct GraphNodeObject *obj);`


## texture_to_lua_table

### Description
Converts a texture's pixels to a Lua table. Returns nil if failed. Otherwise, returns a 1-indexed table of RGBA pixels

### Lua Example
`local tableValue = texture_to_lua_table(tex)`

### Parameters
| Field | Type |
| ----- | ---- |
| tex | `Pointer` <`Texture`> |

### Returns
- `table`

### C Prototype
`LuaTable texture_to_lua_table(const Texture *tex);`


## get_texture_name

### Description
Gets the name of the provided texture pointer `tex`

### Lua Example
`local stringValue = get_texture_name(tex)`

### Parameters
| Field | Type |
| ----- | ---- |
| tex | `Pointer` <`Texture`> |

### Returns
- `string`

### C Prototype
`const char *get_texture_name(const Texture *tex);`


---
# functions from smlua_model_utils.h

<br />


## smlua_model_util_get_id

### Description
Gets the extended model ID for the `name` of a `GeoLayout`

### Lua Example
`local enumValue = smlua_model_util_get_id(name)`

### Parameters
| Field | Type |
| ----- | ---- |
| name | `string` |

### Returns
- [enum ModelExtendedId](constants.md#enum-ModelExtendedId)

### C Prototype
`enum ModelExtendedId smlua_model_util_get_id(const char* name);`


---
# functions from smlua_obj_utils.h

<br />


## spawn_sync_object

### Description
Spawns a synchronized object at `x`, `y`, and `z` as a child object of the local Mario with his rotation.
You can change the fields of the object in `objSetupFunction`

### Lua Example
`local objectValue = spawn_sync_object(behaviorId, modelId, x, y, z, objSetupFunction)`

### Parameters
| Field | Type |
| ----- | ---- |
| behaviorId | [enum BehaviorId](constants.md#enum-BehaviorId) |
| modelId | [enum ModelExtendedId](constants.md#enum-ModelExtendedId) |
| x | `number` |
| y | `number` |
| z | `number` |
| objSetupFunction | `Lua Function` () |

### Returns
- [Object](structs.md#Object)

### C Prototype
`struct Object* spawn_sync_object(enum BehaviorId behaviorId, enum ModelExtendedId modelId, f32 x, f32 y, f32 z, OPTIONAL LuaFunction objSetupFunction);`


## spawn_non_sync_object

### Description
Spawns a non-synchronized object at `x`, `y`, and `z` as a child object of the local Mario with his rotation.
You can change the fields of the object in `objSetupFunction`

### Lua Example
`local objectValue = spawn_non_sync_object(behaviorId, modelId, x, y, z, objSetupFunction)`

### Parameters
| Field | Type |
| ----- | ---- |
| behaviorId | [enum BehaviorId](constants.md#enum-BehaviorId) |
| modelId | [enum ModelExtendedId](constants.md#enum-ModelExtendedId) |
| x | `number` |
| y | `number` |
| z | `number` |
| objSetupFunction | `Lua Function` () |

### Returns
- [Object](structs.md#Object)

### C Prototype
`struct Object* spawn_non_sync_object(enum BehaviorId behaviorId, enum ModelExtendedId modelId, f32 x, f32 y, f32 z, OPTIONAL LuaFunction objSetupFunction);`


## obj_has_behavior_id

### Description
Checks if an object has `behaviorId`

### Lua Example
`local integerValue = obj_has_behavior_id(o, behaviorId)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| behaviorId | [enum BehaviorId](constants.md#enum-BehaviorId) |

### Returns
- `integer`

### C Prototype
`s32 obj_has_behavior_id(struct Object *o, enum BehaviorId behaviorId);`


## obj_has_model_extended

### Description
Checks if an object's model is equal to `modelId`

### Lua Example
`local integerValue = obj_has_model_extended(o, modelId)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| modelId | [enum ModelExtendedId](constants.md#enum-ModelExtendedId) |

### Returns
- `integer`

### C Prototype
`s32 obj_has_model_extended(struct Object *o, enum ModelExtendedId modelId);`


## obj_get_model_id_extended

### Description
Returns an object's extended model id

### Lua Example
`local enumValue = obj_get_model_id_extended(o)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |

### Returns
- [enum ModelExtendedId](constants.md#enum-ModelExtendedId)

### C Prototype
`enum ModelExtendedId obj_get_model_id_extended(struct Object *o);`


## obj_set_model_extended

### Description
Sets an object's model to `modelId`

### Lua Example
`obj_set_model_extended(o, modelId)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| modelId | [enum ModelExtendedId](constants.md#enum-ModelExtendedId) |

### Returns
- None

### C Prototype
`void obj_set_model_extended(struct Object *o, enum ModelExtendedId modelId);`


## get_trajectory

### Description
Gets a trajectory by `name`

### Lua Example
`local pointerValue = get_trajectory(name)`

### Parameters
| Field | Type |
| ----- | ---- |
| name | `string` |

### Returns
- `Pointer` <`Trajectory`>

### C Prototype
`Trajectory* get_trajectory(const char* name);`


## geo_get_current_object

### Description
When used in a geo function, retrieve the current processed object

### Lua Example
`local objectValue = geo_get_current_object()`

### Parameters
- None

### Returns
- [Object](structs.md#Object)

### C Prototype
`struct Object *geo_get_current_object(void);`


## get_current_object

### Description
Gets the object currently being processed

### Lua Example
`local objectValue = get_current_object()`

### Parameters
- None

### Returns
- [Object](structs.md#Object)

### C Prototype
`struct Object *get_current_object(void);`


## get_dialog_object

### Description
Gets the NPC object Mario is talking to

### Lua Example
`local objectValue = get_dialog_object()`

### Parameters
- None

### Returns
- [Object](structs.md#Object)

### C Prototype
`struct Object *get_dialog_object(void);`


## get_cutscene_focus

### Description
Gets the cutscene focus object

### Lua Example
`local objectValue = get_cutscene_focus()`

### Parameters
- None

### Returns
- [Object](structs.md#Object)

### C Prototype
`struct Object *get_cutscene_focus(void);`


## get_secondary_camera_focus

### Description
Gets the secondary camera focus object

### Lua Example
`local objectValue = get_secondary_camera_focus()`

### Parameters
- None

### Returns
- [Object](structs.md#Object)

### C Prototype
`struct Object *get_secondary_camera_focus(void);`


## set_cutscene_focus

### Description
Sets the cutscene focus object

### Lua Example
`set_cutscene_focus(o)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |

### Returns
- None

### C Prototype
`void set_cutscene_focus(struct Object *o);`


## set_secondary_camera_focus

### Description
Sets the secondary camera focus object

### Lua Example
`set_secondary_camera_focus(o)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |

### Returns
- None

### C Prototype
`void set_secondary_camera_focus(struct Object *o);`


## obj_get_first

### Description
Gets the first object in an object list

### Lua Example
`local objectValue = obj_get_first(objList)`

### Parameters
| Field | Type |
| ----- | ---- |
| objList | [enum ObjectList](constants.md#enum-ObjectList) |

### Returns
- [Object](structs.md#Object)

### C Prototype
`struct Object *obj_get_first(enum ObjectList objList);`


## obj_get_first_with_behavior_id

### Description
Gets the first object loaded with `behaviorId`

### Lua Example
`local objectValue = obj_get_first_with_behavior_id(behaviorId)`

### Parameters
| Field | Type |
| ----- | ---- |
| behaviorId | [enum BehaviorId](constants.md#enum-BehaviorId) |

### Returns
- [Object](structs.md#Object)

### C Prototype
`struct Object *obj_get_first_with_behavior_id(enum BehaviorId behaviorId);`


## obj_get_first_with_behavior_id_and_field_s32

### Description
Gets the first object loaded with `behaviorId` and object signed 32-bit integer field
(look in `object_fields.h` to get the index of a field)

### Lua Example
`local objectValue = obj_get_first_with_behavior_id_and_field_s32(behaviorId, fieldIndex, value)`

### Parameters
| Field | Type |
| ----- | ---- |
| behaviorId | [enum BehaviorId](constants.md#enum-BehaviorId) |
| fieldIndex | `integer` |
| value | `integer` |

### Returns
- [Object](structs.md#Object)

### C Prototype
`struct Object *obj_get_first_with_behavior_id_and_field_s32(enum BehaviorId behaviorId, s32 fieldIndex, s32 value);`


## obj_get_first_with_behavior_id_and_field_f32

### Description
Gets the first object loaded with `behaviorId` and object float field
(look in `object_fields.h` to get the index of a field)

### Lua Example
`local objectValue = obj_get_first_with_behavior_id_and_field_f32(behaviorId, fieldIndex, value)`

### Parameters
| Field | Type |
| ----- | ---- |
| behaviorId | [enum BehaviorId](constants.md#enum-BehaviorId) |
| fieldIndex | `integer` |
| value | `number` |

### Returns
- [Object](structs.md#Object)

### C Prototype
`struct Object *obj_get_first_with_behavior_id_and_field_f32(enum BehaviorId behaviorId, s32 fieldIndex, f32 value);`


## obj_get_next

### Description
Gets the next object in an object list

### Lua Example
`local objectValue = obj_get_next(o)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |

### Returns
- [Object](structs.md#Object)

### C Prototype
`struct Object *obj_get_next(struct Object *o);`


## obj_get_next_with_same_behavior_id

### Description
Gets the next object loaded with the same behavior ID

### Lua Example
`local objectValue = obj_get_next_with_same_behavior_id(o)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |

### Returns
- [Object](structs.md#Object)

### C Prototype
`struct Object *obj_get_next_with_same_behavior_id(struct Object *o);`


## obj_get_next_with_same_behavior_id_and_field_s32

### Description
Gets the next object loaded with the same behavior ID and object signed 32-bit integer field
(look in `object_fields.h` to get the index of a field)

### Lua Example
`local objectValue = obj_get_next_with_same_behavior_id_and_field_s32(o, fieldIndex, value)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| fieldIndex | `integer` |
| value | `integer` |

### Returns
- [Object](structs.md#Object)

### C Prototype
`struct Object *obj_get_next_with_same_behavior_id_and_field_s32(struct Object *o, s32 fieldIndex, s32 value);`


## obj_get_next_with_same_behavior_id_and_field_f32

### Description
Gets the next object loaded with the same behavior ID and object float field
(look in `object_fields.h` to get the index of a field)

### Lua Example
`local objectValue = obj_get_next_with_same_behavior_id_and_field_f32(o, fieldIndex, value)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| fieldIndex | `integer` |
| value | `number` |

### Returns
- [Object](structs.md#Object)

### C Prototype
`struct Object *obj_get_next_with_same_behavior_id_and_field_f32(struct Object *o, s32 fieldIndex, f32 value);`


## obj_get_nearest_object_with_behavior_id

### Description
Gets the nearest object with `behaviorId` to `o`

### Lua Example
`local objectValue = obj_get_nearest_object_with_behavior_id(o, behaviorId)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| behaviorId | [enum BehaviorId](constants.md#enum-BehaviorId) |

### Returns
- [Object](structs.md#Object)

### C Prototype
`struct Object *obj_get_nearest_object_with_behavior_id(struct Object *o, enum BehaviorId behaviorId);`


## obj_count_objects_with_behavior_id

### Description
Counts every object with `behaviorId`

### Lua Example
`local integerValue = obj_count_objects_with_behavior_id(behaviorId)`

### Parameters
| Field | Type |
| ----- | ---- |
| behaviorId | [enum BehaviorId](constants.md#enum-BehaviorId) |

### Returns
- `integer`

### C Prototype
`s32 obj_count_objects_with_behavior_id(enum BehaviorId behaviorId);`


## obj_get_collided_object

### Description
Gets the corresponding collided object to an index from `o`

### Lua Example
`local objectValue = obj_get_collided_object(o, index)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| index | `integer` |

### Returns
- [Object](structs.md#Object)

### C Prototype
`struct Object *obj_get_collided_object(struct Object *o, s16 index);`


## obj_get_field_u32

### Description
Gets the unsigned 32-bit integer value of the object field corresponding to `fieldIndex`

### Lua Example
`local integerValue = obj_get_field_u32(o, fieldIndex)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| fieldIndex | `integer` |

### Returns
- `integer`

### C Prototype
`u32 obj_get_field_u32(struct Object *o, s32 fieldIndex);`


## obj_get_field_s32

### Description
Gets the signed 32-bit integer value of the object field corresponding to `fieldIndex`

### Lua Example
`local integerValue = obj_get_field_s32(o, fieldIndex)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| fieldIndex | `integer` |

### Returns
- `integer`

### C Prototype
`s32 obj_get_field_s32(struct Object *o, s32 fieldIndex);`


## obj_get_field_f32

### Description
Gets the float value of the object field corresponding to `fieldIndex`

### Lua Example
`local numberValue = obj_get_field_f32(o, fieldIndex)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| fieldIndex | `integer` |

### Returns
- `number`

### C Prototype
`f32 obj_get_field_f32(struct Object *o, s32 fieldIndex);`


## obj_get_field_s16

### Description
Gets the signed 16-bit integer value of the object field and sub field corresponding to `fieldSubIndex` and `fieldIndex`

### Lua Example
`local integerValue = obj_get_field_s16(o, fieldIndex, fieldSubIndex)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| fieldIndex | `integer` |
| fieldSubIndex | `integer` |

### Returns
- `integer`

### C Prototype
`s16 obj_get_field_s16(struct Object *o, s32 fieldIndex, s32 fieldSubIndex);`


## obj_set_field_u32

### Description
Sets the unsigned 32-bit integer value of the object field corresponding to `fieldIndex`

### Lua Example
`obj_set_field_u32(o, fieldIndex, value)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| fieldIndex | `integer` |
| value | `integer` |

### Returns
- None

### C Prototype
`void obj_set_field_u32(struct Object *o, s32 fieldIndex, u32 value);`


## obj_set_field_s32

### Description
Sets the signed 32-bit integer value of the object field corresponding to `fieldIndex`

### Lua Example
`obj_set_field_s32(o, fieldIndex, value)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| fieldIndex | `integer` |
| value | `integer` |

### Returns
- None

### C Prototype
`void obj_set_field_s32(struct Object *o, s32 fieldIndex, s32 value);`


## obj_set_field_f32

### Description
Sets the float value of the object field corresponding to `fieldIndex`

### Lua Example
`obj_set_field_f32(o, fieldIndex, value)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| fieldIndex | `integer` |
| value | `number` |

### Returns
- None

### C Prototype
`void obj_set_field_f32(struct Object *o, s32 fieldIndex, f32 value);`


## obj_set_field_s16

### Description
Sets the signed 16-bit integer value of the object field and sub field corresponding to `fieldSubIndex` and `fieldIndex`

### Lua Example
`obj_set_field_s16(o, fieldIndex, fieldSubIndex, value)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| fieldIndex | `integer` |
| fieldSubIndex | `integer` |
| value | `integer` |

### Returns
- None

### C Prototype
`void obj_set_field_s16(struct Object *o, s32 fieldIndex, s32 fieldSubIndex, s16 value);`


## obj_get_field_info_from_name

### Description
Gets the object field info (index, sub-index and type) from a field name and a specific mod (if provided). Returns `true` if the field is found, `false` otherwise.
Supported types are `s32`, `u32`, `f32`, `s16`.
This function works with custom object fields as well and is meant to be used with functions that take a field index as parameter, like `obj_get_first_with_behavior_id_and_field_s32` or `obj_get_field_s32`

### Lua Example
`local booleanValue, fieldIndex, fieldSubIndex, fieldType = obj_get_field_info_from_name(fieldName, mod)`

### Parameters
| Field | Type |
| ----- | ---- |
| fieldName | `string` |
| mod | [Mod](structs.md#Mod) |

### Returns
- `boolean`
- `integer`
- `integer`
- `string`

### C Prototype
`bool obj_get_field_info_from_name(const char *fieldName, OPTIONAL struct Mod *mod, RET s32 *fieldIndex, RET s32 *fieldSubIndex, RET const char **fieldType);`


## obj_get_temp_spawn_particles_info

### Description
Returns a temporary particle spawn info pointer with its model loaded in from `modelId`

### Lua Example
`local spawnParticlesInfoValue = obj_get_temp_spawn_particles_info(modelId)`

### Parameters
| Field | Type |
| ----- | ---- |
| modelId | [enum ModelExtendedId](constants.md#enum-ModelExtendedId) |

### Returns
- [SpawnParticlesInfo](structs.md#SpawnParticlesInfo)

### C Prototype
`struct SpawnParticlesInfo* obj_get_temp_spawn_particles_info(enum ModelExtendedId modelId);`


## obj_get_temp_water_droplet_params

### Description
Returns a temporary water droplet params pointer with its model and behavior loaded in from `modelId` and `behaviorId`

### Lua Example
`local waterDropletParamsValue = obj_get_temp_water_droplet_params(modelId, behaviorId)`

### Parameters
| Field | Type |
| ----- | ---- |
| modelId | [enum ModelExtendedId](constants.md#enum-ModelExtendedId) |
| behaviorId | [enum BehaviorId](constants.md#enum-BehaviorId) |

### Returns
- [WaterDropletParams](structs.md#WaterDropletParams)

### C Prototype
`struct WaterDropletParams* obj_get_temp_water_droplet_params(enum ModelExtendedId modelId, enum BehaviorId behaviorId);`


## get_temp_object_hitbox

### Description
Returns a temporary object hitbox pointer

### Lua Example
`local objectHitboxValue = get_temp_object_hitbox()`

### Parameters
- None

### Returns
- [ObjectHitbox](structs.md#ObjectHitbox)

### C Prototype
`struct ObjectHitbox* get_temp_object_hitbox(void);`


## obj_is_attackable

### Description
Checks if `o` is attackable

### Lua Example
`local booleanValue = obj_is_attackable(o)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |

### Returns
- `boolean`

### C Prototype
`bool obj_is_attackable(struct Object *o);`


## obj_is_breakable_object

### Description
Checks if `o` is breakable

### Lua Example
`local booleanValue = obj_is_breakable_object(o)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |

### Returns
- `boolean`

### C Prototype
`bool obj_is_breakable_object(struct Object *o);`


## obj_is_bully

### Description
Checks if `o` is a Bully

### Lua Example
`local booleanValue = obj_is_bully(o)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |

### Returns
- `boolean`

### C Prototype
`bool obj_is_bully(struct Object *o);`


## obj_is_coin

### Description
Checks if `o` is a coin

### Lua Example
`local booleanValue = obj_is_coin(o)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |

### Returns
- `boolean`

### C Prototype
`bool obj_is_coin(struct Object *o);`


## obj_is_exclamation_box

### Description
Checks if `o` is an exclamation box

### Lua Example
`local booleanValue = obj_is_exclamation_box(o)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |

### Returns
- `boolean`

### C Prototype
`bool obj_is_exclamation_box(struct Object *o);`


## obj_is_grabbable

### Description
Checks if `o` is grabbable

### Lua Example
`local booleanValue = obj_is_grabbable(o)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |

### Returns
- `boolean`

### C Prototype
`bool obj_is_grabbable(struct Object *o);`


## obj_is_mushroom_1up

### Description
Checks if `o` is a 1-Up Mushroom

### Lua Example
`local booleanValue = obj_is_mushroom_1up(o)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |

### Returns
- `boolean`

### C Prototype
`bool obj_is_mushroom_1up(struct Object *o);`


## obj_is_secret

### Description
Checks if `o` is a secret

### Lua Example
`local booleanValue = obj_is_secret(o)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |

### Returns
- `boolean`

### C Prototype
`bool obj_is_secret(struct Object *o);`


## obj_is_valid_for_interaction

### Description
Checks if `o` is activated, tangible, and interactible

### Lua Example
`local booleanValue = obj_is_valid_for_interaction(o)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |

### Returns
- `boolean`

### C Prototype
`bool obj_is_valid_for_interaction(struct Object *o);`


## obj_check_hitbox_overlap

### Description
Checks if `o1`'s hitbox is colliding with `o2`'s hitbox

### Lua Example
`local booleanValue = obj_check_hitbox_overlap(o1, o2)`

### Parameters
| Field | Type |
| ----- | ---- |
| o1 | [Object](structs.md#Object) |
| o2 | [Object](structs.md#Object) |

### Returns
- `boolean`

### C Prototype
`bool obj_check_hitbox_overlap(struct Object *o1, struct Object *o2);`


## obj_check_overlap_with_hitbox_params

### Description
Checks if `o`'s hitbox is colliding with the parameters of a hitbox

### Lua Example
`local booleanValue = obj_check_overlap_with_hitbox_params(o, x, y, z, h, r, d)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| x | `number` |
| y | `number` |
| z | `number` |
| h | `number` |
| r | `number` |
| d | `number` |

### Returns
- `boolean`

### C Prototype
`bool obj_check_overlap_with_hitbox_params(struct Object *o, f32 x, f32 y, f32 z, f32 h, f32 r, f32 d);`


## obj_set_vel

### Description
Sets an object's velocity to `vx`, `vy`, and `vz`

### Lua Example
`obj_set_vel(o, vx, vy, vz)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| vx | `number` |
| vy | `number` |
| vz | `number` |

### Returns
- None

### C Prototype
`void obj_set_vel(struct Object *o, f32 vx, f32 vy, f32 vz);`


## obj_move_xyz

### Description
Moves the object in the direction of `dx`, `dy`, and `dz`

### Lua Example
`obj_move_xyz(o, dx, dy, dz)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |
| dx | `number` |
| dy | `number` |
| dz | `number` |

### Returns
- None

### C Prototype
`void obj_move_xyz(struct Object *o, f32 dx, f32 dy, f32 dz);`


## set_whirlpools

### Description
Sets the parameters of one of the two whirlpools (0-indexed) in an area

### Lua Example
`set_whirlpools(x, y, z, strength, area, index)`

### Parameters
| Field | Type |
| ----- | ---- |
| x | `number` |
| y | `number` |
| z | `number` |
| strength | `integer` |
| area | `integer` |
| index | `integer` |

### Returns
- None

### C Prototype
`void set_whirlpools(f32 x, f32 y, f32 z, s16 strength, s16 area, s32 index);`


## obj_skip_interpolation

### Description
Skips object interpolation for a frame

### Lua Example
`obj_skip_interpolation(o)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |

### Returns
- None

### C Prototype
`void obj_skip_interpolation(struct Object *o);`


## obj_anim_skip_interpolation

### Description
Skips animation interpolation for a frame

### Lua Example
`obj_anim_skip_interpolation(o)`

### Parameters
| Field | Type |
| ----- | ---- |
| o | [Object](structs.md#Object) |

### Returns
- None

### C Prototype
`void obj_anim_skip_interpolation(struct Object *o);`


---
# functions from smlua_text_utils.h

<br />


## smlua_text_utils_reset_all

### Description
Resets every modified dialog back to vanilla

### Lua Example
`smlua_text_utils_reset_all()`

### Parameters
- None

### Returns
- None

### C Prototype
`void smlua_text_utils_reset_all(void);`


## smlua_text_utils_dialog_get

### Description
Gets the DialogEntry struct for the given `dialogId`

### Lua Example
`local dialogEntryValue = smlua_text_utils_dialog_get(dialogId)`

### Parameters
| Field | Type |
| ----- | ---- |
| dialogId | [enum DialogId](constants.md#enum-DialogId) |

### Returns
- [DialogEntry](structs.md#DialogEntry)

### C Prototype
`struct DialogEntry* smlua_text_utils_dialog_get(enum DialogId dialogId);`


## smlua_text_utils_dialog_replace

### Description
Replaces `dialogId` with a custom one

### Lua Example
`smlua_text_utils_dialog_replace(dialogId, unused, linesPerBox, leftOffset, width, str)`

### Parameters
| Field | Type |
| ----- | ---- |
| dialogId | [enum DialogId](constants.md#enum-DialogId) |
| unused | `integer` |
| linesPerBox | `integer` |
| leftOffset | `integer` |
| width | `integer` |
| str | `string` |

### Returns
- None

### C Prototype
`void smlua_text_utils_dialog_replace(enum DialogId dialogId, u32 unused, s8 linesPerBox, s16 leftOffset, s16 width, const char* str);`


## smlua_text_utils_dialog_restore

### Description
Restores a replaced DialogEntry to its original state.

### Lua Example
`smlua_text_utils_dialog_restore(dialogId)`

### Parameters
| Field | Type |
| ----- | ---- |
| dialogId | [enum DialogId](constants.md#enum-DialogId) |

### Returns
- None

### C Prototype
`void smlua_text_utils_dialog_restore(enum DialogId dialogId);`


## smlua_text_utils_dialog_is_replaced

### Description
Returns whether the dialog with the given ID has been replaced

### Lua Example
`local booleanValue = smlua_text_utils_dialog_is_replaced(dialogId)`

### Parameters
| Field | Type |
| ----- | ---- |
| dialogId | [enum DialogId](constants.md#enum-DialogId) |

### Returns
- `boolean`

### C Prototype
`bool smlua_text_utils_dialog_is_replaced(enum DialogId dialogId);`


## smlua_text_utils_allocate_dialog

### Description
Allocates a new dialog entry

### Lua Example
`local integerValue = smlua_text_utils_allocate_dialog()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`s32 smlua_text_utils_allocate_dialog(void);`


## smlua_text_utils_dialog_get_type

### Description
Gets the type of a `dialogId`

### Lua Example
`local enumValue = smlua_text_utils_dialog_get_type(dialogId)`

### Parameters
| Field | Type |
| ----- | ---- |
| dialogId | [enum DialogId](constants.md#enum-DialogId) |

### Returns
- [enum DialogType](constants.md#enum-DialogType)

### C Prototype
`enum DialogType smlua_text_utils_dialog_get_type(enum DialogId dialogId);`


## smlua_text_utils_dialog_set_type

### Description
Sets the type of a `dialogId`

### Lua Example
`smlua_text_utils_dialog_set_type(dialogId, dialogType)`

### Parameters
| Field | Type |
| ----- | ---- |
| dialogId | [enum DialogId](constants.md#enum-DialogId) |
| dialogType | [enum DialogType](constants.md#enum-DialogType) |

### Returns
- None

### C Prototype
`void smlua_text_utils_dialog_set_type(enum DialogId dialogId, enum DialogType dialogType);`


## smlua_text_utils_dialog_reset_type

### Description
Resets the type of a `dialogId`

### Lua Example
`smlua_text_utils_dialog_reset_type(dialogId)`

### Parameters
| Field | Type |
| ----- | ---- |
| dialogId | [enum DialogId](constants.md#enum-DialogId) |

### Returns
- None

### C Prototype
`void smlua_text_utils_dialog_reset_type(enum DialogId dialogId);`


## smlua_text_utils_course_acts_replace

### Description
Replaces the act names of `courseNum`

### Lua Example
`smlua_text_utils_course_acts_replace(courseNum, courseName, act1, act2, act3, act4, act5, act6)`

### Parameters
| Field | Type |
| ----- | ---- |
| courseNum | `integer` |
| courseName | `string` |
| act1 | `string` |
| act2 | `string` |
| act3 | `string` |
| act4 | `string` |
| act5 | `string` |
| act6 | `string` |

### Returns
- None

### C Prototype
`void smlua_text_utils_course_acts_replace(s16 courseNum, const char* courseName, const char* act1, const char* act2, const char* act3, const char* act4, const char* act5, const char* act6);`


## smlua_text_utils_secret_star_replace

### Description
Replaces the secret star course name of `courseNum` with `courseName`

### Lua Example
`smlua_text_utils_secret_star_replace(courseNum, courseName)`

### Parameters
| Field | Type |
| ----- | ---- |
| courseNum | `integer` |
| courseName | `string` |

### Returns
- None

### C Prototype
`void smlua_text_utils_secret_star_replace(s16 courseNum, const char* courseName);`


## smlua_text_utils_course_name_replace

### Description
Replaces the name of `courseNum` with `name`

### Lua Example
`smlua_text_utils_course_name_replace(courseNum, name)`

### Parameters
| Field | Type |
| ----- | ---- |
| courseNum | `integer` |
| name | `string` |

### Returns
- None

### C Prototype
`void smlua_text_utils_course_name_replace(s16 courseNum, const char* name);`


## smlua_text_utils_course_name_get

### Description
Gets the name of `courseNum`

### Lua Example
`local stringValue = smlua_text_utils_course_name_get(courseNum)`

### Parameters
| Field | Type |
| ----- | ---- |
| courseNum | `integer` |

### Returns
- `string`

### C Prototype
`const char* smlua_text_utils_course_name_get(s16 courseNum);`


## smlua_text_utils_course_name_mod_index

### Description
Gets the index of the mod that replaced the name of `courseNum`

### Lua Example
`local integerValue = smlua_text_utils_course_name_mod_index(courseNum)`

### Parameters
| Field | Type |
| ----- | ---- |
| courseNum | `integer` |

### Returns
- `integer`

### C Prototype
`s32 smlua_text_utils_course_name_mod_index(s16 courseNum);`


## smlua_text_utils_course_name_reset

### Description
Resets the name of `courseNum`

### Lua Example
`smlua_text_utils_course_name_reset(courseNum)`

### Parameters
| Field | Type |
| ----- | ---- |
| courseNum | `integer` |

### Returns
- None

### C Prototype
`void smlua_text_utils_course_name_reset(s16 courseNum);`


## smlua_text_utils_act_name_replace

### Description
Replaces the act name of `actNum` in `courseNum` with `name`

### Lua Example
`smlua_text_utils_act_name_replace(courseNum, actNum, name)`

### Parameters
| Field | Type |
| ----- | ---- |
| courseNum | `integer` |
| actNum | `integer` |
| name | `string` |

### Returns
- None

### C Prototype
`void smlua_text_utils_act_name_replace(s16 courseNum, u8 actNum, const char* name);`


## smlua_text_utils_act_name_get

### Description
Gets the act name of `actNum` in `courseNum`

### Lua Example
`local stringValue = smlua_text_utils_act_name_get(courseNum, actNum)`

### Parameters
| Field | Type |
| ----- | ---- |
| courseNum | `integer` |
| actNum | `integer` |

### Returns
- `string`

### C Prototype
`const char* smlua_text_utils_act_name_get(s16 courseNum, u8 actNum);`


## smlua_text_utils_act_name_mod_index

### Description
Gets the index of the mod that replaced the act name of `actNum` in `courseNum`

### Lua Example
`local integerValue = smlua_text_utils_act_name_mod_index(courseNum, actNum)`

### Parameters
| Field | Type |
| ----- | ---- |
| courseNum | `integer` |
| actNum | `integer` |

### Returns
- `integer`

### C Prototype
`s32 smlua_text_utils_act_name_mod_index(s16 courseNum, u8 actNum);`


## smlua_text_utils_act_name_reset

### Description
Resets the act name of `actNum` in `courseNum`

### Lua Example
`smlua_text_utils_act_name_reset(courseNum, actNum)`

### Parameters
| Field | Type |
| ----- | ---- |
| courseNum | `integer` |
| actNum | `integer` |

### Returns
- None

### C Prototype
`void smlua_text_utils_act_name_reset(s16 courseNum, u8 actNum);`


## smlua_text_utils_castle_secret_stars_replace

### Description
Replaces the castle secret stars text with `name`

### Lua Example
`smlua_text_utils_castle_secret_stars_replace(name)`

### Parameters
| Field | Type |
| ----- | ---- |
| name | `string` |

### Returns
- None

### C Prototype
`void smlua_text_utils_castle_secret_stars_replace(const char* name);`


## smlua_text_utils_castle_secret_stars_get

### Description
Gets the castle secret stars text

### Lua Example
`local stringValue = smlua_text_utils_castle_secret_stars_get()`

### Parameters
- None

### Returns
- `string`

### C Prototype
`const char* smlua_text_utils_castle_secret_stars_get();`


## smlua_text_utils_castle_secret_stars_mod_index

### Description
Gets the index of the mod that replaced the castle secret stars text

### Lua Example
`local integerValue = smlua_text_utils_castle_secret_stars_mod_index()`

### Parameters
- None

### Returns
- `integer`

### C Prototype
`s32 smlua_text_utils_castle_secret_stars_mod_index();`


## smlua_text_utils_castle_secret_stars_reset

### Description
Resets the castle secret stars text

### Lua Example
`smlua_text_utils_castle_secret_stars_reset()`

### Parameters
- None

### Returns
- None

### C Prototype
`void smlua_text_utils_castle_secret_stars_reset();`


## smlua_text_utils_extra_text_replace

### Description
Replace extra text (e.g. one of the castle's secret stars) with `text`

### Lua Example
`smlua_text_utils_extra_text_replace(index, text)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |
| text | `string` |

### Returns
- None

### C Prototype
`void smlua_text_utils_extra_text_replace(s16 index, const char* text);`


## smlua_text_utils_extra_text_get

### Description
Gets the extra text at `index`

### Lua Example
`local stringValue = smlua_text_utils_extra_text_get(index)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |

### Returns
- `string`

### C Prototype
`const char* smlua_text_utils_extra_text_get(s16 index);`


## smlua_text_utils_extra_text_mod_index

### Description
Gets the index of the mod that replaced the extra text at `index`

### Lua Example
`local integerValue = smlua_text_utils_extra_text_mod_index(index)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |

### Returns
- `integer`

### C Prototype
`s32 smlua_text_utils_extra_text_mod_index(s16 index);`


## smlua_text_utils_extra_text_reset

### Description
Resets the extra text at `index`

### Lua Example
`smlua_text_utils_extra_text_reset(index)`

### Parameters
| Field | Type |
| ----- | ---- |
| index | `integer` |

### Returns
- None

### C Prototype
`void smlua_text_utils_extra_text_reset(s16 index);`


## smlua_text_utils_get_language

### Description
Gets the current language

### Lua Example
`local stringValue = smlua_text_utils_get_language()`

### Parameters
- None

### Returns
- `string`

### C Prototype
`const char* smlua_text_utils_get_language(void);`


---
# functions from sound_init.h

<br />


## reset_volume

### Description
Resets if music volume has been lowered

### Lua Example
`reset_volume()`

### Parameters
- None

### Returns
- None

### C Prototype
`void reset_volume(void);`


## raise_background_noise

### Description
Raises music volume back up to normal levels

### Lua Example
`raise_background_noise(a)`

### Parameters
| Field | Type |
| ----- | ---- |
| a | `integer` |

### Returns
- None

### C Prototype
`void raise_background_noise(s32 a);`


## lower_background_noise

### Description
Lowers the volume of music by 40%

### Lua Example
`lower_background_noise(a)`

### Parameters
| Field | Type |
| ----- | ---- |
| a | `integer` |

### Returns
- None

### C Prototype
`void lower_background_noise(s32 a);`


## disable_background_sound

### Description
Disables background soundbanks

### Lua Example
`disable_background_sound()`

### Parameters
- None

### Returns
- None

### C Prototype
`void disable_background_sound(void);`


## enable_background_sound

### Description
Enables background soundbanks

### Lua Example
`enable_background_sound()`

### Parameters
- None

### Returns
- None

### C Prototype
`void enable_background_sound(void);`


## play_menu_sounds

### Description
Play menu sounds from `SOUND_MENU_FLAG_*` constants and queues rumble if `SOUND_MENU_FLAG_LETGOMARIOFACE` is one of the flags

### Lua Example
`play_menu_sounds(soundMenuFlags)`

### Parameters
| Field | Type |
| ----- | ---- |
| soundMenuFlags | `integer` |

### Returns
- None

### C Prototype
`void play_menu_sounds(s16 soundMenuFlags);`


## play_painting_eject_sound

### Description
Plays the painting eject sound effect if it has not already been played

### Lua Example
`play_painting_eject_sound()`

### Parameters
- None

### Returns
- None

### C Prototype
`void play_painting_eject_sound(void);`


## play_infinite_stairs_music

### Description
Plays the infinite stairs music if you're in the endless stairs room and have less than `gLevelValues.infiniteStairsRequirement` stars

### Lua Example
`play_infinite_stairs_music()`

### Parameters
- None

### Returns
- None

### C Prototype
`void play_infinite_stairs_music(void);`


## set_background_music

### Description
Sets the background music to `seqArgs` on sequence player `a` with a fade in time of `fadeTimer`

### Lua Example
`set_background_music(a, seqArgs, fadeTimer)`

### Parameters
| Field | Type |
| ----- | ---- |
| a | `integer` |
| seqArgs | `integer` |
| fadeTimer | `integer` |

### Returns
- None

### C Prototype
`void set_background_music(u16 a, u16 seqArgs, s16 fadeTimer);`


## fadeout_music

### Description
Fades out level, shell, and cap music

### Lua Example
`fadeout_music(fadeOutTime)`

### Parameters
| Field | Type |
| ----- | ---- |
| fadeOutTime | `integer` |

### Returns
- None

### C Prototype
`void fadeout_music(s16 fadeOutTime);`


## fadeout_level_music

### Description
Fades out the level sequence player

### Lua Example
`fadeout_level_music(fadeTimer)`

### Parameters
| Field | Type |
| ----- | ---- |
| fadeTimer | `integer` |

### Returns
- None

### C Prototype
`void fadeout_level_music(s16 fadeTimer);`


## play_cutscene_music

### Description
Plays and sets the current music to `seqArgs`

### Lua Example
`play_cutscene_music(seqArgs)`

### Parameters
| Field | Type |
| ----- | ---- |
| seqArgs | `integer` |

### Returns
- None

### C Prototype
`void play_cutscene_music(u16 seqArgs);`


## play_shell_music

### Description
Plays shell music

### Lua Example
`play_shell_music()`

### Parameters
- None

### Returns
- None

### C Prototype
`void play_shell_music(void);`


## stop_shell_music

### Description
Stops shell music completely

### Lua Example
`stop_shell_music()`

### Parameters
- None

### Returns
- None

### C Prototype
`void stop_shell_music(void);`


## play_cap_music

### Description
Plays `seqArgs` as cap music

### Lua Example
`play_cap_music(seqArgs)`

### Parameters
| Field | Type |
| ----- | ---- |
| seqArgs | `integer` |

### Returns
- None

### C Prototype
`void play_cap_music(u16 seqArgs);`


## fadeout_cap_music

### Description
Fades out cap music

### Lua Example
`fadeout_cap_music()`

### Parameters
- None

### Returns
- None

### C Prototype
`void fadeout_cap_music(void);`


## stop_cap_music

### Description
Stops cap music completely

### Lua Example
`stop_cap_music()`

### Parameters
- None

### Returns
- None

### C Prototype
`void stop_cap_music(void);`


---
# functions from spawn_sound.h

<br />


## cur_obj_play_sound_if_visible

### Description
Plays a sound if the current object is visible

### Lua Example
`cur_obj_play_sound_if_visible(soundMagic)`

### Parameters
| Field | Type |
| ----- | ---- |
| soundMagic | `integer` |

### Returns
- None

### C Prototype
`void cur_obj_play_sound_if_visible(s32 soundMagic);`


## cur_obj_play_sound_and_rumble_if_visible

### Description
Plays a sound if the current object is visible and queues rumble for the following sounds: `SOUND_OBJ_BOWSER_WALK`, `SOUND_OBJ_POUNDING_LOUD`, `SOUND_OBJ_WHOMP_LOWPRIO`

### Lua Example
`cur_obj_play_sound_and_rumble_if_visible(soundMagic)`

### Parameters
| Field | Type |
| ----- | ---- |
| soundMagic | `integer` |

### Returns
- None

### C Prototype
`void cur_obj_play_sound_and_rumble_if_visible(s32 soundMagic);`


## create_sound_spawner

### Description
Create a sound spawner for objects that need a sound play once.
(Breakable walls, King Bobomb exploding, etc)

### Lua Example
`create_sound_spawner(soundMagic)`

### Parameters
| Field | Type |
| ----- | ---- |
| soundMagic | `integer` |

### Returns
- None

### C Prototype
`void create_sound_spawner(s32 soundMagic);`

---

[< prev](functions-5.md) | [1](functions.md) | [2](functions-2.md) | [3](functions-3.md) | [4](functions-4.md) | [5](functions-5.md) | 6 | [7](functions-7.md) | [next >](functions-7.md)]

