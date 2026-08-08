# lua_xmove

Moves values between Lua threads.

Find coroutine.create via `"isyieldable"` -> xref -> scroll to 0x4175B90. Decompile it:

```c
__int64 __fastcall sub_4175B90(L, ...)
{
  ...
  *(_BYTE *)v11 = 10;                    // tag = thread
  // ... allocate and init new thread ...
  sub_938580(a1, v11, 1);               // <-- lua_xmove(L_main, L_new, 1)
  return 1;
}
```

Double click `sub_938580`:

```c
_OWORD *__fastcall sub_938580(L_from, L_to, int idx)
{
  // barrier check on L_to
  if (idx <= 0) {
    if (idx <= -10000) slot = pseudoaddr(L_from, idx);
    else slot = L_from->top + 16*idx;
  } else {
    slot = nilobject;
    if (L_from->base + 16*idx - 16 < L_from->top)
      slot = L_from->base + 16*idx - 16;
  }
  *L_to->top = *slot;
  L_to->top += 16;
}
```

Takes (L_from, L_to, int idx). Moves the value at idx from L_from's stack to L_to's top.

Offset: **0x938580**
