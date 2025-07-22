---
title: "[Delphi] Assorted Keygens"
date: 2023-01-05 12:00:00 +0800
categories: [Code, Delphi]
tags: [software, keygen, code, delphi]
---


##  Nidesoft Products
---
>Uses Blowfish encryption but with an easy implementation… fun to keygen but the Author uses the same method for all of there 74 products, Meaning you only need to change the Product name to make a valid serial with this keygen.

you will need the blowfish unit [[[Inc] Blowfish]]

```pascal
procedure TForm1.btnGenerateClick(Sender: TObject);
var
  bfKey: TBlowFishKey;
  bInput : array[0..7] of Byte;
  bOutput: array[0..7] of Byte;
  szKey: String;
  szResult: string;
  i: Integer;
begin
  //Set Key
  szKey := 'Nidesoft-DVD-Ripper';

  //Clear buffer
  ZeroMemory(@bOutput[0], SizeOf(bOutput));
  ZeroMemory(@bInput[0], SizeOf(bInput));

  //Random Bytes Max $01869F
  bInput[7]:= Random(Succ($9d));
  bInput[6]:= Random(Succ($85));
  bInput[5]:= Random($01);

  //Key Setup
  bfKeySetup(bfKey, PChar(szKey)^, Length(szKey));

  //Encryp bInput --> bOutput
  bfEncrypt(bfKey, bInput, bOutput);

  //Get Each byte and convert to hex Format
  for i:= Low(bOutput) to High(bOutput) do
   szResult:= szResult + Format('%2.x',[bOutput[i]]);


  //Small fix, Sometime Format function misses $0?
   szResult:= StringReplace(szResult,' ','0',[rfReplaceAll, rfIgnoreCase]);

  //Show Result
  edtSerial.Text := szResult;
end;
```


## Adrosoft Products
---
>Interesting to keygen as some of there products use images and from that it will get byte values based on X and Y coords



