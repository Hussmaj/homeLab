# Feilsøking – Nettverksinterface og Promiscuous Mode

## Problem

Jeg utvidet hjemmelabben ved å sette opp en ny DMZ-server.

Jeg la til et nytt nettverksinterface på Ubuntu-maskinen som kjører Open vSwitch, og konfigurerte nettverket og DHCP-innstillingene i pfSense.

Selv om konfigurasjonen så riktig ut, klarte jeg ikke å pinge gateway-adressen til DMZ-nettverket fra serveren.

## Feilsøking

Jeg kontrollerte nettverksinterfacene og innstillingene i pfSense, men fant ikke årsaken til problemet.

Deretter bestemte jeg meg for å feilsøke systematisk, med utgangspunkt i OSI-modellen. Jeg startet på Layer 1 og undersøkte de grunnleggende innstillingene for det virtuelle nettverket i VirtualBox.

Da oppdaget jeg at Promiscuous Mode var satt til Deny, som er standardinnstillingen i VirtualBox. Jeg hadde oversett denne innstillingen da jeg opprettet det nye nettverksinterfacet.

## Løsning

Jeg endret Promiscuous Mode fra Deny til Allow All på det aktuelle nettverkskortet i VirtualBox.

Dette var nødvendig fordi Open vSwitch fungerer som en virtuell switch og må kunne motta og videresende Ethernet-rammer mellom de forskjellige nettverksinterfacene.

Med Promiscuous Mode satt til Deny kunne VirtualBox begrense hvilke Ethernet-rammer nettverkskortet fikk motta. Dette kunne hindre Open vSwitch i å videresende trafikken som forventet.

## Resultat

Etter at jeg endret Promiscuous Mode til Allow All, fungerte nettverkskommunikasjonen som forventet. Jeg kunne nå pinge gateway-adressen til DMZ-nettverket fra serveren.

Dette viste hvor viktig det er å kontrollere de grunnleggende nettverksinnstillingene i VirtualBox når man bygger virtuelle nettverk med Open vSwitch.
