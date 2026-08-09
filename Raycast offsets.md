Raycast Offsets
For some reason these aren't being dumped often, i mean, there isn't much point in them but, here we go!

WorldRoot_Raycast - used for doing a full physics raycast from scripts - this is what workspace:Raycast() calls internally.

To dump it search string "Raycast", just that same uppercased:
```asm
.rdata:0000000006CB8D78 aRaycast        db 'Raycast',0          ; DATA XREF: sub_2590E20:loc_2590E79↑o
.rdata:0000000006CB8D78                                         ; .rdata:0000000006854528↑o
```
Double click first xref and scroll up until you see SUBROUTINE:
```asm
.text:0000000002590E20
.text:0000000002590E20 ; =============== S U B R O U T I N E =======================================
.text:0000000002590E20
.text:0000000002590E20
.text:0000000002590E20 ; __int64 *__fastcall sub_2590E20(__int64, __int128 *, __int64, __int64, int, int, __int64, __int64, __int128 *, __int64)
.text:0000000002590E20 sub_2590E20     proc near               ; CODE XREF: sub_409580+134↑p
.text:0000000002590E20                                         ; DATA XREF: seg005:0000000008C12F0C↓o
.text:0000000002590E20
```
Double click code xref:
```asm
.text:0000000000409674                 lea     rcx, [rbp+0E0h+var_D0]
.text:0000000000409678                 call    sub_2C4F930
.text:000000000040967D                 movaps  [rbp+0E0h+var_E0], xmm6
.text:0000000000409681                 lea     rax, sub_2559DF0		; <-- WorldRoot_Raycast
.text:0000000000409688                 mov     [rbp+0E0h+var_160], rax
.text:000000000040968C                 mov     [rbp+0E0h+var_158], rbx
.text:0000000000409690                 lea     rax, [rbp+0E0h+var_150]
.text:0000000000409694                 mov     qword ptr [rsp+1E0h+var_198], rax
.text:0000000000409699                 lea     rax, [rbp+0E0h+var_E0]
.text:000000000040969D                 mov     [rsp+1E0h+var_1A0], rax
.text:00000000004096A2                 mov     [rsp+1E0h+var_1A8], rbx
.text:00000000004096A7                 lea     rax, [rbp+0E0h+var_D0]
.text:00000000004096AB                 mov     [rsp+1E0h+var_1B0], rax
.text:00000000004096B0                 lea     rdx, [rbp+0E0h+var_160]
.text:00000000004096B4                 call    sub_2590E20 		; <-- YOU'RE HERE
```

So WorldRoot_Raycast is 0x2559DF0

# SphereCast

Search for string "Spherecast":
```asm
.rdata:0000000006CB8CF8 aSpherecast     db 'Spherecast',0       ; DATA XREF: sub_2590400:loc_2590459↑o
.rdata:0000000006CB8CF8                                         ; .rdata:0000000006854568↑o
```

Second xref, the loc_ thingy:
```asm
.text:000000000259044F                 test    rax, rax
.text:0000000002590452                 jnz     short loc_2590459 ; <-- you're here
.text:0000000002590454                 call    sub_D65BC0
```

Scroll up until you see SUBROUTINE:
```asm
.text:0000000002590400 ; =============== S U B R O U T I N E =======================================
.text:0000000002590400
.text:0000000002590400
.text:0000000002590400 ; __int64 *__fastcall sub_2590400(__int64, __int128 *, __int64, __int64, int, int, int, __int64, __int64, __int128 *, __int64)
.text:0000000002590400 sub_2590400     proc near               ; CODE XREF: sub_40A0B0+132↑p
.text:0000000002590400                                         ; DATA XREF: seg005:0000000008C12ED0↓o
.text:0000000002590400
```

Click sub_2590400 once and press x, go fo first xref:
```asm
.text:000000000040A1A6                 call    sub_2C4F930
.text:000000000040A1AB                 movaps  [rbp+0F0h+var_E0], xmm6
.text:000000000040A1AF                 lea     rax, sub_255B100		; spherecast offset
.text:000000000040A1B6                 mov     [rbp+0F0h+var_160], rax
.text:000000000040A1BA                 mov     [rbp+0F0h+var_158], rbx
.text:000000000040A1BE                 lea     rax, [rbp+0F0h+var_150]
.text:000000000040A1C2                 mov     [rsp+1F0h+var_1A0], rax
.text:000000000040A1C7                 lea     rax, [rbp+0F0h+var_E0]
.text:000000000040A1CB                 mov     [rsp+1F0h+var_1A8], rax
.text:000000000040A1D0                 mov     [rsp+1F0h+var_1B0], rbx
.text:000000000040A1D5                 lea     rax, [rbp+0F0h+var_D0]
.text:000000000040A1D9                 mov     [rsp+1F0h+var_1B8], rax
.text:000000000040A1DE                 lea     rdx, [rbp+0F0h+var_160]
.text:000000000040A1E2                 call    sub_2590400		; <-- you're here
```

