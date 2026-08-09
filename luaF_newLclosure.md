# luaF_newLclosure

Creates a new Lua closure from a Proto object. Found inside luau_load.

Use pattern or sum, it got inlined 😞:

```c
// Inline luaF_newLclosure inside luau_load:
*(BYTE*)cl = 8;                    // GC tag = function
*((BYTE*)cl + 1) = white_flags;    // marked
*((BYTE*)cl + 2) = memcat;         // memory category
*((QWORD*)cl + 1) = proto;         // VMValue encoded: cl+8 = proto - (cl+8)
*((QWORD*)cl + 2) = 0;             // stacksize = 0
*((QWORD*)cl + 3) = 0;             // preload = 0
*((BYTE*)cl + 3) = isVariadic;     // variadic flag
// upvalues initialized to NULL
for (i = 0; i < proto->nups; i++)
    cl->upvals[i] = NULL;
*(QWORD*)stack_top = cl;           // push onto stack
*(DWORD*)(stack_top + 12) = 8;     // TValue tag
stack_top += 16;
```

Key: GC alloc via sub_954490, tag 8 = function, Proto pointer VMValue encoded.
