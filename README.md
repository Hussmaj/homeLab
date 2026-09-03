# Nettverk Hjemme Lab

## Forklaring av lab
**Nettverk – grunnleggende nettverkstjenester og konsepter**

Denne labben går ut på å lære viktige fundamenter innen nettverk og oppsett av nettverkstjenester.

**-DNS** – Domain Name System

**-DHCP** – Dynamic Host Configuration Protocol

**-Subnetting** – CIDR og IP-adressering

**-HTTP vs. HTTPS** – kommunikasjon over nettverk

**-NAT** – Network Address Translation
    - Private 
    - Offentlige IP-adresser

**-OSI- og TCP/IP-modellen**

**-Nettverkssikkerhet**

    - Grunnleggende sikkerhetstiltak

    - Brannmur og tilgangskontroll*

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






