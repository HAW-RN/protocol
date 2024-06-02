# Routing protocol (participants)
    Bastian Basler, Tim Hagedorn, Ruben Marin Grez, Eike Balling
## Requirements
#### Prerequisites
- Participants have to be in the same Network
- Participants must be able to send and receive packages via IPv4 
- Participants must be reachable via their IPv4 adress 
- Participants must have a Timer 
- A connecting participant has to know the IPv4 adress and Port of the participant they want to connect to

#### Protocol Requirements
- Every Participant has to be able to 
start and shutdown themself 
- Every Participant has to be able to give back a List of all Participants at any time 
- There shall be no central Node
Participants must be able to forward Messages 
- The participants must form any partially meshed network
- Participants may send Messages to themselves

## Packet format
### Header
- Packagetype : routing protocol
- IP: Source
- Port: Source
- IP: Destination
- Port: Destination
- ProtokollID : SWAG
- Command : 

### Table
| Target  | Next | Hop-Count  |   
|---|---|---|
|  IP:Port | IP:Port  | Integer  |   
|   |   |   |   
|   |   |   | 

### Example Data

```json
{
  "Data": "Participant A",
  "Table": [
    {
      "Target": "10.0.0.5",
      "Next": "10.0.0.3",
      "Hopcount": "4"
    },
    {
      "Target": "10.0.0.11",
      "Next": "10.0.0.6",
      "Hopcount": "2"
    }
  ]
}

```

## Procedure
1. Participant A starts the Application and sets internal Table update Timer to 30 seconds
2. Participant B sends CR to Participant A and sends current Routingtable
3. Participant A accepts CR from Participant B and answers CRR and sends current Routingtable 
4. Participant A updates updates Routingtable based on the recived Table
5. After A´s Timer expired A sends SCC to all next entrances in its Routingtable
6.  1.  Participant A updates Routingtable based on recived SCCRs
    2. If SCCR isn´t recived after one second Participant A sets Hop Count to 16 (Poison Reverse)
7. Participant A sends STU to all active Participants
8. Participant A resets Timer to 30 seconds

## Example
![Logo](./images/Routing_Protokoll_Sequenz_Diagram.png)


## Commands
- CR: Connection Request (Send Routingtable)
- CRR: Connect Request Reply (Send Routingtable)
- SCC: Send Connection Check
- SCCR: Reply 
- STU: Send Table Update