Spherecast: 0x255B100

# Blockcast

Search for string "Blockcast", first xref:
```asm
.rdata:0000000006CB8E58 aBlockcast      db 'Blockcast',0        ; DATA XREF: sub_2592090:loc_25920E9↑o
.rdata:0000000006CB8E58                                         ; .rdata:00000000068543E8↑o
```

You'll be put here:
```asm
.text:00000000025920E9 loc_25920E9:                            ; CODE XREF: sub_2592090+52↑j
.text:00000000025920E9                 lea     rdx, aBlockcast ; "Blockcast"
```

Scroll up till you see SUBROUTINE:
```asm
.text:0000000002592090
.text:0000000002592090 ; =============== S U B R O U T I N E =======================================
.text:0000000002592090
.text:0000000002592090
.text:0000000002592090 ; __int64 *__fastcall sub_2592090(__int64, __int128 *, __int64, __int64, int, int, int, __int64, __int64, __int128 *, __int64)
.text:0000000002592090 sub_2592090     proc near               ; CODE XREF: sub_407D50+132↑p
.text:0000000002592090                                         ; DATA XREF: seg005:0000000008C12F78↓o
```

Click once on sub_2592090 and press x, go to first xref:
```asm
.text:0000000000407E42                 lea     rcx, [rbp+0F0h+var_D0]
.text:0000000000407E46                 call    sub_2C4F930
.text:0000000000407E4B                 movaps  [rbp+0F0h+var_E0], xmm6
.text:0000000000407E4F                 lea     rax, sub_255AFB0		; <-- Blockcast
.text:0000000000407E56                 mov     [rbp+0F0h+var_160], rax
.text:0000000000407E5A                 mov     [rbp+0F0h+var_158], rbx
.text:0000000000407E5E                 lea     rax, [rbp+0F0h+var_150]
.text:0000000000407E62                 mov     [rsp+1F0h+var_1A0], rax
.text:0000000000407E67                 lea     rax, [rbp+0F0h+var_E0]
.text:0000000000407E6B                 mov     [rsp+1F0h+var_1A8], rax
.text:0000000000407E70                 mov     [rsp+1F0h+var_1B0], rbx
.text:0000000000407E75                 lea     rax, [rbp+0F0h+var_D0]
.text:0000000000407E79                 mov     [rsp+1F0h+var_1B8], rax
.text:0000000000407E7E                 lea     rdx, [rbp+0F0h+var_160]
.text:0000000000407E82                 call    sub_2592090		; <-- you're here
```

Blockcast: 0x255AFB0

# Shapecast

Will be bit harder, since it has more xrefs.

Search string "Shapecast", press x on it, and xref before .rdata will be it (or 4th xref)
```asm
Up	o	sub_25909E0:loc_2590A39	lea     rdx, aShapecast; "Shapecast" ; <-- CLICK THIS
Up	o	.rdata:0000000006854558	dq offset aShapecast
```

Scroll up until you see SUBROUTINE:
```asm
.text:00000000025909E0 ; =============== S U B R O U T I N E =======================================
.text:00000000025909E0
.text:00000000025909E0
.text:00000000025909E0 ; __int64 *__fastcall sub_25909E0(__int64, __int128 *, __int64, __int64, int, int, __int64, __int64, __int128 *, __int64)
.text:00000000025909E0 sub_25909E0     proc near               ; CODE XREF: sub_409A40+F3↑p
.text:00000000025909E0                                         ; DATA XREF: seg005:0000000008C12EF4↓o
```

Click sub_25909E0 once and press x on it, first xref:
```asm
.text:0000000000409AF7                 call    sub_2C4F930
.text:0000000000409AFC                 movaps  [rbp+0E0h+var_C0], xmm6
.text:0000000000409B00                 lea     rax, sub_255B780		; <-- Shapecast
.text:0000000000409B07                 mov     [rbp+0E0h+var_140], rax
.text:0000000000409B0B                 mov     [rbp+0E0h+var_138], rbx
.text:0000000000409B0F                 lea     rax, [rbp+0E0h+var_130]
.text:0000000000409B13                 mov     [rsp+1E0h+var_198], rax
.text:0000000000409B18                 lea     rax, [rbp+0E0h+var_C0]
.text:0000000000409B1C                 mov     [rsp+1E0h+var_1A0], rax
.text:0000000000409B21                 mov     [rsp+1E0h+var_1A8], rbx
.text:0000000000409B26                 lea     rax, [rbp+0E0h+var_B0]
.text:0000000000409B2A                 mov     [rsp+1E0h+var_1B0], rax
.text:0000000000409B2F                 lea     rdx, [rbp+0E0h+var_140]
.text:0000000000409B33                 call    sub_25909E0		; <-- you're here
```

