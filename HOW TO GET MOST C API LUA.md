"_VERSION" string -> its xref -> decompile:
```c
  sub_4B69E30(a1, a2: &off_603A3C8, a3: &off_6BBE0A0);
```
```c
double click off_6BBE0A0 you'll land here:
.rdata:0000000006BBE0A0                                         ; "assert"
.rdata:0000000006BBE0A8                 dq offset sub_4B7DF90
.rdata:0000000006BBE0B0                 dq offset aError_1      ; "error"
.rdata:0000000006BBE0B8                 dq offset sub_4B7DA50
.rdata:0000000006BBE0C0                 dq offset aGcinfo       ; "gcinfo"
.rdata:0000000006BBE0C8                 dq offset sub_4B7DE80
.rdata:0000000006BBE0D0                 dq offset aGetfenv      ; "getfenv"
.rdata:0000000006BBE0D8                 dq offset sub_4B7DBE0
.rdata:0000000006BBE0E0                 dq offset aGetmetatable ; "getmetatable"
.rdata:0000000006BBE0E8                 dq offset sub_4B7DAC0
.rdata:0000000006BBE0F0                 dq offset aNext_4       ; "next"
.rdata:0000000006BBE0F8                 dq offset sub_4B7DF30
.rdata:0000000006BBE100                 dq offset aNewproxy     ; "newproxy"
.rdata:0000000006BBE108                 dq offset sub_4B7E0E0
.rdata:0000000006BBE110                 dq offset aPrint        ; "print"
.rdata:0000000006BBE118                 dq offset sub_4B7D830
.rdata:0000000006BBE120                 dq offset aRawequal     ; "rawequal"
.rdata:0000000006BBE128                 dq offset sub_4B7DD20
.rdata:0000000006BBE130                 dq offset aRawget       ; "rawget"
.rdata:0000000006BBE138                 dq offset sub_4B7DD70
.rdata:0000000006BBE140                 dq offset aRawset       ; "rawset"
.rdata:0000000006BBE148                 dq offset sub_4B7DDC0
.rdata:0000000006BBE150                 dq offset aRawlen       ; "rawlen"
.rdata:0000000006BBE158                 dq offset sub_4B7DE20
.rdata:0000000006BBE160                 dq offset aSelect_1     ; "select"
.rdata:0000000006BBE168                 dq offset sub_4B7E000
.rdata:0000000006BBE170                 dq offset aSetfenv      ; "setfenv"
.rdata:0000000006BBE178                 dq offset sub_4B7DC40
.rdata:0000000006BBE180                 dq offset aSetmetatable ; "setmetatable"
.rdata:0000000006BBE188                 dq offset sub_4B7DB20
.rdata:0000000006BBE190                 dq offset aTonumber     ; "tonumber"
.rdata:0000000006BBE198                 dq offset sub_4B7D910
.rdata:0000000006BBE1A0                 dq offset aTostring     ; "tostring"
```
```c
   ## assert

   sub_4B7DF90:
       sub_4B69480(a1, 1);                                // check any
       if (!sub_4B64E00(a1, 1)) {                         // lua_toboolean?
           v3 = sub_4B69B10(a1, 2, "assertion failed!", 0); // <-- luaL_checklstring
           sub_4B69760(a1, "...", v3);                     // <-- luaL_errorL
       }
       return sub_4B625F0(a1);                             // <-- lua_gettop

   ## error

   sub_4B7DA50:
       v2 = sub_4B69AB0(a1, 2, 1);     // check level
       sub_4B64BC0(a1, 1);             // <-- lua_settop
       if (sub_4B629A0(a1, 1) && v2 > 0) {
           sub_4B6A7A0(a1, v2);        // luaL_where
           sub_4B63740(a1, 1);         // lua_pushvalue
           sub_4B61C30(a1, 2);         // lua_concat
       }
       sub_4B61F50(a1);                // <-- lua_error

   ## gcinfo

   sub_4B7DE80:
       v2 = sub_4B61F60(a1, 3, 0);     // <-- lua_gc(L, count)
       sub_4B63270(a1, v2);            // <-- lua_pushnumber (int→double)
       return 1;

   ## getfenv

   sub_4B7DBE0:
       sub_4B7E170(a1, 1);             // check func/thread
       if (sub_4B628C0(a1, -1))
           sub_4B63740(a1, -10002);    // lua_pushvalue (global env)
       else
           sub_4B621A0(a1, -1);        // <-- lua_getfenv
       sub_4B64AC0(a1, -1, 0);         // set top result
       return 1;

   ## getmetatable

   sub_4B7DAC0:
       sub_4B69480(a1, 1);             // check any
       if (sub_4B623C0(a1, 1))         // <-- lua_getmetatable
           sub_4B698E0(a1, 1, "__metatable"); // luaL_callmeta (locked check)
       else
           sub_4B63430(a1);            // lua_pushnil
       return 1;

   ## next

   sub_4B7DF30:
       sub_4B696A0(a1, 1, 7);          // checktype(L, 1, table)
       sub_4B64BC0(a1, 2);             // <-- lua_settop
       if (sub_4B62E30(a1, 1))         // <-- lua_next
           return 2;                   // pushed key+value
       sub_4B63430(a1);                // <-- lua_pushnil
       return 1;                       // iteration done

   ## newproxy

   sub_4B7E0E0:
       sub_4B65630(a1, 1);             // lua_type
       v2 = sub_4B64E00(a1, 1);        // lua_toboolean?
       sub_4B62CA0(a1, 0, 0x81);       // <-- lua_pushcfunction
       if (v2) {
           sub_4B61D80(a1, 0, 0);      // <-- lua_createtable
           sub_4B64920(a1, -2);        // <-- lua_replace
       }
       return 1;

   ## print

   sub_4B7D830:
       v2 = 1;
       v3 = sub_4B625F0(a1);           // <-- lua_gettop
       if (v3 >= 1) {
           do {
               v4 = sub_4B69F70(a1, v2, &v10); // <-- luaL_tolstring
               // ... print to stdout ...
           } while (v2 <= v3);
       }
       // print newline ...
       return 0;

   ## rawequal

   sub_4B7DD20:
       sub_4B69480(a1, 1);             // check any
       sub_4B69480(a1, 2);             // check any
       v2 = sub_4B63970(a1, 1, 2);     // lua_equal
       sub_4B62FB0(a1, v2);            // <-- lua_pushboolean
       return 1;

   ## rawget

   sub_4B7DD70:
       sub_4B696A0(a1, 1, 7);          // checktype(L, 1, table)
       sub_4B69480(a1, 2);             // check any
       sub_4B64BC0(a1, 2);             // <-- lua_settop
       sub_4B63A40(a1, 1);             // <-- lua_rawget
       return 1;

   ## rawlen

   sub_4B7DE20:
       if (sub_4B65630(a1, 1) - 6 > 1) // lua_type check (6=string, 7=table)
           sub_4B69390(a1, 1, "table or string expected"); // arg error
       v2 = sub_4B62F20(a1, 1);        // <-- lua_objlen
       sub_4B63270(a1, v2);            // <-- lua_pushnumber (int→double)
       return 1;

   ## rawset

   sub_4B7DDC0:
       sub_4B696A0(a1, 1, 7);          // checktype(L, 1, table)
       sub_4B69480(a1, 2);             // check any (key)
       sub_4B69480(a1, 3);             // check any (value)
       sub_4B64BC0(a1, 3);             // <-- lua_settop
       sub_4B63F90(a1, 1);             // <-- lua_rawset
       return 1;

   ## select

   sub_4B7E000:
       v2 = sub_4B625F0(a1);           // <-- lua_gettop
       if (sub_4B65630(a1, 1) == 6     // lua_type check string
           && *sub_4B64FF0(a1, 1, 0) == '#') {  // <-- lua_tolstring
           sub_4B63270(a1, v2 - 1);    // push n-1
           return 1;
       }
       // ... numeric select path ...
       return v2 - v4;                 // return count of remaining args

   ## setfenv

   sub_4B7DC40:
       sub_4B696A0(a1, 2, 7);          // checktype(L, 2, table)
       sub_4B7E170(a1, 0);             // check func/thread
       sub_4B63740(a1, 2);             // <-- lua_pushvalue
       sub_4B64AC0(a1, -1, 0);         // set env
       // ... error check ...
       return 1 or 0;

   ## setmetatable

   sub_4B7DB20:
       sub_4B696A0(a1, 1, 7);          // checktype(L, 1, table)
       sub_4B65630(a1, 2);             // lua_type
       if (sub_4B698E0(a1, 1, "__metatable"))  // <-- luaL_callmeta (locked?)
           sub_4B69760(a1, "cannot change a protected metatable");
       sub_4B64BC0(a1, 2);             // <-- lua_settop
       sub_4B64920(a1, 1);             // <-- lua_replace
       return 1;

   ## tonumber

   sub_4B7D910:
       v2 = sub_4B69AB0(a1, 2, 10);    // check optional arg
       if (v2 != 10) {                 // if base given (string→number)
           // ... base conversion path ...
           sub_4B63490(a1, v5);        // <-- lua_pushnumber (double)
       } else {
           sub_4B69480(a1, 1);         // check any
           sub_4B63430(a1);            // <-- lua_pushnil
       }
       return 1;

   ## tostring

   sub_4B7E0B0:
       sub_4B69480(a1, 1);             // check any
       sub_4B69F70(a1, 1, 0);          // <-- luaL_tolstring
       return 1;
```
   ## Note: Two "push number" variants

   You'll see two functions pushing numbers throughout these decompilations:

   | Function | Signature | Tag | What |
   |----------|-----------|-----|------|
   | `sub_4B63270` | `(L, int)` → double | 3 | Internal convenience. luaB_ functions use this to push ints as doubles.
   |
   | `sub_4B632F0` | `(L, int64, int)` | 2 | **Real C API — `lua_pushinteger`.** Pushes a true Luau integer. |

   The luaB_ wrappers use `0x4B63270` for convenience. Your own code should call the C API `lua_pushinteger` at
   `0x4B632F0`.
