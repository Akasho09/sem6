## 15363049 163A92BC 00004199 700207FF 00000000 02040155 03030700

Options Used

Option 1: Maximum Segment Size (MSS)
Option 2: No-Operation (NOP)
Option 3: Window Scale
i. Values of the Options Used

MSS Value: 0x0155 (341 in decimal)
Window Scale Factor: 0x03 (3 in decimal)

## A router receives an IP packet with source IP address 130.45.3.3 and destination IP address 201.23.4.6. The router cannot find the destination IP address in its routing table. Fill in the fields for the ICMP message sent.
Answer:
Since the destination is unreachable, the router sends an ICMP Destination Unreachable message.

Type: 3 (Destination Unreachable)
Code: 0 (Network Unreachable)
Source IP: 130.45.3.3 (Router's IP)
Destination IP: 201.23.4.6 (Original packet’s sender)
Data: Includes the original packet’s IP header and first 8 bytes of data.

## An ICMP message has arrived with the header (in hexadecimal):
05 00 11 12 11 08 03 02
(a) What is the type of message?
The first byte 05 indicates Redirect Message (ICMP Type 5).
(b) What is the code?
The second byte 00 represents Redirect Datagram for the Network.
(c) What is the purpose of the message?
An ICMP Redirect message informs the sender that there is a better route available for the packet.
(d) What is the value of the last 4 bytes and what do they signify?
The last four bytes (11 08 03 02) indicate the new gateway address to which the sender should send future packets.
