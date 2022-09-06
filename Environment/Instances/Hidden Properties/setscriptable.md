# Set Scriptable
```lua
<nil> setscriptable(object: Instance, property: string, scriptable: bool)
```
---
`Example`
```lua
setscriptable(game:GetService("Lighting"), "Technology", true)
game:GetService("Lighting").Technology=true -- Works perfectly without using sethiddenproperty
```

---
_Non-scriptable properties are also hidden properties_