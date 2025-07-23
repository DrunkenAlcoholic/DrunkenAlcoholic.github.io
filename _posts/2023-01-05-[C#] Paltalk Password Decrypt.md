---
layout: post
canonical_url: https://www.cheesydoodle.com
toc: true
title: "[C#] Paltalk Password Decryptrion"
date: 2023-01-05 12:00:00 +0800
categories: [Code, C#]
tags: [paltalk, decrypt, code, c#]
---

```c#
        //Convert to Ordinal Value
        private int CharToAscii(char a)
        {
            return (int)a;
        }

        public string DecryptPaltalkPassWord(string sNickname,  string sHwId, string sCrypted)
        {
            //Some variables we will use
            string sTemp = "";
            string sFinal = "";
            string sCipher = sCrypted;
            int iLength = sCrypted.Length;

            //Check to make sure it divides into 4
            if (iLength % 4 != 0)
            {
                return "Incorrect encrypted password";
            }
            //Concatenate Nickname & HwId
            for (int i = 0; i <= 7; i++)
            {
                sTemp = sTemp + sNickname[i % sNickname.Length] + sHwId[i % sHwId.Length];
            }
            //Create an array
            string[] aOutPut = new string[iLength / 4];
            //Get longest char of either HwId or Nickname and add it to sTemp(Last longest chars is first to get processed)
            if (sHwId.Length >= sNickname.Length)
            {
                //If the HwID string is longer than password then add last char of to beginning of sTemp
                sTemp = sHwId[sHwId.Length - 1] + sTemp;
            }
            else
            {
                //If the sNickName string is longer than HwId then add last char of to beginning of sTemp
                sTemp = sNickname[sNickname.Length - 1] + sTemp;
            }
            //Process and calculate Password
            for (int i = 0; i <= (aOutPut.Length - 1); i++)
            {
                //Add the first 3 chars of encrypted string to our array(dropping the 4th as its not needed)
                aOutPut[i] = sCipher.Substring(0, 3);
                //Calculate char in password
                sFinal = sFinal + Convert.ToChar((Int32.Parse(aOutPut[i]) - CharToAscii(sTemp[i])) - i - 122);
                //Remove first 4 chars to get ready for processing next
                sCipher = sCipher.Remove(0, 4);
            }
            //Return our Password
            return sFinal;
        }
```

If you're interested in more code like this, feel free to explore the rest of the blog at [cheesydoodle.com](https://www.cheesydoodle.com).
