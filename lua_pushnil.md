# lua_pushnil

To find lua_pushnil search string "getmetatable" go to xref:
```asm
.rdata:0000000006DF44A0 aGetmetatable   db 'getmetatable',0     ; DATA XREF: .rdata:00000000061F5A90↑o
```
double click RVA then find:
```c
.rdata:00000000061F5A90                 dq offset aGetmetatable ; "getmetatable"
.rdata:00000000061F5A98                 dq offset sub_4152BB0
```

Double click RVA and decompile:
```c
  if ( top + 16 <= stack_limit || sub_937DA0(L, 1) != 0 ) {
    *(DWORD*)(*(QWORD*)(a1 + 72) + 12) = 0;  // <-- lua_pushnil: set tag = 0
    *(QWORD*)(a1 + 72) += 16;                 // increment top
    return 1;
  }
```

It got inlined. Formula: `*(DWORD*)(L->top + 12) = 0; L->top += 16;`
