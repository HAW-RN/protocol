# Shared Header

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
