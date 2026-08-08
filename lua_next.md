# lua_next

Pops a key and pushes the next key-value pair from the table at given index.

Inlined into luaB_next (0x4156880). Find via the luaB offsets guide:

Search `"xpcall"` -> xref -> base table at 0x61F5xxx -> find `"next"` string -> next qword is luaB_next at 0x4156880. Decompile it — the full iteration logic is inside:

1. Get table at arg 1
2. Hash the key to find its position
3. Advance to next non-nil entry (array part first, then hash part)
4. Push key + value, return 2 (or push nil, return 1)

No separate C API wrapper. Use luaB_next directly or replicate the inline logic.
