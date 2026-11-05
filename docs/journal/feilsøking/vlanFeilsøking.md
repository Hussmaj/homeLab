**Gammelt VLAN Konfigurasjon**

Open vSwitch bruker en trunkforbindelse mot pfSense som transporterer VLAN 10, 20 og 30.  
VLAN 20 og VLAN 30 har egne access-porter på Open vSwitch.  
Ubuntu Server på VLAN 10 bruker foreløpig et eget VLAN-interface konfigurert med Netplan.   

Dette skyldes at OVS-VM-en i dette oppsettet har fire virtuelle nettverkskort, og alle er allerede i bruk. Derfor har VLAN 10 ikke en egen access-port på OVS.  
