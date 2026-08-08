# Roblox-offsets

# Most of the guides are working again, updated to version d584fb6c717a43d9. Hopefully roblox won't do a massive update again.

This is guide on how to get multiple roblox offsets through ida

**THIS IS FREE TO USE, IF YOU BUILD DUMPER WITH IT - OKAY, CREDIT ME IF YOU WANT, I DON'T EXPECT ANYTHING IN RETURN.**

**SOME OFFSETS COULD BE INCORRECT. I'M ACTIVELY GOING TO RECHECK EVERY SINGLE GUIDE AND FIGURE OUT WHAT IS CORRECT AND WHAT IS WRONG. Sorry about that**

**DM LORDNIKKY IF THERE ARE ANY ISSUES OR YOU WANT OFFSET ADDED**

Made with EVIL

Time spent: 20 hours

1627 lines

59185 characters

**SOME OFFSETS CAN BE PRESENT MULTIPLE TIMES, BECAUSE I'M INATTENTIVE AND I DONT KEEP TRACK OF WHAT I ALREADY DID!!!!**

List of current offsets:

AttachRobloxExtraSpace: 48 89 5C 24 ? 4C 89 4C 24 ? 55 56 57 41 54 41 55 41 56 41 57 48 83 EC 50 4D 8B F9 4D 8B E8

coroutine.close

coroutine.create

coroutine.isyieldable

coroutine.resume

coroutine.running

coroutine.status

coroutine.wrap

coroutine.yield

FireClient: 48 89 5C 24 ? 48 89 74 24 ? 48 89 7C 24 ? 4C 89 74 24 ? 55 48 8B EC 48 81 EC 80 00 00 00 4D 8B F1 49 8B D8 48 8B F2

FireServer: 48 89 5C 24 ? 55 56 57 41 56 41 57 48 8D 6C 24 ? 48 81 EC 60 01 00 00 48 8B 05 ? ? ? ? 48 33 C4 48 89 45 ? 4D 8B F8 48 8B FA

GetCapabilities

GetIdentityStruct

GetLuaStateForInstance: 48 83 EC 38 8B 81 ? ? ? ? 90 83 F8 03 7D ? 48 81 C1 38 01 00 00

Impersonator: 48 89 5C 24 ? 48 89 6C 24 ? 48 89 74 24 ? 57 48 83 EC 60 ? ? ? 48 8B F1 ? ? ? 49 8B D9

InvokeServer: 40 55 53 56 57 41 54 41 55 41 56 41 57 48 8D AC 24 ? ? ? ? 48 81 EC E8 02 00 00 48 8B 05 ? ? ? ? 48 33 C4 48 89 85 ? ? ? ? 49 8B F9 4C 89 4C 24 ? 4D 8B E0 48 8B DA 48 89 54 24

Lua_NewThread: 40 53 48 83 EC 20 48 8B 51 ? 48 8B D9 ? ? ? 48 39 42

Lua_pseudoaddr: 41 B9 EE D8 FF FF // MIGHT BA BAD

Lua_SandBoxThread: 40 53 48 83 EC 20 45 33 C0 33 D2 48 8B D9 E8 ? ? ? ? 45 33 C0

luaA_toobject: 48 83 EC 28 4C 8D 15 // MIGHT BE BAD

luaB_assert

luaB_error

luaB_gcinfo

luaB_getfenv

luaB_getmetatable

luaB_newproxy

luaB_next

luaB_print

luaB_rawequal

luaB_rawget

luaB_rawlen

luaB_rawset

luaB_select

luaB_setfenv

luaB_setmetatable

luaB_tonumber

luaB_tostring

luaC_barrierback: 4C 8B 49 ? ? ? ? 49 8B 41 ? ? ? ? 49 89 51

luaC_barrierf: 48 8B 49 ? 0F B6 41 ? FE C8 3C 02 76 ? 0F B6 49

luaC_step: 48 89 5C 24 ? 48 89 6C 24 ? 48 89 74 24 ? 48 89 7C 24 ? 41 54 41 56 41 57 48 83 EC 30 48 8B 59 ? 0F B6 F2

