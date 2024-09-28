# Challenge Rootme 2

### Objectif : 

**Trouver le mot de passe de l'utilisateur**

A l'aide de Volatility 3 :

Jai afficher les hashs windows des utilisateurs :

    ./vol.py -f ../ch2.dmp windows.hashdump.Hashdump 

Output :

    Volatility 3 Framework 2.7.0
    Progress:  100.00               PDB scanning finished                        
    User    rid     lmhash  nthash

    Administrator   500     aad3b435b51404eeaad3b435b51404ee        31d6cfe0d16ae931b73c59d7e0c089c0
    Guest   501     aad3b435b51404eeaad3b435b51404ee        31d6cfe0d16ae931b73c59d7e0c089c0
    John Doe        1000    aad3b435b51404eeaad3b435b51404ee        b9f917853e3dbf6e6831ecce60725930
                                                                                        

Le hash qui nous interesse est celui de l'utilisateur John :                            
    
    b9f917853e3dbf6e6831ecce60725930

<br>

Ensuite j'ai cracké le hash :

    echo "b9f917853e3dbf6e6831ecce60725930" > hash 
<b>

    john hash --format=NT -w=/usr/share/wordlists/rockyou.txt

Output : 

    Using default input encoding: UTF-8
    Loaded 1 password hash (NT [MD4 128/128 SSE2 4x3])
    Warning: no OpenMP support for this hash type, consider --fork=3
    Press 'q' or Ctrl-C to abort, almost any other key for status
    passw0rd         (?)     
    1g 0:00:00:00 DONE (2024-03-23 16:08) 25.00g/s 33600p/s 33600c/s 33600C/s dragons..phoebe
    Use the "--show --format=NT" options to display all of the cracked passwords reliably
    Session completed. 

Le mot de passe est donc ******.
