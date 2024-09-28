# Challenge Rootme 3

Lien : https://www.root-me.org/fr/Challenges/Forensic/Command-Control-niveau-3

### Objectif : 

**Trouver le chemin du malware hashé en MD5**

A l'aide de Volatility 2 :

    volatility -f ch2.dmp --profile=Win7SP1x86_23418 pstree 

Output : 

    Volatility Foundation Volatility Framework 2.6
    Name                                                  Pid   PPid   Thds   Hnds Time
    -------------------------------------------------- ------ ------ ------ ------ ----
    0x892ac2b8:wininit.exe                               456    396      3     77 2013-01-12 16:38:14 UTC+0000
    . 0x896294c0:services.exe                             560    456      6    205 2013-01-12 16:38:16 UTC+0000
    .. 0x89805420:svchost.exe                             832    560     19    435 2013-01-12 16:38:23 UTC+0000
    ... 0x87c90d40:audiodg.exe                           1720    832      5    117 2013-01-12 16:58:11 UTC+0000
    .. 0x89852918:svchost.exe                             904    560     17    409 2013-01-12 16:38:24 UTC+0000
    ... 0x87ad44d0:dwm.exe                               2496    904      5     77 2013-01-12 16:40:25 UTC+0000
    .. 0x898b2790:svchost.exe                            1172    560     15    475 2013-01-12 16:38:27 UTC+0000
    .. 0x89f3d2c0:svchost.exe                            3352    560      9    141 2013-01-12 16:40:58 UTC+0000
    .. 0x898fbb18:SearchIndexer.                         2900    560     13    636 2013-01-12 16:40:38 UTC+0000
    .. 0x8986b030:svchost.exe                             928    560     26    869 2013-01-12 16:38:24 UTC+0000
    .. 0x8a1d84e0:vmtoolsd.exe                           1968    560      6    220 2013-01-12 16:39:14 UTC+0000
    .. 0x8962f030:svchost.exe                             692    560     10    353 2013-01-12 16:38:21 UTC+0000
    .. 0x898911a8:svchost.exe                            1084    560     10    257 2013-01-12 16:38:26 UTC+0000
    .. 0x898a7868:AvastSvc.exe                           1220    560     66   1180 2013-01-12 16:38:28 UTC+0000
    .. 0x89f1d3e8:svchost.exe                            3624    560     14    348 2013-01-12 16:41:22 UTC+0000
    .. 0x9542a030:TPAutoConnSvc.                         1612    560      9    135 2013-01-12 16:39:23 UTC+0000
    ... 0x87ae2880:TPAutoConnect.                        2568   1612      5    146 2013-01-12 16:40:28 UTC+0000
    .. 0x88cded40:sppsvc.exe                             1872    560      4    143 2013-01-12 16:39:02 UTC+0000
    .. 0x8a102748:svchost.exe                            1748    560     18    310 2013-01-12 16:38:58 UTC+0000
    .. 0x8a0f9c40:spoolsv.exe                            1712    560     14    338 2013-01-12 16:38:58 UTC+0000
    .. 0x9541c7e0:wlms.exe                                336    560      4     45 2013-01-12 16:39:21 UTC+0000
    .. 0x8a1f5030:VMUpgradeHelpe                          448    560      4     89 2013-01-12 16:39:21 UTC+0000
    ... 0x892ced40:winlogon.exe                           500    448      3    111 2013-01-12 16:38:14 UTC+0000
    ... 0x88d03a00:csrss.exe                              468    448     10    471 2013-01-12 16:38:14 UTC+0000
    .... 0x87c595b0:conhost.exe                          3228    468      2     54 2013-01-12 16:44:50 UTC+0000
    .... 0x87a9c288:conhost.exe                          2600    468      1     35 2013-01-12 16:40:28 UTC+0000
    .... 0x954826b0:conhost.exe                          2168    468      2     49 2013-01-12 16:55:50 UTC+0000
    .. 0x87bd35b8:wmpnetwk.exe                           3176    560      9    240 2013-01-12 16:40:48 UTC+0000
    .. 0x87ac0620:taskhost.exe                           2352    560      8    149 2013-01-12 16:40:24 UTC+0000
    .. 0x897b5c20:svchost.exe                             764    560      7    263 2013-01-12 16:38:23 UTC+0000
    . 0x8962f7e8:lsm.exe                                  584    456     10    142 2013-01-12 16:38:16 UTC+0000
    . 0x896427b8:lsass.exe                                576    456      6    566 2013-01-12 16:38:16 UTC+0000
    0x8929fd40:csrss.exe                                 404    396      9    469 2013-01-12 16:38:14 UTC+0000
    0x87978b78:System                                      4      0    103   3257 2013-01-12 16:38:09 UTC+0000
    . 0x88c3ed40:smss.exe                                 308      4      2     29 2013-01-12 16:38:09 UTC+0000
    0x87ac6030:explorer.exe                             2548   2484     24    766 2013-01-12 16:40:27 UTC+0000
    . 0x87b6b030:iexplore.exe                            2772   2548      2     74 2013-01-12 16:40:34 UTC+0000
    .. 0x89898030:cmd.exe                                1616   2772      2    101 2013-01-12 16:55:49 UTC+0000
    . 0x95495c18:taskmgr.exe                             1232   2548      6    116 2013-01-12 16:42:29 UTC+0000
    . 0x87bf7030:cmd.exe                                 3152   2548      1     23 2013-01-12 16:44:50 UTC+0000
    .. 0x87cbfd40:winpmem-1.3.1.                         3144   3152      1     23 2013-01-12 16:59:17 UTC+0000
    . 0x898fe8c0:StikyNot.exe                            2744   2548      8    135 2013-01-12 16:40:32 UTC+0000
    . 0x87b784b0:AvastUI.exe                             2720   2548     14    220 2013-01-12 16:40:31 UTC+0000
    . 0x87b82438:VMwareTray.exe                          2660   2548      5     80 2013-01-12 16:40:29 UTC+0000
    . 0x87c6a2a0:swriter.exe                             3452   2548      1     19 2013-01-12 16:41:01 UTC+0000
    .. 0x87ba4030:soffice.exe                            3512   3452      1     28 2013-01-12 16:41:03 UTC+0000
    ... 0x87b8ca58:soffice.bin                           3564   3512     12    400 2013-01-12 16:41:05 UTC+0000
    . 0x9549f678:iexplore.exe                            1136   2548     18    454 2013-01-12 16:57:44 UTC+0000
    .. 0x87d4d338:iexplore.exe                           3044   1136     37    937 2013-01-12 16:57:46 UTC+0000
    . 0x87aa9220:VMwareUser.exe                          2676   2548      8    190 2013-01-12 16:40:30 UTC+0000
    0x95483d18:soffice.bin                              3556   3544      0 ------ 2013-01-12 16:41:05 UTC+0000