```pascal
var
  Form1: TForm1;
  szSoundRecorder1: array[0..49] of String = (
'1297','1397','1461','1556','1612','2407','2434','2503','2976','3156','3347','3487','3601','3930',
'4105','4118','4356','4363','4401','4543','4558','4852','4982','4993','5186','5377','5654','5691',
'5797','5897','5971','6130','6317','6323','6381','6556','6697','6750','7383','7609','7715','7846',
'7929','8160','8867','8985','9287','9377','9740','9982');

szSoundRecorder2: array[0..49] of String = (
'1157717132','1275215397','1566343884','2565740578','2662106601','2691296134','2891286439','2976152334',
'3129671956','3215798652','3310760636','3408623238','3613335510','3613792109','3682429757','4137188610',
'4342271231','4576195302','4794974223','4866392884','5488323045','5576649531','5705914986','5742793638',
'5843296280','5916854666','5928777782','6239733951','6354493062','6447348785','6470649685','6843086169',
'7137982050','7408689513','7590100831','7712302712','7803659454','7838394308','7873203406','8100684409',
'8552081097','8575123438','8692973288','8728706126','9211123348','9374109406','9507362991','9633769196',
'9755066544','9932579398');


szSteadyRecorder1: Array[0..49] of String = (
'1238','1601','1624','1644','2020','2113','2529','2668','3139','3159','3197','3353','3387','3661',
'3882','3907','4247','4255','4277','4359','4432','5020','5081','5382','5401','5424','5545','5551',
'6018','6076','6099','6107','6126','6363','6841','6953','7077','7100','7431','7572','7677','7735',
'8068','8399','8619','8707','9462','9573','9927','9962');


szSteadyRecorder2: Array[0..49] of String = (
'1114858741','1127105001','1963839159','2132061436','2456051912','2500866621','2932239558','2949368985',
'3101668639','3243491779','3325696050','3373698455','3431288880','3687540518','3773418839','4388281865',
'4388529623','4501905509','4740194923','4805155024','5108617667','5272795599','5352328513','5516555046',
'5766882768','5770665382','5909468076','6212638714','6254592756','6645432608','6945009815','6962820620',
'7149435581','7294514572','7454345566','7533933811','7534147160','7859129548','7862883647','8477070273',
'8724794490','8806707005','8842986005','8873265711','9117210666','9345222645','9434652776','9854114322',
'9894779199','9937214962');

szStereoChanger1: Array[0..49] of String = (
'1034','1480','1575','1658','2028','2265','2596','2735','2944','3172','3196','3409','3511','3808',
'3997','4265','4569','4615','4791','4835','5238','5682','5849','6641','6686','7037','7043','7093',
'7334','7351','7398','7541','7639','7744','7762','7775','7887','7980','8052','8106','8197','8325',
'8462','8771','8922','8947','9393','9768','9853','9942');


szStereoChanger2: Array[0..49] of String = (
'1223536486','1517517785','1647925016','2442271631','2453418468','2586131186','2926633000','2995371926',
'3104008057','3105696798','3231927752','3334642070','3463578617','3773500039','3961989463','4159237008',
'4201554809','4250839857','4630543438','4709558649','5128442399','5582647883','5594712632','5622971485',
'5839107984','5916293114','5979874236','6131027488','6133705762','6485280282','6701103859','6782761295',
'7207613548','7312684440','7441876834','7515449206','7531801001','7781632294','7806706729','8387567862',
'8614122330','8793518206','8809046969','8921834882','9346025534','9443548095','9590062526','9683174945',
'9886914921','9940493063');

szStreamRecorder1: Array[0..49] of String = (
'1014','1530','1542','1686','1941','1966','2203','2219','2256','2400','2759','3124','3153','3201',
'3275','3284','3303','3319','3370','3389','3511','3520','3558','3868','4336','4401','4534','4627',
'4978','5360','5710','5919','5978','6043','6829','6874','6892','7136','7384','7521','7605','7787',
'8149','8329','8727','8928','9108','9198','9457','9811');


szStreamRecorder2: Array[0..49] of String = (
'1222364893','1270287066','1305304841','2598545182','2631440264','2762461399','2790638874','2931377392',
'3102034965','3295791575','3783355659','3842655416','3858899737','3908279940','3975031660','4224548141',
'4435696301','4736102958','4972171360','4995983048','5177857047','5312949967','5382846674','5637988746',
'5770144611','5833220750','5906272922','6278033873','6751510988','6845650629','6964277929','6971848904',
'7207170241','7279800735','7295540016','7772188109','7785709066','7885915183','7889616924','8127366835',
'8165713559','8402192109','8640699795','8761334210','9274566738','9661052246','9711970467','9732086725',
'9874918627','9977903809');
implementation

{$R *.dfm}

procedure TForm1.btnGenerateClick(Sender: TObject);
var
  cColour: TColor;
  iX,iY: Integer;
  szResult: string;
const
  szTable: string = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ';
begin
 Randomize;

 case cbProducts.ItemIndex of
 0: begin
    //Part 1 of Serial
     iX:= Random(9);
     iY:= Random(9);
     cColour:= imCode1.Picture.Bitmap.Canvas.Pixels[iX,iY];
     szResult:= IntToStr(iX) + IntToStr(iY) + szTable[Succ(cColour and $FF)] + szTable[Succ((cColour shr 8) and $FF)] + szTable[Succ((cColour shr 16) and $FF)] + ' ';

     //Part 2 of Serial
     iX:= Random(9);
     iY:= Random(9);
     cColour:= imCode2.Picture.Bitmap.Canvas.Pixels[iX,iY];
     szResult:= szResult + IntToStr(iX) + IntToStr(iY) + szTable[Succ(cColour and $FF)] + szTable[Succ((cColour shr 8) and $FF)] + szTable[Succ((cColour shr 16) and $FF)] + ' ';

     //Part 3 of Serial
     iX:= Random(9);
     iY:= Random(9);
     cColour:= imCode3.Picture.Bitmap.Canvas.Pixels[iX,iY];
     szResult:= szResult + IntToStr(iX) + IntToStr(iY) + szTable[Succ(cColour and $FF)] + szTable[Succ((cColour shr 8) and $FF)] + szTable[Succ((cColour shr 16) and $FF)] + ' ';

     //Part 4 of Serial
     iX:= Random(9);
     iY:= Random(9);
     cColour:= imCode4.Picture.Bitmap.Canvas.Pixels[iX,iY];
     szResult:= szResult + IntToStr(iX) + IntToStr(iY) + szTable[Succ(cColour and $FF)] + szTable[Succ((cColour shr 8) and $FF)] + szTable[Succ((cColour shr 16) and $FF)];

    end;
 1: begin
     //Part 1 of Serial
     iX:= Random(9);
     iY:= Random(9);
     cColour:= imgCode1.Picture.Bitmap.Canvas.Pixels[iX,iY];
     szResult:= IntToStr(iX) + IntToStr(iY) + szTable[Succ(cColour and $FF)] + szTable[Succ((cColour shr 8) and $FF)] + szTable[Succ((cColour shr 16) and $FF)] + ' ';

     //Part 2 of Serial
     iX:= Random(9);
     iY:= Random(9);
     cColour:= imgCode2.Picture.Bitmap.Canvas.Pixels[iX,iY];
     szResult:= szResult + IntToStr(iX) + IntToStr(iY) + szTable[Succ(cColour and $FF)] + szTable[Succ((cColour shr 8) and $FF)] + szTable[Succ((cColour shr 16) and $FF)] + ' ';

     //Part 3 of Serial
     iX:= Random(9);
     iY:= Random(9);
     cColour:= imgCode3.Picture.Bitmap.Canvas.Pixels[iX,iY];
     szResult:= szResult + IntToStr(iX) + IntToStr(iY) + szTable[Succ(cColour and $FF)] + szTable[Succ((cColour shr 8) and $FF)] + szTable[Succ((cColour shr 16) and $FF)] + ' ';

     //Part 4 of Serial
     iX:= Random(9);
     iY:= Random(9);
     cColour:= imgCode4.Picture.Bitmap.Canvas.Pixels[iX,iY];
     szResult:= szResult + IntToStr(iX) + IntToStr(iY) + szTable[Succ(cColour and $FF)] + szTable[Succ((cColour shr 8) and $FF)] + szTable[Succ((cColour shr 16) and $FF)];

    end;
 2: begin szResult:= szSoundRecorder1[Random(Length(szSoundRecorder1))] + '-' + szSoundRecorder2[Random(Length(szSoundRecorder2))]; end;
 3: begin szResult:= szStreamRecorder1[Random(Length(szStreamRecorder1))] + '-' + szStreamRecorder2[Random(Length(szStreamRecorder2))]; end;
 4: begin
    //Part 1 of Serial
     iX:= Random(9);
     iY:= Random(9);
     cColour:= imC1.Picture.Bitmap.Canvas.Pixels[iX,iY];
     szResult:= IntToStr(iX) + IntToStr(iY) + szTable[Succ(cColour and $FF)] + szTable[Succ((cColour shr 8) and $FF)] + szTable[Succ((cColour shr 16) and $FF)] + ' ';

     //Part 2 of Serial
     iX:= Random(9);
     iY:= Random(9);
     cColour:= imC2.Picture.Bitmap.Canvas.Pixels[iX,iY];
     szResult:= szResult + IntToStr(iX) + IntToStr(iY) + szTable[Succ(cColour and $FF)] + szTable[Succ((cColour shr 8) and $FF)] + szTable[Succ((cColour shr 16) and $FF)] + ' ';

     //Part 3 of Serial
     iX:= Random(9);
     iY:= Random(9);
     cColour:= imC3.Picture.Bitmap.Canvas.Pixels[iX,iY];
     szResult:= szResult + IntToStr(iX) + IntToStr(iY) + szTable[Succ(cColour and $FF)] + szTable[Succ((cColour shr 8) and $FF)] + szTable[Succ((cColour shr 16) and $FF)] + ' ';

     //Part 4 of Serial
     iX:= Random(9);
     iY:= Random(9);
     cColour:= imC4.Picture.Bitmap.Canvas.Pixels[iX,iY];
     szResult:= szResult + IntToStr(iX) + IntToStr(iY) + szTable[Succ(cColour and $FF)] + szTable[Succ((cColour shr 8) and $FF)] + szTable[Succ((cColour shr 16) and $FF)];

    end;
 5: begin szResult:= szSteadyRecorder1[Random(Length(szSteadyRecorder1))] + '-' + szSteadyRecorder2[Random(Length(szSteadyRecorder2))]; end;
 6: begin szResult:= szStereoChanger1[Random(Length(szStereoChanger1))] + '-' + szStereoChanger2[Random(Length(szStereoChanger2))]; end;
 else
  szResult:= 'Must select a product first';
 end;

 edtSerial.Text:= szResult;
end;
```



