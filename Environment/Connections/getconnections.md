# Get Connections
```lua
<Connection> getconnections(signal: RBXScriptSignal)
```
Returns a table of all connections to `signal`

`Connection Object`
| Index      | Description                                                                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .Function  | Returns a function value type, which is the function connected to the signal, when this is ran by executing the function, every single function connected to the signal will be fired |
| :Enable    | If the connection was disabled, it'll allow it to be used again                                                                                                                       |
| :Disable   | Disables the connection, so that it doesn't run the connected function even after firing the signal                                                                                   |
| :Fire(...) | Fires the signal with specific arguments, or no arguments at all                                                                                                                      |