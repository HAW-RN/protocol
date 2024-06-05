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
