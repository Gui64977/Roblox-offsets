# GetLuaStateForInstance

GetLuaStateForInstance - gets the lua_State associated with a Roblox Instance.

Search string (shift f12) `"Script Start"` go to **first** xref (ScriptContext). Decompile (f5), look up from  `"Script Start"`:

```c
            }
            v25 = (_DWORD *)sub_2316530(a1: v24 + 312, a2: v247, a3: (__int64 *)&v274); // <-- FIND THIS
            LODWORD(v295) = *v25 - (_DWORD)v25;
            HIDWORD(v295) = v25[1] - (_DWORD)v25;
            v26 = v295;
            if ( *((_QWORD *)&v274 + 1) != 0 )
              sub_799660(a1: *((volatile signed __int32 **)&v274 + 1));
            if ( v26 != 0 )
            {
              v27 = *(_QWORD *)(v26 + 32);
              v28 = *(_QWORD *)(*(_QWORD *)(v27 + 24) + 16LL);
            }
            else
            {
              v27 = 0;
              v28 = *(_QWORD *)(*(_QWORD *)&word_18 + 16LL);
            }
          }
          __unwind
          {
            sub_79AA00(a1: &v274);
          }
          __eh34_enter_wind_state(6, 7);
          v29 = *(_QWORD *)(*(_QWORD *)(v27 + 24) + 40LL);
          v253 = v29;
          v254 = *(_QWORD *)(v29 + 312);
          *(_QWORD *)(v29 + 0x138) = "Script Start"; // <-- YOU'RE HERE
          if ( *(int *)(v28 + 4784) >= 3 )
          {
            v243 = "sor.png";
            sub_2C9AD80(a1: 0, a2: (__int64)&aTexturesCursor_5[-1021808]);
```

Above it:
```c
            v25 = sub_2316530(a1: v24 + 312, a2: v247, a3: &v274);
```

Double click `sub_2316530`, then press X, find its caller `sub_2259730` — double click:

```c
__int64 __fastcall sub_2259730(__int64 a1, __int64 a2, __int64 a3)
{
  if ( *(int *)(a1 + 4784) >= 3 )
    sub_2C9AD80(a1: 0, a2: "...");
  v3 = sub_2316530(a1 + 312, a2, a3);
  return *(_QWORD *)v3;
}
```

`sub_2259730` - GetLuaStateForInstance

Offset: **0x2259730**
