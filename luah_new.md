# luaH_new

**ITS INLINED**

Creates a new Lua table with narray array slots and nhash node slots.

Inlined into luaB_newproxy (0x4157A30). Find it: search `"newproxy"`:
```asm
.rdata:0000000006DF4458 aNewproxy       db 'newproxy',0         ; DATA XREF: .rdata:00000000061F5AB0↑o
```
Dobule click .rdata:00000000 wtv the fuck it ends with
```asm
.rdata:00000000061F5AB0                 dq offset aNewproxy     ; "newproxy"
.rdata:00000000061F5AB8                 dq offset sub_4157A30
```
double click sub_4157A30 and decompile:

```c
*v28 = 7;                        // GC tag = table
*((_BYTE *)v28 + 1) = v32 & 3;   // GC marked flags
*((_BYTE *)v28 + 2) = v6;        // GC memcat
*((_QWORD *)v28 + 2) = &unk_610B760;  // node = dummynode (0x610B760)
*((_QWORD *)v28 + 5) = 0;        // metatable = NULL
v28[1] = -16777216;              // packed flags and sizearray init
*((_QWORD *)v28 + 3) = 0;        // lastfree = NULL
*((_QWORD *)v28 + 1) = 0;        // flags = 0
*((_BYTE *)v28 + 3) = 0;         // lsizenode = 0
*(_QWORD *)v22 = v28;            // push onto stack
*(_DWORD *)(v22 + 12) = 7;       // TValue tag = table
*(_QWORD *)(a1 + 72) += 16;      // increment stack top
```

If existing metatable:
```c
v8 = *(unsigned __int8 **)(top - 16);  // the metatable value
if (v34 == 7) {                         // if tag = table
    v35 = *(QWORD *)(top - 32);         // table pointer
    if (*(BYTE *)(v35 + 5) != 0)       // readonly check
        sub_9782F0(a1);                 // readonly error
    *(QWORD *)(v35 + 40) = v8;          // set table->metatable
}
```

Allocator: sub_954490. dummynode: 0x610B760. Tag 7 = table. Table size: 48 bytes (no array/hash).
