# luau_execute

The Luau VM interpreter loop. Runs Lua bytecode.

**Step 1**: Search `"cannot resume non-suspended coroutine"` -> first xref -> lua_resume at 0x948D40.

**Step 2**: Press X on 0x948D40, find first and the only xref. Decompile it:

```c
__int64 __fastcall sub_948EF0(__int64 a1, __int64 a2, int a3)
{
  result = sub_948D40(a1, a2, a3);
  if (result == 0) {
    v7 = sub_945D50(a1, sub_946EE0, ...);
    return sub_948DF0(a1, v7, v6);    // double click sub_948DF0
  }
}
```

**Step 3**: Double click sub_948DF0. Find this:
```c
  _OWORD *v9; // r8
  unsigned __int64 *v11; // rax
  unsigned __int64 v12; // rcx

  for ( i = a2; i != 0; i = sub_945D50(a1, a2: sub_948390, a3: v6) ) // <-- double click sub_948390
  {
    v6 = sub_9476A0(a1);
    if ( v6 == 0 )
```

**Step 4**: Inside sub_948390, near the end:

```c
  *(_QWORD *)(a1 + 96) = *(_QWORD *)(v3 + 16);
  *(_QWORD *)v3 = *(_QWORD *)(a1 + 72);
  sub_9476D0(a1);
  result = ((__int64 (__fastcall *)(__int64, _QWORD))(v4 + 48 + *(_QWORD *)(v4 + 48)))(a1, a2: v5);
  if ( *(_BYTE *)(a1 + 3) == 0 )
  {
    sub_95E8D0(a1, a2: *(_QWORD *)(a1 + 72) - 16LL * (int)result);
    return sub_946DD0(a1); // <-- double click
  }
  return result;
}
```

**Step 5**: Double click sub_946DD0. Find:

```c
          else
            v11 = 1;
          *(_QWORD *)(*(_QWORD *)(a1 + 88) + 32LL) = v8 + 4LL * v11;
        }
      }
      if ( *(_BYTE *)(a1 + 4) != 0 )
        sub_95E970(a1); // <-- luau_execute (interpreter)
      else
        sub_96AB60(a1); // compiled code path
    }
  }
  return result;
}
```

Copy sub_95E970 and jump to it: 

```asm
.text:000000000095E970 var_360         = xmmword ptr -360h
.text:000000000095E970 var_350         = xmmword ptr -350h
.text:000000000095E970 var_340         = xmmword ptr -340h
.text:000000000095E970 var_330         = qword ptr -330h
.text:000000000095E970 var_328         = dword ptr -328h
.text:000000000095E970 var_320         = xmmword ptr -320h
.text:000000000095E970 var_310         = xmmword ptr -310h
.text:000000000095E970 var_300         = xmmword ptr -300h
.text:000000000095E970 var_2F0         = xmmword ptr -2F0h
.text:000000000095E970 var_2E0         = xmmword ptr -2E0h
.text:000000000095E970 var_2D0         = xmmword ptr -2D0h
.text:000000000095E970 var_2C0         = qword ptr -2C0h
.text:000000000095E970 var_2B8         = dword ptr -2B8h
.text:000000000095E970 Buf1            = byte ptr -2B0h
.text:000000000095E970 var_38          = byte ptr -38h
.text:000000000095E970 arg_0           = qword ptr  10h
.text:000000000095E970 arg_8           = qword ptr  18h
.text:000000000095E970 arg_10          = qword ptr  20h
.text:000000000095E970 arg_18          = word ptr  28h
.text:000000000095E970
.text:000000000095E970                 mov     rax, rsp ; <-- you'll be put here
```
Scroll up until you see **second** subroutine:
```asm
.text:000000000095E8C0 ; =============== S U B R O U T I N E =======================================
.text:000000000095E8C0
.text:000000000095E8C0
.text:000000000095E8C0 ; __int64 __fastcall sub_95E8C0(__int64, __int64, __int64, unsigned __int64)
.text:000000000095E8C0 sub_95E8C0      proc near               ; CODE XREF: sub_95E970+8C51↓p ; <-- luau_execute (sub_95E8C0)
.text:000000000095E8C0                                         ; sub_95E970+95F1↓p ...
.text:000000000095E8C0                 cmp     byte ptr [rcx+4], 0
.text:000000000095E8C4                 jnz     sub_95E970
.text:000000000095E8CA                 jmp     sub_96AB60
.text:000000000095E8CA sub_95E8C0      endp 			; <-- luau_execute
.text:000000000095E8CA
.text:000000000095E8CA ; ---------------------------------------------------------------------------
.text:000000000095E8CF                 align 10h
.text:000000000095E8D0
.text:000000000095E8D0 ; =============== S U B R O U T I N E =======================================
.text:000000000095E8D0
.text:000000000095E8D0
.text:000000000095E8D0 ; __int64 __fastcall sub_95E8D0(_QWORD, _QWORD)
.text:000000000095E8D0 sub_95E8D0      proc near               ; CODE XREF: sub_946DD0+84↑p
.text:000000000095E8D0                                         ; sub_946EE0+6FA↑p ...
.text:000000000095E8D0
.text:000000000095E8D0 arg_0           = qword ptr  8
.text:000000000095E8D0 arg_8           = qword ptr  10h
.text:000000000095E8D0
.text:000000000095E8D0                 mov     [rsp+arg_0], rbx
```


Offset: **0x95E8C0**
