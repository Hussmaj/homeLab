# Feilsøking av VLAN og APIPA-adresse

## Problem

I hjemmelabben min satte jeg opp et nettverk med en server, en Windows-klient og pfSense som router.

Ubuntu Server var allerede satt opp på VLAN 10 med Netplan. Jeg ønsket å plassere Windows-klienten på VLAN 20, og prøvde først å finne en måte å konfigurere VLAN direkte på Windows gjennom Device Manager. Dette fungerte ikke slik jeg hadde tenkt.

Jeg begynte derfor å lete etter en annen løsning og fant ut at Open vSwitch kunne håndtere VLAN tagging. Jeg bestemte meg for å installere Open vSwitch på en egen Ubuntu-maskin, slik at den kunne fungere som en virtual switch i nettverket.

Jeg satte opp en Trunk-connection mot pfSense og en Access Port til Windows-klienten.

Etter at jeg hadde konfigurert alt, forventet jeg at Windows skulle få en IP-adresse fra DHCP-serveren. I stedet fikk den en APIPA-adresse (169.254.x.x). Det betydde at Windows ikke klarte å hente en IP-adresse fra DHCP.

## Feilsøking

Jeg trodde først at problemet lå i DHCP-oppsettet på pfSense. Jeg sjekket firewall-reglene, VLAN-konfigurasjonen og DHCP-innstillingene, men alt så riktig ut.

Jeg brukte nesten to dager på å prøve å finne feilen. Til slutt bestemte jeg meg for å gå tilbake til det grunnleggende og feilsøke systematisk, i stedet for å fortsette å sjekke de samme innstillingene.

Jeg begynte å gå gjennom nettverket steg for steg. Da oppdaget jeg at bridgen (br0) i Open vSwitch faktisk var nede.

Jeg hadde ikke tenkt på dette fordi Ubuntu-maskinen selv fortsatt kjørte. Jeg hadde rett og slett antatt at switchen også fungerte så lenge maskinen var startet. Men det er ikke nødvendigvis slik.

## Løsning

Jeg aktiverte bridgen i Open vSwitch og sjekket at den var oppe.

Deretter gikk jeg tilbake til Windows-klienten og kjørte: `ipconfig /renew`

Denne gangen fikk Windows-klienten IP-adressen den skulle ha på VLAN 20.

## Resultat

Etter at bridgen var aktivert, fungerte DHCP. Windows-klienten fikk riktig IP-adresse, og nettverket fungerte som det skulle.

## Lærdom

Det viktigste jeg lærte av dette, var å feilsøke systematisk i stedet for å anta hvor problemet ligger. Jeg brukte nesten to dager på å undersøke DHCP, mens problemet egentlig lå i Open vSwitch.

Jeg lærte også at selv om en VM kjører, betyr ikke det nødvendigvis at alle nettverkskomponentene inni den fungerer.
