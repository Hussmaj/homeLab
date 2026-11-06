# Feilsøkingslogg – DNS-problemer i DMZ

## Problem

Etter jeg hadde satt opp DMZ nettverket mitt og skulle insatllere Apache så ble jeg møt på problemer i det jeg skulle oppdatere pakkene gjennom kommandoen
DMZ-serveren hadde tilgang til internett, men klarte ikke å utføre DNS-oppslag. Jeg kunne pinge 8.8.8.8, men kommandoen nslookup vg.no fungerte ikke.

## Feilsøking

**1. Kontrollerte internettforbindelsen**  
Jeg testet forbindelsen ved å pinge 8.8.8.8. Dette fungerte, noe som viste at serveren hadde tilgang til internett.

**2. Testet DNS-oppslag**  
Jeg kjørte nslookup vg.no, men domenenavnet ble ikke oversatt til en IP-adresse.

**3. Kontrollerte DNS-serveren**  
Jeg undersøkte DNS-oppsettet og fant ut at DMZ-serveren brukte pfSense (192.168.40.1) som DNS-server.

**4. Testet DNS direkte mot pfSense**  
Jeg kjørte nslookup vg.no 192.168.40.1, men fikk ikke svar fra DNS-serveren.

**5. Undersøkte brannmurreglene i pfSense**  
Jeg fant ut at brannmurregelen som blokkerte tilgang fra DMZ til private nettverk (RFC1918), også blokkerte DNS-forespørsler til pfSense.

