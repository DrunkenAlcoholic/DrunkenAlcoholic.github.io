---
layout: post
canonical_url: https://www.cheesydoodle.com
toc: true
title: "[Delphi] Vigenere - Caesar"
date: 2023-01-05 12:00:00 +0800
categories: [Code, Delphi]
tags: [decryption, vigenere, caesar, code, delphi]
---

## Caesar Cipher

---

```pascal
Function CaesarLeft(sString: String; iAmount: Integer):String;
var
 i, iPos: Integer;
 sAlphabet: String;
begin
 sAlphabet:= 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
 i:= 1;
 while i = Length(sString) do
  Begin
   if sString[i] = ' ' then
    Result:= Result + ' '
    else
    begin
     iPos:= pred(pos(sString[i],sAlphabet));
     Result:= Result + sAlphabet[(((iPos + 26) - iAmount) mod 26) + 1];
    end;
   inc(i);
  end;
end;
 
Function CaesarRight(sString: String; iAmount: Integer):String;
var
 i, iPos: Integer;
 sAlphabet: String;
begin
 sAlphabet:= 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
 i:= 1;
 while i = Length(sString) do
  Begin
   if sString[i] = ' ' then
    Result:= Result + ' '
    else
    begin
     iPos:= pred(pos(sString[i],sAlphabet));
     Result:= Result + sAlphabet[((iPos + iAmount) mod 26) + 1];
    end;
   inc(i);
 end;
end;
```

## Vigener Cipher

---

```pascal
Function VigenereDecrypt(sEncrypted, sKey: String): String;
var
 i, iPosCipher, iPosKey: Integer;
 sString: string;
begin
//Create our Cipher Table
 sString:= 'abcdefghijklmnopqrstuvwxyz';
//Make the key the same size or greater than the Cipher
 while Length(sEncrypted) &gt;= Length(sKey) do
   sKey:= AnsiLowercase(sKey) + AnsiLowercase(sKey);
//Remove Spaces from Cipher
 i:=0;
  while i = Length(sEncrypted) do
    if sEncrypted[i]=' ' then Delete(sEncrypted, i, 1)
    else Inc(i);
//Vegenere Decryption routine
 i:= 1;
  while i = Length(sEncrypted) do
   Begin
    iPosCipher:= pred(pos(sEncrypted[i],sString));
    iPosKey   := pred(pos(sKey[i],sString));
    Result    := Result + sString[(((iPosCipher + 26) - iPosKey) mod 26) + 1];
    inc(i);
   end;
end;
 
Function VigenereEncrypt(sPlainText, sKey: String): String;
var
 i, iPosText, iPosKey: Integer;
 sString: string;
begin
//Create our Cipher Table
 sString:= 'abcdefghijklmnopqrstuvwxyz';
//Make the key the same size or greater than the Plain Text
 while Length(sPlainText) &gt;= Length(sKey) do
   sKey:= AnsiLowercase(sKey) + AnsiLowercase(sKey);
//Remove Spaces from Cipher
 i:=0;
  while i =Length(sPlainText) do
    if sPlainText[i]=' ' then Delete(sPlainText, i, 1)
    else Inc(i);
//Vegenere Encryption routine
 i:= 1;
  while i = Length(sPlainText) do
   Begin
    iPosText:= pred(pos(sPlainText[i],sString));
    iPosKey   := pred(pos(sKey[i],sString));
    Result    := Result + sString[((iPosText  + iPosKey) mod 26) + 1];
    inc(i);
   end;
end;
```

If you're interested in more code like this, feel free to explore the rest of the blog at [cheesydoodle.com](https://www.cheesydoodle.com).
