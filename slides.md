---
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: "text-center"
# https://sli.dev/custom/highlighters.html
# highlighter: shiki
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

  .basso{
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
    width: 35%;
    position: absolute;
    margin: auto;
    top: 45%;
    left: 60%;
    right: 0%;
    bottom: 5%;
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

<br><br><br><br><br><br><br><br><br>
Scopri di più su: [ARP Spoofing](https://en.wikipedia.org/wiki/ARP_spoofing)
---

# Come Funziona l'ARP Poisoning

Le varie fasi dell'ARP Poisoning

- Fase di Scoperta
- Fase di Risposta
- Attacco
- Intercettazione del Traffico

<br><br><br><br><br><br>

<div style="background-color:red;color:white;padding: 10px;">
  La tecnica del ARP poisoning viene presentata solo a scopo didattico
  <br /><br />MAI usare la tecnica del ARP Poisoning per scopi illeciti o per arrecare danno a qualcuno o qualcosa.
</div>

<!-- <img src="/media/portsecurity_05.jpg" class="centro" /> -->

--- #slide 1

# Come funziona l'ARP poisoning

La fase della scoperta

- **Raccolta di informazioni:** L'attaccante inizia raccogliendo dati sulla rete target, come gli indirizzi IP e MAC dei dispositivi connessi, utilizzando strumenti come arp-scan o nmap.

- **Identificazione dei dispositivi:** Viene effettuata l'identificazione dei dispositivi chiave nella rete, come router e gateway, e di altri dispositivi che comunicano frequentemente.

- **Monitoraggio del traffico ARP:** L'attaccante monitora il traffico ARP per associare indirizzi IP e MAC, utilizzando strumenti di sniffing come Wireshark.

- **Preparazione all'attacco:** Una volta raccolte le informazioni, l'attaccante si prepara a inviare pacchetti ARP falsificati per avviare lo spoofing, associando il proprio MAC a quello di un altro dispositivo.


--- #slide 1

# Come funziona l'ARP poisoning

Fase di Risposta

- **Iniezione di Risposte Falsificate**: Un attaccante monitora il traffico ARP sulla rete e invia risposte ARP falsificate a Host A e Host B, facendoli credere che il proprio indirizzo MAC sia quello dell'altro host. Questo attacco consente all'attaccante di intercettare o manipolare il traffico tra i due dispositivi.

- **Aggiornamento della Cache ARP**: Quando Host A e Host B ricevono risposte ARP falsificate, aggiornano la loro cache ARP con informazioni errate, facendo sì che entrambi inviino i dati all'indirizzo MAC dell'attaccante anziché a quello del dispositivo legittimo.

- **Intercettazione del Traffico**: AL'attaccante può intercettare, registrare o modificare il traffico tra due dispositivi, portando a furto di dati, manipolazione delle comunicazioni e iniezione di malware.






--- #slide

# Come funziona l'ARP poisoning

Attacco

- Iniezione di pacchetti ARP:

    - L'attaccante invia pacchetti ARP falsificati nella rete. Un pacchetto ARP contiene informazioni sulle associazioni tra indirizzi IP e MAC.
    - Ad esempio, l'attaccante può inviare un pacchetto ARP che associa il proprio indirizzo MAC all'indirizzo IP di un'altra macchina (ad esempio, il gateway della rete).
    - Questo pacchetto viene inviato sia ai dispositivi target che al gateway, il che porta a una situazione in cui entrambi i dispositivi credono che l'attaccante sia il destinatario legittimo.


<!-- ![/media/portsecurity_01.png](/media/portsecurity_01.png) -->


--- #slide

# Come funziona l'ARP poisoning

Intercettazione del traffico

- Con le tabelle ARP delle due macchine compromesse aggiornate con informazioni false, l'attaccante può ora intercettare il traffico tra i due dispositivi, alterarlo o redirigerlo.
<!-- ![/media/portsecurity_00.png](/media/portsecurity_00.png) -->

- Verifichiamo che i frame in uscita abbiano effettivamente il source MAC address corretto

--- #slide

# Proteggersi dall'ARP Poisoning

Proteggersi dall'ARP Poisoning

- L'ARP poisoning in conclusione é un attacco che sfrutta il protocollo ARP per compromettere le comnicazioni in delle reti locali. Permette a chiunque di reindirizzare il traffico di rete e intercettare i dati o di effettuare attacchi tipo "man-in-the-middle" (come fa dettoni con la rete della scuola)


--- #slide

# Proteggersi dall'ARP Poisoning

Alcuni metodi per proteggersi

- **Static ARP Entries**: Questa tecninca consiste nel configuare le voci del ARP statiche sui dispositivi di rete riducendo il rischio di attacco. Tuttavia, questa soluzione può essere poco pratica in una rete dinamica.
- **ARP Spoofing Detection Tools**: Questa tecnica consiiste nel utilizzare strumenti di monitoraggio che rilevino attiivtà sospette e avvisino gli amministratori in caso di possibili attacchi di ARP poisoning.

- **VPN e Crittografia**: Questa tecnica consiste nel utilizzo di una VPN e protocolli di crittografia per proteggere i dati in transito sulla rete.

- **Utilizzo di protocolli sicuri**: Utilizzare protocolli sicuri come HTTPS, SSH e FTPS per le comunicazioni. Essi offrono una crittografia end-to-end.

-  **Filtraggio dei pacchetti**: Questa tecnica consiste nell' implementare filtri su switch e router per limitare i pacchetti non autorizzati.

--- #slide 1

# Esercitazione #01

Come eseguire un man-in-the-middle (**mitm**)  per intercettare un ping

- Per questa esercitazione ci serviranno:
  - 1 Switch
  - 3 PC (o più)
  - Wireshark
  - Ettercap 
  
<br><br><br><br>
Link al sito: [Ettercap](https://www.ettercap-project.org/)



<div style="background-color:red;color:white;padding: 10px;">
  La tecnica del ARP poisoning viene presentata solo a scopo didattico
  <br /><br />MAI usare la tecnica del ARP Poisoning per scopi illeciti o per arrecare danno a qualcuno o qualcosa.
</div>

--- #slide 1

# Esercitazione #01

Come eseguire un man-in-the-middle (**mitm**)  per intercettare un ping

**1° Step**:
- Accendiamo i PC
- Accendiamo lo switch
- Collegghiamo lo switch alla rete della scuola e 2 pc ad esso:
  - Utilizzando la porta 1 per la connessione alla rete della scuola
  - Utilizzando le porte 17 & 18 per i 2 pc.
- Il 3° PC dovrà rimanere collegato alla rete della scuola

**2° Step**:
- Assicurarsi che i link funzionino correttamente
- Se non dovessero funzionare occorre configurare lo switch

[Configuriamo uno switch Cisco](https://reti.mancusoa.it/3/U6_switch_config/#/1)

<img src="/media/switch_conf.png" class="basso" />


--- #slide 1

# Esercitazione #01


Come eseguire un man-in-the-middle (**mitm**) per intercettare un ping

**3° Step**:
  - Assegnare un gateway agli host:
    - **Host1**: 192.168.111.1
    - **Host2**: 192.168.111.0

**4° Step**:
  - Usando wireshark inizia a tracciare i pacchetti che passano per l'host3

**5° Step**:
  - Eseguire un ping tra l'Host1 al Host2
    - Cosa succede se pingo l'Host2?
    - Cosa succede se pingo l'Host1?


--- #slide 1

# Esercitazione #01

Come eseguire un man-in-the-middle (**mitm**)  per intercettare un ping

**6° Step:**

- Set up di Ettercapx 


--- #slide 1

# Esercitazione #01

Come eseguire un man-in-the-middle (**mitm**)  per intercettare un ping


 