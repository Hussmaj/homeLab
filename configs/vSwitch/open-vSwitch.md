## OVS-oppsett

Open vSwitch brukes som den virtuelle VLAN-switchen i labben. OVS kobler pfSense sammen med server-, klient- og DMZ-nettverkene.

### OVS-porter

| Interface | Nettverk | Type | VLAN | Beskrivelse |
|---|---|---|---:|---|
| `enp0s8` | VLAN-LAB | Trunk | 10, 20, 30 | Forbindelse til pfSense |
| `enp0s9` | CLIENTS-ACCESS | Access | 20 | Windows Client |
| `enp0s10` | DMZ-ACCESS | Access | 30 | Ubuntu DMZ |

### OVS bridge

| Bridge | Formål |
|---|---|
| `br0` | Virtuell switch for VLAN-trafikk |

`enp0s8` fungerer som trunk mellom pfSense og OVS og transporterer VLAN 10, 20 og 30.

`enp0s9` er en access-port for VLAN 20, mens `enp0s10` er en access-port for VLAN 30.

VLAN 10 har ikke en egen access-port i den nåværende VirtualBox-labben. Ubuntu Server bruker derfor VLAN-tagging over trunkforbindelsen.
