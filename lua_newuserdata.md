# lua_newuserdata

Creates a new full userdata and pushes it onto the stack. Returns pointer to data area.

Inlined into sub_4178800 (class constructor, right after luaopen_bit32 at 0x41787D0). Find:

Search `"bit32"`, first xref: 
```asm
.rdata:0000000006DF5064 aBit32          db 'bit32',0            ; DATA XREF: sub_41787D0+B↑o
```

Double click the RVA but don't decompile, look down:
```asm
.text:00000000041787DB                 lea     rdx, aBit32     ; "bit32" <-- YOU'RE HERE
.text:00000000041787E2                 call    sub_93F570
.text:00000000041787E7                 mov     eax, 1
.text:00000000041787EC                 add     rsp, 28h
.text:00000000041787F0                 retn
.text:00000000041787F0 sub_41787D0     endp
.text:00000000041787F0
.text:00000000041787F0 ; ---------------------------------------------------------------------------
.text:00000000041787F1 algn_41787F1:                           ; DATA XREF: seg005:0000000008CE19F0↓o
.text:00000000041787F1                 align 20h
.text:0000000004178800
.text:0000000004178800 ; =============== S U B R O U T I N E =======================================
.text:0000000004178800
.text:0000000004178800
.text:0000000004178800 ; void *__fastcall sub_4178800(__int64, __int64)
.text:0000000004178800 sub_4178800     proc near               ; CODE XREF: sub_411FEF0+47↑p <-- DECOMPILE THIS
.text:0000000004178800                                         ; sub_41211B0+74↑p
.text:0000000004178800                                         ; DATA XREF: ...
.text:0000000004178800
.text:0000000004178800 var_B8          = dword ptr -0B8h
```

Full inlined function (lines ~280 to ~343, basically after that long int and qword list):
```c
  v2 = &off_61F6870;
  result = &off_61F67B0;
  if ( byte_7AA7E00 == 0 )
    v2 = &off_61F67B0;
  v272 = -1;
  v257 = v2;
  v284 = 22500;
  v5 = v2[1];
  if ( v5 != 0 )
  {
    while ( 1 )
    {
      if ( *(_QWORD *)(*(_QWORD *)(a1 + 112) + 88LL) >= *(_QWORD *)(*(_QWORD *)(a1 + 112) + 80LL) )
      {
        LOBYTE(a2) = 1;
        sub_94BEC0(a1, a2);
      }
      v6 = *(_BYTE *)(a1 + 1);
      if ( (v6 & 4) != 0 )
      {
        v7 = *(_QWORD *)(a1 + 112);
        *(_BYTE *)(a1 + 1) = v6 & 0xFB;
        *(_QWORD *)(a1 + 56) = *(_QWORD *)(v7 + 64);
        *(_QWORD *)(v7 + 64) = a1;
      }
      v8 = *(_QWORD *)(a1 + 72);
      if ( (unsigned __int64)(v8 + 16) > **(_QWORD **)(a1 + 88) )
      {
        if ( ((v8 - *(_QWORD *)(a1 + 96)) >> 4) + 1 > 8000 )
          goto LABEL_438;
        if ( *(_QWORD *)(a1 + 104) - v8 <= 16 )
        {
          v266 = 1;
          if ( (unsigned int)sub_945D50(a1, a2: sub_937E70, a3: &v266) != 0 )
            goto LABEL_438;
        }
        v9 = *(unsigned __int64 **)(a1 + 88);
        v10 = *(_QWORD *)(a1 + 72) + 16LL;
        if ( *v9 < v10 )
          *v9 = v10;
      }
      v11 = *(_QWORD *)(a1 + 88);
      if ( v11 == *(_QWORD *)(a1 + 24) )
        v12 = *(_QWORD *)(a1 + 8);
      else
        v12 = *(_QWORD *)(**(_QWORD **)(v11 + 24) + 16LL);
      v13 = *(unsigned __int8 *)(a1 + 6);
      v14 = *(_QWORD *)(a1 + 112);
      if ( byte_7A2DDC8 < 0 )
      {
        v21 = (__int64 *)(v14 + 800);
        v22 = (*(__int64 (__fastcall **)(_QWORD, _QWORD, _QWORD, __int64))(v14 + 24))(
                a1: *(_QWORD *)(v14 + 32),
                a2: 0,
                a3: 0,
                a4: 120);
        v23 = v22;
```

```c
*(BYTE*)v14 = 9;                // GC tag = userdata
*((BYTE*)v14 + 1) = v18 & 3;    // marked flag
*((BYTE*)v14 + 2) = *(a1 + 6);  // memcat
v14[1] = 0;                     // tag = 0
*((QWORD*)v14 + 1) = -(v14 + 8); // metatable = NULL (VMValue encoded)
*((BYTE*)v14 + 3) = 0x81;       // isLuau flag
*(QWORD*)v19 = v14;             // push object
*(DWORD*)(v19 + 12) = 9;        // TValue tag
*(QWORD*)(a1 + 72) += 16;       // increment top
```

```c
void* lua_newuserdata(L, size_t sz) {
    // GC step + barrier
    sub_94BEC0(L, 1);
    sub_93A2B0(L);
    
    Udata* u = luaM_new(L, sizeof(Udata) + sz);
    *u = 9;                         // GC tag = userdata
    *(u + 1) = G->white & 3;        // marked
    *(u + 2) = L->memcat;
    u->metatable = NULL;
    u->len = sz;
    u->tag = 0;
    
    *L->top = u;
    *(L->top + 12) = 9;             // TValue tag
    L->top += 16;
    
    return (void*)(u + 1);          // data after header
}
```

Tag 9 = userdata. Udata header: GC (16b) + metatable (8b) + len (8b) + tag (4b)
