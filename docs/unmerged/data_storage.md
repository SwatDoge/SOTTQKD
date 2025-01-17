# Data storage

## Database <Badge type="tip" text="server-side" vertical="middle" />
**Tags: database**

Databases allow you to store variables permanently, without being able to be modified by others. Its useful for keeping track of currencies, personal best scores and what items a player owns. 


:::tip
To delete data storage values you can use `delete all` as a key
:::

:::warning
- Make sure to use player.accountName (server-side only) instead of player.username
- You can only store and access data from players who are active in game
- set, update, transact every 10 seconds per connection/player
- load every 5 seconds per connection/player
- 30 Keys per map, keys length is 20 characters. (Object properties are treated as unique database keys)
:::

### Set storage <Badge type="tip" text="server-side" vertical="middle" />
```krunkscript
# Set a player value to a specific value
GAME.STORAGE.set(
    "SwatDoge",                     # str accountName
    {kills: 300, nick: "Swat"},     # obj data
    true,                           # bool private (false: private, true: public) Public databases can be accessed by others
    callback                        # action(obj data, bool success, str accountName) callback function
);
```

### Update storage <Badge type="tip" text="server-side" vertical="middle" />
```krunkscript
# Updating ADDS the value you give it to the existing value. Negative values will thus be subtracted.
# Removing 5 kills from SwatDoge's kills
GAME.STORAGE.update(
    "SwatDoge",    # str accountName
    {kills: -5},   # obj data
    true,          # bool private (false: private, true: public) Public databases can be accessed by others
    callback       # action(obj data, bool success, str accountName) callback function
);
```

### Transact storage <Badge type="tip" text="server-side" vertical="middle" />
```krunkscript
# The same as GAME.STORAGE.update but you can not go below 0. If this does happen, the success parameter on the callback function will be false
GAME.STORAGE.transact(
    "SwatDoge",   # str accountName
    {kills: -5},  # obj data
    true,         # bool private (false: private, true: public) Public databases can be accessed by others
    callback      # action(obj data, bool success, str accountName) callback function
);
```

### Loading Data <Badge type="tip" text="server-side" vertical="middle" />

:::warning
Loading from an empty database will result in an error message "No data" and not call the callback
:::

```krunkscript
# Load data you stored on your map
GAME.STORAGE.load(
    "SwatDoge",     # str accountName
    "",             # str name of game with public database. (leave empty)
    callback        # action(obj data, bool success, str accountName) callback function
);
```

```krunkscript
# Load data you stored on another map
GAME.STORAGE.load(
    "SwatDoge",     # str accountName
    "lava_run",     # str name of game with public database. (leave empty)
    callback        # action(obj data, bool success, str accountName) callback function
);
```

## Cookies <Badge type="tip" text="client-side" vertical="middle" />
**Tags: localstorage**

Cookies allow you to store variables on a users browser. These variables can be modified by users and should not be relied on for source of truth.
Useful for settings.

:::warning
Cookies can only store strings as values
:::

```krunkscript
# Save cookie
GAME.COOKIES.save(
    "test",   # str name
    "100"     # str data
);
```

```krunkscript
# Load cookie
str value = GAME.COOKIES.load(
    "test"   # str name
);
```

```krunkscript
# Delete cookie
GAME.COOKIES.remove(
    "test"   # str name
);
```

```krunkscript
# Check if cookie exists
GAME.COOKIES.has(
    "test"    # str name
);
```
