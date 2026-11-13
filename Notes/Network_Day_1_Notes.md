# Computer Networking --- Day 1 Notes

> **Source:** Transcription of the two handwritten Day 1 notebook
> pages.\
> **Purpose:** Beginner-friendly revision notes. Spelling and
> terminology have been cleaned up; the original topics and examples
> have been retained. A few unclear handwritten phrases are explained
> using the standard networking term.

------------------------------------------------------------------------

## 1. Introduction to Computer Networks

### What is a computer network?

A **computer network** is a telecommunications framework that connects
digital devices (called **nodes**) so they can communicate and interact
with one another.

-   Connections can be **wired** or **wireless**.
-   A network allows connected devices to share resources.
-   Shared resources may include hardware, software, files, data, and
    services.

**Example:** The Internet is a large computer network connecting devices
and smaller networks around the world.

### OSI layer memory aid written in the notebook

The first page also contains a seven-layer OSI mnemonic. The layer
names, from top to bottom, are:

1.  Application
2.  Presentation
3.  Session
4.  Transport
5.  Network
6.  Data Link
7.  Physical

A simple initials-based reminder is **A--P--S--T--N--D--P**. The
mnemonic in the handwriting appears to be "All People Should Try New ...
Pizza"; the word for the Data Link layer is not fully clear.

------------------------------------------------------------------------

## 2. Components of Data Communication

A data communication system has five basic components:

  -----------------------------------------------------------------------
  Component                           Meaning
  ----------------------------------- -----------------------------------
  **Sender**                          The device that sends the data.

  **Receiver**                        The device that receives the data.

  **Message**                         The information being communicated,
                                      such as text, numbers, images,
                                      audio, or video.

  **Transmission medium**             The path through which data
                                      travels, such as a cable or
                                      wireless signal.

  **Protocol**                        The set of rules that controls
                                      communication between devices.
  -----------------------------------------------------------------------

**Basic communication flow:**

``` text
Sender  ─────── Message through a medium ───────>  Receiver
                         ^
                  Rules: Protocol
```

For communication to work, the sender and receiver must follow
compatible protocols.

------------------------------------------------------------------------

## 3. Effectiveness of Data Communication

Data communication is considered effective when it satisfies these four
requirements:

### 3.1 Delivery

Data must reach the **correct destination**.

### 3.2 Accuracy

Data should arrive without being changed or corrupted during
transmission. Error detection and correction mechanisms help maintain
accuracy.

### 3.3 Timeliness

Data must be delivered when it is needed. Delayed delivery can be a
problem for real-time applications such as voice and video calls.

### 3.4 Jitter

**Jitter** is the variation in the time delay between arriving data
packets. For real-time audio and video, high or uneven jitter can cause
interruptions or poor quality.

------------------------------------------------------------------------

## 4. Transmission Modes

Transmission mode describes the direction in which data can flow between
two connected devices.

There are three modes:

### 4.1 Simplex

-   Communication takes place in **one direction only**.
-   One device sends; the other device only receives.
-   The receiver cannot send data back through that communication
    channel.

**Examples:** Traditional radio and television broadcasting.

``` text
Sender  ─────────>  Receiver
        One direction
```

### 4.2 Half-duplex

-   Communication can take place in **both directions**, but not at the
    same time.
-   Devices take turns sending and receiving.

**Example:** Walkie-talkies. One person speaks while the other listens;
they take turns.

``` text
Device A  ─────────>  Device B
Device A  <─────────  Device B

Both directions, but one at a time
```

### 4.3 Full-duplex

-   Communication takes place in **both directions simultaneously**.
-   Both devices can send and receive data at the same time.

**Example:** A telephone conversation.

``` text
Device A  <────────>  Device B

Both directions at the same time
```

  -----------------------------------------------------------------------
  Mode              Direction         Simultaneous      Example
                                      communication?    
  ----------------- ----------------- ----------------- -----------------
  Simplex           One direction     No                Radio broadcast

  Half-duplex       Both directions   No; devices take  Walkie-talkie
                                      turns             

  Full-duplex       Both directions   Yes               Telephone call
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 5. Network Criteria

The notebook identifies three important network criteria:

### 5.1 Reliability

Reliability describes how consistently a network works.

It can be considered using: - **Frequency of failure:** How often the
network fails. - **Recovery time:** How long it takes to restore the
network after a failure.

A reliable network has fewer failures and recovers quickly.

### 5.2 Performance

Performance describes how efficiently a network transfers data and
responds to requests.

Factors include: - **Transit time:** Time taken for data to travel from
source to destination. - **Response time:** Time between sending a
request and receiving a response. - **Number of users:** The number of
users sharing the network. - **Transmission medium:** The communication
channel used to carry data.

### 5.3 Security

Network security protects data and network resources. The notes list the
three familiar security goals, commonly called the **CIA triad**:

