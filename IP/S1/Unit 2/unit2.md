## ATM networks ( Asynchronous Transfer Mode )

It is an International Telecommunication Union- Telecommunications Standards Section (ITU-T) efficient for call relay and it transmits all information including multiple service types such as data, video, or voice which is conveyed in small fixed-size packets called cells. Cells are transmitted asynchronously and the network is connection-oriented. 

### Why ATM networks? 

1. Driven by the integration of services and performance requirements of both telephony and data networking: “broadband integrated service vision” (B-ISON). 
1. Telephone networks support a single quality of service and are expensive to boot. 
1. Internet supports no quality of service but is flexible and cheap. 
1. ATM networks were meant to support a range of service qualities at a reasonable cost- intended to subsume both the telephone network and the Internet. 

### ATM Cell Format – 

As information is transmitted in ATM in the form of fixed-size units called cells. As known already each cell is 53 bytes long which consists of a 5 bytes header and 48 bytes payload. 

![alt text](image.png)

- Asynchronous Transfer Mode can be of two format types which are as follows: 

![alt text](image-1.png)

![alt text](image-6.png)

1. UNI (User-Network Interface) Header: This is used within private networks of ATMs for communication between ATM endpoints and ATM switches. It includes the Generic Flow Control (GFC) field. 
1. NNI (Networkx-Network Interface) Header: is used for communication between ATM switches, and it does not include the Generic Flow Control(GFC) instead it includes a Virtual Path Identifier (VPI) which occupies the first 12 bits. 

### Working of ATM: 

ATM standard uses two types of connections. i.e., Virtual path connections (VPCs) which consist of Virtual channel connections (VCCs) bundled together which is a basic unit carrying a single stream of cells from user to user. A virtual path can be created end-to-end across an ATM network, as it does not rout the cells to a particular virtual circuit. In case of major failure, all cells belonging to a particular virtual path are routed the same way through the ATM network, thus helping in faster recovery. 

## ATM Layers

1. ATM Adaptation layer 
2. ATM Layer .
3. Physical Layer .

| AAL Type   | Purpose / Use Case                                                      | Data Type                              | Key Features                                                                      |
| ---------- | ----------------------------------------------------------------------- | -------------------------------------- | --------------------------------------------------------------------------------- |
| **AAL1**   | Constant Bit Rate (CBR) services like voice and video over leased lines | Time-sensitive (e.g., audio)           | - Supports real-time traffic<br>- Provides timing recovery<br>- Error detection   |
| **AAL2**   | Variable Bit Rate (VBR) services like compressed voice/video            | Time-sensitive (but less strict)       | - Low latency<br>- Supports short packets<br>- Multiplexing multiple streams      |
| **AAL3/4** | Connection-oriented and connectionless data (now obsolete)              | Data with possible large messages      | - Complex overhead<br>- Fragmentation and reassembly<br>- Mostly replaced by AAL5 |
| **AAL5**   | Most widely used; for data like IP over ATM                             | Connection-oriented VBR (e.g., TCP/IP) | - Simple, efficient<br>- No error correction<br>- Supports large data transfer    |

1. ATM Adaptation sublayers :
    1. CS (convergence sublayer ):

    The CS handles timing recovery, sequence numbers, and error detection.

    However, in AAL1, most of the header responsibilities are passed down to SAR.

2. SAR (Segmentation and reassembly)

    SAR breaks the CS PDU into 48-byte payloads suitable for insertion into ATM cells.

    ![alt text](image-7.png)

### Types of AAL :

1. AAL1 

- 47 bytes payloads are recieved from CS layer .
- 1 Byte header + 47 = 48 packets. 

    ![alt text](image-8.png)

2. AAL2

- 45 bit payloads and 1 bit header and 2 bit trailer.

    ![alt text](image-9.png)

3. AAL3/4

- takes 44payload + 4 header + 4 trailer bits packets from CS layer and divides them init 44 bit payloads and adds 2 hedare and 2 tarilers .

    ![alt text](image-10.png)

4. AAL5

- 48+8 trailer from CS into 48 payloads in SAR.

    ![alt text](image-11.png)

## Frame Relay :

Frame Relay is a packet-switching network protocol or virtual circuit network protocol that is designed to work at the data link layer of the network. It is used to connect Local Area Networks (LANs) and transmit data across Wide Area Networks (WANs).

![alt text](image-2.png)

- Frame relay frame 

 ![alt text](image-4.png)

 ![alt text](image-3.png)

- Frame Relay normally modifies the HDLC header from a 1 byte address field to a 2 byte address field, as seen above. You can have a 3 or 4 byte format as well. In addition, there is no Control field!

Starting Delimiter Flag - 0x7E

- DLCI (10 bits)	Data Link Connection Identifier, representing the address of the frame, which corresponds to the PVC. It represents the virtual connection between the DTE and the Frame Relay switch.
- C/R (1 bit)	Designates whether the frame is a command or a response.
- EA (1 bit)	Extended Address field, allowing for up to 2 additional bytes in the header, expanding the number of possible addresses.
- FECN (1 bit)	Forward Explicit Congestion Notification, used for congestion control.
- BECN (1 bit)	Backward Explicit Congestion Notification, used for congestion control.
- DE (1 bit)	Discard Eligibility.
- EA (1 bit)	Extended Address.

## 🛰️ HDLC (High-Level Data Link Control)

HDLC is a bit-oriented protocol used for data communication over point-to-point and multipoint links. It is defined by ISO and is used at the Data Link Layer (Layer 2) of the OSI model.

| Feature                      | Description                                        |
| ---------------------------- | -------------------------------------------------- |
| **Protocol Type**            | Bit-oriented protocol                              |
| **Layer**                    | Data Link Layer (Layer 2)                          |
| **Communication**            | Point-to-point and multipoint                      |
| **Error Control**            | Yes (uses CRC)                                     |
| **Flow Control**             | Yes                                                |
| **Framing**                  | Uses flags (`01111110`) to define frame boundaries |
| **Synchronous Transmission** | Yes                                                |

📥 Types of HDLC Frames:

| Frame Type  | Meaning           | Use Case                                         |
| ----------- | ----------------- | ------------------------------------------------ |
| **I-frame** | Information frame | Carries user data and control info               |
| **S-frame** | Supervisory frame | Used for flow and error control                  |
| **U-frame** | Unnumbered frame  | For link management (setup, disconnection, etc.) |

![alt text](image-5.png)