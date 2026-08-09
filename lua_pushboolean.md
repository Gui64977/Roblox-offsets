# lua_pushboolean
# INLINED
Pushes a boolean value (true/false) onto the stack.

Found through luaB_rawequal. Search `"newproxy"` xref find, `"rawequal"`:
```asm
.rdata:00000000061F5AD0                 dq offset aRawequal     ; "rawequal"
.rdata:00000000061F5AD8                 dq offset sub_4153A60
```

Double click the RVA and decompile:


```c
__int64 __fastcall sub_4153A60(__int64 a1)
{
  unsigned __int64 v2; // rcx
  unsigned __int64 v3; // r10
  void *v4; // rdx
  __int64 v5; // r10
  int v6; // edi
  _DWORD *v7; // rdx

  v2 = *(_QWORD *)(a1 + 96);
  v3 = *(_QWORD *)(a1 + 72);
  if ( v2 >= v3 || (_UNKNOWN *)v2 == &unk_610B898 || *(_DWORD *)(v2 + 12) == -1 )
    sub_93C490(a1, a2: (__int64)&aInsufficientPe_5[-666448], 1);
  v4 = (void *)(v2 + 16);
  if ( v2 + 16 >= v3 || v4 == &unk_610B898 || *(_DWORD *)(v2 + 28) == -1 )
    sub_93C490(a1, a2: (__int64)&aInsufficientPe_5[-666448], 2);
  v6 = sub_976FC0(a1: v2, a2: v4);
  if ( (unsigned __int64)(v5 + 16) > **(_QWORD **)(a1 + 88) && (unsigned int)sub_937DA0((_QWORD *)a1, a2: 1) == 0 )
  {
    sub_977900(a1, a2: (__int64)"stack overflow");
    sub_93A2B0(a1);
  }
  v7 = *(_DWORD **)(a1 + 72);
  *v7 = v6 != 0;
  v7[3] = 1;
  *(_QWORD *)(a1 + 72) += 16LL;
  return 1;
}
```

Formula: `*(int*)L->top = (value != 0); *(L->top + 12) = 1; L->top += 16;`

Tag 1 = boolean.
