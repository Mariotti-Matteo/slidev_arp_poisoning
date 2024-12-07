due macchine virtuali una di queste ci metti linux mint l'altra una distro (distribuzione linux) 
con tool di sicurezza (like fedora security lab) devono essere sulla stessa rete su virtual box 
dal pc  
PC MINT: ifconfig per vedere indirizzi IP della macchina sulla rete 
	ip route per vedere default gateway(che serve per ettercap)
	fai un ping al pc fedora per vedere se sono nella stessa rete 



PC fedora sec…: ifconfig per ip 
		sudo ettercap -G  (per aprirlo da amministratore)
		Primary Interface deve essere tipo(enp0s3 ovvero quella uguale per i due pc)
		poi premi ok e avvia 
	Ettercap: tre tacche a destra - host- scan for hosts . host list 		


Casistica: macchina virtuale impostazione - rete - connessa a: scheda con bridge oppure reta con NAT 

continuo Ettercap: prendi ip altra macchina e lo aggiungi come target uno 
			prendi l’ip gateway e lo metti come secondo target 
PREMERE PRIMO TASTO DELLA FILA A DESTRA:
arp poisoning- e poi ok e inizia a fare il poisoning 

apri altro terminale sudo wireshark 
vai sulla interfaccia di prima  tipo(enp0s3 ovvero quella uguale per i due pc)


PC mint: fai un ping ad default gateway



Cercare un modo di sistemare il gateway che sia fatto bene è uguale per i pc  




per configurazione iniziale pc fedora (1 trouble shoting. 2 boot first drive. 3 prima voce)



cosa ho fatto con luca: ovvero arp spoofing senza tool ho connesso i due PC alla stessa rete ho fatto un paio di ping ho cambiato il mio indirizzo mac 



