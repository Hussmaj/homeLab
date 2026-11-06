# Feilsøking - VLAN 

## Problem

I det gamle VLAN-oppsettet hadde VLAN 20 og VLAN 30 egne access-porter på Open vSwitch. Ubuntu Server i VLAN 10 brukte derimot et eget VLAN-interface konfigurert med Netplan.

Årsaken var at OVS-VM-en hadde fire virtuelle nettverkskort, og alle var allerede i bruk. Derfor hadde VLAN 10 ikke en egen access-port på Open vSwitch.

## Feilsøking

* Jeg undersøkte nettverksoppsettet i VirtualBox og Open vSwitch.  
* Jeg fant ut at VirtualBox sitt grafiske brukergrensesnitt begrenset oppsettet til 4 nettverkskort i min konfigurasjon.  
* Jeg undersøkte alternative måter å legge til flere virtuelle nettverkskort på.  
* Jeg fant ut at dette kunne gjøres gjennom kommandolinjeverktøyet VBoxManage, som støtter opptil 8 nettverkskort per virtuell maskin.  


## Løsning

Jeg brukte VBoxManage via CLI for å legge til et ekstra virtuelt nettverkskort på OVS-VM-en.

Det nye nettverksgrensesnittet fikk navnet enp0s16 og ble konfigurert som en access-port på VLAN 10.

Deretter endret jeg nettverkskonfigurasjonen på Ubuntu Server til å bruke DHCP uten manuell VLAN-tagging i Netplan. Det gamle VLAN 10-grensesnittet ble fjernet.

## Resultat

Ubuntu Server i VLAN 10 kunne nå kobles direkte til Open vSwitch gjennom en egen access-port.   
Dette gjorde VLAN-oppsettet mer oversiktlig og likt oppsettet for VLAN 20 og VLAN 30.
