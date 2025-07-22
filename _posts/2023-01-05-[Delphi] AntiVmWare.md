---
title: "[Delphi] AntiVMWare"
date: 2023-01-05 12:00:00 +0800
categories: [Code, Delphi]
tags: [antivmware, code, delphi]
---

```pascal
Function AntiVMware():boolean;
begin
 try
  asm
   push edx;
   push ecx;
   push ebx;
   mov eax, 'VMXh';
   mov ebx, 0; // This can be any value except MAGIC
   mov ecx, 10; // "CODE" to get the VMware Version
   mov edx, 'VX'; // Port Number
   in eax, dx; // Read port
   //On return EAX returns the VERSION
   cmp ebx, 'VMXh'; // is it VMware
   setz Result; //Set flag state
   pop ebx;
   pop ecx;
   pop edx;
  end;
 except
  Result:= False;
 end;
end;

```

> Example

```pascal
if AntiVMware then
  MessageBox(0, 'VMware Instance Detected', 'VMware Detected', +MB_OK +MB_ICONINFORMATION)
  else
  MessageBox(0, 'No VMware Instance Detected', 'No VMware Detected', +MB_OK +MB_ICONINFORMATION);
```
