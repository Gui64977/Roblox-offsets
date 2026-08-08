# coroutineL offsets

All coroutine library function offsets.

Search string (shift f12) `"isyieldable"` -> xref -> you're at the coroutine registration table at 0x61F6630:

```c
.rdata:00000000061F62B0                                         ; "create"
.rdata:00000000061F62B8                 dq offset sub_416FB60
.rdata:00000000061F62C0                 dq offset aFromstring_0 ; "fromstring"
.rdata:00000000061F62C8                 dq offset sub_416FC10
.rdata:00000000061F62D0                 dq offset aTostring_0   ; "tostring"
.rdata:00000000061F62D8                 dq offset sub_416FCE0
.rdata:00000000061F62E0                 dq offset aReadi8       ; "readi8"
.rdata:00000000061F62E8                 dq offset sub_41719B0
.rdata:00000000061F62F0                 dq offset aReadu8       ; "readu8"
.rdata:00000000061F62F8                 dq offset sub_4171B10
.rdata:00000000061F6300                 dq offset aReadi16      ; "readi16"
.rdata:00000000061F6308                 dq offset sub_4171C70
.rdata:00000000061F6310                 dq offset aReadu16      ; "readu16"
.rdata:00000000061F6318                 dq offset sub_4171DD0
.rdata:00000000061F6320                 dq offset aReadi32      ; "readi32"
.rdata:00000000061F6328                 dq offset sub_4171F30
.rdata:00000000061F6330                 dq offset aReadu32      ; "readu32"
.rdata:00000000061F6338                 dq offset sub_4172090
.rdata:00000000061F6340                 dq offset aReadf32      ; "readf32"
.rdata:00000000061F6348                 dq offset sub_41721F0
.rdata:00000000061F6350                 dq offset aReadf64      ; "readf64"
.rdata:00000000061F6358                 dq offset sub_4172350
.rdata:00000000061F6360                 dq offset aWritei8      ; "writei8"
.rdata:00000000061F6368                 dq offset sub_41724B0
.rdata:00000000061F6370                 dq offset aWriteu8      ; "writeu8"
.rdata:00000000061F6378                 dq offset sub_41724B0
.rdata:00000000061F6380                 dq offset aWritei16     ; "writei16"
.rdata:00000000061F6388                 dq offset sub_4172630
.rdata:00000000061F6390                 dq offset aWriteu16     ; "writeu16"
.rdata:00000000061F6398                 dq offset sub_4172630
.rdata:00000000061F63A0                 dq offset aWritei32     ; "writei32"
.rdata:00000000061F63A8                 dq offset sub_41727B0
.rdata:00000000061F63B0                 dq offset aWriteu32     ; "writeu32"
.rdata:00000000061F63B8                 dq offset sub_41727B0
.rdata:00000000061F63C0                 dq offset aWritef32     ; "writef32"
.rdata:00000000061F63C8                 dq offset sub_4172930
.rdata:00000000061F63D0                 dq offset aWritef64     ; "writef64"
.rdata:00000000061F63D8                 dq offset sub_4172AC0
.rdata:00000000061F63E0                 dq offset aReadstring   ; "readstring"
.rdata:00000000061F63E8                 dq offset sub_41704C0
.rdata:00000000061F63F0                 dq offset aWritestring  ; "writestring"
.rdata:00000000061F63F8                 dq offset sub_4170BA0
.rdata:00000000061F6400                 dq offset aLen_0        ; "len"
.rdata:00000000061F6408                 dq offset sub_4170E40
.rdata:00000000061F6410                 dq offset aCopy_0       ; "copy"
.rdata:00000000061F6418                 dq offset sub_4170EF0
.rdata:00000000061F6420                 dq offset aFill_0       ; "fill"
.rdata:00000000061F6428                 dq offset sub_41711E0
.rdata:00000000061F6430                 dq offset aReadbits     ; "readbits"
.rdata:00000000061F6438                 dq offset sub_4171430
.rdata:00000000061F6440                 dq offset aWritebits    ; "writebits"
.rdata:00000000061F6448                 dq offset sub_4171670
.rdata:00000000061F6450                 align 20h
.rdata:00000000061F6460 off_61F6460     dq offset aCreate_1     ; DATA XREF: sub_4171970+12↑o
.rdata:00000000061F6460                                         ; "create"
.rdata:00000000061F6468                 dq offset sub_416FB60
.rdata:00000000061F6470                 dq offset aFromstring_0 ; "fromstring"
.rdata:00000000061F6478                 dq offset sub_416FC10
.rdata:00000000061F6480                 dq offset aTostring_0   ; "tostring"
.rdata:00000000061F6488                 dq offset sub_416FCE0
.rdata:00000000061F6490                 dq offset aReadi8       ; "readi8"
.rdata:00000000061F6498                 dq offset sub_41719B0
.rdata:00000000061F64A0                 dq offset aReadu8       ; "readu8"
.rdata:00000000061F64A8                 dq offset sub_4171B10
.rdata:00000000061F64B0                 dq offset aReadi16      ; "readi16"
.rdata:00000000061F64B8                 dq offset sub_4171C70
.rdata:00000000061F64C0                 dq offset aReadu16      ; "readu16"
.rdata:00000000061F64C8                 dq offset sub_4171DD0
.rdata:00000000061F64D0                 dq offset aReadi32      ; "readi32"
.rdata:00000000061F64D8                 dq offset sub_4171F30
.rdata:00000000061F64E0                 dq offset aReadu32      ; "readu32"
.rdata:00000000061F64E8                 dq offset sub_4172090
.rdata:00000000061F64F0                 dq offset aReadf32      ; "readf32"
.rdata:00000000061F64F8                 dq offset sub_41721F0
.rdata:00000000061F6500                 dq offset aReadf64      ; "readf64"
.rdata:00000000061F6508                 dq offset sub_4172350
.rdata:00000000061F6510                 dq offset aWritei8      ; "writei8"
.rdata:00000000061F6518                 dq offset sub_41724B0
.rdata:00000000061F6520                 dq offset aWriteu8      ; "writeu8"
.rdata:00000000061F6528                 dq offset sub_41724B0
.rdata:00000000061F6530                 dq offset aWritei16     ; "writei16"
.rdata:00000000061F6538                 dq offset sub_4172630
.rdata:00000000061F6540                 dq offset aWriteu16     ; "writeu16"
.rdata:00000000061F6548                 dq offset sub_4172630
.rdata:00000000061F6550                 dq offset aWritei32     ; "writei32"
.rdata:00000000061F6558                 dq offset sub_41727B0
.rdata:00000000061F6560                 dq offset aWriteu32     ; "writeu32"
.rdata:00000000061F6568                 dq offset sub_41727B0
.rdata:00000000061F6570                 dq offset aWritef32     ; "writef32"
.rdata:00000000061F6578                 dq offset sub_4172930
.rdata:00000000061F6580                 dq offset aWritef64     ; "writef64"
.rdata:00000000061F6588                 dq offset sub_4172AC0
.rdata:00000000061F6590                 dq offset aReadstring   ; "readstring"
.rdata:00000000061F6598                 dq offset sub_41704C0
.rdata:00000000061F65A0                 dq offset aWritestring  ; "writestring"
.rdata:00000000061F65A8                 dq offset sub_4170BA0
.rdata:00000000061F65B0                 dq offset aLen_0        ; "len"
.rdata:00000000061F65B8                 dq offset sub_4170E40
.rdata:00000000061F65C0                 dq offset aCopy_0       ; "copy"
.rdata:00000000061F65C8                 dq offset sub_4170EF0
.rdata:00000000061F65D0                 dq offset aFill_0       ; "fill"
.rdata:00000000061F65D8                 dq offset sub_41711E0
.rdata:00000000061F65E0                 dq offset aReadbits     ; "readbits"
.rdata:00000000061F65E8                 dq offset sub_4171430
.rdata:00000000061F65F0                 dq offset aWritebits    ; "writebits"
.rdata:00000000061F65F8                 dq offset sub_4171670
.rdata:00000000061F6600                 dq offset aReadinteger  ; "readinteger"
.rdata:00000000061F6608                 dq offset sub_4170270
.rdata:00000000061F6610                 dq offset aWriteinteger ; "writeinteger"
.rdata:00000000061F6618                 dq offset sub_4170380
.rdata:00000000061F6630 off_61F6630     dq offset aCreate_1     ; DATA XREF: sub_4176EC0+6↑o
.rdata:00000000061F6630                                         ; "create"
.rdata:00000000061F6638                 dq offset sub_4175B90
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
.rdata:00000000061F66B0 off_61F66B0     dq offset aArshift      ; DATA XREF: sub_41787D0+4↑o
.rdata:00000000061F66B0                                         ; "arshift"
.rdata:00000000061F66B8                 dq offset sub_4177EF0
.rdata:00000000061F66C0                 dq offset aBand         ; "band"
.rdata:00000000061F66C8                 dq offset sub_4177960
.rdata:00000000061F66D0                 dq offset aBnot         ; "bnot"
.rdata:00000000061F66D8                 dq offset sub_4177C10
.rdata:00000000061F66E0                 dq offset aBor          ; "bor"
.rdata:00000000061F66E8                 dq offset sub_4177A10
.rdata:00000000061F66F0                 dq offset aBxor         ; "bxor"
.rdata:00000000061F66F8                 dq offset sub_4177B10
.rdata:00000000061F6700                 dq offset aBtest        ; "btest"
.rdata:00000000061F6708                 dq offset sub_4177990
.rdata:00000000061F6710                 dq offset aExtract      ; "extract"
.rdata:00000000061F6718                 dq offset sub_41782B0
.rdata:00000000061F6720                 dq offset aLrotate      ; "lrotate"
.rdata:00000000061F6728                 dq offset sub_41780E0
.rdata:00000000061F6730                 dq offset aLshift_0     ; "lshift"
.rdata:00000000061F6738                 dq offset sub_4177CA0
.rdata:00000000061F6740                 dq offset aReplace      ; "replace"
.rdata:00000000061F6748                 dq offset sub_4178370
.rdata:00000000061F6750                 dq offset aRrotate      ; "rrotate"
.rdata:00000000061F6758                 dq offset sub_4178160
.rdata:00000000061F6760                 dq offset aRshift_0     ; "rshift"
.rdata:00000000061F6768                 dq offset sub_4177DC0
.rdata:00000000061F6770                 dq offset aCountlz      ; "countlz"
.rdata:00000000061F6778                 dq offset sub_41784B0
.rdata:00000000061F6780                 dq offset aCountrz      ; "countrz"
.rdata:00000000061F6788                 dq offset sub_4178600
.rdata:00000000061F6790                 dq offset aByteswap     ; "byteswap"
.rdata:00000000061F6798                 dq offset sub_4178740
.rdata:00000000061F67B0 off_61F67B0     dq offset Source        ; DATA XREF: sub_4178800+25↑o
.rdata:00000000061F67B8                 dq offset sub_4158D10
.rdata:00000000061F67C0                 dq offset aCoroutine    ; "coroutine"
.rdata:00000000061F67C8                 dq offset sub_4176EC0
.rdata:00000000061F67D0                 dq offset aTable        ; "table"
.rdata:00000000061F67D8                 dq offset sub_414E8B0
.rdata:00000000061F67E0                 dq offset aOs_1         ; "os"
.rdata:00000000061F67E8                 dq offset sub_415EE70
.rdata:00000000061F67F0                 dq offset aString       ; "string"
.rdata:00000000061F67F8                 dq offset sub_4168BF0
.rdata:00000000061F6800                 dq offset aMath         ; "math"
.rdata:00000000061F6808                 dq offset sub_416E040
.rdata:00000000061F6810                 dq offset aDebug_0      ; "debug"
.rdata:00000000061F6818                 dq offset sub_41744D0
.rdata:00000000061F6820                 dq offset aUtf8         ; "utf8"
.rdata:00000000061F6828                 dq offset sub_415C2D0
.rdata:00000000061F6830                 dq offset aBit32        ; "bit32"
.rdata:00000000061F6838                 dq offset sub_41787D0
.rdata:00000000061F6840                 dq offset aBuffer_0     ; "buffer"
.rdata:00000000061F6848                 dq offset sub_4171970
.rdata:00000000061F6850                 dq offset aVector_0     ; "vector"
.rdata:00000000061F6858                 dq offset sub_416A6B0
.rdata:00000000061F6870 off_61F6870     dq offset Source        ; DATA XREF: sub_4178800+1E↑o
.rdata:00000000061F6878                 dq offset sub_4158D10
.rdata:00000000061F6880                 dq offset aCoroutine    ; "coroutine"
.rdata:00000000061F6888                 dq offset sub_4176EC0
.rdata:00000000061F6890                 dq offset aTable        ; "table"
.rdata:00000000061F6898                 dq offset sub_414E8B0
.rdata:00000000061F68A0                 dq offset aOs_1         ; "os"
.rdata:00000000061F68A8                 dq offset sub_415EE70
.rdata:00000000061F68B0                 dq offset aString       ; "string"
.rdata:00000000061F68B8                 dq offset sub_4168BF0
.rdata:00000000061F68C0                 dq offset aMath         ; "math"
.rdata:00000000061F68C8                 dq offset sub_416E040
.rdata:00000000061F68D0                 dq offset aDebug_0      ; "debug"
.rdata:00000000061F68D8                 dq offset sub_41744D0
.rdata:00000000061F68E0                 dq offset aUtf8         ; "utf8"
.rdata:00000000061F68E8                 dq offset sub_415C2D0
.rdata:00000000061F68F0                 dq offset aBit32        ; "bit32"
.rdata:00000000061F68F8                 dq offset sub_41787D0
.rdata:00000000061F6900                 dq offset aBuffer_0     ; "buffer"
.rdata:00000000061F6908                 dq offset sub_4171970
.rdata:00000000061F6910                 dq offset aVector_0     ; "vector"
.rdata:00000000061F6918                 dq offset sub_416A6B0
.rdata:00000000061F6920                 dq offset aInteger      ; "integer"

```

coroutine.resume is registered separately — find it via `"coroutine"` string -> xref -> the registration function, just above the table.
