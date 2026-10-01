# Nettverk Hjemmelab

Virtuell hjemmelab for praktisk læring innen nettverk, serverdrift og grunnleggende nettverkssikkerhet.  
Labben er bygget med VirtualBox, pfSense og Open vSwitch. pfSense fungerer som gateway og brannmur, mens Ubuntu Server og Windows brukes som server- og klientmiljø.   

Prosjektet brukes til å teste og dokumentere VLAN, routing, DHCP, DNS, brannmur og virtuelle nettverk.  

## Arkitektur

![Arkitektur](/docs/images/finalArchitecture.drawio.png)  
*Figur 1: Arkitektur av Prosjektet.*


| Enhet | IP-adresse | Nettverk | Rolle |
|---|---|---|---|
| pfSense | `192.168.10.1` | LAN | Gateway |
| OVS | `192.168.10.102` | LAN | Administrasjon |
| pfSense | `192.168.20.1` | SERVERS | Gateway |
| pfSense | `192.168.30.1` | CLIENTS | Gateway |
| Windows | `192.168.30.100` | CLIENTS | Klient |
| pfSense | `192.168.40.1` | DMZ | Gateway |
| Ubuntu DMZ | `192.168.40.101` | DMZ | Server |

## Komponenter
* VirtualBox – virtualisering og virtuelle nettverk  
* pfSense – gateway, DHCP, DNS, routing og brannmur  
* Open vSwitch – virtuell VLAN-switch  
* Ubuntu Server – servermiljø og Apache  
* Windows – klient og testing
* VLAN / 802.1Q


VLAN brukes for å segmentere nettverket mellom servere og klienter.

* VLAN 10 – SERVERS  
* VLAN 20 – CLIENTS  
* VLAN 30 – DMZ 

Open vSwitch bruker en trunk mot pfSense og en access-port for klientnettverket.
Open vSwitch bruker en trunkforbindelse mot pfSense for VLAN 10, 20 og 30.

VLAN 20 og VLAN 30 er konfigurert med egne access-porter på Open vSwitch.

Ubuntu Server på VLAN 10 bruker foreløpig et VLAN-interface konfigurert med Netplan. Dette skyldes begrensningen på fire virtuelle nettverkskort i VirtualBox, hvor alle nettverkskortene på OVS-VM-en allerede er i bruk.


## Tjenester
* DHCP
* DNS
* IPv4 routing
* NAT
* Firewall
* Apache Web Server

## Feilsøking

Labben brukes også til praktisk feilsøking av nettverksproblemer.

Eksempler fra prosjektet:

* DHCP-problemer  
* VLAN-tagging  
* Trunk- og access-porter  
* Virtuelle nettverkskort  
* Routing  
* Brannmurregler  
* Nettverksinterface som ikke var aktive
* VirtualBox nettverksinnstillinger
* Promiscuous Mode


Feilsøkingen dokumenteres underveis i /docs/journal/arbeidslogger, sammen med relevante kommandoer og resultater.

## Status

Labben fungerer og under videre utvikling.

## Ferdig
* VirtualBox-nettverk
* pfSense gateway og brannmur
* LAN
* VLAN 10 / SERVERS
* VLAN 20 / CLIENTS
* VLAN 30 / DMZ
* Open vSwitch
* VLAN trunk
* Access-port for klienter
* Access-port for DMZ
* DHCP
* Ubuntu Server med Netplan
* Ubuntu DMZ
* Apache Web Server
* Nettverkstesting og feilsøking

## Planlagt

* Sette opp en ny versjon av labben i VMware Workstation Pro
* Bruke flere virtuelle nettverkskort for OVS
* Sette opp en egen access-port for VLAN 10
* Flytte Ubuntu Server fra manuell VLAN-tagging til en vanlig access-port
* Videre brannmur- og tilgangskontroll
* Flere tjenester og servere

## Teknologier

* VirtualBox  
* pfSense  
* Open vSwitch  
* Ubuntu Server
* Ubuntu DMZ  
* Windows   
* VLAN/802.1Q  
* IPv4  
* DHCP  
* DNS   
* NAT  
* Routing  
* Firewall  
* Apache  
* Netplan  
