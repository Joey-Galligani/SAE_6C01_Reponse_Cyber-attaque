# Challenge RootMe - Find me again

**url : https://www.root-me.org/fr/Challenges/Forensic/Find-me-again** 

<br><br>

Apres avoir ajouter le profil Ubuntu dans */home/joey/volatility/volatility/plugins/overlays/linux/*, j'ai commencé les investigations.

    python2 vol.py -f memory.raw --profile=LinuxUbuntu16044x64 linux_bash

Output : 

        Pid      Name                 Command Time                   Command
    -------- -------------------- ------------------------------ -------
        1229 bash                 2017-04-14 07:58:36 UTC+0000   history 
        1229 bash                 2017-04-14 07:58:36 UTC+0000   apt-get install linux-image-4.4.0-72-lowlatency linux-headers-lowlatency
        1229 bash                 2017-04-14 07:58:36 UTC+0000   reboot
        1229 bash                 2017-04-14 07:58:36 UTC+0000   apt-get insta
        1229 bash                 2017-04-14 07:59:07 UTC+0000   history 
        1229 bash                 2017-05-05 12:04:44 UTC+0000   apt-get install lynx gnupg
        1229 bash                 2017-05-05 12:06:54 UTC+0000   nano /etc/fstab 
        1229 bash                 2017-05-05 12:06:58 UTC+0000   nano /etc/crypttab 
        1229 bash                 2017-05-05 12:07:08 UTC+0000   cd /mnt/
        1229 bash                 2017-05-05 12:07:29 UTC+0000   cp -R /media/sf_DUMP/dir* .
        1229 bash                 2017-05-05 12:07:38 UTC+0000   ping 8.8.8.8
        1229 bash                 2017-05-05 12:09:14 UTC+0000   gpg --quick-gen-key 'Troll <abuse@root-me.org>' rsa4096 cert 1y
        1229 bash                 2017-05-05 12:09:49 UTC+0000   lynx -accept_all_cookies "https://www.google.com/?=password+porno+collection"
        1229 bash                 2017-05-05 12:10:27 UTC+0000   gpg --yes --batch --passphrase=1m_4n_4dul7_n0w -c findme.txt
        1229 bash                 2017-05-05 12:10:37 UTC+0000   lynx -accept_all_cookies "https://www.google.com/?=password+troll+memes"
        1229 bash                 2017-05-05 12:11:04 UTC+0000   gpg --yes --batch --passphrase=Troll_Tr0ll_TrOll -c end.zip
        1229 bash                 2017-05-05 12:11:20 UTC+0000   nano dir1/dic_fr_l33t.txt 
        1229 bash                 2017-05-05 12:11:28 UTC+0000   rm findme.txt
        1229 bash                 2017-05-05 12:11:35 UTC+0000   rm -rf dir1/
        1229 bash                 2017-05-05 12:11:55 UTC+0000   dd if=/dev/sdb of=/media/sf_DUMP/forensic.img bs=2048

Nous voyons dans la commande *gpg --yes --batch --passphrase=1m_4n_4dul7_n0w -c findme.txt* que le fichier findme.txt est protégé en gpg avec le mot de passe *1m_4n_4dul7_n0w*. Nous voyons ensuite que le fichier end.zip est protégé en gpg par le mot de passe *Troll_Tr0ll_TrOll*.
<br>

Ensuite je vais monter l'image *forensic.img*.

    file forensic.img

Je vois que l'image est chiffré avec LUKS. Il faut donc trouver le mot de passe dans la RAM.

    aeskeyfind backup/memory.raw
<b>

    echo 8d3f527de514872f595908958dbc0ed1 | xxd -r -p > key.bin
<b>

    mkdir mnt6
<b>

    cryptsetup --master-key-file key.bin luksOpen ./backup/forensic.img mnt6
<b>

    mount /dev/mapper/mnt6 mnt6
<b>

    cd mnt6
<b>

    cd dir2
<b>

    gpg --yes --batch --passphrase=1m_4n_4dul7_n0w -d findme.txt.gpg
<b>

Je trouve un fichier *end.png* qui n'est pas le flag et je me rappel que l'utilisateur avais protégé un fichier end.zip et je me demande si ce fichier end.png n'est pas un zip caché.

    binwalk --run-as=root -e end.png
<b>

    cd _end.png.extracted
<b>

    gpg --yes --batch --ignore-mdc-error --passphrase=Troll_Tr0ll_TrOll end.zip.gpg
<b>

    unzip end.zip

Il nous faut trouver un mot de passe pour pouvoir le decompresser. Je vais donc le brutforce.

<b>

    strings memory.raw > dictionnairedejoey.txt
<b>

    zip2john ../_end.png.extracted/end.zip > hashend
<b>

    john --wordlist=dictionnairedejoey.txt hashend
<b>

On obtient le mot de passe : *Cyb3rs3curit3*

    unzip end.zip  -> mdp Cyb3rs3curit3

    gimp flag.gif

Ensuite, en scannant chaque QRcode du GIF j'obtient ********.
