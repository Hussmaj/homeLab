# Nettverk Hjemme Lab

## Om labben

Dette prosjektet er en virtuell hjemmelab laget for å lære og teste grunnleggende nettverk, nettverkstjenester og sikkerhet.

Labben bruker VirtualBox til å kjøre flere virtuelle maskiner. pfSense fungerer som gateway og brannmur, mens Windows brukes som klient og Ubuntu Server brukes som servermiljø.

Denne labben går ut på å lære viktige fundamenter innen nettverk og oppsett av nettverkstjenester.

## Målet med labben er å få praktisk erfaring med:

* Oppsett av virtuelle nettverk

* IPv4-adressering og subnetting

* DHCP og DNS

* Routing mellom nettverk

* VLAN og nettverkssegmentering

* Brannmurregler og tilgangskontroll

* Internett-tilgang fra interne nettverk

* Webservere med Apache

* Feilsøking og dokumentasjon av nettverk

## Lærings mål:

Sette på VM'er og få dem til å kommunisere med hverandre

## Fremgangsmåte

### 1. Oppsett av virtuelle maskiner

**Jeg startet med å opprette virtuelle maskiner i VirtualBox:**

* pfSense

* Windows-klient

* Ubuntu Server

pfSense fikk ett nettverkskort mot WAN og ett mot det interne LAN-nettverket. Windows-klienten ble koblet til et internt VirtualBox-nettverk kalt LAN.

### 2. Konfigurering av pfSense

pfSense ble konfigurert som gateway og brannmur for labben.

**LAN-interfacet ble satt til:**

IP-adresse: 192.168.10.1/24

**DHCP ble aktivert på LAN-nettverket med følgende adresseområde:**

192.168.10.100 – 192.168.10.200

Dette gjorde at klienter på LAN-nettverket kunne få IP-adresse automatisk.

### 3. Oppsett av Ubuntu Server

Ubuntu Server ble først koblet til LAN-nettverket og konfigurert med en IP-adresse i 192.168.10.0/24.

Senere ble serveren flyttet til et eget servernettverk basert på VLAN 10. 

**Ubuntu ble konfigurert til å bruke et VLAN-interface:**

vlan10
VLAN-ID: 10

VLAN-interfacet mottar IP-adresse fra DHCP-serveren på pfSense: 192.168.20.0/24

Netplan ble brukt for å gjøre VLAN-konfigurasjonen permanent, slik at den også fungerer etter omstart.

### 4. VLAN og nettverkssegmentering

For å skille klienter og servere ble det opprettet et eget servernettverk med VLAN 10.

**Servernettverket bruker:**

Nettverk: 192.168.20.0/24
Gateway: 192.168.20.1
VLAN-ID: 10

Ubuntu Server sender trafikken sin med VLAN-taggen 10, og pfSense håndterer dette som et separat interface kalt SERVERS.

Dette gjør at klient- og servernettverket er logisk adskilt.

### 5. Brannmurregler

Det ble konfigurert brannmurregler i pfSense for å tillate nødvendig trafikk.

**Blant annet ble det opprettet regler for:**

* Kommunikasjon fra VLAN 10 til pfSense

* Utgående trafikk fra servernettverket

* Testing av forbindelse mellom nettverkene

Et viktig prinsipp i labben er at trafikk ikke skal tillates automatisk uten at det finnes en relevant brannmurregel. Dette viser hvordan pfSense kan brukes til å kontrollere tilgang mellom nettverk.

### 6. Apache Webserver

Apache2 ble installert på Ubuntu Server for å sette opp en enkel webserver.

## Testing

**Følgende tester ble brukt for å kontrollere nettverket:**

* Ping fra Windows-klienten til pfSense

* Ping fra Ubuntu Server til pfSense

* Kontroll av IP-adresser med ip addr

* Kontroll av routing med ip route

* Kontroll av valgt rute med ip route get

* Test av Internett-tilgang med ping 8.8.8.8

* Test av DNS-oppslag med domenenavn som google.com

Tilgang til Apache-webserveren fra Windows-klienten

## Resultater

**Labben har gitt et fungerende virtuelt nettverk med:**

* pfSense som gateway og brannmur

* Et separat LAN-nettverk for klienter

* Et separat servernettverk med VLAN 10

* DHCP på både LAN og servernettverket

* Routing og Internett-tilgang fra Ubuntu Server

* Permanent VLAN-konfigurasjon i Ubuntu med Netplan

* Apache Webserver på Ubuntu Server

* Grunnleggende brannmurregler og tilgangskontroll

Underveis ble det også feilsøkt problemer med DHCP, VLAN-tagging, brannmurregler og routing. Dette ga praktisk erfaring med hvordan man finner årsaken til nettverksproblemer i stedet for å bare kontrollere om en forbindelse fungerer.

## Teknologier

* VirtualBox

* pfSense

* Ubuntu Server

* Windows

* VLAN / 802.1Q

* IPv4

* DHCP

* DNS

* Routing

* Firewall

* Apache2

* Netplan




