# lua_objlen

To find lua_objlen search string "rawlen" go to find xref and decompile:
```asm
.rdata:0000000006DF442C aRawlen         db 'rawlen',0           ; DATA XREF: .rdata:00000000061F5B00↑o
```
Find 3rd sub in the table and double click off_6BBE0A0, find:
```asm
.rdata:00000000061F5B00                 dq offset aRawlen       ; "rawlen"
.rdata:00000000061F5B08                 dq offset sub_4155B90
```
Double click sub_4155B90, decompile:
```c
__int64 __fastcall sub_4155B90(__int64 a1)
{
  _QWORD *v1; // rdx
  int v3; // eax

  v1 = *(_QWORD **)(a1 + 96);
  if ( (unsigned __int64)v1 >= *(_QWORD *)(a1 + 72)
    || v1 == (_QWORD *)&unk_610B898
    || (unsigned int)(*((_DWORD *)v1 + 3) - 6) > 1 )
  {
    sub_93B840(a1, a2: 1u, a3: (__int64)&aErrorInUgcvali_75[-655704]);
  }
  switch ( *((_DWORD *)v1 + 3) )
  {
    case 6:
      v3 = *(_DWORD *)(*v1 + 20LL);
      break;
    case 7:
      v3 = sub_953BC0(a1: *v1);
      break;
    case 9:
    case 0xB:
      v3 = *(_DWORD *)(*v1 + 4LL);
      break;
    default:
      v3 = 0;
      break;
  }
  sub_938E80(a1, a2: v3);
  return 1;
}
```

Got inlined 😞
