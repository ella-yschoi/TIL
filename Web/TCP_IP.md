# TCP/IP

## 1. IP/IP Packet

### IP (Internet Protocol)

Transmits data in communication units called packets to specified IP addresses

### IP Limitations

- Connectionless: Even if there's no recipient for packets or service is unavailable, client still sends packets as-is
- Unreliable: If there's a failure in servers during data transmission and packets are lost, client cannot detect it, and packets may not arrive in order

<br/>

## 2. TCP

### TCP Segment

Includes source PORT, destination PORT, transmission control, sequence, verification information, etc. that can supplement source IP and destination IP information of IP packets

### TCP (Transmission Control Protocol) Characteristics

- Connection-oriented: TCP 3-way handshake (virtual connection)
- Data transmission guarantee: Because it returns responses
- Order guarantee: If packets don't arrive in order, can request packet retransmission based on information in TCP segment
- Reliable protocol

<br/>

## 3. UDP

### UDP (User Datagram Protocol) Characteristics

- Simple protocol with only PORT and checksum (duplicate check) field information added to IP
- Has almost no functionality but can be customized
- Connectionless: No TCP 3-way handshake
- No data transmission guarantee
- No order guarantee
- Data transmission and order are not guaranteed but simple and fast
- Frequently used for services where continuity is more important than reliability (ex. real-time streaming)
