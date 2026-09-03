# Oppsett av windows klient

<img width="568" height="211" alt="image" src="https://github.com/user-attachments/assets/58fe6564-50a1-4619-b76d-04c5d8bfdbe6" />

## Tests
- Ping gateway: ✓
<img width="495" height="199" alt="image" src="https://github.com/user-attachments/assets/f8008880-1a67-4910-88c2-f8a6ee23b76b" />

- Ping webserver: ✓
<img width="542" height="206" alt="image" src="https://github.com/user-attachments/assets/c2da399c-1836-4d03-aefa-903aabc56b25" />


## Firewall regler
**Ping allowed from and to 192.168.10.10(Webserver)**

- Kjørt kommandoen: netsh advfirewall firewall add rule name="Allow Ping from Ubuntu" protocol=icmpv4:8,any dir=in action=allow remoteip=192.168.10.10

  
