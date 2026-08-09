# lua_settable (C API)

Sets table[key] = value from the stack. The table is at the given index, key above it, value on top.

Found through Lua_SandBoxThread (0x119E530). Search `"__index"` bytes `5F 5F 69 6E 64 65 78 00` -> xref -> SandBoxThread -> sub_119DE10. At the end:

```c
    if ( v35 == nullptr )
      goto LABEL_39;
  }
  v42 = *((_BYTE *)v35 + 1);
  if ( ((v42 ^ ~*(_BYTE *)(v34 + 16) & 3) & 0xB) == 0 )
    *((_BYTE *)v35 + 1) = v42 ^ 3;
LABEL_81:
  v65 = *(_QWORD *)(a1 + 72) - 16LL;
  v69 = v35;
  v70 = 6;
  result = sub_958BE0(a1, a2: v68, a3: &v69, a4: v65); // <-- lua_settable
  *(_QWORD *)(a1 + 72) -= 16LL;
  return result;
}
```

Offset: **0x958BE0**
