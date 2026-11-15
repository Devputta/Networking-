# Computer Networking --- Day 3

## IPv4 Addressing, Network ID, Host ID and Address Classes

> **Source:** Transcription of the uploaded handwritten pages about IPv4
> addressing and classful addressing.
>
> These notes retain the notebook's class-based IPv4 approach. Classful
> addressing is a historical system; modern networks generally use CIDR
> and subnet masks.

------------------------------------------------------------------------

## 1. What is an IP Address?

**IP** means **Internet Protocol**.

An IP address is a logical address used to identify a device/interface
on an IP network.

### IPv4 address

-   IPv4 address size: **32 bits**
-   Number of octets: **4**
-   Bits in each octet: **8**
-   Common display format: **dotted decimal**

``` text
192 . 168 . 1 . 10
 8      8    8    8   = 32 bits
```

Each decimal octet has a value from `0` to `255`.

### Total IPv4 address combinations

\[ 2\^{32}=4,294,967,296 \]

This is approximately 4.29 billion possible 32-bit patterns.

------------------------------------------------------------------------

## 2. Network ID and Host ID

In the classful addressing method, an IPv4 address is divided into:

1.  **Network ID (NID):** Identifies the network.
2.  **Host ID (HID):** Identifies a host within that network.

``` text
IPv4 address
+----------------------+----------------------+
|      Network ID      |        Host ID       |
+----------------------+----------------------+
```

The number of bits used for the Network ID and Host ID depends on the
address class.

### Example: Class A

``` text
+----------+-----------------------------------+
|  8 bits  |              24 bits              |
+----------+-----------------------------------+
| Network  |               Host                |
+----------+-----------------------------------+
```

### Example: Class B

``` text
+------------------+------------------+
|      16 bits     |     16 bits      |
+------------------+------------------+
|     Network     |       Host       |
+------------------+------------------+
```

### Example: Class C

``` text
+--------------------------+----------+
|          24 bits         |  8 bits  |
+--------------------------+----------+
|         Network          |   Host   |
+--------------------------+----------+
```

------------------------------------------------------------------------

## 3. Classful IPv4 Addressing

The notebook describes the original classful IPv4 system, introduced in
the early development of the Internet.

The first bits of the address identify the class.

  ----------------------------------------------------------------------------------
  Class         Leading bit       First-octet              Network ID        Host ID
                  pattern               range                         
  ---------- ----------------- -------------- ----------------------- --------------
  A                 `0`              1--126\*                  8 bits        24 bits

  B                `10`              128--191                 16 bits        16 bits

  C                `110`             192--223                 24 bits         8 bits

  D               `1110`             224--239               Multicast Not split into
                                                                        network/host
                                                                                 IDs

  E               `1111`             240--255   Experimental/reserved Not split into
                                                                        network/host
                                                                                 IDs
  ----------------------------------------------------------------------------------

\*The first-octet value `0` is reserved, and `127` is reserved for
loopback. Therefore, ordinary Class A network numbers use first-octet
values 1 through 126.

### Remember the leading bits

``` text
Class A: 0xxxxxxx
Class B: 10xxxxxx
Class C: 110xxxxx
Class D: 1110xxxx
Class E: 1111xxxx
```

The `x` positions are the remaining bits.

### Class A

-   First bit: `0`
-   Network ID: 8 bits
-   Host ID: 24 bits
-   Intended historically for very large networks.

``` text
0 | 7 remaining network bits | 24 host bits
```

### Class B

-   First two bits: `10`
-   Network ID: 16 bits
-   Host ID: 16 bits
-   Intended historically for medium-sized networks.

``` text
10 | 14 remaining network bits | 16 host bits
```

### Class C

-   First three bits: `110`
-   Network ID: 24 bits
-   Host ID: 8 bits
-   Intended historically for smaller networks.

``` text
110 | 21 remaining network bits | 8 host bits
```

### Class D

