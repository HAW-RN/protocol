# Encoding

## Requirements
- The protocols must use JavaScript Object Notation (JSON).
- The JSON string must be UTF-8 encoded.
- ...

## Format
### Header
| Type  | Name      | Description                                      |
|-------|-----------|--------------------------------------------------|
| int_? | Length    | Message length (including or excluding?) header. | 
| int_? | Checksum  | ...                                              |
TODO:
- Define int sizes. The length cannot exceed the uint16 range. However, it may be more convenient to use int32 in languages that do not support unsigned types.
- Select a checksum algorithm.

### Data
| Type    | Name | Description                             |
|---------|------|-----------------------------------------|
| String  | Data | JSON message encoded as a UTF-8 string. |

## Example
