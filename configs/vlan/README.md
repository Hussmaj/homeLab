# VLAN-plan

VLAN brukes i labben for å dele nettverket opp i separate logiske nettverk. Dette gjør det mulig å skille servere, klienter og DMZ fra hverandre.

## VLAN 10 – SERVERS

- VLAN ID: `10`
- Subnett: `192.168.20.0/24`
- Gateway: `192.168.20.1`
- Bruk: Servere
- Ubuntu Server: `192.168.20.100`

VLAN 10 brukes som servernettverk. Ubuntu Server er plassert i dette nettverket og brukes blant annet til Apache Web Server.

I den nåværende VirtualBox-labben har VLAN 10 ikke en egen access-port på Open vSwitch. Dette skyldes at OVS-VM-en har fire virtuelle nettverkskort, og disse er allerede benyttet av LAN, trunkforbindelsen, CLIENTS og DMZ.

Ubuntu Server håndterer derfor VLAN-taggingen selv gjennom et VLAN-interface. Trafikken sendes tagget over trunkforbindelsen mellom Open vSwitch og pfSense.

## VLAN 20 – CLIENTS

- VLAN ID: `20`
- Subnett: `192.168.30.0/24`
- Gateway: `192.168.30.1`
- Bruk: Klienter
- Windows Client: `192.168.30.100`

VLAN 20 brukes som klientnettverk.

Windows Client er koblet til Open vSwitch gjennom access-porten `enp0s9`. Porten er konfigurert for VLAN 20.

Windows trenger derfor ikke å konfigurere VLAN-tagging selv. OVS håndterer VLAN-tilknytningen på access-porten og sender trafikken videre som VLAN 20 over trunkforbindelsen.

## VLAN 30 – DMZ

- VLAN ID: `30`
- Subnett: `192.168.40.0/24`
- Gateway: `192.168.40.1`
- Bruk: DMZ
- Ubuntu DMZ: `192.168.40.101`

VLAN 30 brukes som DMZ-nettverk.

Ubuntu DMZ er koblet til Open vSwitch gjennom access-porten `enp0s10`, som er konfigurert for VLAN 30.

Trafikken fra Ubuntu DMZ kommer inn på OVS som vanlig Ethernet-trafikk. OVS håndterer VLAN 30 på access-porten før trafikken sendes videre over trunkforbindelsen til pfSense.

## Trunkforbindelse

Open vSwitch har en trunkforbindelse mot pfSense gjennom `enp0s8`.

Trunkforbindelsen transporterer:

- VLAN 10 – SERVERS
- VLAN 20 – CLIENTS
- VLAN 30 – DMZ

På pfSense er VLAN 10, 20 og 30 opprettet på `em0`.

`em0` er nettverkskortet som brukes som parent for VLAN 10, 20 og 30.

## VLAN-oversikt

```text
                    pfSense
                       │
                      em0
                       │
              VLAN-LAB / Trunk
              VLAN 10, 20, 30
                       │
                       ▼
                  Open vSwitch
                       │
          ┌────────────┼────────────┐
          │            │            │
       VLAN 10       VLAN 20      VLAN 30
          │            │            │
      Ubuntu        Windows      Ubuntu
      Server        Client         DMZ
```
