# luaM_new
# luaM_realloc_
Raw GC allocator — calls G->frealloc to allocate a block, then initializes the block header.

**Find**: from luaB_newproxy string "newproxy":
```asm
.rdata:0000000006DF4458 aNewproxy       db 'newproxy',0         ; DATA XREF: .rdata:00000000061F5AB0↑o
```

Double click RVA and then double click the sub_ it puts you on:
```c
  {
    LOBYTE(v3) = 1;
    sub_94BEC0(a1, a2: v3);
  }
  v6 = *(_BYTE *)(a1 + 1);
  if ( (v6 & 4) != 0 )
  {
    v7 = *(_QWORD *)(a1 + 112); // <-- lua_state encryption
    *(_BYTE *)(a1 + 1) = v6 & 0xFB;
    *(_QWORD *)(a1 + 56) = *(_QWORD *)(v7 + 64);
    *(_QWORD *)(v7 + 64) = a1;
  }
  if ( (unsigned __int64)(*(_QWORD *)(a1 + 72) + 16LL) > **(_QWORD **)(a1 + 88)
    && (unsigned int)sub_937DA0((_QWORD *)a1, a2: 1) == 0 )
  {
    goto LABEL_72;
  }
  v8 = nullptr;
  v9 = *(unsigned __int8 *)(a1 + 6);
  v10 = *(_QWORD *)(a1 + 112);
  if ( byte_7A2DDA0 < 0 )
  {
    v16 = (_DWORD *)sub_954490(a1, a2: (int)v10 + 800, a3: 80, a4: 16, a5: 1); // <-- luaM_new
    v14 = v16 + 16;
    v16[12] -= v16[9];
    ++v16[13];
  }
  else
  {
    v11 = 8LL * byte_7A2DDA0;
    v12 = *(_QWORD *)(v11 + v10 + 424);
    if ( v12 == 0 )
      v12 = sub_954540(a1, a2: (int)v10 + 424, a3: (int)v10 + 800, a4: byte_7A2DDA0, a5: 0);
    v13 = *(int *)(v12 + 48);
    if ( (int)v13 < 0 )
    {
```

Double click sub_954540:

```c
_QWORD *__fastcall sub_954540(L, QWORD **head, QWORD **page_anchor, u8 cat, u8 item_flag)
{
  v8 = 16360;                          // page size
  v9 = dword_7A2DCF0[cat];             // item size for category
  if (v9 > 512) v8 = 32744;            // bigger page for large items
  result = sub_954490(L, page_anchor, v8, v9 + 8*item_flag, (v8-64)/(v9+8*item_flag));
  *(QWORD*)(a2 + 8*cat) = result;      // save page in category list
  return result;
}
```

Offset: **0x954540**

It's inlined... im gay
```c
if ( byte_7A2DDA0 < 0 )   // no freelist for this type
{
    // Call the low‑level allocator
    v16 = (_DWORD *)sub_954490(
             a1,                     // L (lua_State*)
             (int)v10 + 800,         // a2 = G + 800 (allocator anchor)
             80,                      // a3 = size class (category) – 80 for userdata
             16,                      // a4 = block size in bytes (here 16 for minimal Udata)
             1 );                     // a5 = flag (1 = alloc new block)
    // v16 points to internal block header; real object starts at +16
    v14 = v16 + 16;                  // v14 = Udata* (the actual GC object)
    v16[12] -= v16[9];               // update free‑block counter?
    ++v16[13];                       // bump allocation count
}
```

That's everything i can give u though
