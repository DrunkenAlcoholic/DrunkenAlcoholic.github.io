---
title: "[Unit] uAddNewSectrionPE"
date: 2023-01-05 12:00:00 +0800
categories: [Code, Delphi, Unit]
tags: [unit, add section, code, delphi]
---


```pascal
(************************************
 Unit    : uAddNewSectionPE
 Author  : JEDI Code Library (JCL)
 Modded  : Departure
 Url     : cheesydoodle.com
************************************)
unit uAddNewSectionPE;

interface

Uses
 Windows, Classes, SysUtils;

function AddNewSection(sFileName, sNewSectionName: String; dwNewSectionSize, dwNewSectionCharacteristics: DWORD): Boolean;

implementation

function PeMapImgSections(const NtHeaders: PImageNtHeaders): PImageSectionHeader;
begin
  if NtHeaders = nil then
    Result := nil
  else
    Result := PImageSectionHeader(DWORD(@NtHeaders^.OptionalHeader) +
      NtHeaders^.FileHeader.SizeOfOptionalHeader);
end;

function PeMapImgFindSection(const NtHeaders: PImageNtHeaders;
  const SectionName: string): PImageSectionHeader;
var
  Header: PImageSectionHeader;
  I: Integer;
  P: PChar;
begin
  Result := nil;
  if NtHeaders &lt;&gt; nil then
  begin
    P := PChar(SectionName);
    Header := PeMapImgSections(NtHeaders);
    with NtHeaders^ do
      for I := 1 to FileHeader.NumberOfSections do
        if StrLComp(PChar(@Header^.Name), P, IMAGE_SIZEOF_SHORT_NAME) = 0 then
        begin
          Result := Header;
          Break;
        end
        else
          Inc(Header);
  end;
end;

function PeMapImgNtHeaders(const BaseAddress: Pointer): PImageNtHeaders;
begin
  Result := nil;
  if IsBadReadPtr(BaseAddress, SizeOf(TImageDosHeader)) then
    Exit;
  if (PImageDosHeader(BaseAddress)^.e_magic &lt;&gt; IMAGE_DOS_SIGNATURE) or
    (PImageDosHeader(BaseAddress)^._lfanew = 0) then
    Exit;
  Result := PImageNtHeaders(DWORD(BaseAddress) + DWORD(PImageDosHeader(BaseAddress)^._lfanew));
  if IsBadReadPtr(Result, SizeOf(TImageNtHeaders)) or
    (Result^.Signature &lt;&gt; IMAGE_NT_SIGNATURE) then
      Result := nil
end;

function AddNewSection(sFileName, sNewSectionName: String; dwNewSectionSize, dwNewSectionCharacteristics: DWORD): Boolean;
var
  ImageStream                       : TMemoryStream;
  NtHeaders                         : PImageNtHeaders;
  Sections, LastSection, NewSection : PImageSectionHeader;
  VirtualAlignedSize                : DWORD;
  I, X, NeedFill                    : Integer;

  procedure Alignment(var Value: DWORD; Alignment: DWORD);
  begin
    if (Value mod Alignment) &lt;&gt; 0 then
      Value := ((Value div Alignment) + 1) * Alignment;
  end;

begin

 ImageStream := TMemoryStream.Create;
  try
    try
      ImageStream.LoadFromFile(sFileName);
      NtHeaders := PeMapImgNtHeaders(ImageStream.Memory);
      Assert(NtHeaders &lt;&gt; nil);
      Sections := PeMapImgSections(NtHeaders);
      Assert(Sections &lt;&gt; nil);
      // Check whether there is not a section with the name already. This
      // should never occur.
      Assert(PeMapImgFindSection(NtHeaders, sNewSectionName) = nil);
      LastSection := Sections;
      Inc(LastSection, NtHeaders^.FileHeader.NumberOfSections - 1);
      NewSection := LastSection;
      Inc(NewSection);

      // Increase the number of sections
      Inc(NtHeaders^.FileHeader.NumberOfSections);
      FillChar(NewSection^, SizeOf(TImageSectionHeader), #0);
      // Virtual Address
      NewSection^.VirtualAddress := LastSection^.VirtualAddress + LastSection^.Misc.VirtualSize;
      Alignment(NewSection^.VirtualAddress, NtHeaders^.OptionalHeader.SectionAlignment);
      // Physical Ofset
      NewSection^.PointerToRawData := LastSection^.PointerToRawData + LastSection^.SizeOfRawData;
      Alignment(NewSection^.PointerToRawData, NtHeaders^.OptionalHeader.FileAlignment);
      // Section name
      StrPLCopy(PChar(@NewSection^.Name), sNewSectionName, IMAGE_SIZEOF_SHORT_NAME);
      // Characteristics flags
      NewSection^.Characteristics := dwNewSectionCharacteristics;

      // Size of virtual data area
      NewSection^.Misc.VirtualSize := dwNewSectionSize;
      VirtualAlignedSize := dwNewSectionSize;
      Alignment(VirtualAlignedSize, NtHeaders^.OptionalHeader.SectionAlignment);
      // Update Size of Image
      Inc(NtHeaders^.OptionalHeader.SizeOfImage, VirtualAlignedSize);
      // Raw data size
      NewSection^.SizeOfRawData := dwNewSectionSize;
      Alignment(NewSection^.SizeOfRawData, NtHeaders^.OptionalHeader.FileAlignment);
      // Update Initialized data size
      Inc(NtHeaders^.OptionalHeader.SizeOfInitializedData, NewSection^.SizeOfRawData);

      // Fill data to alignment
      NeedFill := Integer(NewSection^.SizeOfRawData) + dwNewSectionSize;

      // Note: Delphi linker seems to generate incorrect (unaligned) size of
      // the executable when adding data so the position could be
      // behind the size of the file then.
      ImageStream.Seek(NewSection^.PointerToRawData, soFromBeginning);

      X := 0;
      for I := 1 to NeedFill do
        ImageStream.WriteBuffer(X, 1);

      ImageStream.SaveToFile(sFileName);
      Result := True;
    except
      Result := False;
    end;
  finally
    ImageStream.Free;
  end;
end;

end.
```
