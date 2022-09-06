# Get Global Environment
```lua
<table> getgenv()
```
Returns the global Roblox environment, meaning that it will set a global, For example:

## Script 1
```lua
getgenv().hi="Hello".. game.Players.LocalPlayer.Name .."!"
```

## Script 2
```lua
print(hi) -- Outputs: "Hello sponguss!"
```