# Challenge Rootme 7

Lien : https://www.root-me.org/fr/Challenges/Forensic/Second-entretien-a-l-ANSSI

### Objectif :

**Trouver le flag dans le dossier**

    mkdir ch17
<b>

    cd ch17
<b>

    mv ../Téléchargements/ch17.zip ./
<b>

    unzip ch17.zip
<b>

    xmount --in ewf forensic.E01 /mnt
<b>

    tar -xvf /mnt/forensic.dd -C ./
<b>

    ls

Output :

    ch17.zip  forensic.E01  image.dd  memory.dmp

<br>

    volatility -f memory.dmp imageinfo

Output : 

    Volatility Foundation Volatility Framework 2.6
    INFO    : volatility.debug    : Determining profile based on KDBG search...
            Suggested Profile(s) : Win7SP1x64, Win7SP0x64, Win2008R2SP0x64, Win2008R2SP1x64_23418, Win2008R2SP1x64, Win7SP1x64_23418
                        AS Layer1 : WindowsAMD64PagedMemory (Kernel AS)
                        AS Layer2 : FileAddressSpace (/home/joey/ch17/memory.dmp)
                        PAE type : No PAE
                            DTB : 0x187000L
                            KDBG : 0xf800028520a0L
            Number of Processors : 1
        Image Type (Service Pack) : 1
                    KPCR for CPU 0 : 0xfffff80002853d00L
                KUSER_SHARED_DATA : 0xfffff78000000000L
            Image date and time : 2016-07-02 20:09:29 UTC+0000
        Image local date and time : 2016-07-02 22:09:29 +0200


Installation du plugin Bitlocker : 

    git clone https://github.com/breppo/Volatility-BitLocker
<b>

    mv ./Volatility-BitLocker/bitlocker.py /home/joey/volatility/volatility/plugins
<b>

    cd volatility
<b>

    python2 vol.py -f ../ch17/memory.dmp bitlocker --profile=Win7SP1x64 --dislocker=/home/joey/ch17

Output :

    [FVEK] Address : 0xfa80018be720
    [FVEK] Cipher  : AES 128-bit with Diffuser
    [FVEK] FVEK    : e7e576581fe26aa7c71a7e711c778da2
    [FVEK] Tweak   : b72f4e075edb7e734dfb08638cf29652
    [DISL] FVEK for Dislocker dumped to file: /home/joey/ch17/0xfa80018be720-Dislocker.fvek
<br>


    losetup --partscan --find --show ./ch17/image.dd
<b>

    mkdir /mnt2
<b>

    ls ../ch17

Output :

    0xfa80018be720-Dislocker.fvek  ch17.zip  forensic.E01  image.dd  info  memory.dmp
<br>


    dislocker /dev/loop0p1 -k ../ch17/0xfa80018be720-Dislocker.fvek /mnt2
<b>

    ls /mnt2  

Output :

    dislocker-file
<br>
            
    mount -o loop,ro -t ntfs /mnt2/dislocker-file ../ch17
<b>

    ls ../ch17

Output :

    '$RECYCLE.BIN'   flag.jpg  'System Volume Information'

![](/img/flag2-1.png)


On obtient l'image flag.jpg : 

![](/img/flag2.png)

Le mot de passe du challenge est **B1tL0ck3R_1ts_n0t_sUr3** !