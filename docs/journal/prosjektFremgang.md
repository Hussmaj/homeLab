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


