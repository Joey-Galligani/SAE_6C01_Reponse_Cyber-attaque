# Challenge Rootme 5

Lien : https://www.root-me.org/fr/Challenges/Forensic/Command-Control-niveau-6

### Objectif :

**Trouver l'hostname que le malware contacte**

J'ai *dumpé* la mémoire du processus en un executable :

    volatility -f ch2.dmp --profile=Win7SP0x86  procdump -p 2772 --dump-dir ./  

On va ensuite lancer l'executable dans Virustotal : 

Output : 

    Domain 	 	                                                Created 	Registrar
    api.snapcraft.io 		                                    2016-05-16 	MarkMonitor Inc.
    canonical-lgw01.cdn.snapcraftcontent.com 		            2019-09-05 	MarkMonitor Inc.
    furious.devilslife.com 		                                2020-06-11 	TurnCommerce, Inc. DBA NameBright.com
    hdr-nlb10-d66bbad0736f8259.elb.us-east-2.amazonaws.com 		2005-08-18 	MarkMonitor Inc.
    hdr-nlb4-0bbd2e21834cb637.elb.us-east-2.amazonaws.com 		2005-08-18 	MarkMonitor Inc.
    hdr-nlb5-4e815dd67a14bf7f.elb.us-east-2.amazonaws.com 		2005-08-18 	MarkMonitor Inc.
    hdr-nlb7-aebd5d615260636b.elb.us-east-1.amazonaws.com 		2005-08-18 	MarkMonitor Inc.
    hdr-nlb8-39c51fa8696874ee.elb.us-east-1.amazonaws.com 		2005-08-18 	MarkMonitor Inc.
    ns2.wrauzfevvo.com 		                                    2010-12-28 	NETIM sarl
    th1sis.l1k3ak3y.org 		                                - 	        -
    traff-2.hugedomains.com 		                            2003-10-31 	TurnCommerce, Inc. DBA NameBright.com
    traff-3.hugedomains.com 		                            2003-10-31 	TurnCommerce, Inc. DBA NameBright.com
    traff-4.hugedomains.com 		                            2003-10-31 	TurnCommerce, Inc. DBA NameBright.com
    traff-5.hugedomains.com 		                            2003-10-31 	TurnCommerce, Inc. DBA NameBright.com
    traff-6.hugedomains.com 		                            2003-10-31 	TurnCommerce, Inc. DBA NameBright.com
    y0ug.itisjustluck.com 		                                2019-08-23 	NAMECHEAP INC

Le domain que l'ont cherhce est celui qui n'est pas *Registrar* c'est donc **th1sis.l1k3ak3y.org** !