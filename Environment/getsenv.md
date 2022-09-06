# Get Script Environment
```lua
<table> getsenv(script: LocalScript|ModuleScript)
```
Scripts have environment variables, which are special variables that normally cannot be changed and that can only be used at that script, for example, there's the environment variable "script"
```lua
print(getsenv(workspace.LocalScript).script) -- Outputs: game:GetService("workspace").script
```
