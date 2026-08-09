# GetCapabilities

Returns capability flags for a ScriptContext based on execution state.

Search `"Callbacks cannot yield"` -> xref -> sub_22FC990. Decompile, find:

```c
      v32 = v93;
      if ( v24 == 0 )
        v32 = nullptr;
    }
    __unwind
    {
      sub_2C9ACF0();
    }
    sub_22FA7B0(a1: v31, a2: (unsigned int)&v77, a3: (unsigned int)&v63, a4: v23, a5: v24, a6: (__int64)v32); // <-- Double click this 
    if ( v77 == 1 )
    {
      sub_225CD60(a1: v6);
      sub_2C9D040(a1: "Callbacks cannot yield");
    }
    if ( v77 == 2 )
    {
      sub_225CD60(a1: v6);
      v58 = sub_222B620(a1: v19);
      sub_7B3E80(a1: v96, a2: v58);
      __wind
      {
```

Double click sub_22FA7B0. find:

```c
  if ( v15 != 0 && (v17 = *(_QWORD *)(v15 + 40)) != 0 )
    v18 = *(_QWORD *)(v17 + 32);
  else
    v18 = 0;
  v126 = v18;
  if ( byte_8178A38 != 0 )
  {
    v18 = v126;
    if ( *(_BYTE *)(v13 + 290) != 0 && (sub_8EB520(a1: (_DWORD *)(v126 + 48)) & 8) == 0 ) // <-- getcapabilities
    {
      if ( *a3 != 0 && (v19 = *(_QWORD *)(*a3 + 40)) != 0 )
        v20 = *(_QWORD *)(v19 + 32);
      else
        v20 = 0;
      v21 = sub_21EF430(a1: *(_QWORD *)(*(_QWORD *)(v20 + 24) + 16LL));
      if ( v21 != 0 )
      {
        v22 = sub_232B390(a1: v21 + 456);
        if ( v22 != 0 )
        {
          if ( *a3 != 0 )
            v23 = *(_QWORD *)(*a3 + 40);
          else
            LODWORD(v23) = 0;
          sub_240C630(a1: v22, a2: v23, a3: v122, a4: a5, a5: v131);
        }
      }
      *(_DWORD *)a2 = 1;
      *(_QWORD *)(a2 + 8) = 0;
      *(_DWORD *)(a2 + 16) = 0;
      if ( v10 >= 0x400 )
      {
        if ( byte_7E95465 != 0 && byte_81DCB28 != 0 )
          sub_2C9AD80(a1: 0, a2: (__int64)"invalid memory category"); // <-- kinda anchor
        goto LABEL_247;
      }
      goto LABEL_298;
    }
  }
  if ( __eh34_unwind(2) )
unwind_state_2:
    sub_2C9ACF0();
  __eh34_exit_wind_state(2, -1);
  __eh34_enter_wind_state(-1, 0);
  __eh34_enter_wind_state(0, 3);
  __eh34_enter_wind_state(3, 4);
```

Check if u want:

```c
__int64 __fastcall sub_1408EB520(_DWORD *a1)
{
  __int64 result; // rax

  switch ( *a1 )
  {
    case 1:
    case 4:
      result = 0x2000000000000003LL;
      break;
    case 3:
      result = 0x300000000000000BLL;
      break;
    case 5:
      result = 0x2000000000000001LL;
      break;
    case 6:
      result = 0x700000000000000BLL;
      break;
    case 7:
    case 8:
      result = 0x200000000000003FLL;
      break;
    case 9:
    case 0xD:
      result = 12;
      break;
    case 0xA:
      result = 0x6000000000000003LL;
      break;
    case 0xB:
      result = 0x2000000000000000LL;
      break;
    case 0xC:
      result = 0x1000000000000000LL;
      break;
    default:
      result = 0;
      break;
  }
  return result;
}
```

Offset: **0x8EB520**
