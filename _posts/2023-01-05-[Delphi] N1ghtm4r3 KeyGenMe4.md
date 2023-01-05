---
title: "[Delphi] Nightm4r3 KeyGenMe4"
date: 2023-01-05 12:00:00 +0800
categories: [Code, Delphi]
tags: [keygen, decrypt, code, delphi]
---


```pascal
const
 szBase = 'BCWHSENF91JTLDYMOP2KR4A5';

implementation

{$R *.dfm}

Function Sum(const szInput: String):Integer;
var
 i, iSum, iTotal: Integer;
begin

 iTotal:= 0;
 iSum:= 0;

 for i:= 1 to Length(szInput) do
  begin
   iSum:= ($17 - (Length(szBase) - pos(szInput[i],szBase)));
   iTotal:= iTotal + (ord(szInput[i]) * iSum);
  end;

 Result:= ((iTotal * $4E) + $6486568 + 1);
end;

Function GenSerial (const iSum: Integer; szRandom: String): String;
var
 i, iCalc, iPos : Integer;
 szSerial: String;

begin
 iCalc:= iSum;
 iPos:= 0;

 for i:= 1 to 6 do
  begin
   iPos:= iCalc mod $18;
   szSerial:= szSerial + (szBase[iPos + 1]);
   iCalc:= iCalc div $18;
  end;

 Result:= ReverseString(szSerial);
end;

procedure TForm1.Button1Click(Sender: TObject);
var
 i, iSum: integer;
 szRandom, szSerial: String;
begin
 iSum:= 0;
 Randomize;
 for i:= 1 to 6 do
  szRandom:= szRandom + szBase[Random(pred(Length(szBase)))];

 iSum:= Sum(szRandom);
 edSerial.Text:= szRandom + '-' + GenSerial(iSum, szRandom);

end;
```