1.  **Confidentiality** --- only authorized people or systems should be
    able to access the information.
2.  **Integrity** --- information should remain accurate and should not
    be changed without authorization.
3.  **Availability** --- systems and information should be accessible
    when authorized users need them.

The notebook also distinguishes these two terms:

-   **Authentication:** Verifying **who you are** (identity).
-   **Authorization:** Determining **what you are allowed to access or
    do** (permissions).

------------------------------------------------------------------------

## 6. Types of Network Connections

### 6.1 Point-to-point

A dedicated connection links **two devices** directly.

``` text
Device A  ─────────  Device B
```

### 6.2 Multipoint (multidrop)

A single communication link is shared by **three or more devices**.

-   The devices share the same link or communication resource.
-   The link is not dedicated to only one pair of devices.

``` text
             Device B
                |
Device A ─── Shared link ─── Device C
                |
             Device D
```

------------------------------------------------------------------------

## 7. Network Topology

**Network topology** is the physical or logical layout of devices
(nodes) and the connections (links) between them.

The notebook covers these topologies:

1.  Point-to-point
2.  Bus
3.  Ring
4.  Star
5.  Tree
6.  Mesh

### 7.1 Point-to-point topology

Two devices are connected through a dedicated link.

``` text
[Device A] ───────── [Device B]
```

### 7.2 Bus topology

-   All devices connect to a common main cable called the **backbone**.
-   A device uses a **drop line** to connect to the backbone.
-   A connector called a **tap** can be used to attach a drop line to
    the backbone.
-   If the main backbone fails, communication across the network can
    stop.
-   It is relatively easy to install and reconfigure.

``` text
       |          |          |          |
     Device A  Device B   Device C   Device D
       |          |          |          |
=======+==========+==========+==========+=======
                 Backbone
```

**Advantages noted:** - Easy to install. - Easy to reconfigure.

**Disadvantage noted:** - If the backbone fails, the entire network can
be affected.

### 7.3 Ring topology

-   Each device is connected to two neighbouring devices, forming a
    closed loop.
-   Data travels around the ring from one device to the next until it
    reaches its destination.
-   In the one-direction ring described in the notebook, data travels in
    one direction.
-   Each device forwards the data to the next device; in this sense,
    each device acts as a repeater.
-   A single point of failure can affect the whole system in a basic
    ring design.
-   The notebook notes that a ring can be easy to install and configure.

``` text
       [A] ───── [B]
        |         |
       [D] ───── [C]
```

**Important:** The one-direction behaviour and single-failure issue
describe a basic unidirectional ring. Some ring networks use additional
links or protection mechanisms to improve fault tolerance.

### 7.4 Star topology

-   Every device connects to a central device, commonly a **hub** or
    **switch**.
-   Devices communicate through that central device.
-   The end devices do not normally have direct links to one another.
-   If the central hub or switch fails, communication between the
    connected devices is disrupted.

``` text
             [Device A]
                 |
[Device B] ── [Hub/Switch] ── [Device C]
                 |
             [Device D]
```

**Advantages noted:** - Easy to install. - Easy to configure. - Faults
are relatively easy to identify.

**Disadvantage noted:** - If the central hub fails, the whole star
network can stop working.

### 7.5 Tree topology

-   A hierarchical topology that combines multiple star networks.
-   Devices are arranged in parent-child branches.
-   It is useful when a network needs to be divided into levels or
    sections.

``` text
                 [Root]
                /      \
             [A]        [B]
            /  \       /  \
          [C]  [D]   [E]  [F]
```

### 7.6 Mesh topology

-   Devices are connected through multiple links.
-   In a **full mesh**, every device has a direct connection to every
    other device.
-   Multiple paths can allow data to travel even if one link fails.

#### Number of links in a full mesh

For `n` devices, the number of links is:

\[ L = `\frac{n(n-1)}{2}`{=tex} \]

Where: - `L` = number of links - `n` = number of devices

**Example 1: 4 devices**

\[ L = `\frac{4(4-1)}{2}`{=tex} = `\frac{4 \times 3}{2}`{=tex} = 6 \]

**Example 2: 5 devices**

\[ L = `\frac{5(5-1)}{2}`{=tex} = `\frac{5 \times 4}{2}`{=tex} = 10 \]

#### Advantages noted

1.  Traffic can use alternative paths when a link is unavailable.
2.  Robustness: failure of one link does not necessarily stop the entire
    network.
3.  Fault identification can be easier because links are separate.

#### Disadvantages noted

1.  Expensive because it requires many cables and connections.
2.  Installation and maintenance can be difficult.

------------------------------------------------------------------------

## 8. OSI Model

### Why is the OSI model needed?

Different computer systems and network technologies need a common way to
communicate. The **OSI model** provides a standard conceptual framework
for describing how network communication works in layers.

### Full form

