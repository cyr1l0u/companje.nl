---
title: Lua
---

=====check args=====
```lua
if (table.getn(arg) == 0) then
    print("Usage: ./print-fetch {printerSocket} {remoteURL} {id}")
    return
end
```

=====Sample code=====
http://lua-users.org/wiki/SampleCode

=====Doodle3D publish-wifibox-release.lua "This script requires the Penlight library"=====
  export LUA_CPATH=/opt/local/share/luarocks/lib/lua/5.2/?.so
  export LUA_PATH=/opt/local/share/luarocks/share/lua/5.2/?.lua

=====use the luarocks package manager to install a package / library=====
<code>sudo luarocks install luasocket</code>

=====where are the LUA packages / libraries=====
<code>
print(package.path.."
"..package.cpath)
</code>

===== Luv it =====
Nodejs maar dan voor lua