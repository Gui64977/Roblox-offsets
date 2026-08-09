# luaM_realloc_

GC memory allocators. Used by lua_newuserdata, lua_createtable, luaH_new, bla bla bla.

## sub_954490 - small object (cached) allocator

Fast path for common GC object sizes (< 1024 bytes). Uses per size category freelists.

Find: search `"newproxy"` decompile -> find call to sub_954490 inside the GC alloc pattern:

```c
  }
  if ( (unsigned __int64)(*(_QWORD *)(a1 + 72) + 16LL) > **(_QWORD **)(a1 + 88)
    && (unsigned int)sub_937DA0((_QWORD *)a1, a2: 1) == 0 )
  {
    goto LABEL_72;
  }
  v8 = nullptr;
  v9 = *(unsigned __int8 *)(a1 + 6);
  v10 = *(_QWORD *)(a1 + 112);
  if ( byte_7A2DDA0 < 0 )
  {
    v16 = (_DWORD *)sub_954490(a1, a2: (int)v10 + 800, a3: 80, a4: 16, a5: 1); // <-- luaM_realloc_
    v14 = v16 + 16;
    v16[12] -= v16[9];
    ++v16[13];
  }
  else
  {
    v11 = 8LL * byte_7A2DDA0;
    v12 = *(_QWORD *)(v11 + v10 + 424);
    if ( v12 == 0 )
      v12 = sub_954540(a1, a2: (int)v10 + 424, a3: (int)v10 + 800, a4: byte_7A2DDA0, a5: 0);
    v13 = *(int *)(v12 + 48);
    if ( (int)v13 < 0 )
    {
      v14 = *(_DWORD **)(v12 + 40);
      *(_QWORD *)(v12 + 40) = *((_QWORD *)v14 + 1);
    }
    else
```

Offset: **0x954490**
