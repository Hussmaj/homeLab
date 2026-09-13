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

Jeg startet med å sette opp LAN-nettverket mellom Windows-klienten, Ubuntu-serveren og pfSense. Windows-klienten fikk Internal Network med navnet Lan.

pfSense ble satt opp med to nettverkskort. Adapter 1 ble satt til NAT (WAN) og Adapter 2 til LAN, slik at pfSense fungerer som ruter og brannmur mellom det interne nettverket og WAN.

LAN-adressen i pfSense ble endret til 192.168.10.1. DHCP-serveren ble aktivert med adresseområde 192.168.10.100–192.168.10.200. Webserveren fikk en statisk IP-adresse på 192.168.10.10.

Nettverket ble testet ved å pinge gatewayen, webserveren, 8.8.8.8 og eksterne domener som google.com og vg.no.

Deretter installerte jeg Apache2 og testet webserveren ved å åpne den fra Windows-klienten i nettleseren

## Resultater: 

Nettverket fungerer. Klienten kan kommunisere med pfSense, webserveren og internett. Routing og DHCP fungerer, og Apache-serveren kan nås fra klienten.

Det ble også avklart at webserveren ikke nødvendigvis trenger å kunne pinge Windows-klienten. Windows Firewall kan blokkere ICMP-trafikk, og dette betyr ikke at nettverket er feil konfigurert.

Prinsippet videre er å begrense unødvendige åpninger i nettverket. Færre åpne porter og tjenester gir en mindre angrepsflate og dermed bedre sikkerhet.

## Illustrasjon av arkitekturen:

<img width="1663" height="1639" alt="Blank diagram (1)" src="https://github.com/user-attachments/assets/f8857e22-31d2-4773-8b70-af490c2cba32" />






