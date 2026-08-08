# lua_setfield

Sets a field in a table: value at top of stack → table[idx].key.

Inlined in this build. Composed from smaller ops:

```c
void lua_setfield(lua_State* L, int idx, const char* k) {
    lua_pushstring(L, k);    // push key
    lua_insert(L, -2);       // move key below value
    lua_settable(L, idx);    // table[k] = value
}
```

# luaL_register

Registers a library of functions into a table. Takes (L, libname, func_table).

Inlined in this build. Composed as:

```c
void luaL_register(lua_State* L, const char* libname, const luaL_Reg* l) {
    luaL_newmetatable(L, libname);
    lua_pushvalue(L, -1);
    lua_setfield(L, -2, "__index");
    for (; l->name; l++) {
        lua_pushcfunction(L, l->func);
        lua_setfield(L, -2, l->name);
    }
}
```
