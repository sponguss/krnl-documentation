# Hook Metamethod
```lua
<function> hookmetamethod(instance: Instance, metamethod: string, new: function)
```
Hooks the `metamethod` of `instance`'s metatable with `new`

The original function is returned when using `hookmetamethod`

---

`Example`
```lua
local old
old=hookmetamethod(game, "__namecall", function(self, ...)
    if typeof(self)=="RemoteEvent" and getnamecallmethod():lower()=="fireserver" then
        print(
            ("Remote Name: %s\nArguments: %s\nCalling Script: %s"):format(self.Name, table.concat({...}, ", "), (getcallingscript()~=nil and getcallingscript():GetFullName() or ""))
        )
        -- Lets say you also want to block this remote, for that you should return nil
        return nil
    end
    return old(self, ...)
end)
```

_`Instance.new("RemoteEvent"):FireServer("hello", false) will return "Remote Name: RemoteEvent\nArguments: hello, false\nCalling Script: "`_

---

| Metamethod | Description                                               |
|------------|-----------------------------------------------------------|
| __namecall | Fires when a function is called                           |
| __index    | Fires when a script is trying to index a value            |
| __newindex | Fires when a script tries to change the value of an index |