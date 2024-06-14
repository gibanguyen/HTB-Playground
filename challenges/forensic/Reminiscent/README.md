- `cat cat imageinfo.txt`

![img1](pics/img1.png)

- `python2 /opt/volatility/vol.py -f flounder-pc-memdump.elf --profile=Win7SP1x64 pslist`

```
Volatility Foundation Volatility Framework 2.6.1
Offset(V)          Name                    PID   PPID   Thds     Hnds   Sess  Wow64 Start                          Exit

------------------ -------------------- ------ ------ ------ -------- ------ ------ ------------------------------ ------------------------------
0xfffffa80006b7040 System                    4      0     83      477 ------      0 2017-10-04 18:04:27 UTC+0000
0xfffffa8001a63b30 smss.exe                272      4      2       30 ------      0 2017-10-04 18:04:27 UTC+0000
0xfffffa800169bb30 csrss.exe               348    328      9      416      0      0 2017-10-04 18:04:29 UTC+0000
0xfffffa8001f63b30 wininit.exe             376    328      3       77      0      0 2017-10-04 18:04:29 UTC+0000
0xfffffa8001efa500 csrss.exe               396    384      9      283      1      0 2017-10-04 18:04:29 UTC+0000
0xfffffa8001f966d0 winlogon.exe            432    384      4      112      1      0 2017-10-04 18:04:29 UTC+0000
0xfffffa8001fcdb30 services.exe            476    376     11      201      0      0 2017-10-04 18:04:29 UTC+0000
0xfffffa8001ff2b30 lsass.exe               492    376      8      590      0      0 2017-10-04 18:04:30 UTC+0000
0xfffffa8001fffb30 lsm.exe                 500    376     11      150      0      0 2017-10-04 18:04:30 UTC+0000
0xfffffa8002001b30 svchost.exe             600    476     12      360      0      0 2017-10-04 18:04:30 UTC+0000
0xfffffa800209bb30 VBoxService.ex          664    476     12      118      0      0 2017-10-04 18:04:30 UTC+0000
0xfffffa80020b5b30 svchost.exe             728    476      7      270      0      0 2017-10-04 18:04:30 UTC+0000
0xfffffa80021044a0 svchost.exe             792    476     21      443      0      0 2017-10-04 18:04:30 UTC+0000
0xfffffa8002166b30 svchost.exe             868    476     21      429      0      0 2017-10-04 18:04:30 UTC+0000
0xfffffa800217cb30 svchost.exe             900    476     41      977      0      0 2017-10-04 18:04:30 UTC+0000
0xfffffa80021ccb30 svchost.exe             988    476     13      286      0      0 2017-10-04 18:04:30 UTC+0000
0xfffffa8002204960 svchost.exe             384    476     17      386      0      0 2017-10-04 18:04:30 UTC+0000
0xfffffa8002294b30 spoolsv.exe            1052    476     13      277      0      0 2017-10-04 18:04:31 UTC+0000
0xfffffa80022bbb30 svchost.exe            1092    476     19      321      0      0 2017-10-04 18:04:31 UTC+0000
0xfffffa8002390620 svchost.exe            1196    476     28      333      0      0 2017-10-04 18:04:31 UTC+0000
0xfffffa8002245060 taskhost.exe           1720    476      8      148      1      0 2017-10-04 18:04:36 UTC+0000
0xfffffa8002122060 sppsvc.exe             1840    476      4      145      0      0 2017-10-04 18:04:37 UTC+0000
0xfffffa80022c8060 dwm.exe                2020    868      4       72      1      0 2017-10-04 18:04:41 UTC+0000
0xfffffa80020bb630 explorer.exe           2044   2012     36      926      1      0 2017-10-04 18:04:41 UTC+0000
0xfffffa80022622e0 VBoxTray.exe           1476   2044     13      146      1      0 2017-10-04 18:04:42 UTC+0000
0xfffffa80021b4060 SearchIndexer.         1704    476     16      734      0      0 2017-10-04 18:04:47 UTC+0000
0xfffffa80023ed550 SearchFilterHo          812   1704      4       92      0      0 2017-10-04 18:04:48 UTC+0000
0xfffffa80024f4b30 SearchProtocol         1960   1704      6      311      0      0 2017-10-04 18:04:48 UTC+0000
0xfffffa80007e0b30 thunderbird.ex         2812   2044     50      534      1      1 2017-10-04 18:06:24 UTC+0000
0xfffffa8000801b30 WmiPrvSE.exe           2924    600     10      204      0      0 2017-10-04 18:06:26 UTC+0000
0xfffffa8000945060 svchost.exe            2120    476     12      335      0      0 2017-10-04 18:06:32 UTC+0000
0xfffffa800096eb30 wmpnetwk.exe           2248    476     18      489      0      0 2017-10-04 18:06:33 UTC+0000
0xfffffa8000930b30 WmiPrvSE.exe            592    600      9      127      0      0 2017-10-04 18:06:35 UTC+0000
0xfffffa800224e060 powershell.exe          496   2044     12      300      1      0 2017-10-04 18:06:58 UTC+0000
0xfffffa8000e90060 conhost.exe            2772    396      2       55      1      0 2017-10-04 18:06:58 UTC+0000
0xfffffa8000839060 powershell.exe         2752    496     20      396      1      0 2017-10-04 18:07:00 UTC+0000
```

- `python2 /opt/volatility/vol.py -f flounder-pc-memdump.elf --profile=Win7SP1x64 filescan | grep resume`

![img2](pics/img2.png)

- `python2 /opt/volatility/vol.py -f flounder-pc-memdump.elf --profile=Win7SP1x64 dumpfiles -Q 0x000000001e8feb70 -D .`

![img3](pics/img3.png)

- `ls`

![img4](pics/img4.png)

- `strings file.None.0xfffffa80022ac740.dat`

![img5](pics/img5.png)

- Using **CyberChef** to decode Base64

![img6](pics/img6.png)

- Decode twice

![img7](pics/img7.png)

- Roll down to the bottom, you will see the flag
