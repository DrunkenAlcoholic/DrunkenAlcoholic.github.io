---
title: "[Unit] uMultiMemPatch"
date: 2023-01-05 12:00:00 +0800
categories: [Main, Code, Delphi, Unit]
tags: [unit, patch, memory, code, delphi]
---

```pascal
(* *****************************************************
  Unit             : uMultiMemPatch
  Author           : Departure
  Url              : cheesydoodle.com

  Info:
     An Easy way to patch your Target in memory,
     Just add your VA and your array of bytes,
     it will load the target in suspended mode
     write the bytes to address(s) given and then
     resume the thread with new Patches.

  Usage:
   uses
    uMultiMemPatch;
   Var
    MyArrayOfPatches: APatchRec;
   Being
    AddPatch($0040107B,[$90,$90,$90],MyArrayOfPatches);
    AddPatch($004010B0,[$90,$EB],MyArrayOfPatches);
    WritePatches('CrackMe.exe', MyArrayOfPatches);
    MyArrayOfPatches:= Nil;
   end;
  ***************************************************** *)

unit uMultiMemPatch;

interface

uses
 Windows;

type
 TPatchRec = Record
  dwAddress: Dword;
  baPatches: Array of Byte;
 end;

type
 APatchRec = Array of TPatchRec;

 Procedure AddPatch(dwAddress: Dword; aPatches: Array of byte; var ArrayRecord: APatchRec);

implementation

Procedure AddPatch(dwAddress: Dword; aPatches: Array of byte; var ArrayRecord: APatchRec);
var
 Patch: TPatchRec;
 i: Integer;
begin
 {Set the Address}
 Patch.dwAddress:= dwAddress;
 {Set the Length of Patches}
 SetLength(Patch.baPatches, Length(aPatches));
 {Add the Patches}
 for i:= low(aPatches) to high(aPatches) do
  Patch.baPatches[i]:= aPatches[i];

 {Check if Array is already Built}
 if ArrayRecord = Nil then
   SetLength(ArrayRecord,1)
 else
  SetLength(ArrayRecord,Length(ArrayRecord) +1);
 {Add out Patches to the Array}
 ArrayRecord[high(ArrayRecord)]:= Patch;
end;

Function WritePatches(sFileName: String; ArrayPatches: APatchRec):Boolean;
var
 { Startup and variables used in procedure }
 StartInfo  : TStartupInfo;
 ProcInfo   : TProcessInformation;
 CreateOK   : Boolean;
 Write: Cardinal;
 i: Integer;
begin
  Result:= False;
 { Intinilize }
 FillChar(StartInfo,SizeOf(TStartupInfo),#0);
 FillChar(ProcInfo,SizeOf(TProcessInformation),#0);
 StartInfo.cb := SizeOf(TStartupInfo);

 { Create Process in a suspended state }
 CreateOK := CreateProcess(PChar(sFileName),nil, nil, nil,False,CREATE_SUSPENDED,nil, nil, StartInfo, ProcInfo);

 { check to see if successful }
 if CreateOK then
  try
   Begin
    for i:= low(ArrayPatches) to high(ArrayPatches) do
    { Write MultiPatch to memory }
     WriteProcessMemory(ProcInfo.hProcess,ptr(ArrayPatches[i].dwAddress),@ArrayPatches[i].baPatches,Length(ArrayPatches[i].baPatches[0]),Write);
    { Resume the thread }
    ResumeThread(ProcInfo.hThread);
    CloseHandle(ProcInfo.hProcess);
    Result:= True;
   end;
  except
   Result:= False;
  end;
end;

end.
```
