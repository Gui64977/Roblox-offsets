# TouchInterest

Property on BasePart that controls Touched event generation. Setting it to 1 forces a part to become touchable.

Search `"TouchInterest"` -> first xref -> 0x252EF82 decompile sub_252EF70:

```c
_QWORD *__fastcall sub_252EF70(_QWORD *a1, __int64 a2)
```

Creates a touch interest object. Parent it to a BasePart to enable touch events.

Offset: **0x252EF70**

```c++
auto TT = ((void*(*)(void*))REBASE(0x252EF70))(nullptr);   // create
((void(*)(void*, void*))REBASE(parent_offset))(part, TT);   // parent to part
```
