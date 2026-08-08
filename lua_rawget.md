# lua_rawget (C API)

Does raw table access without invoking metamethods.

Inlined into luaB_rawget (0x4153B70) in this build. Find via the luaB offsets guide:

Search `"xpcall"` -> xref -> luaB_rawget at 0x4153B70. Decompile it - the raw table lookup is inside. No separate C API wrapper.

The raw access logic:
1. Hash the key using value-type-specific hash function
2. Look up in table's hash table
3. Push the result (or nil)

For programmatic use, call luaB_rawget directly or replicate the inline logic.
