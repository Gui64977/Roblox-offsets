# pushinstance

To find it search string "RaycastResult", 5th xref and decompile it:
```c
__int64 __fastcall sub_22B5650(_QWORD *a1)
{
  _DWORD *v1; // rdx
  __int64 v2; // rdx
  __int64 v3; // rdx

  v1 = &unk_610B898;
  if ( a1[12] < a1[9] )
    v1 = (_DWORD *)a1[12];
  if ( v1[3] != 9 || *(unsigned __int8 *)((v2 = *(_QWORD *)v1) + 3) != dword_89AD220 || (v3 = v2 + 16) == 0 )
    sub_93B8C0(a1, a2: 1u, a3: "RaycastResult");
  sub_226A200((__int64)a1, a2: v3 + 40); // <-- pushinstance
  return 1;
}
```

If you canf find it, it should look like code above, not like:
```c
__int64 __fastcall sub_22B54B0(_QWORD *a1)
{
  _DWORD *v1; // rdx
  float *v2; // r8

  v1 = &unk_610B898;
  if ( a1[12] < a1[9] )
    v1 = (_DWORD *)a1[12];
  if ( v1[3] != 9
    || (v2 = *(float **)v1, *(unsigned __int8 *)(*(_QWORD *)v1 + 3LL) != dword_89AD220)
    || v2 == (float *)-16LL )
  {
    sub_93B8C0(a1, a2: 1u, a3: "RaycastResult");
  }
  sub_938FD0((__int64)a1, a2: v2[4], a3: v2[5], a4: v2[6]);
  return 1;
}
```

Even though they look almost identical they're different.
