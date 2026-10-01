# Open vSwitch

Open vSwitch brukes som den virtuelle switchen i labben. Den håndterer VLAN-trafikken mellom pfSense og de virtuelle maskinene.

## Bridge

Open vSwitch bruker bridgen `br0`.

| Bridge | Formål |
|---|---|
| `br0` | Håndterer VLAN-trafikk mellom nettverkskortene |

## Nettverkskort

| Interface | VirtualBox-nettverk | Type | VLAN | Bruk |
|---|---|---|---:|---|
| `enp0s8` | `VLAN-LAB` | Trunk | 10, 20, 30 | Forbindelse til pfSense |
| `enp0s9` | `CLIENTS-ACCESS` | Access | 20 | Windows Client |
| `enp0s10` | `DMZ-ACCESS` | Access | 30 | Ubuntu DMZ |

### Trunk

`enp0s8` brukes som trunk mellom Open vSwitch og pfSense. Trunkforbindelsen transporterer VLAN 10, VLAN 20 og VLAN 30.

### Access-port VLAN 20

`enp0s9` er konfigurert som access-port for VLAN 20. Windows Client er koblet til VirtualBox-nettverket `CLIENTS-ACCESS`.

Trafikken fra Windows Client kommer inn på OVS som vanlig, umerket Ethernet-trafikk. OVS kobler trafikken til VLAN 20 før den sendes videre over trunkforbindelsen.

### Access-port VLAN 30

`enp0s10` er konfigurert som access-port for VLAN 30. Ubuntu DMZ er koblet til VirtualBox-nettverket `DMZ-ACCESS`.

OVS kobler trafikken fra denne porten til VLAN 30 før den sendes videre over trunkforbindelsen.

### VLAN 10

VLAN 10 har ikke en egen access-port i denne versjonen av labben.

VirtualBox-VM-en som kjører OVS har fire tilgjengelige nettverkskort, og alle er allerede i bruk. Ubuntu Server håndterer derfor VLAN-taggingen selv gjennom et VLAN-interface og sender trafikken tagget over `VLAN-LAB`.

Dette er en begrensning i den nåværende VirtualBox-løsningen, og ikke en del av den planlagte løsningen for en eventuell ny VMware-versjon.

## Administrasjon

OVS-VM-en bruker LAN-nettverket til administrasjon:

- IP-adresse: `192.168.10.102/24`
- Nettverk: `LAN`
- Gateway: `192.168.10.1`
