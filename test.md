# Raycast Dump Guide

## WorldRoot_Raycast

Used for doing a full physics raycast from scripts — this is what `workspace:Raycast()` calls internally. Grabbing it lets you bypass the descriptor dispatch and call the raw member function directly.

To dump Raycast you find string (shift f12 in ida, "s" in ghidra) `"Raycast"` exactly, you will land here:

```
.rdata:0000000006CB8D78 aRaycast        db 'Raycast',0
```

Only 1 code xref, go to it — you will be put in `sub_2590E20` which is the descriptor constructor. Scroll to the bottom and you'll see:

```
.text:0000000002590F42                 lea     rax, ??_7?$BoundFuncDesc@VWorldRoot@RBX@@...LuaRaycastResult...`vftable'
.text:0000000002590F49                 mov     cs:qword_81E7150, rax  <-- descriptor base
.text:0000000002590F50                 movaps  xmm0, xmmword ptr [rsi]
.text:0000000002590F53                 movaps  cs:xmmword_81E71D0, xmm0  <-- fn ptr goes here
```

That `BoundFuncDesc<WorldRoot, optional<LuaRaycastResult>(Vector3, Vector3, LuaRaycastParams)>` vftable tells you this is the real Raycast descriptor. But the constructor doesn't show you the actual function — it's passed in by the caller. So go back up and find who calls `sub_2590E20` (only 1 caller: `sub_409580`), and in there:

```
.text:0000000000409681                 lea     rax, sub_2559DF0  <-- Raycast
.text:0000000000409688                 mov     [rbp+0E0h+var_160], rax
.text:00000000004096B4                 call    sub_2590E20
```

**So the offset is 0x2559DF0**

Bonus trick — the descriptor is a global, and the fn ptr slot is always at +0x80:

```
descriptor = 0x81E7150   (base, where the BoundFuncDesc vftable is stored)
fn slot    = 0x80        (offset inside descriptor)
Raycast    = *(uintptr_t*)(REBASE(0x81E7150) + 0x80)  // == 0x2559DF0
```

Example of use:

```cpp
typedef std::optional<LuaRaycastResult>(*RaycastFn)(WorldRoot*, const Vector3&, const Vector3&, const LuaRaycastParams*);
auto Raycast = (RaycastFn)(REBASE(0x2559DF0));
```

---

**Nikky — 8/9/2026 6:14 PM**

## WorldRoot_Shapecast / Spherecast / Blockcast

The other three members of the raycast family. Same exact method, same layout, same +0x80 slot. Different strings:

| Function | String (shift f12) | Descriptor constructor | Registration fn | Member function |
|---|---|---|---|---|
| Shapecast (part) | `"Shapecast"` | `sub_25909E0` | `sub_409A40` | **0x255B780** |
| Spherecast | `"Spherecast"` | `sub_2590400` | `sub_40A0B0` | **0x255B100** |
| Blockcast | `"Blockcast"` | `sub_2592090` | `sub_407D50` | **0x255AFB0** |

Process is identical to Raycast: search string → xref → decompile the constructor → confirm the `BoundFuncDesc` vftable matches the signature you want → go to the constructor's caller → the `lea` right above the `call` is your function. Example for Shapecast:

```
.text:000000000409B00                 lea     rax, sub_255B780  <-- Shapecast
.text:000000000409B33                 call    sub_25909E0
```

To make sure you grabbed the right one, decompile it — `sub_255B780` will have `"Shapecast argument #1 expects a BasePart"` and `"Attempt to shapecast with distance %f"`. `sub_255B100` (Spherecast) and `sub_255AFB0` (Blockcast) will have `"Attempt to blockcast with side length %f"`.

Descriptors + fn slots for the whole family:

```
Raycast    desc 0x81E7150  +0x80 -> 0x2559DF0
Shapecast  desc 0x81E7210  +0x80 -> 0x255B780
Spherecast desc 0x81E7380  +0x80 -> 0x255B100
Blockcast  desc 0x81E6CC0  +0x80 -> 0x255AFB0
```



## Physics core (raw raycast, no descriptors)

If you want to skip the Lua-facing layer entirely and call the physics directly, there's a 2-level chain under all four functions:

```
sub_255B270  - shared dispatcher ("Attempt to shapecast with distance %f. The maximum distance is %d.")
sub_1F24440  - forks raycast vs shapecast ("Shapecast" string)
sub_1F22590  - core broadphase raycast ("Grids hit: %d", "Gjk-Sat calls: %d", "Excluded by RaycastParams: %d")
sub_1F285F0  - ShapecastInternal core ("ShapecastInternal" string)
```

To find the core: search string `"Excluded by RaycastParams: %d"` (shift f12) → 1 xref → that's `sub_1F22590`, **offset 0x1F22590**. It references `"Broadphase units: %d"` and `"Gjk-Sat calls: %d"` so you can't miss it. Not recommended to use unless you know what you're doing — the descriptor calls do validation you'd be skipping.


| Function | Offset | Notes |
|---|---|---|
| WorldRoot::Raycast | `0x2559DF0` | `workspace:Raycast()` |
| WorldRoot::Shapecast | `0x255B780` | part-based, `Shapecast(part, dir, params)` |
| WorldRoot::Spherecast | `0x255B100` | `Spherecast(origin, radius, dir, params)` |
| WorldRoot::Blockcast | `0x255AFB0` | `Blockcast(cframe, size, dir, params)` |
| Raycast descriptor | `0x81E7150` | fn ptr at `+0x80` |
| Shapecast descriptor | `0x81E7210` | fn ptr at `+0x80` |
| Spherecast descriptor | `0x81E7380` | fn ptr at `+0x80` |
| Blockcast descriptor | `0x81E6CC0` | fn ptr at `+0x80` |
| Physics dispatcher | `0x1F24440` | forks raycast/shapecast |
| Core broadphase raycast | `0x1F22590` | GJK/SAT narrowphase |
| ShapecastInternal core | `0x1F285F0` | shapecast physics |
| Space::raycast | `0x1EA03E0` | batched raycast (`"Raycasts"`/`"RaycastBatched"`) |
