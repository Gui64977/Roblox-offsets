# lua_tothread

To find lua_tothread we'll use already known offset lua_pushnumber which in my case is at 0x938E80 jump to it and look up:
```asm 
.text:0000000000938E72
.text:0000000000938E72 loc_938E72:                             ; CODE XREF: sub_938E20+49↑j
.text:0000000000938E72                 mov     rax, [rax]
.text:0000000000938E75                 add     rsp, 28h
.text:0000000000938E79                 retn
.text:0000000000938E79 sub_938E20      endp                    ; <-- lua_tothread
.text:0000000000938E79
.text:0000000000938E79 ; ---------------------------------------------------------------------------
.text:0000000000938E7A algn_938E7A:                            ; DATA XREF: seg005:0000000008B1F504↓o
.text:0000000000938E7A                 align 20h
.text:0000000000938E80
.text:0000000000938E80 ; =============== S U B R O U T I N E =======================================
.text:0000000000938E80
.text:0000000000938E80
.text:0000000000938E80 ; __int64 __fastcall sub_938E80(__int64, int)
.text:0000000000938E80 sub_938E80      proc near               ; CODE XREF: sub_118B1C0+4D↓p
.text:0000000000938E80                                         ; sub_119DE10+1C↓p ...
.text:0000000000938E80
.text:0000000000938E80 arg_0           = qword ptr  8
.text:0000000000938E80
.text:0000000000938E80                 mov     [rsp+arg_0], rbx; <-- you're here
```

So the offset is sub_938E20
