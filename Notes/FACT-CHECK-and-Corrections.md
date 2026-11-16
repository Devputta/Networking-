# Networking Notes — Fact Check and Corrections

This file separates the original notebook ideas from the technically precise version. It covers the Day 2 binary/IPv4 basics and the Day 3 IPv4 addressing/classful-addressing pages.

## Status key

- **Correct** — the notebook idea is technically sound.
- **Clarify** — broadly right, but needs a more exact explanation.
- **Corrected** — the notebook statement or calculation needs changing.
- **Historical only** — useful for learning, but not how modern Internet routing is generally organised.

## Day 2 — Binary and IPv4 representation

| Notebook idea | Status | Fact-checked version |
|---|---|---|
| 1 bit can be `0` or `1` | Correct | A bit has two possible values. |
| `n` bits create `2ⁿ` combinations | Correct | There are `2ⁿ` possible bit patterns. |
| An unsigned `n`-bit number ranges from `0` to `2ⁿ − 1` | Correct | The maximum is `2ⁿ − 1`, not `2ⁿ`. |
| 8 bits have 256 values | Correct | `2⁸ = 256` patterns, with unsigned decimal values `0–255`. |
| One IPv4 octet is 8 bits | Correct | IPv4 has four 8-bit octets, totalling 32 bits. |
| An octet can be 0–256 | Corrected if written this way | The maximum is **255**. 256 is the number of possible values, not a valid octet value. |
| Convert binary to decimal by adding weights for each `1` | Correct | Use weights 128, 64, 32, 16, 8, 4, 2, 1 for an 8-bit octet. |
| Convert decimal to binary by repeated division by 2 | Correct | Read the remainders from bottom to top; pad to 8 bits when representing an IPv4 octet. |

### Verified sample calculations

```text
10110110₂ = 128 + 32 + 16 + 4 + 2 = 182
11001010₂ = 128 + 64 + 8 + 2 = 202
13₁₀ = 1101₂ = 00001101₂ (8-bit form)
```

## Day 3 — IPv4 address structure and classes

| Notebook idea | Status | Fact-checked version |
|---|---|---|
| IPv4 address is 32 bits | Correct | Four octets × 8 bits = 32 bits. |
| IP address has Network ID and Host ID | Clarify | This is a useful classful teaching model. In modern IPv4, the subnet mask/prefix length defines the network and host portions. |
| Class A starts with `0` | Correct | The leading bit is `0`; historical first-octet pattern is 0–127. |
| Class A usable range is 0–126 | Corrected | Conventional Class A unicast first-octet range is **1–126**. `0/8` and `127/8` are special-purpose. |
| Class B starts with `10` | Correct | First-octet range `128–191`; default mask `/16`. |
| Class C starts with `110` | Correct | First-octet range `192–223`; default mask `/24`. |
| Class D is `224–239` | Correct | Class D is used for multicast, not ordinary host/network ID division. |
| Class E is `240–255` | Clarify | Historically reserved/experimental; do not treat it as ordinary host unicast space. |
| Class B has 14 network bits and 16 host bits | Correct | The first two class-identifying bits are fixed (`10`), leaving 14 variable network bits and 16 host bits. |
| Class C has 21 network bits and 8 host bits | Correct | The first three bits are fixed (`110`), leaving 21 variable network bits and 8 host bits. |
| Class B has `2¹⁴` network numbers | Correct in the historical classful model | `2¹⁴ = 16,384` theoretical Class B network numbers. |
| Class C has `2²¹` network numbers | Correct in the historical classful model | `2²¹ = 2,097,152` theoretical Class C network numbers. |
| Usable hosts = `2ʰ − 2` | Clarify | Traditional rule for ordinary IPv4 subnets with `h` host bits. The all-zero host field is the subnet/network address and all-one is the directed broadcast address. There are special cases, including `/31` point-to-point links and `/32` host routes. |
| Class A network count = `2⁷ = 128` | Clarify | There are 128 possible 7-bit network-number patterns, but `0/8` and `127/8` are special, leaving 126 conventional Class A network numbers. |
| `110.5.8.8` is Class C | Corrected | First octet `110` is in `1–126`, so it is historically **Class A**. Under the default Class A mask `/8`, the classful network is `110.0.0.0`. |
| `200.202.63.247` is Class C | Correct | First octet `200` is in `192–223`; default classful network is `200.202.63.0/24`. |
| `150.20.10.5` is Class B | Correct | First octet `150` is in `128–191`; default classful network is `150.20.0.0/16`. |
| `127.x.x.x` is used for loopback | Correct | `127.0.0.0/8` is the loopback block; `127.0.0.1` is the common test address. |
| Loopback checks whether another host/router receives packets | Corrected | Loopback tests the local machine's IP stack. It does not test a remote host, router forwarding, or the physical/network link. |
| `0.0.0.0` is just an unusable host address | Clarify | It is a special-purpose address with context-dependent meaning. `0.0.0.0/32` is the unspecified address; `0.0.0.0/0` is the default route. |
| `255.255.255.255` is broadcast | Correct | It is the limited broadcast address for the local link and is not forwarded by routers. |
| Private addresses include `10.x.x.x` | Clarify | RFC 1918 defines **three** private ranges, not only 10/8. See below. |
| Classful addressing is the modern Internet allocation method | Historical only | CIDR replaced the old Class A/B/C allocation model for modern Internet routing and address allocation. |

