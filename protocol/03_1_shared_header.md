# Shared Header (Laurin Zacharias)

The shared header is part of the data after the initial common header. It has a lot of information that is used to determine the type of the message, potential target and how to handle it.

## Fields

| Name | Description | Target Type |
|------|-------------|-------------|
| Source IP | IPv4 address of the sender | `string` |
| Source Port | Port of the sender | `int` |
| Destination IP | IPv4 address of the destination | `string` |
| Destination Port | Port of the destination | `int` |
| TTL | time to live of the package. maximum of 16 to 64 | `int` |

## Example

```json
{
    "source_ip": "192.168.101.1",
    "source_port": 1234,
    "dest_ip": "192.168.102.1",
    "dest_port": 1234,
    "ttl": 16
}
```

## Source Address Guideline (Tom Hert)

_Defined in Protocol v1.1 (26.06.2024)_

The sending participant **_MUST_** use the port and ip address under which it is reachable via the TCP Socket, _not_ the port and ip it uses to connect to the target participant.

### Example

**Scenario 1: Connection**

- Participant A, Socket Address: 127.0.0.1:46459
- Participant B, Socket Address: 127.0.0.1:54321

1. Participant A sends a CR to Participant B by connect to the socket (127.0.0.1:54321)
2. The system gives Participant A a new port for the connection (127.0.0.1:12345)
3. Participant B receives a connection from 127.0.0.1:12345 (the new port)
4. Participant A _MUST_ send the CR with the source address and _not_ that of the connection
    1. target_ip: 127.0.0.1
    2. target_port: 46459
5. Participant B accepts the CR and internally maps the source address to the connection
    1. For Participant B the peer at 127.0.0.1:12345 is now mapped to 127.0.0.1:46459
6. Participant B sends a CRR to Participant A (127.0.0.1:46459) by looking up the source address in the mapping table
    1. Since the connection between A and B is established via 127.0.0.1:12345 and _NOT_ 127.0.0.1:46459 the client will have to send the CRR via the connection @ 127.0.0.1:12345 to Participant A
7. Participant B must always use the source address of the CR in the routing table so Participant A is globally known as 127.0.0.1:46459 and only Participant B knows the internal mapping to 127.0.0.1:12345

**Scenario 2: Message**

- Participant A, Socket Address: 127.0.0.1:46459
- Participant B, Socket Address: 127.0.0.1:54321
   - Has a connection to Participant A @ 127.0.0.1:12345 (See Scenario 1)
   - Has a connection to Participant C @ 127.0.0.1:34567
- Participant C, Socket Address: 127.0.0.1:23456
    - Has a connection to Participant B @ 127.0.0.1:54321

1. Participant C wants to send a message to Participant A
2. Participant C sends the message to Participant B with the target address of Participant A
    1. target_ip: 127.0.0.1
    2. target_port: _46459_
    3. source_ip: 127.0.0.1
    4. source_port: 23456 (Not the connection port)
3. Participant B receives the message and looks up the target address in the mapping table
    1. It knows that messages from the connection @ 127.0.0.1:34567 are from Participant C (127.0.0.1:23456)
    2. The target address (127.0.0.1:46459) is mapped to 127.0.0.1:12345 internally as Participant B has a connection to Participant A
4. Participant B sends the message to Participant A via the connection @ 127.0.0.1:12345
5. Participant A receives the message and knows that it is from Participant C
