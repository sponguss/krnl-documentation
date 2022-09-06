# Get Nil Instances
```lua
<table> getnilinstances()
```
Returns a table of all instances parented to nil

---

_This function is added at the KRNL init script using this code_
```lua
local list={}
for _, instance in pairs(getinstances()) do
    if (not instance.Parent) then
        table.insert(list,instance)
    end
end
return list
```