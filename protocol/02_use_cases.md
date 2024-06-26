# Use-Cases
<img src="./images/UseCase.png" width="806" height="806">

### 1. Start New Connection (Laurin Zacharias) 
Client A establishes a connection to another Client B using TCP. Client A sends a CR message inculding its routing table to Client B which responds with a CRR containing its routing table. Both Clients update their routing tables and add information about their new connection to their routing tables.

### 2. Forward Message (Laurin Zacharias) 
Client A receives a message and checks its destination address. If Client A is not the destination, Client A checks its routing table for the destination address and sends the message to the destination, if directly connected or to the next address on the route, if one is available.

### 3. Update Routing Table (Daniil Khoma)
Every 10 seconds Client A requests all directly connected Clients to send a SCCR containing all information in their routing table besides the routing information it got from Client A. When receiving SCCR, Client A will update its routing table with any new information from it. If a Client does not answer this request, they will be marked as unavailable in the routing table.

### 4. Send Routing Table (Hyunki Son)  
When requested Client A sends a SCCR to the requesting Client containing all information in Client A's routing table besides the information it got from the requesting Client.

### 5. Quit Client (Hyunki Son) 
Client A marks all connections through itself as unreachable and sends a STU to all directly connected Clients. Afterwards the program ends itself.

### 6. source is unavailable (Daniil Khoma)
Client A marks all routes in its routing table reachable through the source including the source itself as unreachable and sends a routing table update.

#### Client specific (Laurin Zacharias)
Client specific use cases are use cases whos details are up to the implementing clients, these include:
- send message
- receive message
- display message
- display available participants
