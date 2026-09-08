# Prosjektets fremgang

Her så skriver jeg ned hvilken versjon av prosjektet jeg er på nå og forklarer forskjellen fra den ene til den andre.


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
       Klient       Webserver

**Versjon-2**

Startet: 09.08.2026
Ferdig:


***Satt opp slik:*** 


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
