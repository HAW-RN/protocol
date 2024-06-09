# Encoding

## Requirements
- The protocols must use JavaScript Object Notation (JSON).
- The JSON string must be UTF-8 encoded.
- ...

## Format
A message is made up of two JSON strings, one for the header and the other for the data.

### Header
The header is always 56 _UTF-8_ characters long. That means the payload should be exactly 56 bytes long. 

This allows the receiving side to first fill an input buffer with the data for exactly one JSON string, and extract further information from there. The content of the header is `{"length":"01234","crc32":"0123456789","type_id":"1"}`, or formatted to look more legible:
```json
{
  "length": "01234",
  "crc32" : "0123456789",
  "type_id": "1"
}
```

The information here is used to receive the data JSON.

| Name   | Description                                             | Target Type         |
|--------|---------------------------------------------------------|---------------------|
| length | Length of the 2nd JSON string (Data) in bytes.          | `uint16` or `int32` | 
| crc32  | CRC32 checksum over the buffer of the 2nd JSON string.  | `uint32` or `int64` |
| type_id| The type of the message.                                | `byte (uint8)`      |

To ensure that the header is always 56 characters long, all values are encoded as strings with leading zeros. The number of digits depends on the largest possible number of these values. All values must be treated as unsigned integers. If the chosen programming language does not support this, a larger data type must be selected. The recommended types are listed in the table above.

### Packet Type
The `type_id` field is used to determine the type of the message. The following types are defined:

| ID | Type          | Description                |
|----|---------------|----------------------------|
| 1  | Message       | A routed message packet             |
| 2  | CR            | Connection Request (Send Routingtable)  |
| 3  | CRR           | Connect Request Reply (Send Routingtable)  |
| 4  | SCC           | Send Connection Check  |
| 5  | SCCR          | Reply |
| 6  | STU           | Send Table Update  |

## Handling Headers

If a client is sending a message, it should first write a header. To do this, the size of the string-formatted JSON data and the CRC32 checksum of this data must be calculated and packed into a JSON-formatted header. This header must be aligned to 56 bytes as stated above. The header and the data are then sent immediately one after the other, with the header preceding the data (encapsulation).

If a client is receiving a message, it should read 56 bytes from the input buffer to receive the header. After reading the data size from the header, the client can start reading the data section of the message using the data size. Then, the CRC32 checksum of the data section should be calculated and compared to the checksum specified in the header:  
If the checksums are equal, the client can proceed with further processing, such as message forwarding or updating the routing table.  
If the checksums are not equal, the message can be discarded and ignored.
