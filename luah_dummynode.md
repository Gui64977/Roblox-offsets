# luah_dummynode

To find luah_dummynode search string "newproxy":
```asm
.rdata:0000000006DF4458 aNewproxy       db 'newproxy',0         ; DATA XREF: .rdata:00000000061F5AB0↑o
```
Double click rdata:
```asm
.rdata:00000000061F5AB0                 dq offset aNewproxy     ; "newproxy"
.rdata:00000000061F5AB8                 dq offset sub_4157A30
```
Double click rva:
```c
      if ( v28 != nullptr )
      {
        *(_QWORD *)(v24 + 88) += 48LL;
        *(_QWORD *)(v24 + 8 * v23 + 11312) += 48LL;
        v31 = *(void (__fastcall **)(__int64, _QWORD, __int64))(v24 + 1336);
        if ( v31 != nullptr )
          v31(a1, a2: 0, a3: 48);
        v32 = *(_BYTE *)(*(_QWORD *)(a1 + 112) + 16LL);
        *(_BYTE *)v28 = 7;
        *((_BYTE *)v28 + 1) = v32 & 3;
        *((_BYTE *)v28 + 2) = *(_BYTE *)(a1 + 6);
        *((_QWORD *)v28 + 2) = &unk_610B760; // <-- luah_dummynode (there's only 2 RVA's with unk_ suffix, if you cant find it just search for unk_ and flip a coin, i mean the lowest one is correct one)
        *((_QWORD *)v28 + 5) = 0;
        v28[1] = -16777216;
        *((_QWORD *)v28 + 3) = 0;
        *((_QWORD *)v28 + 1) = 0;
        *((_BYTE *)v28 + 3) = 0;
        *(_QWORD *)v22 = v28;
        *(_DWORD *)(v22 + 12) = 7;
        *(_QWORD *)(a1 + 72) += 16LL;
        v33 = *(_QWORD *)(a1 + 72);
        if ( *(_DWORD *)(v33 - 4) != 0 )
          v8 = *(unsigned __int8 **)(v33 - 16);
        v34 = *(_DWORD *)(v33 - 20);
        if ( v34 == 7 )
        {
          v35 = *(_QWORD *)(v33 - 32);
          if ( *(_BYTE *)(v35 + 5) != 0 )
            sub_9782F0(a1);
          *(_QWORD *)(v35 + 40) = v8;
```

So the offset is 0x610B760
