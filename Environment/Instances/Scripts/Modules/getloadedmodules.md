# Get Loaded Modules
```lua
<table> getloadedmodules()
```
Returns a table of all ModuleScripts that are loaded in the game.

---

_This function is added at the KRNL init script using this code_
```lua
local old=getloadedmodules
getgenv().getloadedmodules=function()
    local filteredModules={}
    for _,obj in pairs(old()) do
        if (obj:IsDescendantOf(CoreGui) or obj:IsDescendantOf(CorePackages)) then continue end
        table.insert(filteredModules, obj)
    end
    return filteredModules
end
```