## mIRC
---
> While generating a serial using this will provide a valid key, you either have to patch the phone home checks, or add the mIRC register server to your host file


```pascal
function Generate(const szName: string): string;
var
  iPos, iKey1, iKey2: Integer;
const
  iaMirc: array[0..35] of Integer = (11,6,17,12,12,14,5,12,16,10,11,6,
                                     14,14,4,11,9,12,11,10,8,10,8,10,
                                     10,16,8,4,6,10,12,16,8,10,4,16);
begin

  iKey1:= 0;
  iKey2:= 0;

  if ((Length(szName) > 3) and (Length(szName) < 36)) then
   begin
    for iPos:= 4 to Succ(Length(szName)) do
     begin
       iKey1:= iKey1 + (Ord(szName[iPos]) * iaMirc[iPos - 4]);
       iKey2:= iKey2 + (Ord(szName[iPos]) * Ord(szName[iPos - 1]) * iaMirc[iPos - 4]);
     end;
   end
   else
    Result:= 'Name Length Too Short/Long';

  Result:= IntToStr(iKey1) + '-' + IntToStr(iKey2);
end;
```

#Delphi #Code #Keygen 


## Sentry 3
---

```pascal
var
  Form1: TForm1;
const
  strPosTable  = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
  strSwapTable = 'DEFACzIJGHy01KS34VYZabcPQRjklmTo8pqrWXstuvLwdeBfghiMNOx256Un79';

implementation

{$R *.dfm}

function SHA1(const sBuffer: string): string;
var
  Context: TSHA1Context;
  Digest: TSHA1Digest;
  i: Integer;
begin
  SHA1Init(Context);
  SHA1Update(Context,@sBuffer[1],length(sBuffer));
  SHA1Final(Context,Digest);

  for i:= 0 to 19 do
   result := result + IntToHex(Digest[i],2);
end;


function SwapTable(const strSource: String):string;
var
  strFinal: string;
  i: Integer;
begin
   if Length(strSource) > 0 then
   begin
     for i:= 1 to Length(strSource) do
      if Pos(strSource[i],strPosTable) > 0 then
       strFinal:= strFinal + strSwapTable[Pos(strSource[i],strPosTable)]
      else
       strFinal:= strFinal + strSource[i]
   end;
  Result:= strFinal;
end;


procedure TForm1.btn1Click(Sender: TObject);
var
  strName, strEmail, strSerial1, strSerial2,
  strSerial3, strSerial4, strSerial5, strTemp: string;
const
  strSeperator = '-';
begin
  strName:= edtName.Text;
  strEmail:= edtEmail.Text;
  if (Length(strName) > 1) and (length(strEmail) > 1) then
   begin
    //Stage 1
    strSerial1:= Copy(SHA1(SwapTable(strName) + '.m' + strName + '3y'), 1, 5) + strSeperator;

    //Stage 2
    strTemp:= strEmail + '$' + strEmail;
    strTemp:= copy(strTemp,length(strTemp),1) + copy(strTemp,2,(length(strTemp) - 2)) + copy(strTemp,1,1);
    strSerial2:= Copy(SHA1(strTemp + SwapTable('p3' + strName + strEmail + '_x')), 1, 5) + strSeperator;

    //Stage 3
    strSerial3:= Copy(SHA1(SwapTable('0' + strName) + '. ' + strEmail + 'Q'), 1, 5) + strSeperator;

    //Stage 4
    strSerial4:= Copy(SHA1('f3' + strName + strEmail + 'yc3' + SwapTable('1' + strEmail + ']')), 1, 5) + strSeperator;

    //Stage 5
    strSerial5:= Copy(SHA1(';' + Copy(strName,2,Length(strName)) + '1330d' + Copy(strName,1,1) + '=N-'),1,5);

    edtResults.Text:= Concat(strSerial1,strSerial2,strSerial3,strSerial4,strSerial5);
   end
  else
   edtResults.Text:= 'Must fill in both Name & Email';
end;

end.
```



