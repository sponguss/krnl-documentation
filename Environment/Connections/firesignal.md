# Fire Signal
```lua
<nil> firesignal(signal: RBXScriptSignal, ...)
```
Fires a signal using specific arguments

_This is equivalent to_
```lua
for _, connection in pairs(getconnections(signal)) do
    connection.Function(...)
end
```