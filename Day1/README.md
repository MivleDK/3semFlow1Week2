**What is your public IP address right now, and how did you find it?**  

Den nemmeste måde at finde sin public IP på er at google "What's my IP".
Google returnerer din ip.
Hvis ikke er [whatismyipaddress.com](whatismyipaddress.com) en løsning.

**What is your private IP address right now (do this both at home and in school), and who/what gave you that address?**  

På windows kan man skrive ``ipconfig`` i terminalen returnerer en liste over installerede netværkskort. 
Hver enhed har fået tildelt en IP adresse af routeren.

På ét af disse netværkskort er "Default Gateway" udfyldt.
Denne addresse tildeles, i private hjem, typisk af en router. 
I virksomheder mm. tildeles IP adressen typisk af DHCP serveren.

**What’s special about these address ranges?**  

- ***10.0.0.0 – 10.255.255.255***  

10.0.0.0/8 IP addresses: 10.0.0.0 – 10.255.255.255

- ***172.16.0.0 – 172.31.255.255***  

172.16.0.0/12 IP addresses: 172.16.0.0 – 172.31.255.255

- ***192.168.0.0 – 192.168.255.255***  

192.168.0.0/16 IP addresses: 192.168.0.0 – 192.168.255.255

De tre *ranges* er reserverede IP-adresser og anvendes kun på private / "Lokale" intra/internet. 

**What’s special about this ip-address: 127.0.0.1?**  

Refererer til *Localhost*. Dvs. klientens egen adresse.

**What kind of service would you expect to find on a server using these ports:**  

- 22: SSH - Secure shell
- 23: Telnet - Gammel remote login service (Ukrypteret og usikker)
- 25: SMTP - Email protokol (Simple mail transfer protokol)
- 53: DNS - Domain name system. En form for adressebog der oversætter domænenavne til IP-adresser
- 80: HTTP protokollen
- 443: HTTPS over TSL/SSL?

**What is the IP address of studypoints.info and how did you find it?**  

Man kan pinge adresser i terminalen med `ping studypoints.info`.
Ping sender *pakker* afsted og siger noget om forbindelsen. 
(IP'en er 157.230.21.145)

**If you write https://studypoints.info in your browser, how did “it” figure out that it should go to the IP address you discovered above?**  

Når jeg skriver studypoints.info i browseren går forespørgslen fra min klient til min egen router.
Routeren sender forespørgslen til en DNS server (Det kunne være en ISP's eller googles DNS 8.8.8.8). 
  
Hvis DNS serveren kender domænenavnet returneres IP-adressen så klienten kan åbne siden.  
Kender DNS serveren ikke navnet spørger den, den næste næste DNS-server osv.

**Explain shortly the purpose of an ip-address and a port-number and why we need both**  

En server har én enkelt IP-adresse (Ud af til). Serveren kan eksempelvis have adskillige services såsom SSH, HTTP, SMTP mm.

Hvis en klient er intereseret i at se en hjemmeside der hostes på serveren er det nødvendigt at kende serverens IP adresse *og* angive et portnummer.
Hvis ikke man angiver portnummeret kan serveren ikke vide, hvilken service den skal sende klientens forespørgsel hen til.
  
**What is your (nearest) DNS server?**  

Med `nslookup` fremgår det af terminalen, at min nærmeste DNS er dns.google på 8.8.8.8

**What is (conceptually) the DNS system and the purpose with a DNS Server?**  

DNS Serveren fungerer som en form for adressebog / telefonbog.
I stedet for at skrive `172.217.21.142` i browseren skriver vi "google.com".  

Vores nærmeste DNS-server sørger for at oversættes navnet til en ip-adresse som serveren kan arbejde med.  
Kender DNS-serveren ikke navnet spørger den en anden DNS server. 
Antallet af forespørgsler fra DNS til DNS kaldes også "Hop" og kan sige noget om forbindelsen til den ønskede server.  
  
Desuden kan man se på TTL eller Time to live som beskriver hvor længe en record gemmes på en DNS server - typisk 3600 sekunder.
  
**What is your current Gateway, and how did you find it?**  

`ipconfig` angiver default gateway til `192.168.0.1`  

**What is the address of your current DHCP-Server, and how did you find it?**  

`ipconfig -all` På samme netværkskort som default gateway kan vi se, at adressen er den samme `192.168.0.1`. Dette skyldes, at de fleste private forbrugers router håndterer delegeringen af IP-adresser på det lokale netværk.  
I større virksomheder mm. håndteres denne fordeling af en dedikeret DHCP server.

**Explain (conceptually) about the TCP/IP-protocol stack**  

**TCP**/IP er 2 forskellige protokoller, på forskellige lag i OSI modellen som arbejder sammen.
I TCP ser man ofte "Three way handshake" som sikrer en *loss-less* forsendelse af data. Det handshake kan forsimples imellem 2 maskiner til at være:
- MACH1 SYN: Hey, I want to SYNchronize and talk with you
- MACH2 SYN-ACK: I ACKnowledge that you want to SYNchronize with me
- MAC1 ACK: I ACKnowledge that you ACKnowledge that i want to SYNchronize with you
  
SYN | SYN-ACK | SYN

I TCP sendes hver pakke med en ACK for at indikere "Jeg modtog den". Hvis ikke den modtages sendes pakken igen for at sikre at al data leveres.
Ovenstående proces finder sted for at sikre, at 2-vejs kommunikation kan åbnes og datatransmission kan finde sted. 

**IP** eller "Internet protokol" handler om IP-pakker. I en IP pakke står der bl.a. hvor den kommer fra og hvor den skal hen.

**Explain about the HTTP Protocol (The following exercises will go much deeper into this protocol)**

- En klient (Browser) sender en HTTP request til en server
- En web server modtager requesten
- Serveren kører et program som kan håndtere denne request. 
- Serveren returnerer et HTTP svar til browseren "Fx. 200, 404, 301" mm.
- Browseren modtager svaret fra serveren. 

Et forløb kunne være

1. Browseren beder om en HTML side. Serveren returnerer en HTML fil
2. Browseren beder om et style sheet. Serveren returnerer en css fil
3. Browseren beder om et JPG billede. Serveren returnerer et jpg billede
4. Browseren beder om javascript kode. Serveren returnerer en .js fil
5. Browseren beder om en data. Serveren returnerer JSON eller XML.


**Explain (conceptually) how HTTP and TCP/IP are connected (what can HTTP do, and where does it fit into TCP/IP)**  

HTTP anvender TCP protokollen til at overføre data, da det er en sikker måde at overføre data på, takket være SYN SYN-ACK ACK.  
HTTP binder altså en klient forespørgsel på TCP og IP protokollen beskriver opbygningen af de pakker der sendes fra serveren til klienten.
