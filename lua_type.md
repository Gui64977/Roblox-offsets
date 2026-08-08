# lua_type

Returns the type tag of the value at the given index.

Inline macro in this build:

```c
int lua_type(lua_State* L, int idx) {
    TValue* tv = luaA_toobject(L, idx);  // 0x937CC0
    if (tv == NULL || tv == &nilobject) return -1;
    return tv->tt;  // tag at offset +12
}
```

Tags in Roblox Luau:
- 0 = nil, 1 = boolean, 2 = lightuserdata, 3 = number
- 4 = integer, 5 = vector, 6 = string, 7 = table
- 9 = function, 10 = thread, 11 = userdata
