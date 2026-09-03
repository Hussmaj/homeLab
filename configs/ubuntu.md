# Oppsett av ubuntu som webserver

<img width="811" height="211" alt="image" src="https://github.com/user-attachments/assets/e8b384ca-3188-410a-b9fc-5a1431437bd5" />

## Tests
- Ping gateway: ✓
- Ping klient: ✓

## Firewall
- ping allowed to 192.168.10.100 (Klient)
<img width="555" height="164" alt="image" src="https://github.com/user-attachments/assets/b19d2eb2-f20f-4695-ad8f-0abe0c4505a8" />

**Denne kommandoen kjøres på klientmaskinen for å lage en regel som gjør at kun webserveren kan kommunisere med klienten:**

netsh advfirewall firewall add rule name "Allow ping from webserver" protocol=icmp4:8,any dir=in action=allow remoteip="192.168.10.10"

- ping allowed to 192.168.10.1 (Gateway)
<img width="519" height="163" alt="image" src="https://github.com/user-attachments/assets/30ecffa1-7c41-42f9-b164-697114ce8acb" />
