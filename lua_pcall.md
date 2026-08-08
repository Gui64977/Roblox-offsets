# lua_pcall

Calls a function in protected mode. Catches errors and returns an error code.

Found in the base library table. Search `"rawget"` → xref → in the base table area (0x61F5xxx), scroll to find the `pcall` entry. The function pointer next to the string is luaB_pcall (0x41574E0). Decompile it:

```c
__int64 __fastcall sub_41574E0(__int64 a1)
{
  ...
  return sub_939430(a1, nargs, &nilobject, 0);  // <-- lua_pcall
}
```

Double click `sub_939430`:

```c
__int64 __fastcall sub_939430(L, int nargs, int nresults, int errfunc)
{
  sub_945D50(a1, sub_939720, &stack_state);  // run protected
}
```

Offset: **0x939430**

```c++
int r = ((int(*)(lua_State*, int, int, int))REBASE(0x939430))(L, nargs, nresults, errfunc);
```
