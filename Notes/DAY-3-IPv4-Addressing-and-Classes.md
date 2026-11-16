# Day 3 — IPv4 Addressing, Network ID, Host ID, and Address Classes

> These notes organise the uploaded Day 3 notebook pages. Class A–E is explained as the historical classful IPv4 model. Modern networks generally use CIDR, which is covered near the end.

## 1. IPv4 address structure

An IPv4 address contains **32 bits**.

It is written as four 8-bit octets in dotted-decimal notation:

```text
192 . 168 . 1 . 10
 8     8    8    8   = 32 bits
```

Each octet ranges from `0` to `255`.

Example:

```text
192.168.1.10
11000000.10101000.00000001.00001010
```

## 2. Network ID and Host ID

An IP address can be understood as having:

- **Network ID** — identifies the network.
- **Host ID** — identifies an interface/host within that network.

The subnet mask or prefix length determines which bits belong to the network and which belong to the host. In the old classful model, the default division was determined by the address class.

```text
IPv4 address
┌─────────────────────┬─────────────────────┐
│      Network ID     │       Host ID       │
└─────────────────────┴─────────────────────┘
```

## 3. Historical IPv4 address classes

The first bits identify the historical class.

| Class | Leading bits | First-octet range | Default mask | Network bits* | Host bits |
|---|---|---:|---|---:|---:|
| A | `0` | 0–127** | `255.0.0.0` (`/8`) | 7 | 24 |
| B | `10` | 128–191 | `255.255.0.0` (`/16`) | 14 | 16 |
| C | `110` | 192–223 | `255.255.255.0` (`/24`) | 21 | 8 |
| D | `1110` | 224–239 | Not divided into network/host IDs | — | — |
| E | `1111` | 240–255 | Reserved/experimental historical class | — | — |

\* For A, B, and C, “network bits” here means the variable network-number bits after the fixed class-identifying bits.

\** Class A's numerical first-octet pattern is 0–127, but `0.0.0.0/8` is special-purpose and `127.0.0.0/8` is loopback. The conventional usable Class A unicast first-octet range is therefore `1–126`.

### Class A

- Leading bit: `0`
- Default prefix: `/8`
- Network-number bits: `7`
- Host bits: `24`
- Historical network count: `2⁷ = 128` bit patterns; 0 and 127 are special, leaving 126 conventional Class A network numbers.
- Traditional usable hosts per network: `2²⁴ − 2 = 16,777,214`

### Class B

- Leading bits: `10`
- First-octet range: `128–191`
- Default prefix: `/16`
- Network-number bits: `14`
- Host bits: `16`
- Network count: `2¹⁴ = 16,384`
- Traditional usable hosts per network: `2¹⁶ − 2 = 65,534`

### Class C

- Leading bits: `110`
- First-octet range: `192–223`
- Default prefix: `/24`
- Network-number bits: `21`
- Host bits: `8`
- Network count: `2²¹ = 2,097,152`
- Traditional usable hosts per network: `2⁸ − 2 = 254`

### Class D

- Leading bits: `1110`
- First-octet range: `224–239`
- Used for IPv4 multicast.
- It is not divided into the normal Network ID and Host ID fields used by Classes A–C.

### Class E

- Leading bits: `1111`
- First-octet range: `240–255`
- Historically reserved for experimental/future use; not ordinary unicast host addressing.

## 4. Why are 2 addresses subtracted?

For a conventional IPv4 subnet with at least two host bits:

- All host bits `0` identify the **network address**.
- All host bits `1` identify the **directed broadcast address**.
- These two addresses are not assigned to ordinary hosts.

Therefore, the traditional usable-host formula is:

`Usable hosts = 2ʰ − 2`

where `h` is the number of host bits.

### Example: Class C default network

A Class C default network has 8 host bits:

```text
2⁸ = 256 total addresses
256 − 2 = 254 traditional usable host addresses
```

For `192.168.1.0/24`:

| Purpose | Address |
|---|---|
| Network address | `192.168.1.0` |
| First traditional host | `192.168.1.1` |
| Last traditional host | `192.168.1.254` |
| Broadcast address | `192.168.1.255` |

This example assumes the default `/24` subnet.

## 5. Class B calculation example

Class B uses 14 variable network bits and 16 host bits:

```text
Network numbers = 2¹⁴ = 16,384
Host addresses  = 2¹⁶ = 65,536
Traditional usable hosts = 65,536 − 2 = 65,534
```

The relationship in the notebook can be written:

```text
2ᵐ = 2¹⁴       → m = 14
2ⁿ − 2 = 2¹⁶ − 2 → n = 16

m / n = 14 / 16 = 7 / 8

Cross-multiplication:
8m = 7n
```

