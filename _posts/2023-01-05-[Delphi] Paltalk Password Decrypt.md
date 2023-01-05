---
title: "[Delphi] Paltalk Password Decryption"
date: 2023-01-05 12:00:00 +0800
categories: [Code, Delphi]
tags: [decryption, paltalk, code, delphi]
---


```pascal
Function Decrypt(sNickName, sHwID, sCrypted: String): String;
var
aOutPut : array of string;
iLen, i : Integer;
sTemp, sFinal : String;
const
 iOffset = 122;
begin
 Result:= '';
 iLen:= length(sCrypted);

 If (iLen mod 4) <> 0 then
  begin
   Result:= 'incorrect encrypted password';
   exit;
  end;

 for i:= 0 to 7 do
  begin
   sTemp:= sTemp + sNickName[(i mod length(sNickName))+ 1] + sHwID[(i mod length(sHwID))+ 1]
  end;

 Setlength(aOutPut, (iLen div 4));

 If Length(sHwID) >= Length(sNickName) then
  sTemp:= sHwID[Length(sHwID)] + sTemp
  else
   sTemp:= sNickName[Length(sNickName)] + sTemp;

 for i:= 0 to pred(Length(aOutPut)) do
  begin
   aOutPut[i]:= Copy(sCrypted,1,3);
   sFinal:=  sFinal + Chr((strtoint(aOutPut[i]) - ord(sTemp[i+1])) - i - iOffset);
   Delete(sCrypted,1,4);
  end;

 aOutPut:= Nil;
 Result:= sFinal;

end;
```


>Example

```pascal
function FindNickPass(const sNickname: String): String;
begin
  with TRegistry.Create do
    try
      RootKey := HKEY_CURRENT_USER;
      if OpenKey('\Software\Paltalk\' + sNickname, False) then
       begin
        Result:= (ReadString('pwd'));
        CloseKey;
      end;
    finally
      Free;
    end;
end;

function FindVolumeSerial(const Drive : PChar) : string;
var
   VolumeSerialNumber : DWORD;
   MaximumComponentLength : DWORD;
   FileSystemFlags : DWORD;
begin
   Result:='';

   GetVolumeInformation(Drive, nil, 0, @VolumeSerialNumber,
                        MaximumComponentLength, FileSystemFlags, nil, 0) ;

   Result :=  Format('%8.8X',[VolumeSerialNumber]);
end;

procedure TForm1.Button1Click(Sender: TObject);
begin
Showmessage(Decrypt('Departure', trim(FindVolumeSerial('C:\')),FindNickPass('Departure')));
end;
```