On voit les processus parents et enfants, on remarque un cmd.exe enfant d'un iexplore.exe avec pid *2772*.

<br>


    volatility -f ch2.dmp --profile=Win7SP1x86_23418 cmdline

Output : 

    Volatility Foundation Volatility Framework 2.6
    ************************************************************************
    System pid:      4
    ************************************************************************
    smss.exe pid:    308
    Command line : \SystemRoot\System32\smss.exe
    ************************************************************************
    csrss.exe pid:    404
    Command line : %SystemRoot%\system32\csrss.exe ObjectDirectory=\Windows SharedSection=1024,12288,512 Windows=On SubSystemType=Windows ServerDll=basesrv,1 ServerDll=winsrv:UserServerDllInitialization,3 ServerDll=winsrv:ConServerDllInitialization,2 ServerDll=sxssrv,4 ProfileControl=Off MaxRequestThreads=16
    ************************************************************************
    wininit.exe pid:    456
    ************************************************************************
    csrss.exe pid:    468
    Command line : %SystemRoot%\system32\csrss.exe ObjectDirectory=\Windows SharedSection=1024,12288,512 Windows=On SubSystemType=Windows ServerDll=basesrv,1 ServerDll=winsrv:UserServerDllInitialization,3 ServerDll=winsrv:ConServerDllInitialization,2 ServerDll=sxssrv,4 ProfileControl=Off MaxRequestThreads=16
    ************************************************************************
    winlogon.exe pid:    500
    Command line : 
    ************************************************************************
    services.exe pid:    560
    Command line : C:\Windows\system32\services.exe
    ************************************************************************
    lsass.exe pid:    576
    Command line : C:\Windows\system32\lsass.exe
    ************************************************************************
    lsm.exe pid:    584
    Command line : C:\Windows\system32\lsm.exe
    ************************************************************************
    svchost.exe pid:    692
    Command line : C:\Windows\system32\svchost.exe -k DcomLaunch
    ************************************************************************
    svchost.exe pid:    764
    Command line : C:\Windows\system32\svchost.exe -k RPCSS
    ************************************************************************
    svchost.exe pid:    832
    Command line : C:\Windows\System32\svchost.exe -k LocalServiceNetworkRestricted
    ************************************************************************
    svchost.exe pid:    904
    Command line : C:\Windows\System32\svchost.exe -k LocalSystemNetworkRestricted
    ************************************************************************
    svchost.exe pid:    928
    Command line : C:\Windows\system32\svchost.exe -k netsvcs
    ************************************************************************
    svchost.exe pid:   1084
    Command line : C:\Windows\system32\svchost.exe -k LocalService
    ************************************************************************
    svchost.exe pid:   1172
    Command line : C:\Windows\system32\svchost.exe -k NetworkService
    ************************************************************************
    AvastSvc.exe pid:   1220
    Command line : "C:\Program Files\AVAST Software\Avast\AvastSvc.exe"
    ************************************************************************
    spoolsv.exe pid:   1712
    Command line : C:\Windows\System32\spoolsv.exe
    ************************************************************************
    svchost.exe pid:   1748
    Command line : C:\Windows\system32\svchost.exe -k LocalServiceNoNetwork
    ************************************************************************
    sppsvc.exe pid:   1872
    ************************************************************************
    vmtoolsd.exe pid:   1968
    Command line : "C:\Program Files\VMware\VMware Tools\vmtoolsd.exe"
    ************************************************************************
    wlms.exe pid:    336
    ************************************************************************
    VMUpgradeHelpe pid:    448
    ************************************************************************
    TPAutoConnSvc. pid:   1612
    Command line : "C:\Program Files\VMware\VMware Tools\TPAutoConnSvc.exe"
    ************************************************************************
    taskhost.exe pid:   2352
    Command line : "taskhost.exe"
    ************************************************************************
    dwm.exe pid:   2496
    Command line : "C:\Windows\system32\Dwm.exe"
    ************************************************************************
    explorer.exe pid:   2548
    Command line : C:\Windows\Explorer.EXE
    ************************************************************************
    TPAutoConnect. pid:   2568
    Command line : TPAutoConnect.exe -q -i vmware -a COM1 -F 30
    ************************************************************************
    conhost.exe pid:   2600
    Command line : 
    ************************************************************************
    VMwareTray.exe pid:   2660
    Command line : "C:\Program Files\VMware\VMware Tools\VMwareTray.exe" 
    ************************************************************************
    VMwareUser.exe pid:   2676
    Command line : "C:\Program Files\VMware\VMware Tools\VMwareUser.exe" 
    ************************************************************************
    AvastUI.exe pid:   2720
    Command line : "C:\Program Files\AVAST Software\Avast\AvastUI.exe" /nogui
    ************************************************************************
    StikyNot.exe pid:   2744
    Command line : "C:\Windows\System32\StikyNot.exe" 
    ************************************************************************
    iexplore.exe pid:   2772
    Command line : "C:\Users\John Doe\AppData\Roaming\Microsoft\Internet Explorer\Quick Launch\iexplore.exe" 
    ************************************************************************
    SearchIndexer. pid:   2900
    Command line : C:\Windows\system32\SearchIndexer.exe /Embedding
    ************************************************************************
    wmpnetwk.exe pid:   3176
    Command line : "C:\Program Files\Windows Media Player\wmpnetwk.exe"
    ************************************************************************
    svchost.exe pid:   3352
    Command line : C:\Windows\system32\svchost.exe -k LocalServiceAndNoImpersonation
    ************************************************************************
    swriter.exe pid:   3452
    ************************************************************************
    soffice.exe pid:   3512
    Command line : 
    ************************************************************************
    soffice.bin pid:   3556
    ************************************************************************
    soffice.bin pid:   3564
    Command line : "C:\Program Files\LibreOffice 3.6\program\swriter.exe" "-o" "C:\Users\John Doe\Documents\Procedure Winpmemdump.odt" "--writer" "-env:OOO_CWD=2C:\\Users\\John Doe\\Documents"
    ************************************************************************
    svchost.exe pid:   3624
    Command line : C:\Windows\System32\svchost.exe -k secsvcs
    ************************************************************************
    taskmgr.exe pid:   1232
    Command line : "C:\Windows\system32\taskmgr.exe" /4
    ************************************************************************
    cmd.exe pid:   3152
    Command line : "C:\Windows\system32\cmd.exe" 
    ************************************************************************
    conhost.exe pid:   3228
    Command line : 
    ************************************************************************
    cmd.exe pid:   1616
    Command line : cmd.exe
    ************************************************************************
    conhost.exe pid:   2168
    Command line : \??\C:\Windows\system32\conhost.exe
    ************************************************************************
    iexplore.exe pid:   1136
    Command line : "C:\Program Files\Internet Explorer\iexplore.exe" 
    ************************************************************************
    iexplore.exe pid:   3044
    Command line : "C:\Program Files\Internet Explorer\iexplore.exe" SCODEF:1136 CREDAT:71937
    ************************************************************************
    audiodg.exe pid:   1720
    Command line : C:\Windows\system32\AUDIODG.EXE 0x298
    ************************************************************************
    winpmem-1.3.1. pid:   3144
    Command line : winpmem-1.3.1.exe  ram.dmp
                                           
Nous voyons que pour le pid *2772* le chemin est **C:\Users\John Doe\AppData\Roaming\Microsoft\Internet Explorer\Quick Launch\iexplore.exe** sont hash md5 est ********9632639432397b3a1df8cb43d** !
