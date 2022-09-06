# Get Instance Cache
```lua
<table> getinstancecache()
```
When the game is loaded, KRNL looks for a table with all the instances within the cache inside of the Lua registry and put's the table in a variable, which its value can then be obtained by using this function

I dont really know what you could use this for

---

_This function is added at the KRNL init script using this code_
```lua
local instances
for key, value in pairs(getreg()) do
    if (type(key) == "userdata" and type(value) == "table" and rawget(value, "__mode")) then
        instances = value
        break
    end
end

getgenv().getinstancecache=function() return instances end
```