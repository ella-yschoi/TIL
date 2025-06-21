# Network Layer

## 1. OSI 7-Layer Model

### Model Characteristics

- Network standard specification established by ISO
- Enables common network usage regardless of computer manufacturer
- Each layer is independent, so it's not affected by other layers during data transmission process

### Characteristics of Each Layer

#### Layer 1 (Physical Layer)

- Controls physical connections between systems and converts electrical signals
- e.g. Convert signals to digital or analog

#### Layer 2 (Data Link Layer)

- Determines data transmission between network devices and physical addresses
- e.g. Bridge/switch, MAC address

#### Layer 3 (Network Layer)

- Responsible for data routing between actual networks and selects optimal paths
- e.g. IP packet transmission

#### Layer 4 (Transport Layer)

- Provides services to enable reliable data exchange between computers
- e.g. TCP/UDP connections

#### Layer 5 (Session Layer)

- Functions such as setting and releasing session connections, transmitting session messages
- In other words, determines communication methods between computers

#### Layer 6 (Presentation Layer)

- Encodes or decodes data passed to or received from application layer
- e.g. Data conversion such as character codes, compression, encryption

#### Layer 7 (Application Layer)

- Layer that ultimately provides interface with users
- Application programs executed by users
- e.g. File transfer, website viewing, etc.

#### Data Transmission Side

- Data transmission side passes data from upper layers to lower layers
- Each layer adds necessary information to data, and this information is called 'header' or 'trailer'
- Adding headers is called 'encapsulation'

#### Data Receiving Side

- Receives data passed through each layer from lower layers to upper layers
- Passing data to upper layers and removing headers at each layer is called 'de-encapsulation'
- After de-encapsulation, when reaching the final application layer, only the original data intended to be transmitted remains

<br/>

## 2. TCP/IP 4-Layer Model

### Model Characteristics

- Model simplified and made practical for real-world use based on OSI model

### Characteristics of Each Layer

#### Layer 1 (Network Interface Layer)

- Corresponds to physical layer and data link layer of OSI layers
- Uses MAC as physical address
- LAN, packet network, etc.

#### Layer 2 (Internet Layer)

- Corresponds to network layer of OSI layers
- Responsible for transmitting IP packets between communication nodes and routing
- e.g. IP, ARP, RARP

#### Layer 3 (Transport Layer)

- Corresponds to transport layer of OSI layers
- Controls connections between communication nodes and is responsible for reliable data transmission
- e.g. TCP, UDP

#### Layer 4 (Application Layer)

- Corresponds to session, presentation, and application layers of OSI layers
- Used when implementing applications based on TCP/UDP
- e.g. FTP, HTTP, SSH
