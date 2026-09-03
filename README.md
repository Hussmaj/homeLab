# Nettverk Hjemme Lab

## Forklaring av lab

Denne labben går ut på å lære viktige fundamenter innen Nettverk og oppsett av nettverkstjenster.
- DNS
- DHCP
- Subnetting: CIDR
- CI/CD Pipelines
- HTTP vs HTTPS
- NAT (Network address Translation)
    - Private and Public IP-addresses
- OSI og TCP/IP Modellen
- Sikkerhets tilltak

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





