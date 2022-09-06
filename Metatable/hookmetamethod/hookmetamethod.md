# Hook Metamethod
```lua
<function> hookmetamethod(instance: Instance, metamethod: string, new: function, useArgGuard?=true)
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

---

_This function is added at the KRNL init script using this code_
```lua
getgenv().hookmetamethod=function(object, method, hook, useArgGuard)
    if useArgGuard == nil then useArgGuard = true end

    local metatable = getrawmetatable(object)

    assert(type(metatable) == "table",
        "invalid argument #1 to 'hookmetamethod' (object with metatable expected)")
    assert(type(method) == "string",
        string.format("invalid argument #2 to 'hookmetamethod' (string expected, got %s)", type(method)))
    assert(type(hook) == "function",
        string.format("invalid argument #3 to 'hookmetamethod' (function expected, got %s)", type(hook)))

    local hookMethod = metatable[method]
    assert(type(hookMethod) == "function",
        string.format("object does not have metamethod '%s'", method))

    if islclosure(hook) then hook = newcclosure(hook) end

    local needsArgs = (method == "__index" and 2) or (method == "__namecall" and 1) or (method == "__newindex" and 3) or 0

    local oldMethod

    if useArgGuard then
        local argHandler = newcclosure(function(...)
            if hasvoid(needsArgs, ...) then
                return oldMethod(...)
            end
            return hook(...)
        end)

        oldMethod = hookfunction(hookMethod, argHandler)
    else
        oldMethod = hookfunction(hookMethod, hook)
    end

    return oldMethod
end
```