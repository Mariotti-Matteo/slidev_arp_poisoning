---
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
#background: https://source.unsplash.com/collection/94734566/1920x1080
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: "text-center"
# https://sli.dev/custom/highlighters.html
#highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
aspectRatio: "16_/9"
routerMode: "hash"
version: "1.0.1"
---  

<style>
  .alto {
    width: 50%;
    position: absolute;
    margin: auto;
    top: -40%;
    left: 50%;
    right: 0%;
    bottom: 0%;
  }

  .centro {
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
    width: 40%;
    position: absolute;
    margin: auto;
    top: 0%;
    left: 45%;
    right: 0%;
    bottom: 0%;
  }
</style>


# SISTEMI & RETI

ARP Spoofing o ARP Poisoning

<div class="pt-12">
  <span class="px-2 py-1">
    Premi spazio o <carbon:arrow-right class="inline"/> per la prossima slide
  </span>
</div>

--- #slide 1

# Il protocollo ARP

- Il protocollo ARP(**Address Resolution Protocol**) è utilizzato per mappare gli indirizzi IP (Internet Protocol) agli indirizzi MAC (Media Access Control) nei LAN (Local Area Network). Quando un dispositivo desidera comunicare con un altro dispositivo nella stessa rete locale, utilizza l'ARP per scoprire l'indirizzo MAC corrispondente all'indirizzo IP di destinazione.

<br><br><br><br><br>

Documentazione in più:

