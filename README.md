# Nettverk Hjemmelab

Virtuell hjemmelab for praktisk læring innen nettverk, serverdrift og grunnleggende nettverkssikkerhet.

Labben er bygget med VirtualBox, pfSense og Open vSwitch. pfSense fungerer som gateway og brannmur, mens Ubuntu Server og Windows brukes som server- og klientmiljø.

## Arkitektur

```text
                         INTERNET
                            │
                     VirtualBox NAT
                            │
                       pfSense WAN
                            │
                    ┌───────┴────────┐
                    │    pfSense     │
                    │                │
                    │ LAN            │
                    │ 192.168.10.1   │
                    │                │
                    │ VLAN 10        │
                    │ 192.168.20.1   │
                    │ SERVERS        │
                    │                │
                    │ VLAN 20        │
                    │ 192.168.30.1   │
                    │ CLIENTS        │
                    └───────┬────────┘
                            │
                       VLAN-LAB
                            │
                       SWITCH-OVS
                       Open vSwitch
                            │
                 ┌──────────┴──────────┐
                 │                     │
            VLAN trunk             Access VLAN 20
            VLAN 10/20/30               │
                 │                 CLIENTS-ACCESS
                 │                     │
          Ubuntu Server            Windows
          VLAN 10                  VLAN 20
          192.168.20.100           192.168.30.100


| Nettverk | VLAN | Subnett | Gateway | Bruk |
|---|---:|---|---|---|
| LAN | - | `192.168.10.0/24` | `192.168.10.1` | Administrasjon |
| SERVERS | 10 | `192.168.20.0/24` | `192.168.20.1` | Servere |
| CLIENTS | 20 | `192.168.30.0/24` | `192.168.30.1` | Klienter |
| DMZ | 30 | - | - | Planlagt |

## Komponenter
* VirtualBox – virtualisering og virtuelle nettverk  
* pfSense – gateway, DHCP, DNS, routing og brannmur  
* Open vSwitch – virtuell VLAN-switch  
* Ubuntu Server – servermiljø og Apache  
* Windows – klient og testing  
* VLAN   

VLAN brukes for å segmentere nettverket mellom servere og klienter.

* VLAN 10 – SERVERS  
* VLAN 20 – CLIENTS  
* VLAN 30 – DMZ (planlagt)  

Open vSwitch bruker en trunk mot pfSense og en access-port for klientnettverket.

Ubuntu Server bruker et VLAN-interface konfigurert med Netplan.

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

Feilsøkingen dokumenteres underveis sammen med relevante kommandoer og resultater.

## Status

Labben er under utvikling.

## Ferdig
* VirtualBox-nettverk  
* pfSense gateway og brannmur  
* LAN  
* VLAN 10 / SERVERS  
* VLAN 20 / CLIENTS  
* Open vSwitch  
* VLAN trunk  
* Access-port for klienter  
* DHCP  
* Ubuntu Server med Netplan  
* Apache Web Server  
* Nettverkstesting og feilsøking  

## Planlagt
* VLAN 30 / DMZ  
* Videre brannmur- og tilgangskontroll  
* Flere tjenester og servere

## Teknologier

* VirtualBox  
* pfSense  
* Open vSwitch  
* Ubuntu Server  
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
