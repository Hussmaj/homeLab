Mandag 09.03.2026



#### Dagens arbeids log:



I dag har jeg jobbet med oppsett av nettverket, slik at alle står på samme lan nettverk .



I windows klient maskinen har jeg satt opp Adapter 1 til Internal Network og kalt det Lan.



i pf sense er adapter satt til NAT(WAN) og Adapter 2 til LAN, fordi den skal representere to forskjellige sider av nettverket. og derfor trenger den 2 nettverkskort. pfSense fungerer som en ruter og brannmur.



Logget inn i pfSense gjennom linken: https://192.168.1.1



Logget inn med bruker:admin og passord:pfsense



Etter dette endret vi ip addressen til 192.168.10.1 for å endre subnettet.Dette var ikke nødvendig, men kun for å skjønne hva subbnettet er.



Dette er viktig for det etterligner hvordan ekte nettverk fungerer. Som følgende:
\[Devices] → LAN → Router/Firewall → WAN → Internet



Etter oppsettet nå

Så er gatewayen satt til 192.168.10.1

DHCP Serveren er på og gir ut ip addresser til alle klienter på nettverket, fra rekkevidden mellom 192.168.10.100 -> 192.168.10.200.



Webserveren har fått ett statisk ip addresse: 192.168.10.10



klienten når serveren



routing fungerer



pfSense fungerer



serveren svarer



Så nettverket ditt er riktig satt opp.



Neste steg i morgen er oppsett av Apache serveren.





#### **Dagens kunnskap.**

* Enhetnene(Tlf, PC, TV) kobles til nettverket ditt hjemme
* LAN: Alle enhetene i ett hjemmenettverk er kobblet sammen. Alle disse enhetene får en ip addresse fra ruteren. De kan finne hverandre og kommunisere(sende/mota) data.
* Ruter/Brannmar: Jobben til ruteren er å sende trafikk mellom to nettverk. Firewall bestemmer hva som kan sendes og mottas gjennom nettverkene. Den står som en vakt forran en inngangsdør. Det er gatewayen i ett nettverk.
* WAN: Wide area Network, dette er siden ruteren som peker mot internettet.
* Nettverk: Dette er resten av verden.



Når du søker på google.com, så skjer følgende:



PC → pfSense → WAN → Internet → Google



**Hva er ett subnett?**



**Hva er gateway?**

