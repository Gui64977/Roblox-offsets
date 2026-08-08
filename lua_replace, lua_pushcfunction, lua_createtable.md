# lua_replace / lua_createtable / lua_pushcfunction

## lua_replace

Moves the top value to a given index, replacing whatever was there.

Can be found via "getfenv" string and choose first .rdata xref:
```asm
.rdata:0000000006CA7840 aGetfenv        db 'getfenv',0          ; DATA XREF: sub_2418F90+58↑o
.rdata:0000000006CA7840                                         ; .rdata:00000000061F5A80↑o ...
```

Double click the RVA:
```asm
.rdata:00000000061F5A80                 dq offset aGetfenv      ; "getfenv"
.rdata:00000000061F5A88                 dq offset sub_4153770
```

```c
      sub_977900(a1, a2: (__int64)"stack overflow");
      sub_93A2B0(a1);
    }
    *(_OWORD *)*(_QWORD *)(a1 + 72) = *(_OWORD *)sub_937C00(a1, a2: 4294957294LL); // <-- lua_replace
    *(_QWORD *)(a1 + 72) += 16LL;
  }
  else
  {
    sub_9392C0(a1);
  }
  *(_BYTE *)(*(_QWORD *)(*(_QWORD *)(a1 + 72) - 16LL) + 6LL) = 0;
  return 1;
}
```

## lua_createtable

Creates a new empty table. Find through luaB_newproxy. Search `"newproxy"`:
```asm
.rdata:00000000061F5AB0                 dq offset aNewproxy     ; "newproxy"
.rdata:00000000061F5AB8                 dq offset sub_4157A30
```

Double click sub_4157A30
Function inlined 😞
```c
      {
        *(_QWORD *)(v24 + 88) += 48LL;
        *(_QWORD *)(v24 + 8 * v23 + 11312) += 48LL;
        v31 = *(void (__fastcall **)(__int64, _QWORD, __int64))(v24 + 1336);
        if ( v31 != nullptr )
          v31(a1, a2: 0, a3: 48);
        v32 = *(_BYTE *)(*(_QWORD *)(a1 + 112) + 16LL);
        *(_BYTE *)v28 = 7;
        *((_BYTE *)v28 + 1) = v32 & 3;
        *((_BYTE *)v28 + 2) = *(_BYTE *)(a1 + 6);
        *((_QWORD *)v28 + 2) = &unk_610B760;
        *((_QWORD *)v28 + 5) = 0;
        v28[1] = -16777216;
        *((_QWORD *)v28 + 3) = 0;
        *((_QWORD *)v28 + 1) = 0;
        *((_BYTE *)v28 + 3) = 0;
        *(_QWORD *)v22 = v28;
        *(_DWORD *)(v22 + 12) = 7;
        *(_QWORD *)(a1 + 72) += 16LL;
        v33 = *(_QWORD *)(a1 + 72);
        if ( *(_DWORD *)(v33 - 4) != 0 )
          v8 = *(unsigned __int8 **)(v33 - 16);
        v34 = *(_DWORD *)(v33 - 20);
        if ( v34 == 7 )
        {
          v35 = *(_QWORD *)(v33 - 32);
          if ( *(_BYTE *)(v35 + 5) != 0 )
            sub_9782F0(a1);
          *(_QWORD *)(v35 + 40) = v8;
```

The table is allocated via sub_954490 with 48 bytes (sizeof(Table) with 0 array/hash). For custom sizes, same allocator with narr*16 + nrec*32.

## lua_pushcfunction

Pushes a C function onto the stack. Calls lua_pushcclosure internally.

```c
void lua_pushcfunction(L, lua_CFunction fn) {
    lua_pushcclosure(L, fn, 0);
}
```

See lua_pushcclosure guide for the full alloc/fill logic.
