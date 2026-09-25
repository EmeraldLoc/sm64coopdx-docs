# Player Indexes

A player index is an identifier for who a player is. There are 2 types:

- A local index is the index of each player locally. `0` is always you, the current Mario. What player a index points to is different for each player
- A global index is the index of each player globally. What a player's global index is is the same between all players. `0` is always the server. The server's local index is equivalent to the global index

## Converting Between Local and Global Indexes

The modding api has 2 functions called `network_global_index_from_local` and `network_local_index_from_global`. These functions allows you to convert indexes to global and local indexes. An example usage of these would be:

```lua
local function send_winner_to_players(globalIndex)
    ...
end

local function set_winner(localIndex)
    -- create a table that will have the time of the winner and the global index
    local winner = {
        globalIndex = network_global_index_from_local(localIndex)
        time = gPlayerSyncTable[localIndex].time
    }

    send_winner_to_players(winner)
end
```

You can also grab both the `localIndex` and `globalIndex` from a `NetworkPlayer`:

```lua
local send_warped_to_secret_act(globalIndex)
    ...
end

local function on_warp(...)
    ---@type NetworkPlayer
    local np = gNetworkPlayers[0]

    if np.currActNum == 12 then
        send_warped_to_secret_act(np.globalIndex)
    end
end

hook_event(HOOK_ON_WARP, on_warp)
```
