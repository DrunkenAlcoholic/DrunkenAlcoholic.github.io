---
title: "[Delphi] Beyluxe Password Decryption"
date: 2023-01-05 12:00:00 +0800
categories: [Code, Delphi]
tags: [decryption, beyluxe, code, delphi]
---

```pascal
Function Decrypt(sNickName, sHwID, sCrypted: String): String;
var
 aOutPut : array of string;
 iLen, i: Integer;
 sTemp, sFinal : String;
const
 iOffset = $74;
begin
 Result:= '';
 iLen:= length(sCrypted);
 
 If (iLen mod 3) <> 0 then
  begin
   Result:= 'incorrect encrypted password';
   exit;
  end;
 
 for i:= 0 to pred(iLen div 3) do
  begin
   sTemp:= sTemp + sNickName[(i mod length(sNickName))+ 1] + sHwID[(i mod length(sHwID))+ 1]
  end;
 
 Setlength(aOutPut, (iLen div 3));
 
 for i:= 0 to pred(Length(aOutPut)) do
  begin
   aOutPut[i]:= Copy(sCrypted,1,3);
   sFinal:=  sFinal + Chr((strtoint(aOutPut[i]) - (ord(sTemp[i+1]) xor 4)) - iOffset);
   Delete(sCrypted,1,3);
  end;
 
 aOutPut:= Nil;
 Result:= sFinal;
end;
```
