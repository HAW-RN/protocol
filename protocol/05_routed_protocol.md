# Routed protocol (messages)
The task of the routed protocol is to transfer chat messages from one client to another. Therefor it needs to have metadata that contains the sender and receiver information.
## Requirements

## Packet format
| Content          | Size in Byte | Max. size in JSON |
|:---------------- | ------------:|------------------:|
| Packagetyp       |            1 |                15 |
| Source IP        |            4 |                 5 |
| Source Port      |            2 |                15 |
| Destination IP   |            4 |                 5 |
| Destination Port |            2 |                 5 |
| TTL              |            1 |                 2 |
| Data             |          128 |               128 |

## Procedure

## Example

```json
{
    "package_type":       "data_message"
    "source_ip":          "192.168.123.122"
    "source_port":        "6827"
    "destination_ip":     "192.168.234.233"
    "destination_port":   "234"
    "ttl":                "16"
    "data":               "Test Data"
}
```

Flag: differentiation between Message, Routing-protocol, disconnection, connection failure ...
Source IP: IPv4 address of the sender
Source Port: Port of the sender
Destination IP: IPv4 address of the destination
Destination Port: Port of the destination
TTL: time to live of the package. maximum of 16 to 64
Data: message value limited to 128 chars in utf-8 for smaller package size
