# lua_pushcfunction / lua_pushcclosure

Push C function or C closure onto the stack.

Not standalone in this build. The allocator (`sub_94A480` or similar in your range) does:

```c
// lua_pushcfunction(L, fn) = lua_pushcclosure(L, fn, 0)
void lua_pushcclosure(L, lua_CFunction fn, int nup) {
    CClosure* cl = luaM_new(L, sizeof(CClosure) + nup*sizeof(TValue));
    cl->gc.tt = 8;                 // function tag
    cl->isLuau = 0;                // C function flag
    cl->f = fn;
    cl->nupvalues = nup;
    *L->top = cl;
    *(L->top + 12) = 8;           // tag
    L->top += 16;
    // wire upvalues if nup > 0
}
```

The GC object allocator is at `sub_954490` (small objects) or `sub_954650` (custom alloc). Tag 8 = function.
