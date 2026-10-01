# Nettverk Hjemmelab

Virtuell hjemmelab for praktisk læring innen nettverk, serverdrift og grunnleggende nettverkssikkerhet.  
Labben er bygget med VirtualBox, pfSense og Open vSwitch. pfSense fungerer som gateway og brannmur, mens Ubuntu Server og Windows brukes som server- og klientmiljø.   

Prosjektet brukes til å teste og dokumentere VLAN, routing, DHCP, DNS, brannmur og virtuelle nettverk.  

## Arkitektur

![Arkitektur](/docs/images/finalArchitecture.drawio.png)  
*Figur 1: Arkitektur av Prosjektet.*

## Komponenter
* VirtualBox – virtualisering og virtuelle nettverk  
* pfSense – gateway, DHCP, DNS, routing og brannmur  
* Open vSwitch – virtuell VLAN-switch  
* Ubuntu Server – servermiljø og Apache  
* Windows – klient og testing
* VLAN / 802.1Q

## IP Plan

| Enhet | IP-adresse | Nettverk | Rolle |
|---|---|---|---|
| pfSense | `192.168.10.1` | LAN | Gateway |
| OVS | `192.168.10.102` | LAN | Administrasjon |
| pfSense | `192.168.20.1` | SERVERS | Gateway |
| Ubuntu Server | `192.168.20.100` | SERVERS | Server |
| pfSense | `192.168.30.1` | CLIENTS | Gateway |
| Windows Client | `192.168.30.100` | CLIENTS | Klient |
| pfSense | `192.168.40.1` | DMZ | Gateway |
| Ubuntu DMZ | `192.168.40.101` | DMZ | DMZ-server |

## OVS-oppsett

Open vSwitch brukes som den virtuelle VLAN-switchen i labben. OVS kobler pfSense sammen med server-, klient- og DMZ-nettverkene.

| Interface | Nettverk | Type | VLAN |
|---|---|---|---:|
| `enp0s8` | VLAN-LAB | Trunk | 10, 20, 30 |
| `enp0s9` | CLIENTS-ACCESS | Access | 20 |
| `enp0s10` | DMZ-ACCESS | Access | 30 |

VLAN 10 har ikke en egen access-port i den nåværende VirtualBox-labben. Ubuntu Server bruker derfor VLAN-tagging over trunkforbindelsen.

## pfSense-oppsett

pfSense fungerer som gateway, DHCP-server, DNS, routing og brannmur i labben.

| Nettverk | Interface | IP-adresse |
|---|---|---|
| LAN | LAN | `192.168.10.1/24` |
| SERVERS | VLAN 10 | `192.168.20.1/24` |
| CLIENTS | VLAN 20 | `192.168.30.1/24` |
| DMZ | VLAN 30 | `192.168.40.1/24` |

VLAN 10, 20 og 30 er opprettet på `em0`, som er parent-interface for VLAN-nettverkene.

## VLAN-plan

VLAN brukes for å dele nettverket opp i separate logiske nettverk.

| VLAN | Navn | Subnett | Gateway | Bruk |
|---:|---|---|---|---|
| 10 | SERVERS | `192.168.20.0/24` | `192.168.20.1` | Servere |
| 20 | CLIENTS | `192.168.30.0/24` | `192.168.30.1` | Klienter |
| 30 | DMZ | `192.168.40.0/24` | `192.168.40.1` | DMZ |

VLAN brukes for å dele nettverket opp mellom servere, klienter og DMZ.  
- VLAN 10 – SERVERS  
- VLAN 20 – CLIENTS  
- VLAN 30 – DMZ  

Open vSwitch bruker en trunkforbindelse mot pfSense som transporterer VLAN 10, 20 og 30.  
VLAN 20 og VLAN 30 har egne access-porter på Open vSwitch.  
Ubuntu Server på VLAN 10 bruker foreløpig et eget VLAN-interface konfigurert med Netplan.   
Dette skyldes at OVS-VM-en i dette oppsettet har fire virtuelle nettverkskort, og alle er allerede i bruk. Derfor har VLAN 10 ikke en egen access-port på OVS.  

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