[Address Resolution Protocol 1](https://it.wikipedia.org/wiki/Address_Resolution_Protocol)

[Address Resolution Protocol 2](http://lia.deis.unibo.it/Courses/AmmSistemi1819/ARP-Forwarding-Walter-Cerroni.pdf)

[Address Resolution Protocol 3](http://wpage.unina.it/rcanonic/didattica/rc/lucidi_2017/RC1-2018-L08-a.pdf)

<br />  

--- #slide 1

# Cosa é l'ARP Poisoning?

- L'ARP poisoning, noto anche come ARP spoofing, è una tecnica di attacco utilizzata in reti informatiche che sfrutta il protocollo ARP (**Address Resolution Protocol**) per inviare messaggi falsi a una rete locale. Questo tipo di attacco può compromettere la sicurezza della rete e consentire a un attaccante di intercettare, modificare o bloccare la comunicazione tra i dispositivi di rete.
  
Scopri di più su: [ARP Spoofing](https://en.wikipedia.org/wiki/ARP_spoofing)
---

# Come Funziona l'ARP Poisoning

Le varie fasi dell'ARP Poisoning

- Fase di Scoperta
- Fase di Risposta
- Attacco
- Intercettazione del Traffico

<!-- <img src="/media/portsecurity_05.jpg" class="centro" /> -->

--- #slide 1

# Fase di Scoperta

La fase della scoperta

- La funzionalità di **port security** si applica a <br />specifiche interfacce
- In pratica per ogni interfaccia si specifica uno o più <br />indirizzi MAC sorgente che sono abilitati a <br />transitare per la porta in questione.
- Qualsiasi frame con un indirizzo MAC sorgente diverso <br />da quello/i configurati genera un'eccezione nello <br />switch che porta lo stato in una modalità <br />di protezione (drop del frame).

  <!-- <img src="/media/portsecurity_07.png" class="centro" /> -->


--- #slide 1

# MAC address Spoofing

Cambiamo identità alla NIC card

- MAC spoofing è una tecnica per cambiare il MAC address di una scheda di rete originariamente assegnato dal costruttore.
- Questo ci permette di cambiare completamente l'identità della nostra scheda nella rete in cui opera.
- Il MAC è hard-coded nella scheda di rete.
- Tuttavia molti driver permettono di cambiare il valore del MAC address.
- Ci possono essere molti  motivi per cui effettuare un MAC spoofing:
  - aggirare meccanismi di sicurezza a livello 2
  - impersonare un'altra scheda di rete
  - aggirare la verifica di licenze software
  - evitare la tracciabilità di un dispositivo (Android, iOS implementano una tecnica chiamata MAC Address Randomization per l'accesso alle reti WiFi pubbliche)

<div style="background-color:red;color:white;padding: 10px;">
  La tecnica del MAC spoofing viene presentata solo a scopo didattico
  <br /><br />MAI usare la tecnica del MAC spoofing per scopi illeciti o per arrecare danno a qualcuno o qualcosa.
</div>


--- #slide

# MAC address Spoofing

Cambiamo identità alla NIC card

- Iniziamo a verificare il nostro MAC address


<!-- ![/media/portsecurity_01.png](/media/portsecurity_01.png) -->


--- #slide

# MAC address Spoofing

Cambiamo identità alla NIC card

- Facciamo un ping a google e sniffiamo i pacchetti

<!-- ![/media/portsecurity_00.png](/media/portsecurity_00.png) -->

- Verifichiamo che i frame in uscita abbiano effettivamente il source MAC address corretto

--- #slide

# MAC address Spoofing

Cambiamo identità alla NIC card

- Per cambiare il MAC addrss (spoofing) dobbiamo:
  1. fare lo shutdown dell'interfaccia
  2. cambiare l'indirizzo MAC (hardware) di tipo ether(net)
  3. riattivare l'interfaccia

<br />

```bash
sudo ifconfig wlo1 down
sudo ifconfig wlo1 hw ether 24:E3:14:11:f6:93
sudo ifconfig wlo1 up

# PS: per chi vuole si può anche usare il tool macchanger

```
<br />

<!-- ![/media/portsecurity_02.png](/media/portsecurity_02.png) -->


--- #slide

# MAC address Spoofing

Cambiamo identità alla NIC card

- Facciamo nuovamente un ping a google e sniffiamo i pacchetti

<!-- ![/media/portsecurity_03.png](/media/portsecurity_03.png) -->

- Verifichiamo che i frame in uscita abbiano effettivamente il source MAC address di cui abbiamo fatto lo spoofing
- Ora la nostra scheda di rete è identificata come una scheda di Apple
- Questo a conferma che abbiamo realmente cambiato l'identità della nostra scheda di rete


--- #slide 1

# Port Security

Proteggiamo la rete da attacchi di livello 2

**Esercizio #01:**

1. Realizza una rete come in figura
2. Fare il ping dal PC1 al PC2 e verificare che tutto <br />funzioni correttamente
3. Modificare il MAC address del PC1 e verificare <br />che tutto funzioni correttamente
4. Modificare il MAC address del PC2 e verificare <br />che tutto funzioni correttamente
5. Ripristinare il MAC originale del PC1 e del PC2
  
<!-- <img src="/media/portsecurity_08.png" class="centro" /> -->

--- #slide 1

# Port Security

Proteggiamo la rete da attacchi di livello 2

**Esercizio #02:**

1. Abilitare il port security sulla porta dello switch **Fa 0/1**
```bash
Switch# conf t
Switch(config)# interface fastEthernet 0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport port-security
```

2. Configurare il MAC1 sulla porta Fa 0/1 come MAC sicuro
```bash
Switch(config-if)# switchport port-security maximum 1
Switch(config-if)# switchport port-security violation shutdown 
Switch(config-if)# switchport port-security mac-address 0090.0CB5.5B39
Switch(config-if)# end
```

--- #slide 1

# Port Security

Proteggiamo la rete da attacchi di livello 2

**Esercizio #02:**

3. Verificare la configurazione della porta
```bash
Switch#show running-config

!
interface FastEthernet0/1
 switchport mode access
 switchport port-security
 switchport port-security mac-address 0090.0CB5.5B39
!
interface FastEthernet0/2
```

--- #slide 1

# Port Security

Proteggiamo la rete da attacchi di livello 2

**Esercizio #02:**

4. Verificare la configurazione del port security
```bash
Switch# show port-security 

Secure Port MaxSecureAddr CurrentAddr SecurityViolation Security Action
               (Count)       (Count)        (Count)
--------------------------------------------------------------------
        Fa0/1        1          1                 0         Shutdown
----------------------------------------------------------------------
```

--- #slide 1

# Port Security

Proteggiamo la rete da attacchi di livello 2

**Esercizio #02:**

5. Verificare la configurazione del port security
```bash
Switch#show port-security address 
			
      Secure Mac Address Table
-------------------------------------------------------------------------------
Vlan	Mac Address	Type			Ports		Remaining Age
								(mins)
----	-----------	----			-----		-------------
1	0090.0CB5.5B39	SecureConfigured	FastEthernet0/1		-
------------------------------------------------------------------------------
Total Addresses in System (excluding one mac per port)     : 0
Max Addresses limit in System (excluding one mac per port) : 1024
```

--- #slide 1

# Port Security

Proteggiamo la rete da attacchi di livello 2

**Esercizio #02:**

6. Verificare la configurazione del port security
```bash
Switch#show port-security interface fastEthernet 0/1

Port Security              : Enabled
Port Status                : Secure-up
Violation Mode             : Shutdown
Aging Time                 : 0 mins
Aging Type                 : Absolute
SecureStatic Address Aging : Disabled
Maximum MAC Addresses      : 1
Total MAC Addresses        : 1
Configured MAC Addresses   : 1
Sticky MAC Addresses       : 0
Last Source Address:Vlan   : 0090.0CB5.5B39:1
Security Violation Count   : 0
```

--- #slide 1

# Port Security

Proteggiamo la rete da attacchi di livello 2

**Esercizio #02:**

7. Fare il ping dal PC1 al PC2 e verificare che tutto funzioni correttamente
8. Modificare il MAC address del PC1
9. Fare il ping dal PC1 al PC2 ed osservare il comportamento
      - il ping funziona ancora? PC1 può ancora raggiungere PC2?
      - cose è successo nella console dello switch?
      - qual'è lo stato della porta 0/1? 

```bash
Switch#
%LINK-5-CHANGED: Interface FastEthernet0/1, changed state to administratively down

%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/1, changed state to down
```
--- #slide 1

# Port Security

Proteggiamo la rete da attacchi di livello 2

**Esercizio #02:**

10. Verificare la configurazione del port security
```bash
Switch#show port-security interface fastEthernet 0/1

Port Security              : Enabled
Port Status                : Secure-shutdown
Violation Mode             : Shutdown
Aging Time                 : 0 mins
Aging Type                 : Absolute
SecureStatic Address Aging : Disabled
Maximum MAC Addresses      : 1
Total MAC Addresses        : 1
Configured MAC Addresses   : 1
Sticky MAC Addresses       : 0
Last Source Address:Vlan   : 0090.0CB5.5B40:1
Security Violation Count   : 1
```

--- #slide 1

# Port Security

Proteggiamo la rete da attacchi di livello 2

**Esercizio #02:**

- Lo switch vedendo arrivare un frame da un MAC non valido (0090.0CB5.5B40) applica la policy impostata in fase di configurazione (shutdown)
- Quindi mette la porta in modalità **shutdown** e pertanto non può transitare più nessun frame attraverso questa porta.
- In questo modo lo switch ha rilevato un **possibile** attacco ed ha reagito bloccando ogni ulteriore possibilità di attacco.

--- #slide 1

# Port Security

Proteggiamo la rete da attacchi di livello 2

**Esercizio #02:**

11. Ripristinare il MAC corretto sul PC1
12. Fare il ping dal PC1 al PC2 ed osservare il comportamento
       - il ping funziona ancora? PC1 può ancora raggiungere PC2?
       - qual'è lo stato della porta 0/1? 

--- #slide 1

# Port Security

Proteggiamo la rete da attacchi di livello 2

**Esercizio #02:**

13. Anche se il MAC del PC1 è ora corretto, lo switch mantiene la porta in shutdown perchè si apsetta che venga ripristinata manualmente dal network engineer
```bash
Switch# conf t
Switch(config)# interface fastEthernet 0/1
Switch(config-if)# no shutdown
Switch(config-if)# end
```

14. Fare il ping dal PC1 al PC2 ed osservare il comportamento
       - il ping funziona ancora? PC1 può ancora raggiungere PC2?
       - qual'è lo stato della porta 0/1? 


--- #slide 1

# Port Security

Proteggiamo la rete da attacchi di livello 2

**Esercizio #03:**

- Ripetere l'esercizio 2 modificando questa volta il MAC del PC 2