## Correct private IPv4 ranges

All three RFC 1918 ranges must be remembered:

| Range | Prefix | Notes |
|---|---|---|
| `10.0.0.0 – 10.255.255.255` | `10.0.0.0/8` | Entire 10/8 block |
| `172.16.0.0 – 172.31.255.255` | `172.16.0.0/12` | Only 172.16 through 172.31 are private |
| `192.168.0.0 – 192.168.255.255` | `192.168.0.0/16` | Entire 192.168/16 block |

**Common mistake:** `172.32.1.1` is not inside the RFC 1918 private range. The 172 private range stops at `172.31.255.255`.

## Important correction: classful calculations

### Class A

- Leading bit: `0`
- Variable network bits: 7
- Host bits: 24
- Historical patterns: `2⁷ = 128`
- Conventional network numbers: 126 after excluding the special 0/8 and 127/8 blocks
- Traditional usable hosts per network: `2²⁴ − 2 = 16,777,214`

### Class B

- Leading bits: `10`
- Variable network bits: 14
- Host bits: 16
- Network numbers: `2¹⁴ = 16,384`
- Traditional usable hosts per network: `2¹⁶ − 2 = 65,534`

### Class C

- Leading bits: `110`
- Variable network bits: 21
- Host bits: 8
- Network numbers: `2²¹ = 2,097,152`
- Traditional usable hosts per network: `2⁸ − 2 = 254`

## Clarification: the `8m = 7n` relationship

If:

```text
m / n = 14 / 16 = 7 / 8
```

Cross-multiply:

```text
8m = 7n
```

Therefore, **`8m = 7n` is correct**. `7m = 8n` would correspond to a different ratio.

## What to keep separate while studying

1. **Classful defaults**: A `/8`, B `/16`, C `/24`. These explain the historical class system.
2. **Actual subnet**: The configured mask/prefix length determines the network/host boundary in a real network.
3. **Network address**: Host bits all zero (under the traditional subnet rule).
4. **Directed broadcast**: Host bits all one (under the traditional subnet rule).
5. **Loopback**: Traffic stays within the same device.
6. **Private address**: An address from one of the RFC 1918 blocks; private does not mean encrypted or automatically secure.
7. **CIDR**: Modern classless prefix-based addressing and routing.

## Sources used for this fact check

- RFC 4632 — CIDR and the move away from classful A/B/C allocation: https://www.rfc-editor.org/rfc/rfc4632
- RFC 1918 — private IPv4 address ranges: https://www.rfc-editor.org/rfc/rfc1918
- IANA — IPv4 Special-Purpose Address Registry: https://www.iana.org/assignments/iana-ipv4-special-registry
- Cisco — IPv4 address classes, default masks, and traditional host calculations: https://www.cisco.com/c/en/us/td/docs/routers/ios-xe/ip-addressing/ip-addressing/m_config-ipv4-addr-0.html
- RFC 1365 — historical description of class A/B/C/D/E fields: https://www.rfc-editor.org/rfc/rfc1365

---

**Study recommendation:** Learn the classful table for exams, but always solve practical subnetting questions from the given subnet mask or CIDR prefix, not from the first octet alone.