So `8m = 7n` is correct for `m/n = 7/8`. It is not `7m = 8n`.

## 6. Worked class-identification examples

### Example A: `150.20.10.5`

- First octet = `150`
- `150` is in `128–191`
- Historical class = **Class B**
- Default classful mask = `255.255.0.0` (`/16`)
- Default classful Network ID = `150.20.0.0`
- Host portion = `10.5`

### Example B: `200.202.63.247`

- First octet = `200`
- `200` is in `192–223`
- Historical class = **Class C**
- Default classful mask = `255.255.255.0` (`/24`)
- Default classful Network ID = `200.202.63.0`
- Host portion = `247`

### Example C: `110.5.8.8`

- First octet = `110`
- `110` is in `1–126`
- Historical class = **Class A**, not Class C
- Default classful mask = `255.0.0.0` (`/8`)
- Default classful Network ID = `110.0.0.0`
- Host portion = `5.8.8`

**Note:** These Network ID results use historical default classful masks. In a real network, use the actual subnet mask/prefix length.

## 7. Special IPv4 addresses from the notebook

### `0.0.0.0`

This is not an ordinary host address. Its meaning depends on context; for example, it can represent an unspecified source address or be used in the default route `0.0.0.0/0`.

### `127.0.0.0/8` — loopback

- Loopback traffic returns to the same computer.
- `127.0.0.1` is the common loopback address.
- It is used to test the local TCP/IP stack.
- It does **not** test whether a remote computer, switch, router, or internet connection is working.

Example:

```bash
ping 127.0.0.1
```

### All-zero and all-one host fields

For a conventional subnet:

- Host field all `0` → network address.
- Host field all `1` → directed broadcast address.

The special limited-broadcast address is:

`255.255.255.255`

It is intended for the local link and is not forwarded by routers.

## 8. Private IPv4 address ranges

Private addresses are used inside private networks and are not globally routed on the public Internet.

| Private block | CIDR prefix |
|---|---|
| `10.0.0.0 – 10.255.255.255` | `10.0.0.0/8` |
| `172.16.0.0 – 172.31.255.255` | `172.16.0.0/12` |
| `192.168.0.0 – 192.168.255.255` | `192.168.0.0/16` |

Example: `10.31.82.57` belongs to the private `10.0.0.0/8` block.

A private address can be used by many separate networks. A router/NAT gateway is commonly used when devices on a private network need to access the public Internet.

## 9. DHCP and loopback are different

- **DHCP** — a protocol used to automatically provide IP configuration to clients, such as an IP address, subnet mask, default gateway, and DNS server.
- **Loopback** — sends traffic back to the same device to test its local networking stack.

A loopback test does not prove that DHCP, the router, or another host is working.

## 10. Classful addressing versus CIDR

Class A/B/C addressing is important for understanding the history and basic address calculations. Modern IPv4 allocation and routing use **CIDR (Classless Inter-Domain Routing)**.

CIDR writes a prefix length after the address:

- `/8` means 8 network-prefix bits.
- `/16` means 16 network-prefix bits.
- `/24` means 24 network-prefix bits.

In CIDR, the network/host boundary is determined by the prefix length, not by the first-octet class. For example, `192.168.1.0/26` is not a default Class C `/24` network; it is a smaller subnet with 6 host bits.

## 11. Quick revision table

| Topic | Formula / fact |
|---|---|
| IPv4 size | 32 bits |
| Octets | 4 × 8 bits |
| Octet range | 0–255 |
| Class A default | `/8` |
| Class B default | `/16` |
| Class C default | `/24` |
| Class B network count | `2¹⁴` |
| Class B traditional usable hosts | `2¹⁶ − 2` |
| Class C network count | `2²¹` |
| Class C traditional usable hosts | `2⁸ − 2` |
| Loopback block | `127.0.0.0/8` |
| Private IPv4 blocks | `10/8`, `172.16/12`, `192.168/16` |

## 12. Practice questions

1. Identify the historical class of `172.20.5.10`.
2. What is the default classful mask of a Class C address?
3. How many traditional usable hosts are in a default Class B network?
4. What is the network address of `200.202.63.247` using the default Class C mask?
5. Does `ping 127.0.0.1` test your router?
6. Is `172.32.1.1` inside the RFC 1918 private range?
7. What does `/24` mean in CIDR?

### Answers

1. Class B.
2. `255.255.255.0` (`/24`).
3. `65,534`.
4. `200.202.63.0`.
5. No. It tests the local loopback/TCP-IP stack.
6. No. The private 172 range ends at `172.31.255.255`.
7. The first 24 bits are the network prefix; the remaining 8 bits are host bits.

---

**Next topic:** Subnetting and calculating network address, broadcast address, usable host range, and subnet masks.
