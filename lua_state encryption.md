# lua_state encryption

The global_State pointer G is stored at `*(L + 0x28)` (hex) or `*(L + 40)` (decimal).

Find in any function that accesses G. Open lua_tolstring (0x93DB50) decompilation:

```c
if ( (unsigned __int64)(16LL * a2 + *(_QWORD *)(a1 + 96) - 16LL) < *(_QWORD *)(a1 + 72) )
      v6 = (_DWORD *)(16LL * a2 + *(_QWORD *)(a1 + 96) - 16LL);
  }
  if ( v6[3] != 6 )
  {
    v7 = *(_BYTE *)(a1 + 1);
    if ( (v7 & 4) != 0 )
    {
      v8 = *(_QWORD *)(a1 + 112); // <-- THIS IS THE ENCRYPTION OFFSET!!!!!
      *(_BYTE *)(a1 + 1) = v7 & 0xFB;
      *(_QWORD *)(a1 + 56) = *(_QWORD *)(v8 + 64);
      *(_QWORD *)(v8 + 64) = a1;
    }
    if ( (unsigned int)sub_956130(a1) == 0 )
    {
      if ( a3 != nullptr )
        *a3 = 0;
      goto LABEL_26;
```

Click on 112 once and press h, it'll become 0x70 which is the offset :D
