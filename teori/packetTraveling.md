Dato: 09/24/2026

# Packet Traveling

Målet med dette er å forstå hvordan nettverkskommunikasjon henger sammen.   
Det jeg ønsker og åpne med dette er å skape en modell eller ett kart over hvordan datamaskiner og nettverk kommuniserer. 

Jeg ønsker og kunne se på nettverksdiagrammer og mentalt se for meg hvordan ting henger sammen og beveger seg, på samme måte som jeg leser en plantegning eller teknisk tegning av et bygg.  

### Hvordan beveger packets seg gjennom internettet. 

Hvordan kommer data fra én maskin til en annen?

## OSI Modell: 

OSI-Modellen er delt i 7 deler, der hver del har spesifikk funksjon som den skal utføre. 
Når man kombinerer alle disse 7 delene sammen, så bidrar hver funksjon til å kunne veksle data / kommunisere mellom datamaskiner.

![OSI Modell](../docs/images/packtrav-osi-layers-236x300.png)  
*Figure 1: OSI Modell. Source: [Practicalnetworking](https://www.practicalnetworking.net/series/packet-traveling/osi-model/)*

### OSI Layer 1 - Physical: 
Det denne delen av OSI modellen har ansvar over å sende bits 1 og 0 som lager alt data koder. 
Ett eksempel på dette er da en **Ethernet-kabel** 

Ikke heng deg opp i ordet physical fordi, dette ble laget på 1970 tallet. Lenge før trådløs kommunikasjon i networking var ett konsept.
Wi-fi f.eks, har ikke noe kabler eller fysysike komponenter som kobler Data 1 til Data 2. Men, er fortsatt beregent som en del av Layer 1. 
En hub opererer også på dette nivået. 

### OSI Layer 2 - Data Link: 
Data link laget sin jobb er å kommunisere med Layer 1(Physical Layer)

Den har som ett ansvar for å sende ut 1 og 0 ut til kablene og hente ut 1 og 0 fra kablene.

Nettverkskortet (NIC) i min datamaskin, der jeg setter inn ethernet kabelen min inn håndtere funksjonalitet til Layer 2.  
Den mottar signaler fra kablene og sender signaler tilbake til kablene. 

Wi-fi Nettverkskortet, funker på samme måte ved å sende og motta radiobølger som deretter tolkes som en serie med 1'ere og 0'ere (sekvens/rekke med bits. F.eks: 1011010010110100)  

Layer 2 kommer da til å dele disse 1'ere og 0'ere vi har fått i noe som heter **Frames**

I lag 2 så har vi en addresseringsystem som heter Media Access Control-addressen eller MAC-Addresse. Jobben til MAC-addressen er at den indentifiserer hver enkelt nettverkskort(NIC) unikt.  
Hvert nettverkskort er forhåndsregistrert med en MAC-addresse av produsenten, som er brent inn i nettverskortet og er noen ganger referert til som Burned In Address (BIA). 

En **Switch** opererer også på dette laget. En switch sin jobb er å legge til rette for kommunikasjon innenfor ett nettverk. 

**Sammendrag:**

Data Link-laget (lag 2) sin jobb er å levere pakker fra ett nettverkskort (NIC) til et annet. Med andre ord er rollen til lag 2 å levere pakker fra hop til hop(nettverksenhet til nettverksenhet).


### OSI Layer 3 - Network:



### OSI Layer 4 - Transport:

### OSI Layer 5 - Session: 

### OSI Layer 6 - Presentation:

### OSI Layer 7 - Application:



### Kilder

https://www.practicalnetworking.net/  
https://www.practicalnetworking.net/series/packet-traveling/packet-traveling/
