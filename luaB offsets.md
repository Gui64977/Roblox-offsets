# luaB offsets (base library functions)

All base library function.

Search string (shift f12) `"xpcall"` go to xref, decompile:

```c
sub_4158D10:  // luaopen_base - registers all base functions
```

Inside you'll find the registration table with {name, func} pairs:

```asm
rdata:00000000061F56B0                                         ; "concat"
.rdata:00000000061F56B8                 dq offset sub_414B680
.rdata:00000000061F56C0                 dq offset aForeach_0    ; "foreach"
.rdata:00000000061F56C8                 dq offset sub_4147A90
.rdata:00000000061F56D0                 dq offset aForeachi     ; "foreachi"
.rdata:00000000061F56D8                 dq offset sub_4146DD0
.rdata:00000000061F56E0                 dq offset aGetn         ; "getn"
.rdata:00000000061F56E8                 dq offset sub_4148E00
.rdata:00000000061F56F0                 dq offset aMaxn         ; "maxn"
.rdata:00000000061F56F8                 dq offset sub_4148B40
.rdata:00000000061F5700                 dq offset aInsert_0     ; "insert"
.rdata:00000000061F5708                 dq offset sub_4149EB0
.rdata:00000000061F5710                 dq offset aRemove_0     ; "remove"
.rdata:00000000061F5718                 dq offset sub_414A0B0
.rdata:00000000061F5720                 dq offset aSort         ; "sort"
.rdata:00000000061F5728                 dq offset sub_414D720
.rdata:00000000061F5730                 dq offset aPack_2       ; "pack"
.rdata:00000000061F5738                 dq offset sub_414B9A0
.rdata:00000000061F5740                 dq offset aUnpack       ; "unpack"
.rdata:00000000061F5748                 dq offset sub_414C180
.rdata:00000000061F5750                 dq offset aMove_0       ; "move"
.rdata:00000000061F5758                 dq offset sub_414A420
.rdata:00000000061F5760                 dq offset aCreate_1     ; "create"
.rdata:00000000061F5768                 dq offset sub_414D8A0
.rdata:00000000061F5770                 dq offset aFind         ; "find"
.rdata:00000000061F5778                 dq offset sub_414E030
.rdata:00000000061F5780                 dq offset aClear_0      ; "clear"
.rdata:00000000061F5788                 dq offset sub_414E570
.rdata:00000000061F5790                 dq offset aFreeze       ; "freeze"
.rdata:00000000061F5798                 dq offset sub_414E5C0
.rdata:00000000061F57A0                 dq offset aIsfrozen_0   ; "isfrozen"
.rdata:00000000061F57A8                 dq offset sub_414E710
.rdata:00000000061F57B0                 dq offset aClone_0      ; "clone"
.rdata:00000000061F57B8                 dq offset sub_414E7C0
.rdata:00000000061F57D0 off_61F57D0     dq offset aCreate_1     ; DATA XREF: sub_4151570+1C↑o
.rdata:00000000061F57D0                                         ; "create"
.rdata:00000000061F57D8                 dq offset sub_414F260
.rdata:00000000061F57E0                 dq offset aTonumber     ; "tonumber"
.rdata:00000000061F57E8                 dq offset sub_414F600
.rdata:00000000061F57F0                 dq offset aNeg          ; "neg"
.rdata:00000000061F57F8                 dq offset sub_414F6B0
.rdata:00000000061F5800                 dq offset aAdd_0        ; "add"
.rdata:00000000061F5808                 dq offset sub_414F700
.rdata:00000000061F5810                 dq offset aSub          ; "sub"
.rdata:00000000061F5818                 dq offset sub_414F780
.rdata:00000000061F5820                 dq offset aMul          ; "mul"
.rdata:00000000061F5828                 dq offset sub_414F800
.rdata:00000000061F5830                 dq offset aDiv          ; "div"
.rdata:00000000061F5838                 dq offset sub_414F880
.rdata:00000000061F5840                 dq offset aMin_0        ; "min"
.rdata:00000000061F5848                 dq offset sub_414FD40
.rdata:00000000061F5850                 dq offset aMax_0        ; "max"
.rdata:00000000061F5858                 dq offset sub_414FE70
.rdata:00000000061F5860                 dq offset aRem          ; "rem"
.rdata:00000000061F5868                 dq offset sub_414FA50
.rdata:00000000061F5870                 dq offset aIdiv         ; "idiv"
.rdata:00000000061F5878                 dq offset sub_414F960
.rdata:00000000061F5880                 dq offset aUdiv         ; "udiv"
.rdata:00000000061F5888                 dq offset sub_414FC00
.rdata:00000000061F5890                 dq offset aUrem         ; "urem"
.rdata:00000000061F5898                 dq offset sub_414FCA0
.rdata:00000000061F58A0                 dq offset aMod_0        ; "mod"
.rdata:00000000061F58A8                 dq offset sub_414FB10
.rdata:00000000061F58B0                 dq offset aClamp_0      ; "clamp"
.rdata:00000000061F58B8                 dq offset sub_41511E0
.rdata:00000000061F58C0                 dq offset aBand         ; "band"
.rdata:00000000061F58C8                 dq offset sub_414FFA0
.rdata:00000000061F58D0                 dq offset aBor          ; "bor"
.rdata:00000000061F58D8                 dq offset sub_41500A0
.rdata:00000000061F58E0                 dq offset aBnot         ; "bnot"
.rdata:00000000061F58E8                 dq offset sub_4150190
.rdata:00000000061F58F0                 dq offset aBxor         ; "bxor"
.rdata:00000000061F58F8                 dq offset sub_41501E0
.rdata:00000000061F5900                 dq offset unk_6BD78AC
.rdata:00000000061F5908                 dq offset sub_41502D0
.rdata:00000000061F5910                 dq offset aLe_0         ; "le"
.rdata:00000000061F5918                 dq offset sub_41503E0
.rdata:00000000061F5920                 dq offset aUlt          ; "ult"
.rdata:00000000061F5928                 dq offset sub_41504F0
.rdata:00000000061F5930                 dq offset aUle          ; "ule"
.rdata:00000000061F5938                 dq offset sub_4150600
.rdata:00000000061F5940                 dq offset aGt_0         ; "gt"
.rdata:00000000061F5948                 dq offset sub_4150710
.rdata:00000000061F5950                 dq offset aGe           ; "ge"
.rdata:00000000061F5958                 dq offset sub_4150820
.rdata:00000000061F5960                 dq offset aUgt          ; "ugt"
.rdata:00000000061F5968                 dq offset sub_4150930
.rdata:00000000061F5970                 dq offset aUge          ; "uge"
.rdata:00000000061F5978                 dq offset sub_4150A40
.rdata:00000000061F5980                 dq offset aLshift_0     ; "lshift"
.rdata:00000000061F5988                 dq offset sub_4150B50
.rdata:00000000061F5990                 dq offset aRshift_0     ; "rshift"
.rdata:00000000061F5998                 dq offset sub_4150BF0
.rdata:00000000061F59A0                 dq offset aArshift      ; "arshift"
.rdata:00000000061F59A8                 dq offset sub_4150C90
.rdata:00000000061F59B0                 dq offset aLrotate      ; "lrotate"
.rdata:00000000061F59B8                 dq offset sub_4150D70
.rdata:00000000061F59C0                 dq offset aRrotate      ; "rrotate"
.rdata:00000000061F59C8                 dq offset sub_4150E00
.rdata:00000000061F59D0                 dq offset aExtract      ; "extract"
.rdata:00000000061F59D8                 dq offset sub_4150E90
.rdata:00000000061F59E0                 dq offset aReplace      ; "replace"
.rdata:00000000061F59E8                 dq offset sub_4151010
.rdata:00000000061F59F0                 dq offset aBtest        ; "btest"
.rdata:00000000061F59F8                 dq offset sub_41512C0
.rdata:00000000061F5A00                 dq offset aCountrz      ; "countrz"
.rdata:00000000061F5A08                 dq offset sub_41513C0
.rdata:00000000061F5A10                 dq offset aCountlz      ; "countlz"
.rdata:00000000061F5A18                 dq offset sub_4151420
.rdata:00000000061F5A20                 dq offset aBswap        ; "bswap"
.rdata:00000000061F5A28                 dq offset sub_4151490
.rdata:00000000061F5A30                 dq offset aFromstring_0 ; "fromstring"
.rdata:00000000061F5A38                 dq offset sub_414F370
.rdata:00000000061F5A50 off_61F5A50     dq offset aAssert_0     ; DATA XREF: sub_4158D10+44C↑o
.rdata:00000000061F5A50                                         ; "assert"
.rdata:00000000061F5A58                 dq offset sub_4157330
.rdata:00000000061F5A60                 dq offset dword_6B46AD8
.rdata:00000000061F5A68                 dq offset sub_4152170
.rdata:00000000061F5A70                 dq offset aGcinfo       ; "gcinfo"
.rdata:00000000061F5A78                 dq offset sub_4155C30
.rdata:00000000061F5A80                 dq offset aGetfenv      ; "getfenv"
.rdata:00000000061F5A88                 dq offset sub_4153770
.rdata:00000000061F5A90                 dq offset aGetmetatable ; "getmetatable"
.rdata:00000000061F5A98                 dq offset sub_4152BB0
.rdata:00000000061F5AA0                 dq offset aNext_1       ; "next"
.rdata:00000000061F5AA8                 dq offset sub_4156880
.rdata:00000000061F5AB0                 dq offset aNewproxy     ; "newproxy"
.rdata:00000000061F5AB8                 dq offset sub_4157A30
.rdata:00000000061F5AC0                 dq offset aPrint_1      ; "print"
.rdata:00000000061F5AC8                 dq offset sub_4151D20
.rdata:00000000061F5AD0                 dq offset aRawequal     ; "rawequal"
.rdata:00000000061F5AD8                 dq offset sub_4153A60
.rdata:00000000061F5AE0                 dq offset aRawget       ; "rawget"
.rdata:00000000061F5AE8                 dq offset sub_4153B70
.rdata:00000000061F5AF0                 dq offset aRawset       ; "rawset"
.rdata:00000000061F5AF8                 dq offset sub_41540C0
.rdata:00000000061F5B00                 dq offset aRawlen       ; "rawlen"
.rdata:00000000061F5B08                 dq offset sub_4155B90
.rdata:00000000061F5B10                 dq offset aSelect_1     ; "select"
.rdata:00000000061F5B18                 dq offset sub_41573E0
.rdata:00000000061F5B20                 dq offset aSetfenv      ; "setfenv"
.rdata:00000000061F5B28                 dq offset sub_4153830
.rdata:00000000061F5B30                 dq offset aSetmetatable ; "setmetatable"
.rdata:00000000061F5B38                 dq offset sub_4152D30
.rdata:00000000061F5B40                 dq offset aTonumber     ; "tonumber"
.rdata:00000000061F5B48                 dq offset sub_4151DF0
.rdata:00000000061F5B50                 dq offset aTostring_0   ; "tostring"
.rdata:00000000061F5B58                 dq offset sub_41579D0
.rdata:00000000061F5B60                 dq offset aType         ; "type"
.rdata:00000000061F5B68                 dq offset sub_4155C50
.rdata:00000000061F5B70                 dq offset aTypeof       ; "typeof"
.rdata:00000000061F5B78                 dq offset sub_4156260
.rdata:00000000061F5B90 off_61F5B90     dq offset dword_6B88954 ; DATA XREF: sub_415C2D0+6↑o
.rdata:00000000061F5B98                 dq offset sub_415BA40
.rdata:00000000061F5BA0                 dq offset aCodepoint    ; "codepoint"
.rdata:00000000061F5BA8                 dq offset sub_415AEE0
.rdata:00000000061F5BB0                 dq offset aChar         ; "char"
.rdata:00000000061F5BB8                 dq offset sub_415B280
.rdata:00000000061F5BC0                 dq offset aLen_0        ; "len"
.rdata:00000000061F5BC8                 dq offset sub_415AC00
.rdata:00000000061F5BD0                 dq offset aCodes        ; "codes"
.rdata:00000000061F5BD8                 dq offset sub_415BF90


```

Scroll through the function to find more. The data table at 0x61F58B8 contains the full `{string_ptr, func_ptr}` array.