luaD_rawrunprotected: 48 89 4C 24 ? 48 83 EC 38 48 8B C2

luaD_throw: 48 83 EC 58 44 8B C2 // MIGHT BE BAD

luaG_addinfo: 48 89 6C 24 ? 48 89 74 24 ? 57 48 81 EC 30 01 00 00 48 8B 71 ? 48 8B EA

luaG_runerror: 48 8B C4 48 89 50 ? 4C 89 40 ? 4C 89 48 ? 53 48 81 EC 20 02 00 00

luaL_argerrorL: 48 89 5C 24 ? 48 89 74 24 ? 57 48 83 EC 30 49 8B F8 8B F2

luaL_getmetafield: 48 89 5C 24 ? 57 48 83 EC 20 49 8B F8 48 8B D9 E8 ? ? ? ? 85 C0 74 ? 48 8B D7

luaL_checkinteger

luaL_checklstring: 48 89 5C 24 ? 48 89 6C 24 ? 48 89 74 24 ? 57 48 83 EC 20 49 8B F9 49 8B D8 8B F2

luaL_errorL: 48 89 54 24 ? 4C 89 44 24 ? 4C 89 4C 24 ? 53 57 48 83 EC 28

luaL_register: 48 89 5C 24 ? 48 89 6C 24 ? 56 57 41 56 48 83 EC 30 45 33 F6 49 8B D8

luaL_tolstring: 48 89 5C 24 ? 48 89 6C 24 ? 48 89 74 24 ? 57 48 81 EC E0 00 00 00 8D 82

luaL_tostring: 48 89 5C 24 ? 48 89 6C 24 ? 48 89 74 24 ? 57 48 81 EC E0 00 00 00 8D 82

luaM_free_: 48 89 5C 24 ? 48 89 74 24 ? 57 48 83 EC 30 48 8B 79 ? 49 8D 40

LuaO_nilobject

luaS_newlstr: 48 89 5C 24 ? 48 89 6C 24 ? 48 89 74 24 ? 48 89 7C 24 ? 41 55 41 56 41 57 48 83 EC 30 33 ED 4D 8B C8

luah_dummynode

luah_new: 48 89 5C 24 ? 48 89 6C 24 ? 56 57 41 54 41 56 41 57 48 83 EC 30 41 8B E8 48 63 F2

luau_execute

luau_load: 48 89 5C 24 ? 48 89 6C 24 ? 48 89 74 24 ? 57 41 56 41 57 48 81 EC 80 00 00 00 49 8B E9 4D 8B F0

luaopen_base: 48 89 5C 24 ? 57 48 83 EC 30 BA EE D8 FF FF

lua_bit32

lua_concat: 48 89 5C 24 ? 57 48 83 EC 20 48 63 DA 48 8B F9 83 FB 02

lua_createtable: 48 89 6C 24 ? 48 89 74 24 ? 57 48 83 EC 20 4C 8B 49 ? 41 8B F0

lua_encodepointer: 4C 8B 41 ? 48 8B C2 49 0F AF 80

lua_equal: 48 89 5C 24 ? 57 48 83 EC 20 49 63 D8 4C 8B D9 48 8D 3D ? ? ? ? 85 D2 CC

lua_error: 

lua_gc: 48 89 5C 24 ? 48 89 6C 24 ? 48 89 74 24 ? 57 41 56 41 57 48 83 EC 40 48 8B 59

lua_getfenv: 48 89 5C 24 ? 57 48 83 EC 20 ? ? ? 48 8B D9 48 63 FA CC CC 4C 8D 41 ? 48 8B D1 E8 ? ? ? ? 80 3D ? ? ? ? ? 74 ? 48 8B 4B ? 48 8B 43 ? 48 83 C0 10 48 3B 41 ? 76 ? BA 01 00 00 00 48 8B CB E8 ? ? ? ? 85 C0 0F 84

lua_getfield: 48 89 5C 24 ? 48 89 74 24 ? 57 48 83 EC 30 ? ? ? 49 8B F0 48 63 FA

