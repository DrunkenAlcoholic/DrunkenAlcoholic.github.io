---
title: "[C#] Vigenere - Caesar - Rot13"
date: 2023-01-05 12:00:00 +0800
categories: [Main, Code, C#]
tags: [vigenere, rot13, decrypt, code, c#]
---

```c#
using System;
/*
Class  : StringCrypt.cs
Aurthor: Departure
Url    : im-integrations.com
Info:
Encrypt Strings with Vigenere Cipher and ROT Cipher(Caesar Cipher, Rot13 ect..)
Based on information from wiki
*/
 
internal class StringCrypt
{
public static string Vigenere(string sSource, string sKey, int iTableSize = 94, bool bDecrypt = false)
{
//Variables
int i = 32;
int iPosText;
int iPosKey;
string sTable = "";
string sResult = "";

//Create Table
while (i &lt; (iTableSize + 32))             {                 sTable +=  ((char)i);                 i++;             }             //Make Key same size as Cipher             while (sSource.Length &gt;= sKey.Length)
{
sKey = string.Concat(sKey, sKey);
}

//Vigenere Routine
i = 0;
while (i &lt;= (sSource.Length - 1))
{
if (sTable.IndexOf(sSource[i]) == -1)
sResult += sSource[i];
else
{
iPosText = sTable.IndexOf(sSource[i]);
iPosKey = sTable.IndexOf(sKey[i]);
if (bDecrypt)
sResult += sTable[(((iPosText + iTableSize) - iPosKey) % iTableSize)];
else
sResult += sTable[((iPosText + iPosKey) % iTableSize)];
}
i++;

}

return sResult;

}

public static string Caesar(string sSource, int iKey, bool bDecrypt = false)
{
//Variables
string sResult = "";
string sTable = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
int iPosText;
int i;

//Convert to Uppercase
sSource = sSource.ToUpper();

//Caesar Routine
i = 0;
while (i &lt;= (sSource.Length - 1))
{
if (sTable.IndexOf(sSource[i]) == -1)
sResult += sSource[i];
else
{
iPosText = sTable.IndexOf(sSource[i]);
if (bDecrypt)
sResult += sTable[(((iPosText + sTable.Length) - iKey) % sTable.Length)];
else

sResult += sTable[((iPosText + iKey) % sTable.Length)];
}
i++;
}

return sResult;

}

public static string ROT13(string sSource)
{
return Caesar(sSource, 13, false);
}
}
```