## MalwareBytes
---


```pascal
uses
  MD5;

function Malware():string;
var
  szCode, szHash, szSerial: string;
  iHex2Int, i: Integer;
const
  szTable: string = '0123456789ABCDEFGHJKLMNPQRTUVWXY';
begin
  Randomize;

  //Generate Code
  szCode:= Format('%d%s%s%d%d',[Random(10), szTable[Random(Pred(Length(szTable)))+1], szTable[Random(Pred(Length(szTable)))+1], Random(10), Random(10)]);

  //Create Hash From Code
  szHash:= StrMD5(szCode);

  //Convert Each byte in Hash string to Integer and bitwise(and)31 = Position in szTable
  for i:=0 to pred(Length(szHash) div 2) do
  begin
   //Insert Seperators every 4th Char
   if ((i mod 4 = 0) and (i > 1)) then
    szSerial:= szSerial + '-';
   //Convert Hash byte to Integer then Integer Result and 31 = position in szTable
   szSerial:= szSerial +  szTable[(StrToInt('$'+Copy(szHash, (i * 2) + 1, 2)) and 31) + 1];
  end;

  //Return  Code:Serial
  Result:= Format('%s:%s',[szCode, szSerial]);
end;
```



## WinASO Products
---
>Very easy products to keygem if starting from WinASO Disk Cleaner, As all there other products are based on this idea but slight variations, basic math to defeat WinASo Disk Cleaner, it idiv the sum of given part of serial with a constant value, if there is any remainder it will fail to register, so to defeat this wee find out what does multiply into these constants without going over the the max value(9999). the only part that is not calculated is the first poart of serial which can be anything from 0000…9999 (4 digits) the sum of second parts is idiv with constant 19, Sum of third part is idiv with 511, sum of Last part is idiv with 177. Also note that on newer products the position of each value is placed differently, and then in the “prized” software WinASO Registry Optimizer it also has a internet check. below is source for the basic Disk Cleaner. Hence the reason the code is setup to copy positions of each part of the serial, while not needed for Disk Cleaner, WinASO Easy Tweak is different positions.


