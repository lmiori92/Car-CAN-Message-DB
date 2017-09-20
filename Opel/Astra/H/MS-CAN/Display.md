

## Display protocol

#### Transport protocol

Data is sent to the display via a multi-frame protocol which is standardized in the ISO 15765-2 specification.
Basically, the message can potentially carry 4K of data split across several frames. The start frame contains the length information and the rest is a sequence number and the actual data.
This data is then a packet that the display interprets by writing lines and/or clearing lines.

TODO: insert information about the multi-frame message protocol

#### Generic details

CAN-ID: 0x6C1

Period: =< 3ms (between frames; packets are sent at display content change or from time to time to refresh it)

#### Packet format

2-bytes: display command and / or addressing. TODO: write here what has been found

0x4000 / 0xC000: maybe related to the time it stays on the screen as well ??

0x5000: used to change / address status labels (e.g. RDS, TP, REG...). Interestingly pressing the buttons to change the label status generates single frame messages of 6 or 7 bytes and there seems not to be an obvious indexing. Is this perhaps enabling some sort of direct drawing? To be explored :-)

1-byte: length of the display packet i.e. the data that comes after.

1-byte: 0x03 ? changing it seems not affecting the functionality? needs testing. datatype is a good assumption, check.

1-byte: string type / position / address ?

1-byte: UTF-16 character count

n-bytes: UTF-16 characters.

####  BID: Board Info Display (i.e. the Time/Temperature + 2 info lines LCD display)

A string type / position / address of 0x10 writes data to the first display line without hiding the 2nd line data (from the board computer)

0xB0 is instead writing data on the first line hiding the second line.

| Address | Data | Function | Byte1 | Byte2 | Byte3 | Byte4 | Byte5 | Byte6 | Byte7 | Byte8 |
| ------- | ---- | -------- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| `6C1` | - | - | - | - | - | - | - | - | - | - |


