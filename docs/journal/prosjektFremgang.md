# Prosjektets fremgang

Her oppdaterer jeg arkitekturen i prosjektet med forskjellige versjon-nr. 
Viser fremgangen i prosjektet.


**Versjon-1**

Startet: 
Ferdig: 27.07.2026

Satt opp ett LAN nettverk med tilgang til internett gjennom pfSense. 
Det interne LAN nettverket er sattopp bak pfSense og NAT brukes til å kommunisere med Internettet. 


***Satt opp slik:***

                   INTERNETT
                       │
                    NAT/WAN
                       │
                    pfSense
                       │
                      LAN
                ┌──────┴──────┐
                │             │
            Klient        Webserver

**Versjon-1.5**

Startet 09.08.2026
Ferdig 09.10.2026

***Satt opp slik:***

                    Internet
                       │
                 VirtualBox NAT
                       │
                 pfSense WAN
                  10.0.2.15
                       │
                 ┌─────┴─────┐
                 │           │
                LAN       VLAN 10
                 │           │
         192.168.10.0/24   192.168.20.0/24
                 │           │
                 │           │
              Windows      Ubuntu
         192.168.10.100  192.168.20.10*
         

**Versjon-2**

Starter 09.11.2026 kl:10:15
Ferdig: 09.11.2026 kl:16:25

Fått en permanent VLAN 10-konfigurasjon på Ubuntu, DHCP fra pfSense og utgående Internett-tilgang. Neste gang jeg skrur på maskinene, så vill ikke IP-addressen være borte.

***Satt opp slik:***

```text

                    INTERNET
                       │
                       │
                  VirtualBox NAT
                   10.0.2.0/24
                       │
                       │
                   pfSense WAN
                   10.0.2.15/24
                       │
            ┌──────────┴──────────┐
            │                     │
            │       pfSense       │
            │                     │
            │  LAN: 192.168.10.1  │
            │SERVERS: 192.168.20.1│
            │                     │
            └──────────┬──────────┘
                       │
       ┌───────────────┴───────────────┐
       │                               │
 VirtualBox LAN                 VirtualBox VLAN-LAB
       │                               │
   LAN / Klientnett                 VLAN-trafikk
   192.168.10.0/24                  VLAN ID 10
       │                               │
       │                               │
Windows Client                    Ubuntu Server
192.168.10.100                    vlan10
                                       │
                                       │ DHCP
                                       ▼
                                  192.168.20.100

```


**Versjon-2.5**

Startet: 09.15.2026
Ferdig: 09.18.2026

***Satt opp slik:***

                         INTERNET
                            │
                            │
                     VirtualBox NAT
                            │
                            │
                       pfSense WAN
                            │
                    ┌───────┴────────┐
                    │                │
                    │    pfSense     │
                    │                │
                    │ LAN:           │
                    │ 192.168.10.1   │
                    │                │
                    │ VLAN 10:        │
                    │ 192.168.20.1   │
                    │ SERVERS        │
                    │                │
                    │ VLAN 20:        │
                    │ 192.168.30.1   │
                    │ CLIENTS        │
                    │                │
                    └───────┬────────┘
                            │
              ┌─────────────┴─────────────┐
              │                           │
              │                           │
       VirtualBox LAN              VirtualBox VLAN-LAB
              │                           │
       Administrasjonsnett             VLAN-trunk
       192.168.10.0/24                 VLAN 10, 20, 30
              │                           │
              │                           │
       Windows-klient                SWITCH-OVS
       192.168.10.100                Open vSwitch
       Administrasjon                     │
                                          │
                                   enp0s8 – trunk
                                   VLAN 10, 20, 30
                                          │
                                          │
                                   enp0s9 – access
                                   VLAN 20
                                          │
                                          │
                                   CLIENTS-ACCESS
                                          │
                                          │
                                   Windows-klient
                                   VLAN 20
                                   192.168.30.100
                                   DHCP

### pfSense oppsett: 

```text
WAN  → VirtualBox NAT
LAN  → LAN
em0  → VLAN-LAB

VLAN 10 → SERVERS → 192.168.20.1/24
VLAN 20 → CLIENTS → 192.168.30.1/24
```

### SWITCH-OVS oppsett:
```text
enp0s3 → LAN
         Administrasjon
         192.168.10.102

enp0s8 → VLAN-LAB
         Trunk
         VLAN 10, 20, 30

enp0s9 → CLIENTS-ACCESS
         Access-port
         VLAN 20
```
### Klienter og servere oppsett:
```text
Windows administrasjonsforbindelse
└── LAN
    └── 192.168.10.100

Windows klientforbindelse
└── CLIENTS-ACCESS
    └── VLAN 20
        └── 192.168.30.100 via DHCP

Ubuntu Server
└── VLAN 10
    └── 192.168.20.100 via DHCP
```