Shapecast: 0x255B780

# Minimal use examples

All four share the same calling convention (MSVC x64 member fn with big return):
`rcx = this (WorldRoot)`, `rdx = hidden return buffer (64 bytes, the LuaRaycastResult)`, then args in `r8/r9/stack`.

IMPORTANT: `params` (LuaRaycastParams*) CANNOT be null when calling internally - the engine derefs it. In Lua it's optional, but the binding always passes a real object. Pass a valid one.

Result buffer layout (64 bytes, from the write pattern in the decompile):
```cpp
struct LuaRaycastResult {
    float position[3];   // +0x00
    float normal[3];     // +0x10
    int   material;      // +0x20
    float distance;      // +0x24
    __int64 instance;    // +0x28  (hit instance, 0 = miss)
    __int64 sharedPtr;   // +0x30
    char   valid;        // +0x38  (1 = hit)
};
```

## Raycast (0x2559DF0)

```cpp
typedef LuaRaycastResult* (__fastcall* RaycastFn)(void* worldRoot, LuaRaycastResult* out, float* origin, float* dir, void* params);

auto Raycast = (RaycastFn)(REBASE(0x2559DF0));

float origin[3] = { 0, 0, 0 };
float dir[3]    = { 0, -100, 0 };
LuaRaycastResult res;
Raycast(workspace, &res, origin, dir, myParams);
// res.valid == 1 -> hit, res.instance = hit part, res.distance, res.position = hit point
```

## Shapecast (0x255B780) - part-based

```cpp
typedef LuaRaycastResult* (__fastcall* ShapecastFn)(void* worldRoot, LuaRaycastResult* out, void* part, float* dir, void* params);

auto Shapecast = (ShapecastFn)(REBASE(0x255B780));

float dir[3] = { 0, -100, 0 };
LuaRaycastResult res;
Shapecast(workspace, &res, somePart, dir, myParams);
```

## Spherecast (0x255B100) - note radius is a FLOAT BY VALUE in r8, not a pointer

```cpp
typedef LuaRaycastResult* (__fastcall* SpherecastFn)(void* worldRoot, LuaRaycastResult* out, float* origin, float radius, float* dir, void* params);

auto Spherecast = (SpherecastFn)(REBASE(0x255B100));

float origin[3] = { 0, 0, 0 };
float dir[3]    = { 0, -100, 0 };
LuaRaycastResult res;
Spherecast(workspace, &res, origin, 2.0f, dir, myParams);  // radius = 2
```

## Blockcast (0x255AFB0) - cframe + size

```cpp
typedef LuaRaycastResult* (__fastcall* BlockcastFn)(void* worldRoot, LuaRaycastResult* out, float* cframe, float* size, float* dir, void* params);

auto Blockcast = (BlockcastFn)(REBASE(0x255AFB0));

float cframe[12] = { 1,0,0,0, 1,0,0, 0,1,0,0, 0,0,0 };  // identity CFrame (rotation matrix + position)
float size[3]    = { 4, 4, 4 };
float dir[3]     = { 0, -100, 0 };
LuaRaycastResult res;
Blockcast(workspace, &res, cframe, size, dir, myParams);
```

# Using the descriptors (+0x80)

Same result, but reads the fn ptr from the descriptor at runtime, survives Roblox updates since the descriptor is re constructed each build and stores the new function pointer:

```cpp
template <typename T>
inline T BoundFn(uintptr_t descriptor) {
    return (T)(*(uintptr_t*)(REBASE(descriptor) + 0x80));
}

// Raycast    desc 0x81E7150  -> 0x2559DF0
// Shapecast  desc 0x81E7210  -> 0x255B780
// Spherecast desc 0x81E7380  -> 0x255B100
// Blockcast  desc 0x81E6CC0  -> 0x255AFB0

auto Raycast = BoundFn<RaycastFn>(0x81E7150);
// same call as above
```

You may ask how both 0x81E7150 and 0x2559DF0 can work, and its quite easy. So, 0x2559DF0 is an ACTUAL function, contains code bla bla, 0x2559DF0 is the raycast, 0x81E7150 just contains call to it if you use 0x81E7150 + 0x80
