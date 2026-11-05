# VLAN Feilsøking

I mitt gamle VLAN oppsett hadde VLAN 20 og VLAN 30 har egne access-porter på Open vSwitch. Ubuntu Server på VLAN 10 brukte foreløpig et eget VLAN-interface konfigurert med Netplan.   

Dette skyldes at OVS-VM-en i dette oppsettet har fire virtuelle nettverkskort, og alle er allerede i bruk. Derfor hadde ikke VLAN 10 ikke en egen access-port på OVS. 

## Løsning

Gjennom brukergrensesnittet til VBox kan jeg maksimalt ta i bruk 4 NIC, men etter litt søking så fant jeg ut at jeg kan konfigurere 8 stk gjennom CLI til VBox som heter VboxMAnage. 

Og da kunne jeg legge ett til nettverkskort som fikk navnet 'enp0s16', og den ble lagt til som en access-port på VLAN 10.   
Deretter endret jeg nettverkskonfigurasjonen på Ubuntu Server til å bruke DHCP uten manuell VLAN-tagging i Netplan, og fjernet det gamle VLAN 10-grensesnittet.  