-   Leading bits: `1110`
-   Used for multicast addressing.
-   It does not use the normal Network ID / Host ID split.

### Class E

-   Leading bits: `1111`
-   Reserved for experimental purposes in the classful system.
-   It does not use the normal Network ID / Host ID split.

------------------------------------------------------------------------

## 4. Number of Networks and Hosts

For Class A, B, and C, the classful structure gives different numbers of
network bits and host bits.

### Formulas

If there are `n` variable network bits:

\[ `\text{Possible network numbers}`{=tex}=2\^n \]

If there are `h` host bits:

\[ `\text{Host address patterns per network}`{=tex}=2\^h \]

In ordinary traditional IPv4 subnets, two host patterns are reserved:

-   All host bits `0`: network address.
-   All host bits `1`: directed broadcast address.

Therefore:

\[ `\text{Usable host addresses per subnet}`{=tex}=2\^h-2 \]

### Class A calculation

-   1 leading class bit is fixed to `0`.
-   7 bits remain for the network number.
-   24 bits are used for the host portion.

\[ `\text{Network numbers}`{=tex}=2\^7 \]

There are 128 possible 7-bit patterns, but the all-zero and all-one
network numbers are reserved in the traditional classful scheme. This
leaves **126 usable Class A network numbers**.

\[ `\text{Usable hosts per network}`{=tex}=2\^{24}-2 \]

\[ =16,777,216-2=16,777,214 \]

### Class B calculation

-   2 leading bits are fixed to `10`.
-   14 bits remain for the network number.
-   16 bits are used for the host portion.

\[ `\text{Network numbers}`{=tex}=2\^{14}=16,384 \]

\[ `\text{Usable hosts per network}`{=tex}=2\^{16}-2 \]

\[ =65,536-2=65,534 \]

### Class C calculation

-   3 leading bits are fixed to `110`.
-   21 bits remain for the network number.
-   8 bits are used for the host portion.

\[ `\text{Network numbers}`{=tex}=2\^{21}=2,097,152 \]

\[ `\text{Usable hosts per network}`{=tex}=2\^8-2 \]

\[ =256-2=254 \]

### Classful addressing comparison

  ---------------------------------------------------------------------------------
  Class                  Network bits      Host bits Usable networks   Usable hosts
                                                       (traditional)    per network
  ----------- ----------------------- -------------- --------------- --------------
  A              8 total (7 variable)             24             126     16,777,214

  B            16 total (14 variable)             16          16,384         65,534

  C            24 total (21 variable)              8       2,097,152            254

  D                         Multicast            ---             ---            ---

  E             Experimental/reserved            ---             ---            ---
  ---------------------------------------------------------------------------------

------------------------------------------------------------------------

## 5. Example: Identify the Class of an IP Address

Use the **first octet** to identify the class in classful addressing.

### Example 1

``` text
25.10.20.30
```

-   First octet: `25`
-   25 is in the range 1--126.
-   Therefore: **Class A**

Class A default division:

``` text
25        . 10 . 20 . 30
Network ID     |       Host ID
   8 bits      |      24 bits
```

### Example 2

``` text
150.20.10.5
```

-   First octet: `150`
-   150 is in the range 128--191.
-   Therefore: **Class B**

Default division: 16-bit Network ID and 16-bit Host ID.

### Example 3

``` text
200.202.63.247
```

-   First octet: `200`
-   200 is in the range 192--223.
-   Therefore: **Class C**

Default classful division:

``` text
200.202.63 | 247
  Network  | Host
  24 bits  | 8 bits
```

For this Class C example:

-   Network address: `200.202.63.0`
-   First host address: `200.202.63.1`
-   Last host address: `200.202.63.254`
-   Broadcast address: `200.202.63.255`

These network/host results assume the traditional Class C default `/24`
boundary.

------------------------------------------------------------------------

## 6. Network Address and Broadcast Address

