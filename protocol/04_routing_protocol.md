# Routing protocol (participants)
    Bastian Basler, Tim Hagedorn, Ruben Marin Grez, Eike Balling
## Requirements
#### Prerequisite
- Teilnehmer müssen im selben Netz sein
- Die Teilnehmer müssen auf ipv4 Broadcast Anfragen reagieren können
        - Empfangen und Senden können
- Müssen über Ipv4 Adresse pakete empfangen und senden können
- Müssen einen Timer haben
#### Protocol Requirements
- Jeder Teilnehmer soll sich beenden und starten könne
- Jeder Teilnehmer kann eine Liste über alle Teilnehmer ausgeben
    - zu jedem Zeitpunkt
- Kein Zentraler Knoten
- Knoten müssen Nachrichten weiterleiten
- Die Teilnehmer müssen ein beliebiges Teilvermaschtes Netz bilden
- Man soll sich selbst Nachrichten schicken können

## Packet format
### Header
- Packettype : routing protocol
- IP: Source
- IP: Destination
- Port: Source
- Port: Destination
- ProtokollID : 
- Command :

### Table
| Ziel  | Next | Hop-Count  |   
|---|---|---|
|  IP:Port | IP:Port  | Integer  |   
|   |   |   |   
|   |   |   |   
## Procedure


## Example



BFN: Broadcast Fetch Nodes
BFNR : BFN reply
CR: Connection Request (Tabelle wird verschickt)
CRR: Connect Request Reply (Tabelle mit schicken)
SCC: Send Connection Check
SCCR: Reply 
STU: Send Table Update


# Questions
- TCP Broadcast?
- Muss man die Teilnehmer über die Broadcast Adresse ermitteln, oder kriegt man IP:Port (So wie Telefonnummer)
- Brauchen wir den Port wirklich? Oder ist der Fest?
- Sind wir zwei verscheidene Protokolle oder ein größeres
- TTL?


