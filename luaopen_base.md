# luaopen_base

Registers all base library functions (_G, assert, error, print, etc).

Search `"xpcall"` -> xref -> sub_4158D10. This is luaopen_base:
```asm
.rdata:0000000006DF441C aXpcall         db 'xpcall',0           ; DATA XREF: sub_4158D10+1610↑o
.rdata:0000000006DF441C                                         ; sub_4158D10+1837↑r ...
```

```c
__int64 __fastcall sub_4158D10(__int64 a1)
```

Same function as luaB offsets guide - it registers every luaB_ function.

Alternatively: search `"rawget"` -> xref in the base table -> scroll up to find the function that references the whole table.

Offset: **0x4158D10**
