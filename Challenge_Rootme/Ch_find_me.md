# Challenge Forensic - Find me

**url : https://www.root-me.org/fr/Challenges/Forensic/Find-me**

<br><br>

    volatility -f dump imageinfo 

    volatility -f --profile=Win7SP1x86_23418 filescan | grep Desktop

Output :

    0x000000001ee20110      3      0 R--rwd \Device\HarddiskVolume2\Users\info\Desktop\findme

<b>

    volatility -f dump --profile=Win7SP1x86_23418 dumpfiles -Q 0x000000001ee20110 -D ./ 

Nous obtenons un fichier **file.None.0x84e13338.dat** qui correspond au fichier suspect **findme**.

<br>

    volatility -f --profile=Win7SP1x86_23418 pstree 

Cela montre que TrueCrypt est utiliser pour protéger des données

    volatility -f --profile=Win7SP1x86_23418 truecryptsummary

Password : R3sqdl3Fuuz2ZdbdYsf56opFFLe9sAsx at offset 0x87433e44

<br>

Après avoir installé TrueCrypt, j'ai réussi à monter avec truecrypt avec le mot de passe ci-dessus : **R3sqdl3Fuuz2ZdbdYsf56opFFLe9sAsx**.

<br>

En cherchant dans les fichiers j'ai trouver un dossier intéressant : **my_safety_box**.

<b>

C'est une base de données de mots de passe Keepass 2.x (KDBX)

<br>

Après avoir installé keepass2 je doit trouver le mot de passe pour s'identifier dessus.


    volatility -f dump --profile=Win7SP1x86_23418 hashdump


Output: 

    Volatility Foundation Volatility Framework 2.6
    Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
    Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
    HomeGroupUser$:1001:aad3b435b51404eeaad3b435b51404ee:57e82f46aff390080f143c09ab2c5b68:::
    info:1002:aad3b435b51404eeaad3b435b51404ee:dc3817f29d2199446639538113064277:::


J'ai trouvé que le deuxieme hash du user info est le bon mot de passe pour le keepass **#1Godfather**.
<br>

Ensuite j'ai exporter la base de données en CSV 

    cat my_safety_box.csv 

J'ai reconnu un mot de passe chiffré en base64

<br>

En le dechiffrant en ligne à l'aide de Cyberchef j'obtient le flag : **K33p4ss_its_a_gR3at_T00l_4_P@sSw0rD!**

