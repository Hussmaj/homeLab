# VLAN Feilsøking

I mitt gamle VLAN oppsett hadde VLAN 20 og VLAN 30 har egne access-porter på Open vSwitch. Ubuntu Server på VLAN 10 brukte foreløpig et eget VLAN-interface konfigurert med Netplan.   

Dette skyldes at OVS-VM-en i dette oppsettet har fire virtuelle nettverkskort, og alle er allerede i bruk. Derfor hadde ikke VLAN 10 ikke en egen access-port på OVS. 

## Løsning

Løsningen på dette var å bruke
