## \#Dag 1:



Snakket med chatgpt, bedt han om om å lage en oppgave for meg for øve på oppsett av nettverk og nettverkstjenester

for en liten bedrift med høy sikkerhet.



Gjennomført:



Lastet ned VMbox for å sette opp 3 virutelle maskiner. Firewall, Linux server og Windows 10  for klient.

Laget bruker for ubuntu, admin: lab, passord:1037



Firewall:



* lastet ned pfSense som jobber som brannmur



Linux server:

* Lastet ned ubuntu server for oppsett av Linux server



Klient:

* Lastet ned windows 10 som klient for å teste

### 

##### Hyper - V problememet: "CPU doesn't support long mode"

##### 

For å kunne kjøre pfSense så måtte jeg disable Hyper - v. Det er grunnet feilmeldingen "CPU doesn't support long mode".



**Svar fra chatgpt:**



Oracle VM VirtualBox and Hyper-V both want to control the CPU’s virtualization features. Only one can use them directly.



When Hyper-V starts first, VirtualBox cannot access the CPU correctly, which causes errors like: Only one can use them directly.





Det er ikke farlig og ha denne av, og den må InFact være av for å la Hyper-V ta kontroll over CPU-virtualisering, og da får ikke Oracle VM VirtualBox bruke den direkte.



**Skru av Hyper - V:**



Command: bcdedit /set hypervisorlaunchtype off





**Skru på Hyper - V:**

For å skru denne på igjen skrives denne kommandoen inn i terminal vindet når du er innlogget som administrator:



Command: bcdedit /set hypervisorlaunchtype auto


