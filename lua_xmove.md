# lua_xmove

Moves values between Lua threads.

Find coroutine.create via `"isyieldable"` -> xref -> find "create" near "running":
```asm
.rdata:00000000061F662F                 db    0
.rdata:00000000061F6630 off_61F6630     dq offset aCreate_1     ; DATA XREF: sub_4176EC0+6↑o
.rdata:00000000061F6630                                         ; "create"
.rdata:00000000061F6638                 dq offset sub_4175B90   ; // <-- decompile this
.rdata:00000000061F6640                 dq offset aRunning_1    ; "running"
.rdata:00000000061F6648                 dq offset sub_4176390
.rdata:00000000061F6650                 dq offset dword_6B442B0
.rdata:00000000061F6658                 dq offset sub_4174500
.rdata:00000000061F6660                 dq offset aWrap_0       ; "wrap"
.rdata:00000000061F6668                 dq offset sub_41760D0
.rdata:00000000061F6670                 dq offset aYield        ; "yield"
.rdata:00000000061F6678                 dq offset sub_4176330
.rdata:00000000061F6680                 dq offset aIsyieldable  ; "isyieldable"
.rdata:00000000061F6688                 dq offset sub_4176400
.rdata:00000000061F6690                 dq offset aClose_0      ; "close"
.rdata:00000000061F6698                 dq offset sub_4176480
```

Decompile:

```c
        v29 = *(_QWORD *)(a1 + 72);
        *(_QWORD *)v29 = v11;
        *(_DWORD *)(v29 + 12) = 10;
        *(_QWORD *)(a1 + 72) += 16LL;
        v30 = *(void (__fastcall **)(__int64, __int64))(*(_QWORD *)(a1 + 112) + 1328LL);
        if ( v30 != nullptr )
          v30(a1, a2: v11);
        sub_938580(a1, a2: v11, a3: 1);
        return 1;
      }
    }
  }
  sub_945D80(a1, a2: 4u); // <-- double click this
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
