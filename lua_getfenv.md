# lua_getfenv

To find lua_getfenv search string "newproxy", first xref:
```asm
.rdata:0000000006DF4458 aNewproxy       db 'newproxy',0         ; DATA XREF: .rdata:00000000061F5AB0↑o
```
Find getfenv:
```asm
.rdata:00000000061F5A80                 dq offset aGetfenv      ; "getfenv"
.rdata:00000000061F5A88                 dq offset sub_4153770
```
Double click the rva and decompile

```c
__int64 __fastcall sub_4153770(__int64 a1)
{
  __int64 v2; // rax
  char v3; // al
  __int64 v4; // rcx

  sub_4152F40(a1, a2: 1);
  v2 = *(_QWORD *)(a1 + 72);
  if ( *(_DWORD *)(v2 - 4) == 8 && *(_BYTE *)(*(_QWORD *)(v2 - 16) + 3LL) != 0 )
  {
    v3 = *(_BYTE *)(a1 + 1);
    if ( (v3 & 4) != 0 )
    {
      v4 = *(_QWORD *)(a1 + 112);
      *(_BYTE *)(a1 + 1) = v3 & 0xFB;
      *(_QWORD *)(a1 + 56) = *(_QWORD *)(v4 + 64);
      *(_QWORD *)(v4 + 64) = a1;
    }
    if ( (unsigned __int64)(*(_QWORD *)(a1 + 72) + 16LL) > **(_QWORD **)(a1 + 88)
      && (unsigned int)sub_937DA0((_QWORD *)a1, a2: 1) == 0 )
    {
      sub_977900(a1, a2: (__int64)"stack overflow");
      sub_93A2B0(a1);
    }
    *(_OWORD *)*(_QWORD *)(a1 + 72) = *(_OWORD *)sub_937C00((_QWORD *)a1, a2: -10002);
    *(_QWORD *)(a1 + 72) += 16LL;
  }
  else
  {
    sub_9392C0(a1); // <-- lua_getfenv
  }
  *(_BYTE *)(*(_QWORD *)(*(_QWORD *)(a1 + 72) - 16LL) + 6LL) = 0;
  return 1;
}
```

So the offset is 0x9392C0
