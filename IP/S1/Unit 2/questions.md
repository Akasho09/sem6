## If an application uses AAL3/4 and there are 47,787 bytes of data coming into the CS, how many padding bytes are necessary? How many data units get passed from the SAR to the ATM layer? How many cells are produced?
ans:
---
In AAL3/4, the total data passed to the SAR sublayer must be a multiple of 44 bytes. This total includes:

- 4 bytes of Convergence Sublayer (CS) header
- 47,787 bytes of actual data
- Padding bytes (to be calculated)
- 4 bytes of CS trailer
- 
=> 
4 (header) + 47,787 (data) + Padding + 4 (trailer) ≡ 0 mod 44
47,787 + 8 = 47,795
=> Padding = (44 - 11) mod 44 = 33 bytes

- Total = 4 (header) + 47,787 (data) + 33 (padding) + 4 (trailer) = 47,828 bytes
Number of SAR-PDUs = 47,828 / 44 = 1,087
Thus, 1,087 data units are passed from the SAR to the ATM layer.

- In AAL3/4, each SAR-PDU maps directly to one ATM cell. Therefore, the number of ATM cells produced is equal to the number of SAR-PDUs:

1,087 ATM cells are produced.


## Name the ATM layers and their functions?
- Asynchronous Transfer Mode (ATM) is a high-speed, connection-oriented networking technology designed to handle voice, video, and data traffic. Its architecture is structured into several layers, each with specific functions to ensure efficient data transmission.

- 📚 ATM Protocol Layers and Their Functions
| **Layer**                         | **Function**                                                                                                                                                                                                                                                                                                                                |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. Physical Layer**             | Responsible for the transmission and reception of raw bits over a physical medium. It comprises two sublayers: the Physical Medium (PM) sublayer, which deals with the physical transmission, and the Transmission Convergence (TC) sublayer, which prepares cells for transmission and extracts them upon reception.                       |
| **2. ATM Layer**                  | Handles the creation, transmission, and reception of fixed-size cells (53 bytes: 5-byte header and 48-byte payload). It manages cell multiplexing and demultiplexing, routing based on Virtual Path Identifier (VPI) and Virtual Channel Identifier (VCI), traffic management, and switching functions.                                     |
| **3. ATM Adaptation Layer (AAL)** | Adapts user data from higher layers into ATM cells and vice versa. It segments and reassembles data, adds necessary headers and trailers, and ensures proper timing and error control. -Different AAL types (e.g., AAL1, AAL2, AAL5) cater to various service requirements like constant bit rate (CBR) or variable bit rate (VBR) traffic. |

## High-Level Data Link Control (HDLC) and Frame Relay are both data link layer protocols, but they differ in frame structure and functionality. Here's a comparative analysis of their frame formats:

| **Feature**           | **HDLC**                                                       | **Frame Relay**                                                             |                                                                                                                                                                    |
| --------------------- | -------------------------------------------------------------- | --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Flag**              | 8-bit flag (`01111110`) at both start and end                  | Same as HDLC                                                                |                                                                                                                                                                    |
| **Address Field**     | 8 or more bits identifying the destination station             | 2-byte field containing DLCI, congestion control bits, EA bits, and C/R bit |                                                                                                                                                                    |
| **Control Field**     | Present; specifies frame type and manages flow/error control   | **Absent**; Frame Relay omits this field to reduce overhead                 |                                                                                                                                                                    |
| **Information Field** | Variable length; carries payload data                          | Variable length; carries payload data                                       |                                                                                                                                                                    |
| **FCS**               | 16 or 32-bit CRC over Address, Control, and Information fields | 16-bit CRC over Address and Information fields                              | 

## An IP datagram is carrying 5000 bytes and needs to be fragmented into 5 fragments of 1000 bytes. Show the values of fragmentation offset in each fragment. Suppose the third fragment is further required to be fragmented into three fragments of 400 bytes each. Show fragment offset values with respect to the original datagram.

> The Fragment Offset is a field in the IPv4 header that indicates the position of a fragment's data relative to the beginning of the original unfragmented datagram. This field is essential for the reassembly of fragmented packets at the destination.

Total size = 5000 bytes
Header size = 20 bytes (default IP header)
Data = 4980 bytes

Each fragment:
Fragment 1: Offset = 0, Size = 1000 bytes
Fragment 2: Offset = 1000/8 = 125, Size = 1000 bytes
Fragment 3: Offset = 2000/8 = 250, Size = 1000 bytes
Fragment 4: Offset = 3000/8 = 375, Size = 1000 bytes
Fragment 5: Offset = 4000/8 = 500, Size = 980 bytes

Third Fragment (1000 bytes) → broken into 3 fragments of 400 bytes:
Fragment 3.1: Offset = 250, Size = 400 bytes
Fragment 3.2: Offset = (250×8 + 400)/8 = 300, Size = 400 bytes
Fragment 3.3: Offset = (300×8 + 400)/8 = 350, Size = 200 bytes


## What is Sliding Window Protocol? A TCP connection is using a window size of 10,000 bytes and the previous acknowledgment number was 22,001. It receives a segment with acknowledgment number 24,001 and window size advertisement of 12,000. Draw a diagram to show the situation of the window before and after.

Sliding Window Protocol: It allows multiple packets to be sent before receiving an acknowledgment for the first one, increasing throughput.

- 🔍 Analyzing the Scenario
 - Before Receiving the New Segment:

    - Bytes Sent and Acknowledged: Up to byte 22,000

    - Bytes Sent but Not Yet Acknowledged: 22,001 to 32,000 (since the window size is 10,000 bytes)

 - After Receiving the New Segment:

    - Acknowledgment Number: 24,001 indicates that bytes up to 24,000 have been received and acknowledged.

    - New Window Size: 12,000 bytes

    - New Send Window: 24,001 to 36,000