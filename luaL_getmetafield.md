# luaL_getmetafield

This will be dumped with the help of luaB offsets we found (search string "_VERSION" go to the only xref and decompile code:
There you will see this line (3rd line in the table)
  sub_4B69E30(a1, a2: &off_603A3C8, a3: &off_6BBE0A0);)

So. to get luaL_callmeta locate:
```c
.rdata:0000000006BBE0E0                 dq offset aGetmetatable ; "getmetatable"
.rdata:0000000006BBE0E8                 dq offset sub_4B7DAC0
```
Double click the sub_RVA and decompile:
```c
        break;
    }
    if ( v8 != 0 )
    {
      *(_QWORD *)v6 = v8;
      *(_DWORD *)(v6 + 12) = 7;
      *(_QWORD *)(a1 + 72) += 16LL;
      sub_93E0C0(a1, a2: 1, a3: &qword_6B5F4C0); // <-- luaL_getmetafield
      return 1;
    }
    if ( v6 + 16 <= **(_QWORD **)(a1 + 88) || (unsigned int)sub_937DA0(a1, a2: 1) != 0 )
    {
```

So the offset is 0x93E0C0
