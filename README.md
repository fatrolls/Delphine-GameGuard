Easy AntiCheat coded in Delphi called (Delphine) used in MMORPG's

Here is the code to detect multiple instances of games running

Replace strings `tdphhelper` and `JesusOnMySide` to bypass the Client limit.

```
char IsGameRunning()
{
  int v0; // eax
  int v1; // eax
  int v3; // [esp+0h] [ebp-Ch] BYREF
  int v4; // [esp+4h] [ebp-8h]
  int v5; // [esp+8h] [ebp-4h]

  HIBYTE(v5) = sub_2E65139C("delphine");
  if ( !HIBYTE(v5) )
  {
    v0 = CheckString((int)"tdphhelper", (int)"dphhelper");
    HIBYTE(v5) = v0 != 0;
    if ( !v0 )
    {
      v4 = CheckString((int)"JesusOnMySide", 0);
      HIBYTE(v5) = v4 != 0;
      if ( v4 )
      {
        sub_2E5F77D0(v4, &v3);
        v1 = sub_2E5F6F58(v3, v4, v5);
        HIBYTE(v5) = v1 != v3;
      }
    }
  }
  return HIBYTE(v5);
}

void __usercall sub_2E6E7D58(int a1@<eax>, __int32 a2@<esi>)
{
  bool v2; // cf
  int v3; // eax
  int v4; // eax
  int v5; // ecx

  v2 = a1 == 0;
  v3 = a1 - 1;
  if ( v2 )
  {
    sub_2E6E2464("Delphine Unloaded");
    *off_2E6F0080 = 1;
    sub_2E6E33CC(0x3E8u);
    if ( *(_DWORD *)off_2E6F0118 )
      ((void (__cdecl *)(_DWORD))sub_2E5F6DC0)(*(_DWORD *)off_2E6F0118);
    sub_2E6E7B00();
  }
  else if ( !v3 )
  {
    sub_2E5F71C0("Loaded");
    *(_BYTE *)DetectGameRunning = IsGameRunning();
    if ( *(_BYTE *)DetectGameRunning )
    {
      if ( *MessageBoxTimeOutA )
        ((void (__stdcall *)(_DWORD, const char *, const char *, int, _DWORD, int))*MessageBoxTimeOutA)(
          0,
          "Another Game already running",
          "Error",
          16,
          0,
          10000);
      v4 = sub_2E5F6F50(0);
      sub_2E5F7280(v4);
      sub_2E5F6EC0(0);
    }
    else
    {
      *(_DWORD *)off_2E6F0118 = sub_2E5F6E10(0, 0, (int)"delphine");
      sub_2E6E7B48();
      sub_2E6D0E64(v5, a2);
    }
  }
}
```
