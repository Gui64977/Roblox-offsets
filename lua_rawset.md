# lua_rawset (C API)

Does a raw table set without invoking metamethods.

Inlined into luaB_rawset (0x41540C0). Find via luaB offsets guide: search `"newproxy"`, xref:
```asm
.rdata:0000000006DF4458 aNewproxy       db 'newproxy',0         ; DATA XREF: .rdata:00000000061F5AB0↑o
```
Formula:
```c
void lua_rawset(L, int t_idx) {
    TValue* table = luaA_toobject(L, t_idx);  // 0x937CC0
    TValue* key   = luaA_toobject(L, -2);     // key at top-2
    TValue* val   = luaA_toobject(L, -1);     // value at top-1
    
    sub_958BE0(L, table, key, val);  // luaH_set — table set
    L->top -= 32;                     // pop key and value
}
```

Inlined logic:
```c
LABEL_320:
  *(_OWORD *)j = *(_OWORD *)(v201 - 16);
  v170 = *(_QWORD *)(a1 + 72);
  if ( *(int *)(v170 - 4) >= 6 && (*(_BYTE *)(*v9 + 1) & 4) != 0 )
  {
    v171 = *(_QWORD *)(v170 - 16);
    if ( (*(_BYTE *)(v171 + 1) & 3) != 0 )
      sub_94C450(a1, a2: *v9, a3: v171, a4);
  }
  *(_QWORD *)(a1 + 72) -= 32LL;
  return 1;
}
```

