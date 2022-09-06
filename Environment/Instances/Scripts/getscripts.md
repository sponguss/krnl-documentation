# Get Scripts
```lua
<table> getscripts()
```
Returns a table with all of the LocalScript(s) and ModuleScript(s) in-game

---

_A similar thing to this could be done using this code_
```lua
local function GetScripts()
    local list={}
    table.foreach(getinstances(), function(_, script)
        if typeof(script)=="ModuleScript" or typeof(script)=="LocalScript" then
            table.insert(list, script)
        end
    end)
    return list
end
```