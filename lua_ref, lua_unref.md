# lua_ref / lua_unref

## lua_ref

Search `"[FLog::Error] Exception caught during ModuleScript reference weakening. {}"`:
```asm
.rdata:0000000006CA72A0 aFlogErrorExcep_0 db '[FLog::Error] Exception caught during ModuleScript reference weak'
.rdata:0000000006CA72A0                                         ; DATA XREF: sub_5C43680+2F↑o
.rdata:0000000006CA72E1                 db 'ening. {}',0
.rdata:0000000006CA72EB ; _BYTE algn_6CA72EB[]
.rdata:0000000006CA72EB algn_6CA72EB:
.rdata:0000000006CA72EB                 align 4
.rdata:0000000006CA72EC word_6CA72EC    dw 766Bh                ; DATA XREF: sub_23034E0+574↑r
```
For some reason it's placed really weirdly, double click sub_23034E0, decompile it and scroll all the way down:
```c
  }
  v148[0] = v107;
  HIDWORD(v148[1]) = 6;
  sub_958BE0(a1: v2, a2: v103, a3: (int *)v148, a4: (int *)(*(_QWORD *)(v2 + 72) - 16LL));
  v135 = *(_QWORD *)(v2 + 72) - 16LL;
  *(_QWORD *)(v2 + 72) = v135;
  *(_BYTE *)(*(_QWORD *)(v135 - 16) + 5LL) = 1;
  *(_DWORD *)(v92 + 28) = sub_93A810(a1: (_QWORD *)v2, a2: 0xFFFFFFFFLL); // <-- lua_ref
  *(_QWORD *)(v2 + 72) -= 16LL;
  if ( __eh34_catch(0) )
  {
catch_state_0:
    if ( __eh34_catch_type(0, &std::exception `RTTI Type Descriptor', &v151) )
    {
      if ( (unsigned __int8)qword_7A85F90 >= 6u && BYTE1(qword_7A85F90) >= 3u )
      {
        *(_QWORD *)&v152 = "[FLog::Error] Exception caught during ModuleScript reference weakening. {}";
        v137 = (*(__int64 (__fastcall **)(const std::exception *))(*(_QWORD *)v151 + 8LL))(a1: v151);
        v147[0] = "[FLog::Error] Exception caught during ModuleScript reference weakening. {}";
        v139 = -1;
        do
          ++v139;
        while ( aFlogErrorExcep_0[v139] != 0 );
```
```c
    return;
  }
  __eh34_exit_try_state(0, -1);
  v136 = *(unsigned int *)(v92 + 24);
  if ( byte_81735F8 != 0 )
  {
    *(_DWORD *)(v92 + 24) = sub_93A990(a1: v2, a2: v136); // <-- lua_unref
  }
  else
  {
    sub_93A990(a1: v2, a2: v136); // <-- lua_unref
    *(_DWORD *)(v92 + 24) = -1;
  }
}
```
