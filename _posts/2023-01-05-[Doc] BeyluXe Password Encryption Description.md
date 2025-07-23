---
layout: post
canonical_url: https://www.cheesydoodle.com
toc: true
title: "[Doc] Beyluxe Password Encryption Description"
date: 2023-01-05 12:00:00 +0800
categories: [Blog, Posts]
tags: [decryption, encryption, beyluxe, code, doc]
---

**The Registry**

Beyluxe passwords are encrypted very similar to Paltalk, you can read that Article [here](https://web.archive.org/web/20130131043054/http://www.cheesydoodle.com/?p=27) about paltalk decrpytion from registry. BeyluXe saves your password in the Registry in a subkey under your nickname  HKEY_CURRENT_USER\Software\Beyluxe Messenger\  and the sub key “Password”  for example I could find the encrypted password for my nickname in the registry at “HKEY_CURRENT_USER\Software\Beyluxe Messenger\Departure\Password”.

**The Encrypted Password**

After retrieving the encrypted password from the registry it might look similar to “229226264233285234272” Which is my Encrypted password for BeyluXe, Just this alone tells us a few things, Divide the length of the password into 3 and you will have the length of the original password.. In my case the length of the encrypted password is 21 characters in length, So that would make my original password Length 7 characters long. Lets visualize splitting this encrypted password up into 3′s

“229226264233285234272”

229 = 1st char

226 = 2nd char

264 = 3th char

233 = 4th char

285 = 5th char

234= 6th char

272= 7th char

At the moment it does not tell us much except the length of the Unencrypted Password…

**Decryption Process**

The decryption process requires a couple of variables and some small mathematics, The variables required is the System Hard drive serial Number in Hex format and your username, These two variables get mix by using 1 char of user name and then 1 char of Hard drive Serial, Then concatenated  so the mixed string is equal or greater than the Unencrypted password length( in my case 7 characters) For Example My Hard drive serial in hex format is “8ED93AAE” and my Username is “Departure” so my mixed string would look like…

“D8eEpDa9r3tAuArEe We wont need to concatenate this string because its already longer than Unencrypted password length, The next stage is the mathematical part.

This is where our Encrypted password from the registry comes in to play, So we know our password is 7 characters long(by dividing Encrypted password by 3)  and we also know the encrypted value for each character of our password.  Now would be a good time to get familiar with the  [ASCII](https://web.archive.org/web/20130131043054/http://www.asciitable.com/) chart and understand for each character of the alphabet there is a decimal and a hex representation,  So with that in mind we do something like this to decrypt it.

1st Unencrypted Character = Char(229 - (ord(“D“) xor 4) – 116) = “1″

Let me try explain what just happened, we took the first 3 Encrypted password characters “229“, Then we took the decimal value(ord) of  ”D” and [Xor’ed](https://web.archive.org/web/20130131043054/http://en.wikipedia.org/wiki/XOR) it with 4, lets break this down a little more, going by the ASCII chart “D” = 68 in decimal, so we can say that “68 xor 4″ then we minuses 116 so the whole sum looks like “229 – (68 xor 4) – 116″

68 xor 4 = 64  so we can also say “229 – 64 – 116″ which of cause equals 49, So we convert 49 to its character value which is “1″ so the first Character of our password = “1″

Keeping the above logic lets decrypt the rest..

2nd Unencrypted Character = Char(226- (ord(“8“) xor 4) – 116) = “2″

3rd Unencrypted Character = Char(264- (ord(“e“) xor 4) – 116) = “3″

4th Unencrypted Character = Char(233- (ord(“E“) xor 4) – 116) = “4″

5th Unencrypted Character = Char(285- (ord(“p“) xor 4) – 116) = “5″

6th Unencrypted Character = Char(234- (ord(“D“) xor 4) – 116) = “6″

7th Unencrypted Character = Char(272- (ord(“a“) xor 4) – 116) = “7″

And we have the original Password which was “1234567″

To be continued……..

If you're interested in more code like this, feel free to explore the rest of the blog at [cheesydoodle.com](https://www.cheesydoodle.com).
