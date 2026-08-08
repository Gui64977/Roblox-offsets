# lua_pushvalue

Pushes a copy of the value at the given index onto the stack.

Inlined in this build. luaB_getfenv (0x4153770) uses:

```c
*L->top = *sub_937C00(L, -2);  // copy value from index
L->top += 16;
```

The formula:
```c
void lua_pushvalue(L, int idx) {
    TValue* slot = sub_937C00(L, idx);  // 0x937C00
    *L->top = *slot;                     // copy 16 bytes
    L->top += 16;
}
```
