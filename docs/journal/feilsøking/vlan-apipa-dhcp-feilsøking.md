# Feilsøking av VLAN og APIPA-adresse

## Problem

II hjemmelabben satte jeg opp et nettverk bestående av en server, en klient og en router som kjører pfSense.

Ubuntu Server var allerede konfigurert på VLAN 10 ved hjelp av Netplan. Jeg ønsket deretter å plassere Windows-klienten på VLAN 20. Først forsøkte jeg å konfigurere VLAN direkte på Windows-maskinen gjennom Device Manager, men dette fungerte ikke som forventet.

Jeg undersøkte alternative løsninger og fant ut at Open vSwitch kunne håndtere VLAN tagging. Dette ga meg også muligheten til å gjøre labben mer realistisk ved å introdusere en egen virtual switch i nettverket.

Jeg installerte Open vSwitch på en separat Ubuntu-maskin og konfigurerte en Trunk-forbindelse mot pfSense og en Access Port for Windows-klienten.

Etter konfigurasjonen forventet jeg at Windows-klienten skulle motta en IP-adresse fra DHCP-serveren. I stedet fikk den en APIPA-adresse (169.254.x.x). Dette betydde at Windows ikke klarte å hente en IP-adresse fra DHCP-serveren.

## Feilsøking

Min første antakelse var at problemet lå i DHCP-konfigurasjonen på pfSense. Jeg kontrollerte firewall-reglene, VLAN-konfigurasjonen og DHCP-innstillingene, men alt så ut til å være riktig.

Jeg brukte nesten to dager på å undersøke problemet. Til slutt bestemte jeg meg for å ta et steg tilbake og feilsøke nettverket mer systematisk, i stedet for å kontrollere de samme innstillingene gjentatte ganger.

Jeg begynte å undersøke komponentene én etter én. Da oppdaget jeg at bridgen (br0) i Open vSwitch var nede.

Jeg hadde ikke forventet dette fordi Ubuntu-maskinen fortsatt kjørte. Jeg hadde antatt at virtual switch også fungerte så lenge selve maskinen var startet. Jeg lærte at dette ikke nødvendigvis er tilfellet, og at nettverkskomponentene må kontrolleres separat.

## Løsning

Jeg aktiverte bridgen i Open vSwitch og kontrollerte at statusen var riktig.

Deretter gikk jeg tilbake til Windows-klienten og kjørte kommandoen:

ipconfig /renew

Denne gangen fikk Windows-klienten tildelt IP-adressen jeg hadde konfigurert for VLAN 20.

## Resultat

Windows-klienten mottok nå riktig IP-adresse fra DHCP-serveren i pfSense, og nettverkskommunikasjonen fungerte som forventet.

## Lærdom

Den viktigste lærdommen fra denne feilsøkingen var hvor viktig det er å arbeide systematisk og ikke trekke forhastede konklusjoner. Jeg brukte mye tid på å undersøke DHCP-konfigurasjonen, selv om det egentlige problemet lå i det virtuelle switching-laget.

Jeg lærte også at det ikke er nok at den virtuelle maskinen kjører. Man må kontrollere at nettverkskomponentene, som Open vSwitch bridge, også er aktive.