lua_getmetatable: 48 89 5C 24 ? 57 48 83 EC 20 ? ? ? 48 8B D9 48 63 FA 74 ? 4C 8D 41 ? 48 8B D1 E8 ? ? ? ? 80 3D ? ? ? ? ? 74 ? 48 8B 4B ? 48 8B 43 ? 48 83 C0 10 48 3B 41 ? 76 ? BA 01 00 00 00 48 8B CB E8 ? ? ? ? 85 C0 0F 84

lua_gettop: E8 ? ? ? ? 2B 43 ? 48 98 // might not be good

lua_loadsafe: 48 89 54 24 ? 48 89 4C 24 ? 53 55 56 57 41 54 41 55 41 56 41 57 48 81 EC F8 04 00 00

lua_newuserdata: 48 89 5C 24 ? 57 48 83 EC 20 4C 8B 41 ? 48 8B FA 48 8B D9 ? ? ? 49 39 40

lua_next: 48 89 5C 24 ? 57 48 83 EC 20 ? ? ? 48 8B D9 48 63 FA 74 ? 4C 8D 41 ? 48 8B D1 E8 ? ? ? ? 85 FF 7E ? 48 8B 43 ? 48 8B CF 48 8B 53

lua_objlen: 48 83 EC 28 85 D2 7E ? 4C 8B 41 ? 48 8D 05 ? ? ? ? 49 83 C0 F0 48 63 D2 48 C1 E2 04 4C 03 C2 4C 3B 41 ? 49 0F 42 C0 EB ? 81 FA F0 D8 FF FF 7E ? 48 63 C2 48 C1 E0 04 48 03 41 ? EB ? E8 ? ? ? ? 8B 50

lua_pcall: 48 89 74 24 ? 57 48 83 EC 20 0F B6 41 ? 48 8B F9

lua_pushboolean: 48 89 5C 24 ? 57 48 83 EC 20 80 3D ? ? ? ? ? 8B FA 48 8B D9 74

lua_pushcclosure: 48 89 5C 24 ? 48 89 74 24 ? 57 48 83 EC 20 4C 8B 49 ? 41 8B F8

lua_pushcfunction: 48 89 5C 24 ? 48 89 74 24 ? 57 48 83 EC 20 4C 8B 49 ? 41 8B F8

lua_pushinteger: 48 89 5C 24 ? 48 89 74 24 ? 57 48 83 EC 20 80 3D ? ? ? ? ? 41 8B F8 48 8B F2

lua_pushnumber: 40 53 48 83 EC 30 80 3D ? ? ? ? ? 48 8B D9 0F 29 74 24 ? 0F 28 F1 74 ? 48 8B 51

lua_pushstring: 48 89 6C 24 ? 48 89 74 24 ? 57 48 83 EC 20 48 8B EA 48 8B F9 48 85 D2

lua_pushvalue: 48 89 5C 24 ? 57 48 83 EC 20 ? ? ? 48 8B D9 48 63 FA CC CC 4C 8D 41 ? 48 8B D1 E8 ? ? ? ? 80 3D ? ? ? ? ? 74 ? 48 8B 4B ? 48 8B 43 ? 48 83 C0 10 48 3B 41 ? 76 ? BA 01 00 00 00 48 8B CB E8 ? ? ? ? 85 C0 74

lua_rawcheckstack: 48 89 5C 24 ? 57 48 83 EC 20 48 8B D9 48 63 FA 48 8B 49 ? 8B C7

lua_rawget: 48 89 5C 24 ? 57 48 83 EC 20 ? ? ? 48 8B D9 48 63 FA 74 ? 4C 8D 41 ? 48 8B D1 E8 ? ? ? ? 85 FF 7E ? 48 8B 43 ? 48 8B CF 48 8B 53

lua_rawset: 48 89 74 24 ? 57 48 83 EC 20 48 8B F1 85 D2

lua_replace: 40 53 48 83 EC 20 48 8B D9 85 D2 7E ? 4C 8B 41

lua_resume: 40 53 48 83 EC 20 0F B6 41 ? 48 8B D9 3C 01

