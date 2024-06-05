# Encoding

## Requirements
- The protocols must use JavaScript Object Notation (JSON).
- The JSON string must be UTF-8 encoded.
- ...

## Format
A message is made up of two JSON strings, one for the header and the other for the data.

### Header
The header is always 50 characters long. This allows the receiving side to first fill an input buffer with the data for exactly one JSON string, and extract further information from there. The content of the header is `{"Header":{"Length":"01234","CRC32":"0123456789"}}`, or formatted to look more legible:
```json
{
  "Header": {
      "Length": "01234",
      "CRC32" : "0123456789"
    }
}
```

The information here is used to receive the data JSON.

| Name   | Description                                             | Target Type         |
|--------|---------------------------------------------------------|---------------------|
| Length | Length of the 2nd JSON string (Data) in bytes.          | `uint16` or `int32` | 
| CRC32  | CRC32 checksum over the buffer of the 2nd JSON string.  | `uint32` or `int64` |

To ensure that the header is always 50 characters long, all values are encoded as strings with leading zeros. The number of digits depends on the largest possible number of these values. Both values must be treated as unsigned integers. If the chosen programming language does not support this, a larger data type must be selected. The recommended types are listed in the table above.

### Data
This JSON contains the payload. Its content is defined by the appropriate sections.

## Example


## Handling Headers

If a client is sending a message, it should first write a header. To do this, the size of the string-formatted JSON data and the CRC32 checksum of this data must be calculated and packed into a JSON-formatted header. This header must be aligned to 50 bytes as stated above. The header and the data are then sent immediately one after the other, with the header preceding the data (encapsulation).

If a client is receiving a message, it should read 50 bytes from the input buffer to receive the header. After reading the data size from the header, the client can start reading the data section of the message using the data size. Then, the CRC32 checksum of the data section should be calculated and compared to the checksum specified in the header:  
If the checksums are equal, the client can proceed with further processing, such as message forwarding or updating the routing table.  
If the checksums are not equal, the message can be discarded and ignored.