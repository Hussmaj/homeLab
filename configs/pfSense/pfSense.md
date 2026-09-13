# Oppsett av pfSense som gateway og ruter

<img width="675" height="215" alt="image" src="https://github.com/user-attachments/assets/170f322d-db7f-497b-a4b5-102051affdce" />


## Tests

Ping webserver fra gateway:

<img width="680" height="362" alt="image" src="https://github.com/user-attachments/assets/2c0e6aac-a5a7-46f4-9c06-9d2c1bcd5795" />

Ping klient fra gateway: 

<img width="649" height="364" alt="image" src="https://github.com/user-attachments/assets/64b60fd9-4612-4052-a258-78fc9ef392e1" />


## Firewall regler

Å pinge klienten fra pfSense var ikke mulig først fordi icmp blokkerer dette så klart, så det ble lagt inn en ny regel i klient maskien som klar gateway pinge klient.

netsh advfirewall firewall add rule name="Allow Ping from pfSense" protocol=icmpv4:8,any dir=in action=allow remoteip=192.168.10.1
