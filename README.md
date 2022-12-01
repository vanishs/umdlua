## umdlua (URL Module Definition of Lua)
this is a UMD Module and also is a UMD tool


### WHY UMD? 
----------------------------
- Using umd to write lua, you can directly reference modules written by others on the network in the code without pre-installation. like this(using tsort):
```lua
return require("umd").define({
    "exports",
    "github.com/vanishs/lua-resty-tsort-release001/lib/resty/tsort"
}, function(exports, tsort)
```
- You can package UMD Module (including the UMDs they refer to) into a single lua file. like this(package github.com/vanishs/umdluam2-tag1/main to single.lua):
```shell
umd.lua src single.lua github.com/vanishs/umdluam2-tag1/main
```
- You can package UMD Module and execute a function in a single lua file. like this(package github.com/vanishs/umdluam2-tag1/main to func1.lua and execute function func1)
```shell
umd.lua src func1 github.com/vanishs/umdluam2-tag1/main
```

### HOW TO WRITE A UMD?
----------------------------

- Modules of Lua (old way)
```lua
local m2={}
local m1=require("m1")
    function m2.func1()
        print("m2")
        m1.func1()
    end
return m2
```
- UMD of Lua
```lua
return require("umd").define({
    "exports",
    "m1",
}, function(m2, m1)
    function m2.func1()
        print("m2")
        m1.func1()
    end
end)
```

- [You can check out this commit to learn how to make old code changes](https://github.com/vanishs/lua-resty-tsort/commit/81a5634954be9bddcf1020f7a376f44bc297da36)

- "exports" is this module table.
- modname can be a URL. like: "github.com/vanishs/lua-resty-tsort-release001/lib/resty/tsort" . (release001 is a tag name)
### INSTALLATION
----------------------------
- Using LuaRocks
```shell
luarocks install umdlua
```
- copy amd.lua to lua search path