```pascal
procedure TForm1.btnGenerateClick(Sender: TObject);
var
  szPart1, szPart2, szPart3, szPart4, szFinal: string;
begin
  Randomize;
  szPart1:= IntToStr(Random(8999)+ 1000); //RandomRange between 1000..9999
  szPart2:= IntToStr(19  * (Random(465)+ 55));
  szPart3:= IntToStr(511 * (Random(17)+2));
  szPart4:= IntToStr(177 * (Random(51)+5));

  szFinal:= szPart1;
  szFinal:= szFinal + Copy(szPart2,1,1)+ Copy(szPart2,4,1) + Copy(szPart2,2,1) + Copy(szPart2,3,1);
  szFinal:= szFinal + Copy(szPart3,4,1)+ Copy(szPart3,1,1) + Copy(szPart3,3,1) + Copy(szPart3,2,1);
  szFinal:= szFinal + Copy(szPart4,4,1)+ Copy(szPart4,2,1) + Copy(szPart4,1,1) + Copy(szPart4,3,1);

  mSerial.Text:= szFinal;

end;
```



## Xilisoft Products
---
>Xilisoft is very easy once you find how they are generating a valid serial, basically it does the following…
>
>-  must be equal or greater than $27 chars(39 decimal)  
>- must only contain chars A..F and 0..9 in other words hex format…..  
>- it takes the first part of the serial and prefixes the product name at the begining followed by 2 0′s  
>- it then take every second char and replaces it with position byte value, for example if the producted was called “xilisoftblah” it would produce “x#1l#2s#3f#4b#5a#6″ ect.. ect…  
>- it also prefixes “1″ at the very begining  
>- it then appends the product name at the very end  
>- it creates a MD5 hash of concated prefix, first part of serial, appended product name.  
>- takes this MD5 result and uses every second char for second part of serial with inserted “-”

```pascal
var
  Form1: TForm1;
  sPreFix: string = Char($31) + Char($58) + Char($01) + Char($6C) + Char($03) +
                    Char($73) + Char($05) + Char($66) + Char($07) + Char($6D) +
                    Char($09) + Char($76) + Char($0B) + Char($65) + Char($0D) +
                    Char($61) + Char($0F) + Char($65) + Char($11) + Char($69) +
                    Char($02) + Char($69) + Char($04) + Char($6F) + Char($06) +
                    Char($74) + Char($08) + Char($6F) + Char($0A) + Char($69) +
                    Char($0C) + Char($6D) + Char($0E) + Char($6B) + Char($10) +
                    Char($72) + Char($12) + Char($30) + Char($30);

  sRept: string = '5265-7074'; // Re-PT

  sSuffix: string = 'Xilisoftmoviemaker';

-------------------------------------------------------------------------------------

procedure TForm1.btnGenerateClick(Sender: TObject);
var
  sHashString, sRan, sMD5, sModedMD5, sLastPart: string;
  i: Integer;
begin

  Randomize;

  //Create random part of serial
  sRan := Format('-%2.x-%2.x-', [Random($FFFF), Random($FFFF)]);

  //Create string to be hashed with MD5
  sHashString := sPreFix + sRept + sRan + sSuffix;

  //Hash the String
  sMD5 := UpperCase(RivestStr(sHashString));

  //Copy every second char of MD5 result
  for i := 0 to Length(sMD5) do
    if i mod 2 = 0 then
      sModedMD5 := sModedMD5 + sMD5[i + 1];

  //Create last part of serial from Modded MD5 Result
  for i := 0 to Pred(Length(sModedMD5)) do
  begin
    if ((i > 0) and (i < Pred(Length(sModedMD5)))) then
      if i mod 4 = 0 then
        sLastPart := sLastPart + '-';
    sLastPart := sLastPart + sModedMD5[i + 1];
  end;

  //Display the result joined together
  mSerial.Text := sRept + sRan + Trim(sLastPart);
end;
```


