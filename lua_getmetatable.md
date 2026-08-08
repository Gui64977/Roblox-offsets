# lua_getmetatable

Pushes the metatable of the object at the given index. Returns 1 if a metatable exists.

Inlined into luaB_getmetatable (0x4152BB0). The metatable lookup logic:

```c
int lua_getmetatable(L, int idx) {
    TValue* tv = luaA_toobject(L, idx);
    if (tv == NULL || tv->tt < 0) return 0;
    
    void* mt = NULL;
    switch (tv->tt) {
        case 7:  mt = tv->table->metatable; break;     // table
        case 9:  mt = tv->closure->env; break;          // function
        case 13: mt = tv->object->metatable; break;     // proxy
        default: mt = G->mt[tv->tt]; break;             // G + 0x440 + tag*8
    }
    if (mt == NULL) return 0;
    push_table(L, mt);
    return 1;
}
```

G->mt array at G + 0x440 (1088 decimal).
