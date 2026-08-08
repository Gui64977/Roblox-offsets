# lua_getfield

Pushes onto the stack the value of table[k].

Found through the Lua_SandBoxThread guide chain: `"__index"` -> SandBoxThread -> sub_119E530 -> sub_119DE10 -> sub_93E0C0.

```c
__int64 __fastcall sub_93E0C0(L, int idx, const char* k)
{
  // pushes TString from k
  // calls lua_gettable(L, idx)
  return result;
}
```

Takes (L, table_index, key_string). Creates a TString from the key, pushes it, then does agettable.

Offset: **0x93E0C0**