lua_setfield: 48 89 5C 24 ? 57 48 83 EC 20 4D 8B D0 48 8B F9

lua_setmetatable

lua_settable: 40 53 48 83 EC 20 48 8B D9 85 D2 7E ? 48 8B 41

lua_settop: 48 89 5C 24 ? 57 48 83 EC 20 48 63 FA 48 8B D9 85 D2 0F 88

lua_topointer: 48 83 EC 28 4D 8B D0 85 D2 7E ? 4C 8B 49 ? 48 8D 05 ? ? ? ? 49 83 C1 F0 48 63 D2 48 C1 E2 04 4C 03 CA 4C 3B 49 ? 49 0F 42 C1 EB ? 81 FA F0 D8 FF FF 7E ? 48 63 C2 48 C1 E0 04 48 03 41 ? EB ? E8 ? ? ? ? 83 78 ? ? 75

lua_tothread: 48 83 EC 28 85 D2 7E ? 4C 8B 41 ? 48 8D 05 ? ? ? ? 49 83 C0 F0 48 63 D2 48 C1 E2 04 4C 03 C2 4C 3B 41 ? 49 0F 42 C0 EB ? 81 FA F0 D8 FF FF 7E ? 48 63 C2 48 C1 E0 04 48 03 41 ? EB ? E8 ? ? ? ? 83 78 ? ? 74 

lua_type: 48 83 EC 28 85 D2 7E ? 48 8B 41 ? 48 83 C0 F0 48 63 D2 48 C1 E2 04 48 03 C2 48 3B 41 ? 73

pushinstance: 48 89 5C 24 ? 57 48 83 EC 20 48 8B FA 48 8B D9 E8 ? ? ? ? 48 8B CB 84 C0 74 ? 48 8B D7

Require Bypass

ScriptContextResume: 4C 8B DC 49 89 5B ? 49 89 73 ? 57 41 54 41 55 41 56 41 57 48 81 EC F0 00 00 00

SetFFlag: 48 89 5C 24 ? 55 56 57 41 54 41 55 41 56 41 57 48 8D AC 24 ? ? ? ? 48 81 EC D0 01 00 00 48 8B 05 ? ? ? ? 48 33 C4 48 89 85 ? ? ? ? 44 89 4C 24

TaskCancel: 48 89 5C 24 ? 57 48 83 EC 20 BA 01 00 00 00 48 8B F9 E8 ? ? ? ? 48 8B D8

TaskDefer: 48 89 5C 24 ? 48 89 74 24 ? 55 57 41 54 41 56 41 57 48 8D 6C 24 ? 48 81 EC 80 01 00 00 48 8B 05 ? ? ? ? 48 33 C4 48 89 45 ? 48 8B F1

TouchInterest: 48 89 4C 24 ? 53 48 83 EC 20 48 8B D9 4C 8D 05 ? ? ? ? E8 ? ? ? ? 90 48 8D 05 ? ? ? ? ? ? ? E8 ? ? ? ? 48 89 43 ? E8 ? ? ? ? 48 8B C8 E8 ? ? ? ? 48 8B C8 E8 ? ? ? ? 90 F0 FF 05

luaF_newLclosure: 48 89 5C 24 ? 48 89 6C 24 ? 48 89 74 24 ? 57 48 83 EC 20 8B EA 49 8B F8

luaF_newCclosure: 48 89 5C 24 ? 48 89 74 24 ? 57 48 83 EC 20 48 63 F2 49 8B F8

lua_state encryption

luaM_new:

luaM_realloc_:

lua_ref: 

lua_unref: 

print: 

luaV_settable:

luaV_concat: 

luaH_getn:

lua_gettable:

luaV_gettable: 

raknetrecieve: 

RakNetReliabilityLayerSend:

RaknetReportNetworkError:

RaknetHandleConnectionState:

RaknetSend:

RakPeerProcessNetworkPacket:

SendPacketsToSelf:

UpdateNetworkLoop:

RakPeerReceive:

luaVM_new:

NewInstance: 