**OSI --- Open Systems Interconnection**

It was developed by the **International Organization for Standardization
(ISO)**.

### Important points

-   The OSI model helps explain communication between different systems,
    regardless of their internal architecture.
-   It is a **conceptual reference model**, not a network protocol
    itself.
-   It divides network communication into seven layers.
-   Each layer has its own responsibilities and interacts with the
    layers above and below it.
-   Corresponding (peer) layers on two devices communicate according to
    agreed rules and protocols.

### The seven OSI layers

  ------------------------------------------------------------------------
                  Layer number Layer name            Basic role
  ---------------------------- --------------------- ---------------------
                             7 **Application**       Provides network
                                                     services to
                                                     user-facing
                                                     applications.

                             6 **Presentation**      Handles data
                                                     representation,
                                                     translation,
                                                     encryption, and
                                                     compression.

                             5 **Session**           Establishes, manages,
                                                     and ends
                                                     communication
                                                     sessions.

                             4 **Transport**         Provides end-to-end
                                                     delivery; may handle
                                                     segmentation,
                                                     reassembly, and
                                                     reliability.

                             3 **Network**           Handles logical
                                                     addressing and
                                                     routing between
                                                     networks.

                             2 **Data Link**         Handles framing,
                                                     link-level
                                                     addressing, and error
                                                     detection on a link.

                             1 **Physical**          Transmits raw bits
                                                     through the physical
                                                     medium.
  ------------------------------------------------------------------------

**Layer order --- top to bottom:**

``` text
+----------------------+
| 7. Application       |
+----------------------+
| 6. Presentation      |
+----------------------+
| 5. Session           |
+----------------------+
| 4. Transport         |
+----------------------+
| 3. Network           |
+----------------------+
| 2. Data Link         |
+----------------------+
| 1. Physical          |
+----------------------+
```

### Peer-to-peer communication

When two devices communicate, each layer on one device follows the rules
associated with the corresponding layer on the other device. The data
also moves down the layers on the sender's side, travels through the
network, and moves up the layers on the receiver's side.

``` text
Sender device                         Receiver device

Application  <---- peer rules ---->   Application
Presentation <---- peer rules ---->   Presentation
Session      <---- peer rules ---->   Session
Transport    <---- peer rules ---->   Transport
Network      <---- peer rules ---->   Network
Data Link    <---- peer rules ---->   Data Link
Physical     ===== transmission ====  Physical
```

The horizontal peer relationship is a logical way to understand the
model. Actual data travels down the sender's protocol stack, across the
medium, and up the receiver's stack.

### Services and functions mentioned in the notebook

The handwritten notes list these terms:

-   **Flow control:** Helps prevent a sender from overwhelming a
    receiver with data.
-   **Error control:** Detects, and in some systems helps recover from,
    transmission errors.
-   **Framing:** Divides a stream of bits into manageable units called
    frames (a Data Link layer function).
-   **Segmentation:** Divides data into smaller units for transport (a
    Transport layer function).

These functions belong to different layers; they are not all performed
by every OSI layer.

------------------------------------------------------------------------

## 9. Quick Revision

  -----------------------------------------------------------------------
  Topic                               Remember
  ----------------------------------- -----------------------------------
  Computer network                    Connected nodes that communicate
                                      and share resources

  Data communication components       Sender, receiver, message, medium,
                                      protocol

  Effective communication             Delivery, accuracy, timeliness,
                                      jitter

  Simplex                             One-way communication

  Half-duplex                         Two-way communication, one
                                      direction at a time

  Full-duplex                         Two-way communication
                                      simultaneously

  Network criteria                    Reliability, performance, security

  Security goals                      Confidentiality, integrity,
                                      availability

  Authentication                      Who you are

  Authorization                       What you are allowed to do

  Connection types                    Point-to-point, multipoint

  Topology                            Layout of nodes and links

  Full mesh links                     `n(n-1)/2`

  OSI full form                       Open Systems Interconnection

  OSI layers                          Application, Presentation, Session,
                                      Transport, Network, Data Link,
                                      Physical
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 10. Self-Test Questions

1.  What is a computer network?
2.  List the five components of data communication.
3.  Explain delivery, accuracy, timeliness, and jitter.
4.  Differentiate simplex, half-duplex, and full-duplex transmission.
5.  What are the three network criteria?
6.  Differentiate authentication and authorization.
7.  What is the difference between point-to-point and multipoint
    connections?
8.  Define network topology and list its types.
9.  Explain bus, ring, and star topologies with diagrams.
10. What are the advantages and disadvantages of mesh topology?
11. Calculate the number of links in a full mesh with 6 devices.
12. What is the OSI model, and why is it used?
13. List the seven OSI layers in order.
14. What are flow control, error control, framing, and segmentation?

------------------------------------------------------------------------

*End of Day 1 notes.*
