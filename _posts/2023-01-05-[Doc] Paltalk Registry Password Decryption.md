---
title: "[Doc] Paltalk Registry Password Decryption"
date: 2023-01-05 12:00:00 +0800
categories: [Blog, Posts]
tags: [decryption, encryption, paltalk, registry, code, doc]
---

String1 = 1 charactor from username and 1 charactor from HD serial

so if ..

Username = Departure

HD serial = 08DE56F

Then String1 would = D0e8pDaEr5t6uFre

Now we take String1 and add i together 3 times…

String2 = String1 + String1 +String1

String2 = D0e8pDaEr5t6uFreD0e8pDaEr5t6uFreD0e8pDaEr5t6uFre

Okay now we know this string…

in the password kept in the registry of paltalk we have 4 digits for each character of password, for example if my password was “Freak”

then paltalk registry would like this

F r e a k

xxxx xxxx xxxx xxxx xxxx <— paltalk registry encrypted password.

So thats a 5 Character password, in each 4 digits (xxxx) we drop the last digit, its not used and has something to do with time, Say for example the 5 lots of digits looked like this…

2341 8256 2516 4098 3789

we would drop the last digit of each group of digits like this

234 825 251 409 378

so now we **start from the LAST** character of our String2 and we create something

like this…

String2 = D0e8pDaEr5t6uFreD0e8pDaEr5t6uFreD0e8pDaEr5t6uFre <— Last Charactor gets processed first

paltalk registry encrypted value after droping last digit = 234 825 251 409 378

So…….

1st Password Char = char(234 – ascii code(e) – 0 – 122)  <— Last Character of our mixed string

2nd Password Char = char(825 – ascii code(D) – 1 – 122)

3rd Password Char = char(251 – ascii code(0) – 2 – 122)

4th Password Char = char(409 – ascii code(e) – 3 – 122)

5th Password Char = char(378 – ascii code(8) – 5 – 122)

Notice how we get the Ordinal value of each char?

example from above..

ascii values: e = 101, D = 68, 0 = 48, e = 101, 8 = 56

so the sum would look like this…

1st. 234 – 101 – 0 – 122 = 11

2nd 825 – 68 – 1 – 122 = 634

3rd 251 – 48 – 2 – 122 = 79

4th 409 – 101 – 3 – 122 = 183

5th 378 – 56 – 4 -122 = 196

Then just convert the result for each charactor back to ascii, No point doing it for this eaxmple as I just made these values up randomly and proberly wont convert to a real value in the ascii table…

Hope you get the idea of how to decrypt the paltalk encrypted passwords from registry, here is an example coded in delphi…

```pascal
Function Decrypt(sNickName, sHwID, sCrypted: String): String;
var
aOutPut : array of string;
iLen, i: Integer;
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

You might have noticed I didn’t Concatenate the mixed string 3 times,  
This is because Max passwords length is 12 and min password length is 5, as with the username.

## [Paltalk Website Login Decryption](https://web.archive.org/web/20120625140306/http://www.cheesydoodle.com/?p=20 "Permalink to Paltalk Website Login Decryption")

Posted by [Departure](https://web.archive.org/web/20120625140306/http://www.cheesydoodle.com/?author=1 "View all posts by Departure") on [February 8, 2010](https://web.archive.org/web/20120625140306/http://www.cheesydoodle.com/?p=20 "09:53") [3 comments](https://web.archive.org/web/20120625140306/http://www.cheesydoodle.com/?p=20#comments "Comment on Paltalk Website Login Decryption")

[](https://web.archive.org/web/20120625140306/http://www.cheesydoodle.com/?p=20 "Paltalk Website Login Decryption")

well I was  checking with different nicknames that use the password 123456 and it seems every nick I tested had the same encryption string, Which means paltalk has pre set value for each position of the password, then it just adds the matching charactor of your password

**Example:**

1.Position 1 of password = 241

2.Position 2 of password = 287

3.Position 3 of password = 302

4.Position 4 of password = 303

5.Position 5 of password = 307

6.Position 6 of password = 324

Now if you have a password “123456″ then

Position Paltalk Your password Result Final 1. 241 + 1 = 242 + RandomNumber 2. 287 + 2 = 289 + RandomNumber 3. 302 + 3 = 305 + RandomNumber 4. 303 + 4 = 307 + RandomNumber 5. 307 + 5 = 312 + RandomNumber 6. 324 + 6 = 330 + RandomNumber

Or lets say you had a password with “476987″

Position Paltalk Your password Result Final 1. 241 + 4 = 245 + RandomNumber 2. 287 + 7 = 294 + RandomNumber 3. 302 + 6 = 308 + RandomNumber 4. 303 + 9 = 312 + RandomNumber 5. 307 + 8 = 315 + RandomNumber 6. 324 + 7 = 331 + RandomNumber

Test it for your self, make a new nick with a password “476987″ and see if you get the same result ![;)](https://web.archive.org/web/20120625140306im_/http://www.cheesydoodle.com/wp-includes/images/smilies/icon_wink.gif)

X = Random Number

so the pass should look like this: 245X294X308X312X315X331X

**Update:**

Paltalk Only allows 12 characters max length for password, so here are the paltalk static numbers for each positions

1.241

2.287

3.302

4.303

5.307

6.324

7.244

8.331

9.307

10.321

11.232

12.289

I got this by using a password “000000000000″ then removing the random number, as you can see it matches in perfect with what I was explaining above ![;)](https://web.archive.org/web/20120625140306im_/http://www.cheesydoodle.com/wp-includes/images/smilies/icon_wink.gif)

so my paltalk encrypted password = “241928743028303730703240244233193071321423242898″

Now to make a password stealer would be very easy, But because im against that sort of activity I wont be explaining the methods you need to use.

**Update 2:**

here are the character values if you use ascii in your password

“a..z” = “49..74″ for Example (“a” = 49) (“b” = 50) (“c” = 51) ect….

This is for lower case characters!!

“A..Z” = “17..42″ for Example (“A” = 17) (“B” = 18) (“C” = 19) ect….

This is for Upper case characters!!

Example if I had a password called “cunix1″ the value you need to add to the paltalk static positions would be

1. 51 = c

2. 69 = u

3. 62 = n

4. 57 = i

5. 72 = x

6. 1 = 1

so going by our paltalk magic numbers…

Position Paltalk Your password Result Final 1. 241 + 51 = 292 + RandomNumber 2. 287 + 69 = 356 + RandomNumber 3. 302 + 62 = 364 + RandomNumber 4. 303 + 57 = 360 + RandomNumber 5. 307 + 72 = 379 + RandomNumber 6. 324 + 1 = 325 + RandomNumber

X = Random Number

your encrypted password = 292X356X364X360X379X325X
