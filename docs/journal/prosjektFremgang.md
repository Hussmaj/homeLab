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

***Skal se slik ut opp slik:*** 

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


**Sluttmål**


***Illustrasjon*** 


                   INTERNETT
                       │
                  VirtualBox
                      NAT
                       │
                    pfSense
                       │
              ┌────────┴────────┐
              │                 │
            VLAN 10           VLAN 20
            Klienter           Servere
              │                 │
            Klient            Webserver