Within a traditional IPv4 subnet:

### Network address

All host bits are set to `0`.

Example for `192.168.1.0/24`:

``` text
Network address: 192.168.1.0
Host portion:    00000000
```

The network address identifies the subnet and is not assigned to an
ordinary host.

### Broadcast address

All host bits are set to `1`.

Example for `192.168.1.0/24`:

``` text
Broadcast address: 192.168.1.255
Host portion:      11111111
```

This address is used to send a packet to all hosts on that IPv4 subnet.

### Usable host range

For the same `/24` subnet:

``` text
Network address:   192.168.1.0
First usable host: 192.168.1.1
Last usable host:  192.168.1.254
Broadcast address:192.168.1.255
```

So there are:

\[ 2\^8-2=254 \]

usable host addresses.

------------------------------------------------------------------------

## 7. Special IPv4 Addresses Mentioned in the Notes

### 127.0.0.1 --- Loopback

-   `127.0.0.0/8` is reserved for loopback.
-   `127.0.0.1` is the commonly used loopback address.
-   Used to test IP networking on the local device.

### 0.0.0.0 --- Unspecified address

-   Represents an unspecified IPv4 address in relevant contexts.
-   It is not an ordinary host address to assign to a device.
-   `0.0.0.0/0` is also used to represent the default route in routing
    tables.

### All host bits set to zero or one

For a normal IPv4 subnet:

-   Host bits all `0` → network address.
-   Host bits all `1` → directed broadcast address.

These two addresses are not assigned to ordinary hosts on a conventional
subnet.

------------------------------------------------------------------------

## 8. Historical Note: Classful Addressing and Modern Networks

The notebook refers to the early classful addressing system and the role
of IANA.

-   IANA coordinates global IP address resources, working with Regional
    Internet Registries (RIRs).
-   Classful addressing used fixed Class A, B, and C network/host
    boundaries.
-   This fixed division could waste addresses when an organization
    needed a network size between the class sizes.
-   Modern IPv4 networks use **CIDR (Classless Inter-Domain Routing)**
    and prefix lengths such as `/8`, `/16`, `/24`, or other values.
-   CIDR allows more flexible network sizes than the old classful
    system.

**Important:** Class A/B/C ranges are still useful for learning the
history and recognizing address classes, but modern network
configuration should be understood using subnet masks and CIDR prefixes.

------------------------------------------------------------------------

## 9. Quick Revision

  Topic               Remember
  ------------------- ----------------------------------
  IPv4 size           32 bits
  IPv4 format         4 octets
  One octet           8 bits
  Each octet range    0--255
  Network ID          Identifies the network
  Host ID             Identifies a host in the network
  Class A             8-bit network / 24-bit host
  Class B             16-bit network / 16-bit host
  Class C             24-bit network / 8-bit host
  Class D             Multicast
  Class E             Experimental/reserved
  Network address     Host bits all 0
  Broadcast address   Host bits all 1
  Loopback example    127.0.0.1
  Modern addressing   CIDR

------------------------------------------------------------------------

## 10. Practice Questions

1.  What is the size of an IPv4 address?
2.  What is an octet?
3.  What is the difference between Network ID and Host ID?
4.  Write the leading bit patterns for Classes A, B, C, D, and E.
5.  Identify the class of `25.10.20.30`.
6.  Identify the class of `150.20.10.5`.
7.  Identify the class of `200.202.63.247`.
8.  How many host bits are present in a Class A address?
9.  How many host bits are present in a Class B address?
10. How many host bits are present in a Class C address?
11. Calculate the traditional usable host count for a Class C `/24`
    network.
12. Why are the all-zero and all-one host portions reserved in a
    conventional subnet?
13. What is the purpose of `127.0.0.1`?
14. What does `0.0.0.0/0` represent in a routing table?
15. What is the difference between classful addressing and CIDR?

------------------------------------------------------------------------

*End of Day 3 notes.*
