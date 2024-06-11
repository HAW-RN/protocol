# Routed protocol (messages)
## (Tom Westendorf)
The task of the routed protocol is to transfer chat messages from one client to another. Therefor it needs to have metadata that contains the sender and receiver information.
## Requirements

## Packet format (Jeremy Reimers)

| Name     | Description | Target Type |
|----------|-------------|-------------|
| nickname | The nickname of the sender | `string` |
| message  | The message to be sent | `string` |

## Example

```json
{
    "header":     {[...]}, // SEE SHARED HEADER
    "nickname":           "Max Mustermann",
    "message":               "Hello World!"
}
```
