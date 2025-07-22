---
title: "[Inc] Blowfish"
date: 2023-01-05 12:00:00 +0800
categories: [Main, Code, Delphi, Inc]
tags: [blowfish, inc, code, delphi]
---

usage: [[Keygen Code]]

#Delphi #Code #Unit

```pascal
//BF_Int.Inc
const

initialParray : TPArr = (
  $243F6A88, $85A308D3, $13198A2E, $03707344, $A4093822, $299F31D0,
  $082EFA98, $EC4E6C89, $452821E6, $38D01377, $BE5466CF, $34E90C6C,
  $C0AC29B7, $C97C50DD, $3F84D5B5, $B5470917, $9216D5D9, $8979FB1B
);

initialSbox1 : TSBox = (
  $D1310BA6, $98DFB5AC, $2FFD72DB, $D01ADFB7, $B8E1AFED, $6A267E96,
  $BA7C9045, $F12C7F99, $24A19947, $B3916CF7, $0801F2E2, $858EFC16,
  $636920D8, $71574E69, $A458FEA3, $F4933D7E, $0D95748F, $728EB658,
  $718BCD58, $82154AEE, $7B54A41D, $C25A59B5, $9C30D539, $2AF26013,
  $C5D1B023, $286085F0, $CA417918, $B8DB38EF, $8E79DCB0, $603A180E,
  $6C9E0E8B, $B01E8A3E, $D71577C1, $BD314B27, $78AF2FDA, $55605C60,
  $E65525F3, $AA55AB94, $57489862, $63E81440, $55CA396A, $2AAB10B6,
  $B4CC5C34, $1141E8CE, $A15486AF, $7C72E993, $B3EE1411, $636FBC2A,
  $2BA9C55D, $741831F6, $CE5C3E16, $9B87931E, $AFD6BA33, $6C24CF5C,
  $7A325381, $28958677, $3B8F4898, $6B4BB9AF, $C4BFE81B, $66282193,
  $61D809CC, $FB21A991, $487CAC60, $5DEC8032, $EF845D5D, $E98575B1,
  $DC262302, $EB651B88, $23893E81, $D396ACC5, $0F6D6FF3, $83F44239,
  $2E0B4482, $A4842004, $69C8F04A, $9E1F9B5E, $21C66842, $F6E96C9A,
  $670C9C61, $ABD388F0, $6A51A0D2, $D8542F68, $960FA728, $AB5133A3,
  $6EEF0B6C, $137A3BE4, $BA3BF050, $7EFB2A98, $A1F1651D, $39AF0176,
  $66CA593E, $82430E88, $8CEE8619, $456F9FB4, $7D84A5C3, $3B8B5EBE,
  $E06F75D8, $85C12073, $401A449F, $56C16AA6, $4ED3AA62, $363F7706,
  $1BFEDF72, $429B023D, $37D0D724, $D00A1248, $DB0FEAD3, $49F1C09B,
  $075372C9, $80991B7B, $25D479D8, $F6E8DEF7, $E3FE501A, $B6794C3B,
  $976CE0BD, $04C006BA, $C1A94FB6, $409F60C4, $5E5C9EC2, $196A2463,
  $68FB6FAF, $3E6C53B5, $1339B2EB, $3B52EC6F, $6DFC511F, $9B30952C,
  $CC814544, $AF5EBD09, $BEE3D004, $DE334AFD, $660F2807, $192E4BB3,
  $C0CBA857, $45C8740F, $D20B5F39, $B9D3FBDB, $5579C0BD, $1A60320A,
  $D6A100C6, $402C7279, $679F25FE, $FB1FA3CC, $8EA5E9F8, $DB3222F8,
  $3C7516DF, $FD616B15, $2F501EC8, $AD0552AB, $323DB5FA, $FD238760,
  $53317B48, $3E00DF82, $9E5C57BB, $CA6F8CA0, $1A87562E, $DF1769DB,
  $D542A8F6, $287EFFC3, $AC6732C6, $8C4F5573, $695B27B0, $BBCA58C8,
  $E1FFA35D, $B8F011A0, $10FA3D98, $FD2183B8, $4AFCB56C, $2DD1D35B,
  $9A53E479, $B6F84565, $D28E49BC, $4BFB9790, $E1DDF2DA, $A4CB7E33,
  $62FB1341, $CEE4C6E8, $EF20CADA, $36774C01, $D07E9EFE, $2BF11FB4,
  $95DBDA4D, $AE909198, $EAAD8E71, $6B93D5A0, $D08ED1D0, $AFC725E0,
  $8E3C5B2F, $8E7594B7, $8FF6E2FB, $F2122B64, $8888B812, $900DF01C,
  $4FAD5EA0, $688FC31C, $D1CFF191, $B3A8C1AD, $2F2F2218, $BE0E1777,
  $EA752DFE, $8B021FA1, $E5A0CC0F, $B56F74E8, $18ACF3D6, $CE89E299,
  $B4A84FE0, $FD13E0B7, $7CC43B81, $D2ADA8D9, $165FA266, $80957705,
  $93CC7314, $211A1477, $E6AD2065, $77B5FA86, $C75442F5, $FB9D35CF,
  $EBCDAF0C, $7B3E89A0, $D6411BD3, $AE1E7E49, $00250E2D, $2071B35E,
  $226800BB, $57B8E0AF, $2464369B, $F009B91E, $5563911D, $59DFA6AA,
  $78C14389, $D95A537F, $207D5BA2, $02E5B9C5, $83260376, $6295CFA9,
  $11C81968, $4E734A41, $B3472DCA, $7B14A94A, $1B510052, $9A532915,
  $D60F573F, $BC9BC6E4, $2B60A476, $81E67400, $08BA6FB5, $571BE91F,
  $F296EC6B, $2A0DD915, $B6636521, $E7B9F9B6, $FF34052E, $C5855664,
  $53B02D5D, $A99F8FA1, $08BA4799, $6E85076A
);

initialSbox2 : TSBox = (
  $4B7A70E9, $B5B32944, $DB75092E, $C4192623, $AD6EA6B0, $49A7DF7D,
  $9CEE60B8, $8FEDB266, $ECAA8C71, $699A17FF, $5664526C, $C2B19EE1,
  $193602A5, $75094C29, $A0591340, $E4183A3E, $3F54989A, $5B429D65,
  $6B8FE4D6, $99F73FD6, $A1D29C07, $EFE830F5, $4D2D38E6, $F0255DC1,
  $4CDD2086, $8470EB26, $6382E9C6, $021ECC5E, $09686B3F, $3EBAEFC9,
  $3C971814, $6B6A70A1, $687F3584, $52A0E286, $B79C5305, $AA500737,
  $3E07841C, $7FDEAE5C, $8E7D44EC, $5716F2B8, $B03ADA37, $F0500C0D,
  $F01C1F04, $0200B3FF, $AE0CF51A, $3CB574B2, $25837A58, $DC0921BD,
  $D19113F9, $7CA92FF6, $94324773, $22F54701, $3AE5E581, $37C2DADC,
  $C8B57634, $9AF3DDA7, $A9446146, $0FD0030E, $ECC8C73E, $A4751E41,
  $E238CD99, $3BEA0E2F, $3280BBA1, $183EB331, $4E548B38, $4F6DB908,
  $6F420D03, $F60A04BF, $2CB81290, $24977C79, $5679B072, $BCAF89AF,
  $DE9A771F, $D9930810, $B38BAE12, $DCCF3F2E, $5512721F, $2E6B7124,
  $501ADDE6, $9F84CD87, $7A584718, $7408DA17, $BC9F9ABC, $E94B7D8C,
  $EC7AEC3A, $DB851DFA, $63094366, $C464C3D2, $EF1C1847, $3215D908,
  $DD433B37, $24C2BA16, $12A14D43, $2A65C451, $50940002, $133AE4DD,
  $71DFF89E, $10314E55, $81AC77D6, $5F11199B, $043556F1, $D7A3C76B,
  $3C11183B, $5924A509, $F28FE6ED, $97F1FBFA, $9EBABF2C, $1E153C6E,
  $86E34570, $EAE96FB1, $860E5E0A, $5A3E2AB3, $771FE71C, $4E3D06FA,
  $2965DCB9, $99E71D0F, $803E89D6, $5266C825, $2E4CC978, $9C10B36A,
  $C6150EBA, $94E2EA78, $A5FC3C53, $1E0A2DF4, $F2F74EA7, $361D2B3D,
  $1939260F, $19C27960, $5223A708, $F71312B6, $EBADFE6E, $EAC31F66,
  $E3BC4595, $A67BC883, $B17F37D1, $018CFF28, $C332DDEF, $BE6C5AA5,
  $65582185, $68AB9802, $EECEA50F, $DB2F953B, $2AEF7DAD, $5B6E2F84,
  $1521B628, $29076170, $ECDD4775, $619F1510, $13CCA830, $EB61BD96,
  $0334FE1E, $AA0363CF, $B5735C90, $4C70A239, $D59E9E0B, $CBAADE14,
  $EECC86BC, $60622CA7, $9CAB5CAB, $B2F3846E, $648B1EAF, $19BDF0CA,
  $A02369B9, $655ABB50, $40685A32, $3C2AB4B3, $319EE9D5, $C021B8F7,
  $9B540B19, $875FA099, $95F7997E, $623D7DA8, $F837889A, $97E32D77,
  $11ED935F, $16681281, $0E358829, $C7E61FD6, $96DEDFA1, $7858BA99,
  $57F584A5, $1B227263, $9B83C3FF, $1AC24696, $CDB30AEB, $532E3054,
  $8FD948E4, $6DBC3128, $58EBF2EF, $34C6FFEA, $FE28ED61, $EE7C3C73,
  $5D4A14D9, $E864B7E3, $42105D14, $203E13E0, $45EEE2B6, $A3AAABEA,
  $DB6C4F15, $FACB4FD0, $C742F442, $EF6ABBB5, $654F3B1D, $41CD2105,
  $D81E799E, $86854DC7, $E44B476A, $3D816250, $CF62A1F2, $5B8D2646,
  $FC8883A0, $C1C7B6A3, $7F1524C3, $69CB7492, $47848A0B, $5692B285,
  $095BBF00, $AD19489D, $1462B174, $23820E00, $58428D2A, $0C55F5EA,
  $1DADF43E, $233F7061, $3372F092, $8D937E41, $D65FECF1, $6C223BDB,
  $7CDE3759, $CBEE7460, $4085F2A7, $CE77326E, $A6078084, $19F8509E,
  $E8EFD855, $61D99735, $A969A7AA, $C50C06C2, $5A04ABFC, $800BCADC,
  $9E447A2E, $C3453484, $FDD56705, $0E1E9EC9, $DB73DBD3, $105588CD,
  $675FDA79, $E3674340, $C5C43465, $713E38D8, $3D28F89E, $F16DFF20,
  $153E21E7, $8FB03D4A, $E6E39F2B, $DB83ADF7
);

initialSbox3 : TSBox = (
  $E93D5A68, $948140F7, $F64C261C, $94692934, $411520F7, $7602D4F7,
  $BCF46B2E, $D4A20068, $D4082471, $3320F46A, $43B7D4B7, $500061AF,
  $1E39F62E, $97244546, $14214F74, $BF8B8840, $4D95FC1D, $96B591AF,
  $70F4DDD3, $66A02F45, $BFBC09EC, $03BD9785, $7FAC6DD0, $31CB8504,
  $96EB27B3, $55FD3941, $DA2547E6, $ABCA0A9A, $28507825, $530429F4,
  $0A2C86DA, $E9B66DFB, $68DC1462, $D7486900, $680EC0A4, $27A18DEE,
  $4F3FFEA2, $E887AD8C, $B58CE006, $7AF4D6B6, $AACE1E7C, $D3375FEC,
  $CE78A399, $406B2A42, $20FE9E35, $D9F385B9, $EE39D7AB, $3B124E8B,
  $1DC9FAF7, $4B6D1856, $26A36631, $EAE397B2, $3A6EFA74, $DD5B4332,
  $6841E7F7, $CA7820FB, $FB0AF54E, $D8FEB397, $454056AC, $BA489527,
  $55533A3A, $20838D87, $FE6BA9B7, $D096954B, $55A867BC, $A1159A58,
  $CCA92963, $99E1DB33, $A62A4A56, $3F3125F9, $5EF47E1C, $9029317C,
  $FDF8E802, $04272F70, $80BB155C, $05282CE3, $95C11548, $E4C66D22,
  $48C1133F, $C70F86DC, $07F9C9EE, $41041F0F, $404779A4, $5D886E17,
  $325F51EB, $D59BC0D1, $F2BCC18F, $41113564, $257B7834, $602A9C60,
  $DFF8E8A3, $1F636C1B, $0E12B4C2, $02E1329E, $AF664FD1, $CAD18115,
  $6B2395E0, $333E92E1, $3B240B62, $EEBEB922, $85B2A20E, $E6BA0D99,
  $DE720C8C, $2DA2F728, $D0127845, $95B794FD, $647D0862, $E7CCF5F0,
  $5449A36F, $877D48FA, $C39DFD27, $F33E8D1E, $0A476341, $992EFF74,
  $3A6F6EAB, $F4F8FD37, $A812DC60, $A1EBDDF8, $991BE14C, $DB6E6B0D,
  $C67B5510, $6D672C37, $2765D43B, $DCD0E804, $F1290DC7, $CC00FFA3,
  $B5390F92, $690FED0B, $667B9FFB, $CEDB7D9C, $A091CF0B, $D9155EA3,
  $BB132F88, $515BAD24, $7B9479BF, $763BD6EB, $37392EB3, $CC115979,
  $8026E297, $F42E312D, $6842ADA7, $C66A2B3B, $12754CCC, $782EF11C,
  $6A124237, $B79251E7, $06A1BBE6, $4BFB6350, $1A6B1018, $11CAEDFA,
  $3D25BDD8, $E2E1C3C9, $44421659, $0A121386, $D90CEC6E, $D5ABEA2A,
  $64AF674E, $DA86A85F, $BEBFE988, $64E4C3FE, $9DBC8057, $F0F7C086,
  $60787BF8, $6003604D, $D1FD8346, $F6381FB0, $7745AE04, $D736FCCC,
  $83426B33, $F01EAB71, $B0804187, $3C005E5F, $77A057BE, $BDE8AE24,
  $55464299, $BF582E61, $4E58F48F, $F2DDFDA2, $F474EF38, $8789BDC2,
  $5366F9C3, $C8B38E74, $B475F255, $46FCD9B9, $7AEB2661, $8B1DDF84,
  $846A0E79, $915F95E2, $466E598E, $20B45770, $8CD55591, $C902DE4C,
  $B90BACE1, $BB8205D0, $11A86248, $7574A99E, $B77F19B6, $E0A9DC09,
  $662D09A1, $C4324633, $E85A1F02, $09F0BE8C, $4A99A025, $1D6EFE10,
  $1AB93D1D, $0BA5A4DF, $A186F20F, $2868F169, $DCB7DA83, $573906FE,
  $A1E2CE9B, $4FCD7F52, $50115E01, $A70683FA, $A002B5C4, $0DE6D027,
  $9AF88C27, $773F8641, $C3604C06, $61A806B5, $F0177A28, $C0F586E0,
  $006058AA, $30DC7D62, $11E69ED7, $2338EA63, $53C2DD94, $C2C21634,
  $BBCBEE56, $90BCB6DE, $EBFC7DA1, $CE591D76, $6F05E409, $4B7C0188,
  $39720A3D, $7C927C24, $86E3725F, $724D9DB9, $1AC15BB4, $D39EB8FC,
  $ED545578, $08FCA5B5, $D83D7CD3, $4DAD0FC4, $1E50EF5E, $B161E6F8,
  $A28514D9, $6C51133C, $6FD5C7E7, $56E14EC4, $362ABFCE, $DDC6C837,
  $D79A3234, $92638212, $670EFA8E, $406000E0
);

initialSbox4 : TSBox = (
  $3A39CE37, $D3FAF5CF, $ABC27737, $5AC52D1B, $5CB0679E, $4FA33742,
  $D3822740, $99BC9BBE, $D5118E9D, $BF0F7315, $D62D1C7E, $C700C47B,
  $B78C1B6B, $21A19045, $B26EB1BE, $6A366EB4, $5748AB2F, $BC946E79,
  $C6A376D2, $6549C2C8, $530FF8EE, $468DDE7D, $D5730A1D, $4CD04DC6,
  $2939BBDB, $A9BA4650, $AC9526E8, $BE5EE304, $A1FAD5F0, $6A2D519A,
  $63EF8CE2, $9A86EE22, $C089C2B8, $43242EF6, $A51E03AA, $9CF2D0A4,
  $83C061BA, $9BE96A4D, $8FE51550, $BA645BD6, $2826A2F9, $A73A3AE1,
  $4BA99586, $EF5562E9, $C72FEFD3, $F752F7DA, $3F046F69, $77FA0A59,
  $80E4A915, $87B08601, $9B09E6AD, $3B3EE593, $E990FD5A, $9E34D797,
  $2CF0B7D9, $022B8B51, $96D5AC3A, $017DA67D, $D1CF3ED6, $7C7D2D28,
  $1F9F25CF, $ADF2B89B, $5AD6B472, $5A88F54C, $E029AC71, $E019A5E6,
  $47B0ACFD, $ED93FA9B, $E8D3C48D, $283B57CC, $F8D56629, $79132E28,
  $785F0191, $ED756055, $F7960E44, $E3D35E8C, $15056DD4, $88F46DBA,
  $03A16125, $0564F0BD, $C3EB9E15, $3C9057A2, $97271AEC, $A93A072A,
  $1B3F6D9B, $1E6321F5, $F59C66FB, $26DCF319, $7533D928, $B155FDF5,
  $03563482, $8ABA3CBB, $28517711, $C20AD9F8, $ABCC5167, $CCAD925F,
  $4DE81751, $3830DC8E, $379D5862, $9320F991, $EA7A90C2, $FB3E7BCE,
  $5121CE64, $774FBE32, $A8B6E37E, $C3293D46, $48DE5369, $6413E680,
  $A2AE0810, $DD6DB224, $69852DFD, $09072166, $B39A460A, $6445C0DD,
  $586CDECF, $1C20C8AE, $5BBEF7DD, $1B588D40, $CCD2017F, $6BB4E3BB,
  $DDA26A7E, $3A59FF45, $3E350A44, $BCB4CDD5, $72EACEA8, $FA6484BB,
  $8D6612AE, $BF3C6F47, $D29BE463, $542F5D9E, $AEC2771B, $F64E6370,
  $740E0D8D, $E75B1357, $F8721671, $AF537D5D, $4040CB08, $4EB4E2CC,
  $34D2466A, $0115AF84, $E1B00428, $95983A1D, $06B89FB4, $CE6EA048,
  $6F3F3B82, $3520AB82, $011A1D4B, $277227F8, $611560B1, $E7933FDC,
  $BB3A792B, $344525BD, $A08839E1, $51CE794B, $2F32C9B7, $A01FBAC9,
  $E01CC87E, $BCC7D1F6, $CF0111C3, $A1E8AAC7, $1A908749, $D44FBD9A,
  $D0DADECB, $D50ADA38, $0339C32A, $C6913667, $8DF9317C, $E0B12B4F,
  $F79E59B7, $43F5BB3A, $F2D519FF, $27D9459C, $BF97222C, $15E6FC2A,
  $0F91FC71, $9B941525, $FAE59361, $CEB69CEB, $C2A86459, $12BAA8D1,
  $B6C1075E, $E3056A0C, $10D25065, $CB03A442, $E0EC6E0E, $1698DB3B,
  $4C98A0BE, $3278E964, $9F1F9532, $E0D392DF, $D3A0342B, $8971F21E,
  $1B0A7441, $4BA3348C, $C5BE7120, $C37632D8, $DF359F8D, $9B992F2E,
  $E60B6F47, $0FE3F11D, $E54CDA54, $1EDAD891, $CE6279CF, $CD3E7E6F,
  $1618B166, $FD2C1D05, $848FD2C5, $F6FB2299, $F523F357, $A6327623,
  $93A83531, $56CCCD02, $ACF08162, $5A75EBB5, $6E163697, $88D273CC,
  $DE966292, $81B949D0, $4C50901B, $71C65614, $E6C6C7BD, $327A140A,
  $45E1D006, $C3F27B9A, $C9AA53FD, $62A80F00, $BB25BFE2, $35BDD2F6,
  $71126905, $B2040222, $B6CBCF7C, $CD769C2B, $53113EC0, $1640E3D3,
  $38ABBD60, $2547ADF0, $BA38209C, $F746CE76, $77AFA1C5, $20756060,
  $85CBFE4E, $8AE88DD8, $7AAAF9B0, $4CF9AA7E, $1948C25C, $02FB8A8C,
  $01C36AE4, $D6EBE1F9, $90D4F869, $A65CDEA0, $3F09252D, $C208E69F,
  $B74E6132, $CE77E25B, $578FDFE3, $3AC372E6
);

==================================================================================================================================================================================================================
//Blowfish.pas

unit Blowfish;
{
  (c) 1998, 1999, 2000 Budi Sukmawan
  mailto:budskman [at] yahoo [dot] com
  http://www.bimacipta.com/

  1998.04.17 written by Budi Sukmawan
  1999.03.25 Add ECB, CBC, CTS, CFB, OFB routine.
  1999.11.06 Change Setup key routine.
             Fix CBC, CBC CTS, CFB, OFB routine.
  1999.12.03 change type casting at endian conversion
             small performance adv. [-12 clock/round)
  2000.04.21 Simplify routine for publication
             CBC mode only
}
interface

uses Windows, SysUtils;

const
  BF_BLOCKSIZE = 8;    { Blowfish block size }
  BF_SBOX_SIZE = 256;  { Number of S-box entries }
  BF_SBOX_SIZE_BYTES = ( BF_SBOX_SIZE * 4 );
  BF_PARRAY_SIZE = 18; { Number of P-array entries }
  BF_NO_ROUNDS = 16;
  IVSIZE = BF_BLOCKSIZE;

type
{$ifndef VER80}{$ifndef VER90}{$ifndef VER93}
{$ifndef VER100}{$ifndef VER110}
 {$define D4UP}
{$endif}{$endif}{$endif}{$endif}{$endif}

{$ifndef D4UP}
  LongWord = LongInt;
{$endif}

  TSBox = array [0..BF_SBOX_SIZE-1] of LongWord;
  TPArr = array [0..BF_PARRAY_SIZE-1] of LongWord;
  TBFBlock = array [0..BF_BLOCKSIZE-1] of Byte;
  TIV = array [0..IVSIZE-1] of Byte;
  PBA = PByteArray;
  PLA = ^TLongArray;
  TLongArray = array[0..(4*1024)-1] of LongWord;

{$I BF_Init.Inc}

type
  PBlowFishKey = ^TBlowFishKey;
  TBlowFishKey = record
    P: TPArr;                { P-array }
    S1, S2, S3, S4: TSBox;   { S-boxes }
  end;

  TCryptCtx = record
    { User encryption key }
    key: TBlowFishKey; { kunci Blowfish }
    IV,                { Initial IV }
    currentIV: TIV;    { IV }
  end;

  procedure bfEncrypt(const key: TBlowFishKey;const inBlock;var outBlock);
  procedure bfDecrypt(const key: TBlowFishKey;const inBlock;var outBlock);
  procedure bfKeySetup(var key: TBlowFishKey;const pUserKey;
                       userKeyLen: Integer );
  function bfSelfTest: Integer;
  procedure bfEncryptCBC(var cryptCtx: TCryptCtx; var pBuffer; bufLen: Integer);
  procedure bfDecryptCBC(var cryptCtx: TCryptCtx; var pBuffer; bufLen: Integer);
  procedure bfResetContext(var cryptCtx: TCryptCtx);
  function bfModeSelfTest: Integer;

implementation

procedure bfEncrypt(const key: TBlowFishKey;const inBlock;var outBlock);
var
  L, R, i: LongWord;

begin
  { get data  }
  L := (LongWord(TByteArray(inBlock)[0]) shl 24) or
       (LongWord(TByteArray(inBlock)[1]) shl 16) or
       (LongWord(TByteArray(inBlock)[2]) shl 8) or
        LongWord(TByteArray(inBlock)[3]);
  R := (LongWord(TByteArray(inBlock)[4]) shl 24) or
       (LongWord(TByteArray(inBlock)[5]) shl 16) or
       (LongWord(TByteArray(inBlock)[6]) shl 8) or
        LongWord(TByteArray(inBlock)[7]);
  { Perform 16 rounds of encryption }
  with key do
  begin
    i := 1;
    L := L xor P[0];
    while i <= BF_NO_ROUNDS do
    begin
      R := R xor P[i] xor
           (((S1[L shr 24] + S2[Byte(L shr 16)]) xor
              S3[Byte(L shr 8)]) + S4[Byte(L)]);
      inc(i);
      L := L xor P[i] xor
           (((S1[R shr 24] + S2[Byte(R shr 16)]) xor
              S3[Byte(R shr 8)]) + S4[Byte(R)]);
      inc(i);
    end;
    R := R xor P[BF_NO_ROUNDS + 1];
  end;
  { put data back }
  TByteArray(outBlock)[0] := R shr 24;
  TByteArray(outBlock)[1] := Byte(R shr 16);
  TByteArray(outBlock)[2] := Byte(R shr  8);
  TByteArray(outBlock)[3] := Byte(R);
  TByteArray(outBlock)[4] := L shr 24;
  TByteArray(outBlock)[5] := Byte(L shr 16);
  TByteArray(outBlock)[6] := Byte(L shr  8);
  TByteArray(outBlock)[7] := Byte(L);
end;

procedure bfDecrypt(const key: TBlowFishKey;const inBlock;var outBlock);
var
  L, R, i: LongWord;

begin
  { get data }
  R := (LongWord(TByteArray(inBlock)[0]) shl 24) or
       (LongWord(TByteArray(inBlock)[1]) shl 16) or
       (LongWord(TByteArray(inBlock)[2]) shl 8) or
        LongWord(TByteArray(inBlock)[3]);
  L := (LongWord(TByteArray(inBlock)[4]) shl 24) or
       (LongWord(TByteArray(inBlock)[5]) shl 16) or
       (LongWord(TByteArray(inBlock)[6]) shl 8) or
        LongWord(TByteArray(inBlock)[7]);
  { Perform 16 rounds of decryption }
  with key do
  begin
    i := BF_NO_ROUNDS;
    R := R xor P[BF_NO_ROUNDS + 1];
    while i >= 1 do
    begin
      L := L xor P[i] xor
           (((S1[R shr 24] + S2[Byte(R shr 16)]) xor
              S3[Byte(R shr 8)]) + S4[Byte(R)]);
      dec(i);
      R := R xor P[i] xor
           (((S1[L shr 24] + S2[Byte(L shr 16)]) xor
              S3[Byte(L shr 8)]) + S4[Byte(L)]);
      dec(i);
    end;
    L := L xor P[0];
  end;
  { put data back }
  TByteArray(outBlock)[0] := L shr 24;
  TByteArray(outBlock)[1] := Byte(L shr 16);
  TByteArray(outBlock)[2] := Byte(L shr  8);
  TByteArray(outBlock)[3] := Byte(L);
  TByteArray(outBlock)[4] := R shr 24;
  TByteArray(outBlock)[5] := Byte(R shr 16);
  TByteArray(outBlock)[6] := Byte(R shr  8);
  TByteArray(outBlock)[7] := Byte(R);
end;

{These only for key setup, no endian conversion needed}
procedure bfInitEncrypt(const key: TBlowFishKey;var data1, data2: LongWord);
var
  L, R, i: LongWord;
begin
  L := data1;
  R := data2;
  with key do
  begin
    i := 1;
    L := L xor P[0];
    while i <= BF_NO_ROUNDS do
    begin
      R := R xor P[i] xor
           (((S1[L shr 24] + S2[Byte(L shr 16)]) xor
              S3[Byte(L shr 8)]) + S4[Byte(L)]);
      inc(i);
      L := L xor P[i] xor
           (((S1[R shr 24] + S2[Byte(R shr 16)]) xor
              S3[Byte(R shr 8)]) + S4[Byte(R)]);
      inc(i);
    end;
    R := R xor P[BF_NO_ROUNDS + 1];
  end;
  data1 := R;
  data2 := L;
end;

procedure bfKeySetup(var key: TBlowFishKey;const pUserKey; userKeyLen: Integer);
var
  userKey: PByte;
  keyIndex, i, j, byteIndex: Integer;
  data1, data2: LongWord;
  sBox: PLA;
begin
  userKey := @pUserKey;
  for i := 0 to (BF_NO_ROUNDS + 2) - 1 do
    key.P[i] := initialParray[i];
  for i := 0 to BF_SBOX_SIZE-1 do
  begin
    key.S1[i] := initialSbox1[i];
    key.S2[i] := initialSbox2[i];
    key.S3[i] := initialSbox3[i];
    key.S4[i] := initialSbox4[i];
  end;
  keyIndex := 0;
  for i := 0 to (BF_NO_ROUNDS + 2) - 1 do
  begin
    data1 := 0;
    for byteIndex := 0 to 3 do
    begin
      data1 := data1 shl 8;
      data1 := data1 or LongWord(PByteArray(userKey)[keyIndex]);
      inc(keyIndex);
      keyIndex := keyIndex mod userKeyLen;
    end;
    key.P[i] := key.P[i] xor data1;
  end;
  data1 := 0;
  data2 := 0;
  i := 0 ;
  while i < (BF_NO_ROUNDS + 2) do
  begin
    bfInitEncrypt(key, data1, data2);
    key.P[i] := data1;
    key.P[i+1] := data2;
    inc(i,2);
  end;
  sBox := nil;
  for j := 0 to 3 do
  begin
    case j of
     0: sBox := @key.S1;
     1: sBox := @key.S2;
     2: sBox := @key.S3;
     3: sBox := @key.S4;
    end;
    i := 0;
    while i < BF_SBOX_SIZE do
    begin
      bfInitEncrypt(key, data1, data2);
      sBox[i] := data1;
      sBox[i+1] := data2;
      Inc(i, 2);
    end;
  end;
end;

(***************************************************************
 *                 Blowfish Mode of Operation                  *
 ***************************************************************)

procedure bfResetContext(var cryptCtx: TCryptCtx);
begin
  Move(cryptCtx.IV, cryptCtx.currentIV, IVSIZE);
end;

{ Encrypt data in CBC (Cipher Block Chaining) Mode}
procedure bfEncryptCBC(var cryptCtx: TCryptCtx; var pBuffer; bufLen: Integer);
var
  buffer, currentIV: PByte;
begin
  assert( ( bufLen mod BF_BLOCKSIZE ) = 0,
         'Data length is must be multiple of the block size');
  buffer := @pBuffer;
  currentIV := @cryptCtx.currentIV;
  while bufLen >= BF_BLOCKSIZE do
  begin
    PLA(buffer)^[0] := PLA(buffer)^[0] xor PLA(currentIV)^[0];
    PLA(buffer)^[1] := PLA(buffer)^[1] xor PLA(currentIV)^[1];
    bfEncrypt(cryptCtx.key, buffer^, buffer^);
    currentIV := buffer;
    Inc(buffer, BF_BLOCKSIZE);
    Dec(bufLen, BF_BLOCKSIZE);
  end;
  {Move(currentIV^, cryptCtx.currentIV, BF_BLOCKSIZE);}
  PLA(@cryptCtx.currentIV)^[0] := PLA(currentIV)^[0];
  PLA(@cryptCtx.currentIV)^[1] := PLA(currentIV)^[1];
end;

{ Decrypt data in CBC mode }
procedure bfDecryptCBC(var cryptCtx: TCryptCtx; var pBuffer; bufLen: Integer);
var
  buffer: PByte;
  temp: TbfBlock;
begin
  assert( ( bufLen mod BF_BLOCKSIZE ) = 0,
         'Data length is must be multiple of the block size');
  buffer := @pBuffer;
  while bufLen >= BF_BLOCKSIZE do
  begin
    {Move(buffer^, temp, BF_BLOCKSIZE);}
    PLA(@temp)^[0] := PLA(buffer)^[0];
    PLA(@temp)^[1] := PLA(buffer)^[1];
    bfDecrypt(cryptCtx.key, buffer^, buffer^);
    PLA(buffer)^[0] := PLA(buffer)^[0] xor PLA(@cryptCtx.currentIV)^[0];
    PLA(buffer)^[1] := PLA(buffer)^[1] xor PLA(@cryptCtx.currentIV)^[1];
    {Move(temp, cryptCtx.currentIV, BF_BLOCKSIZE);}
    PLA(@cryptCtx.currentIV)^[0] := PLA(@temp)^[0];
    PLA(@cryptCtx.currentIV)^[1] := PLA(@temp)^[1];
    Inc(buffer, BF_BLOCKSIZE);
    Dec(bufLen, BF_BLOCKSIZE);
  end;
end;

(***************************************************************
 *                      Blowfish Self Test                     *
 ***************************************************************)
type
  TBlock64 = array [0..7] of byte;
  TBfTest = record
    key: TBlock64;
    pt: TBlock64;
    ct: TBlock64;
  end;

const
  plain1: PChar = 'BLOWFISH';
  key1: PChar = 'abcdefghijklmnopqrstuvwxyz';
  cipher1: TBFBlock = ($32,$4E,$D0,$FE,$F4,$13,$A2,$03);

  plain2: TBFBlock = ($FE,$DC,$BA,$98,$76,$54,$32,$10);
  key2: PChar = 'Who is John Galt?';
  cipher2: TBFBlock = ($CC,$91,$73,$2B,$80,$22,$F6,$84);

  plain3: TBFBlock = ($FE, $DC, $BA, $98, $76, $54, $32, $10);
  key3: TBFBlock = ($41, $79, $6E, $A0, $52, $61, $6E, $E4);
  cipher3: TBFBlock = ($E1, $13, $F4, $10, $2C, $FC, $CE, $43);

  bfTest : array[0..33] of TBfTest = (
    (key : ($00, $00, $00, $00, $00, $00, $00, $00);
     pt  : ($00, $00, $00, $00, $00, $00, $00, $00);
     ct  : ($4E, $F9, $97, $45, $61, $98, $DD, $78)),
    (key : ($FF, $FF, $FF, $FF, $FF, $FF, $FF, $FF);
     pt  : ($FF, $FF, $FF, $FF, $FF, $FF, $FF, $FF);
     ct  : ($51, $86, $6F, $D5, $B8, $5E, $CB, $8A)),
    (key : ($30, $00, $00, $00, $00, $00, $00, $00);
     pt  : ($10, $00, $00, $00, $00, $00, $00, $01);
     ct  : ($7D, $85, $6F, $9A, $61, $30, $63, $F2)),
    (key : ($11, $11, $11, $11, $11, $11, $11, $11);
     pt  : ($11, $11, $11, $11, $11, $11, $11, $11);
     ct  : ($24, $66, $DD, $87, $8B, $96, $3C, $9D)),
    (key : ($01, $23, $45, $67, $89, $AB, $CD, $EF);
     pt  : ($11, $11, $11, $11, $11, $11, $11, $11);
     ct  : ($61, $F9, $C3, $80, $22, $81, $B0, $96)),
    (key : ($11, $11, $11, $11, $11, $11, $11, $11);
     pt  : ($01, $23, $45, $67, $89, $AB, $CD, $EF);
     ct  : ($7D, $0C, $C6, $30, $AF, $DA, $1E, $C7)),
    (key : ($00, $00, $00, $00, $00, $00, $00, $00);
     pt  : ($00, $00, $00, $00, $00, $00, $00, $00);
     ct  : ($4E, $F9, $97, $45, $61, $98, $DD, $78)),
    (key : ($FE, $DC, $BA, $98, $76, $54, $32, $10);
     pt  : ($01, $23, $45, $67, $89, $AB, $CD, $EF);
     ct  : ($0A, $CE, $AB, $0F, $C6, $A0, $A2, $8D)),
    (key : ($7C, $A1, $10, $45, $4A, $1A, $6E, $57);
     pt  : ($01, $A1, $D6, $D0, $39, $77, $67, $42);
     ct  : ($59, $C6, $82, $45, $EB, $05, $28, $2B)),
    (key : ($01, $31, $D9, $61, $9D, $C1, $37, $6E);
     pt  : ($5C, $D5, $4C, $A8, $3D, $EF, $57, $DA);
     ct  : ($B1, $B8, $CC, $0B, $25, $0F, $09, $A0)),
    (key : ($07, $A1, $13, $3E, $4A, $0B, $26, $86);
     pt  : ($02, $48, $D4, $38, $06, $F6, $71, $72);
     ct  : ($17, $30, $E5, $77, $8B, $EA, $1D, $A4)),
    (key : ($38, $49, $67, $4C, $26, $02, $31, $9E);
     pt  : ($51, $45, $4B, $58, $2D, $DF, $44, $0A);
     ct  : ($A2, $5E, $78, $56, $CF, $26, $51, $EB)),
    (key : ($04, $B9, $15, $BA, $43, $FE, $B5, $B6);
     pt  : ($42, $FD, $44, $30, $59, $57, $7F, $A2);
     ct  : ($35, $38, $82, $B1, $09, $CE, $8F, $1A)),
    (key : ($01, $13, $B9, $70, $FD, $34, $F2, $CE);
     pt  : ($05, $9B, $5E, $08, $51, $CF, $14, $3A);
     ct  : ($48, $F4, $D0, $88, $4C, $37, $99, $18)),
    (key : ($01, $70, $F1, $75, $46, $8F, $B5, $E6);
     pt  : ($07, $56, $D8, $E0, $77, $47, $61, $D2);
     ct  : ($43, $21, $93, $B7, $89, $51, $FC, $98)),
    (key : ($43, $29, $7F, $AD, $38, $E3, $73, $FE);
     pt  : ($76, $25, $14, $B8, $29, $BF, $48, $6A);
     ct  : ($13, $F0, $41, $54, $D6, $9D, $1A, $E5)),
    (key : ($07, $A7, $13, $70, $45, $DA, $2A, $16);
     pt  : ($3B, $DD, $11, $90, $49, $37, $28, $02);
     ct  : ($2E, $ED, $DA, $93, $FF, $D3, $9C, $79)),
    (key : ($04, $68, $91, $04, $C2, $FD, $3B, $2F);
     pt  : ($26, $95, $5F, $68, $35, $AF, $60, $9A);
     ct  : ($D8, $87, $E0, $39, $3C, $2D, $A6, $E3)),
    (key : ($37, $D0, $6B, $B5, $16, $CB, $75, $46);
     pt  : ($16, $4D, $5E, $40, $4F, $27, $52, $32);
     ct  : ($5F, $99, $D0, $4F, $5B, $16, $39, $69)),
    (key : ($1F, $08, $26, $0D, $1A, $C2, $46, $5E);
     pt  : ($6B, $05, $6E, $18, $75, $9F, $5C, $CA);
     ct  : ($4A, $05, $7A, $3B, $24, $D3, $97, $7B)),
    (key : ($58, $40, $23, $64, $1A, $BA, $61, $76);
     pt  : ($00, $4B, $D6, $EF, $09, $17, $60, $62);
     ct  : ($45, $20, $31, $C1, $E4, $FA, $DA, $8E)),
    (key : ($02, $58, $16, $16, $46, $29, $B0, $07);
     pt  : ($48, $0D, $39, $00, $6E, $E7, $62, $F2);
     ct  : ($75, $55, $AE, $39, $F5, $9B, $87, $BD)),
    (key : ($49, $79, $3E, $BC, $79, $B3, $25, $8F);
     pt  : ($43, $75, $40, $C8, $69, $8F, $3C, $FA);
     ct  : ($53, $C5, $5F, $9C, $B4, $9F, $C0, $19)),
    (key : ($4F, $B0, $5E, $15, $15, $AB, $73, $A7);
     pt  : ($07, $2D, $43, $A0, $77, $07, $52, $92);
     ct  : ($7A, $8E, $7B, $FA, $93, $7E, $89, $A3)),
    (key : ($49, $E9, $5D, $6D, $4C, $A2, $29, $BF);
     pt  : ($02, $FE, $55, $77, $81, $17, $F1, $2A);
     ct  : ($CF, $9C, $5D, $7A, $49, $86, $AD, $B5)),
    (key : ($01, $83, $10, $DC, $40, $9B, $26, $D6);
     pt  : ($1D, $9D, $5C, $50, $18, $F7, $28, $C2);
     ct  : ($D1, $AB, $B2, $90, $65, $8B, $C7, $78)),
    (key : ($1C, $58, $7F, $1C, $13, $92, $4F, $EF);
     pt  : ($30, $55, $32, $28, $6D, $6F, $29, $5A);
     ct  : ($55, $CB, $37, $74, $D1, $3E, $F2, $01)),
    (key : ($01, $01, $01, $01, $01, $01, $01, $01);
     pt  : ($01, $23, $45, $67, $89, $AB, $CD, $EF);
     ct  : ($FA, $34, $EC, $48, $47, $B2, $68, $B2)),
    (key : ($1F, $1F, $1F, $1F, $0E, $0E, $0E, $0E);
     pt  : ($01, $23, $45, $67, $89, $AB, $CD, $EF);
     ct  : ($A7, $90, $79, $51, $08, $EA, $3C, $AE)),
    (key : ($E0, $FE, $E0, $FE, $F1, $FE, $F1, $FE);
     pt  : ($01, $23, $45, $67, $89, $AB, $CD, $EF);
     ct  : ($C3, $9E, $07, $2D, $9F, $AC, $63, $1D)),
    (key : ($00, $00, $00, $00, $00, $00, $00, $00);
     pt  : ($FF, $FF, $FF, $FF, $FF, $FF, $FF, $FF);
     ct  : ($01, $49, $33, $E0, $CD, $AF, $F6, $E4)),
    (key : ($FF, $FF, $FF, $FF, $FF, $FF, $FF, $FF);
     pt  : ($00, $00, $00, $00, $00, $00, $00, $00);
     ct  : ($F2, $1E, $9A, $77, $B7, $1C, $49, $BC)),
    (key : ($01, $23, $45, $67, $89, $AB, $CD, $EF);
     pt  : ($00, $00, $00, $00, $00, $00, $00, $00);
     ct  : ($24, $59, $46, $88, $57, $54, $36, $9A)),
    (key : ($FE, $DC, $BA, $98, $76, $54, $32, $10);
     pt  : ($FF, $FF, $FF, $FF, $FF, $FF, $FF, $FF);
     ct  : ($6B, $5C, $5A, $9C, $5D, $9E, $0A, $5A))
  );

function bfSelfTest: Integer;
var
  bfKey: TBlowFishKey;
  buffer: TBlock64;
  i: Integer;
begin
  { Test #1 }
  Move(plain1^, buffer, 8 );
  bfKeySetup(bfKey, key1^, StrLen(key1));
  bfEncrypt(bfKey, buffer, buffer);
  if not (CompareMem(@buffer[0], @cipher1[0], 8 )) then
  begin
    Result := -11;
    exit;
  end;
  bfDecrypt(bfKey, buffer, buffer);
  if not (CompareMem(@buffer[0], @plain1^, 8 )) then
  begin
    Result := -21;
    exit;
  end;
  { Test #2 }
  Move(plain2, buffer, 8 );
  bfKeySetup(bfKey, key2^, StrLen(key2));
  bfEncrypt(bfKey, buffer, buffer);
  if not (CompareMem(@buffer[0], @cipher2[0], 8 )) then
  begin
    Result := -12;
    exit;
  end;
  bfDecrypt(bfKey, buffer, buffer);
  if not (CompareMem(@buffer[0], @plain2, 8 )) then
  begin
    Result := -22;
    exit;
  end;
  { Test #3 }
  Move(plain3, buffer, 8);
  bfKeySetup(bfKey, key3, SizeOf(key3));
  bfEncrypt(bfKey, buffer, buffer);
  if not (CompareMem(@buffer[0], @cipher3[0], 8 )) then
  begin
    Result := -13;
    exit;
  end;
  bfDecrypt(bfKey, buffer, buffer);
  if not (CompareMem(@buffer[0], @plain3, 8 )) then
  begin
    Result := -23;
    exit;
  end;
  { Test #4 }
  for i := 0 to (SizeOf(bfTest) div SizeOf(TBfTest))-1 do
  begin
    bfKeySetup(bfKey, bfTest[i].key, SizeOf(bfTest[i].key));
    Move(bfTest[i].pt, buffer, SizeOf(TBlock64));
    bfEncrypt(bfKey, buffer, buffer);
    if not CompareMem(@buffer, @bfTest[i].ct, SizeOf(TBlock64)) then
    begin
      Result := -100 - i ;
      Exit;
    end;
    bfDecrypt(bfKey, buffer, buffer);
    if not CompareMem(@buffer, @bfTest[i].pt, SizeOf(TBlock64)) then
    begin
      Result := -200 - i ;
      Exit;
    end;
  end;
  Result := 0;
end;

function bfModeSelfTest: Integer;
var
  data: PByte;
  retval: Integer;
  CryptCtx: TCryptCtx;
begin
  retval := 0;
  GetMem(data, SizeOf(bfTest));
  try
    Move(bfTest, data^, SizeOf(bfTest));
    {Init.}
    FillChar(CryptCtx, SizeOf(TCryptCtx), 0);
    bfKeySetup(CryptCtx.key, key1^, StrLen(key1));
    {Encrypt}
    bfResetContext(cryptCtx);
    bfEncryptCBC(cryptCtx, data^, SizeOf(bfTest));
    {Decrypt}
    bfResetContext(cryptCtx);
    bfDecryptCBC(cryptCtx, data^, SizeOf(bfTest));
    if not CompareMem(data, @bfTest, SizeOf(bfTest)) then
      retval := -300
  finally
    FreeMem(data, SizeOf(bfTest));
  end;
  Result := retval;
end;

end.
```
