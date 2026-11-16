# Day 2 — Binary Number System and IPv4 Representation

> Study notes based on the earlier Day 2 notebook material. The examples below are worked out explicitly so the conversion method is easy to follow.

## 1. Why binary is used

Computers represent data using two states:

- `0` — LOW / OFF
- `1` — HIGH / ON

A binary digit is called a **bit**.

## 2. Place values in binary

Each position has a power-of-two weight. Read an 8-bit number from left to right:

| Bit position | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Weight | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| Power | 2⁷ | 2⁶ | 2⁵ | 2⁴ | 2³ | 2² | 2¹ | 2⁰ |

The value of a binary number is the sum of the weights whose bits are `1`.

### Example: binary to decimal

Convert `10110110₂` to decimal:

```text
Bits:      1 0 1 1 0 1 1 0
Weights: 128 64 32 16  8  4  2  1

= 128 + 32 + 16 + 4 + 2
= 182
```

Therefore:

`10110110₂ = 182₁₀`

### Another example

```text
11001010₂
= 128 + 64 + 8 + 2
= 202₁₀
```

## 3. Decimal to binary

Repeatedly divide the decimal number by `2`, record each remainder, and read the remainders from bottom to top.

### Example: convert 13 to binary

| Division | Quotient | Remainder |
|---|---:|---:|
| 13 ÷ 2 | 6 | 1 |
| 6 ÷ 2 | 3 | 0 |
| 3 ÷ 2 | 1 | 1 |
| 1 ÷ 2 | 0 | 1 |

Read the remainders upward:

`13₁₀ = 1101₂`

As an 8-bit value:

`00001101₂`

## 4. Powers of 2

| Power | Value |
|---|---:|
| 2⁰ | 1 |
| 2¹ | 2 |
| 2² | 4 |
| 2³ | 8 |
| 2⁴ | 16 |
| 2⁵ | 32 |
| 2⁶ | 64 |
| 2⁷ | 128 |
| 2⁸ | 256 |

For `n` bits:

- Number of possible bit patterns = `2ⁿ`
- If interpreted as an unsigned number, the range is `0` through `2ⁿ − 1`

Examples:

- 1 bit → `2¹ = 2` patterns: `0, 1`
- 4 bits → `2⁴ = 16` patterns: `0000` through `1111`
- 8 bits → `2⁸ = 256` patterns: `00000000` through `11111111`

**Important:** 8 bits provide 256 different values, but the largest unsigned value is 255, not 256.

## 5. One IPv4 octet

An IPv4 address contains 32 bits, divided into four groups of 8 bits. Each 8-bit group is called an **octet**.

```text
32 bits
┌────────┬────────┬────────┬────────┐
│ 8 bits │ 8 bits │ 8 bits │ 8 bits │
└────────┴────────┴────────┴────────┘
 Octet 1  Octet 2  Octet 3  Octet 4
```

An octet has:

- `2⁸ = 256` possible bit patterns
- Unsigned decimal range: `0–255`

Examples:

| Binary octet | Decimal |
|---|---:|
| `00000000` | 0 |
| `00000001` | 1 |
| `01111111` | 127 |
| `10000000` | 128 |
| `11111110` | 254 |
| `11111111` | 255 |

## 6. Converting an IPv4 address

Example: `192.168.1.10`

Convert each octet separately:

| Decimal | 8-bit binary |
|---:|---|
| 192 | `11000000` |
| 168 | `10101000` |
| 1 | `00000001` |
| 10 | `00001010` |

Therefore:

```text
192.168.1.10
=
11000000.10101000.00000001.00001010
```

Each dot separates one 8-bit octet.

## 7. Quick rules

- `n` bits → `2ⁿ` possible patterns.
- Unsigned maximum → `2ⁿ − 1`.
- One IPv4 octet → 8 bits.
- Four IPv4 octets → 32 bits.
- Valid decimal value of an octet → `0–255`.

## 8. Practice

Try these before checking the answers.

1. Convert `10010101₂` to decimal.
2. Convert `45₁₀` to 8-bit binary.
3. How many patterns can 5 bits represent?
4. What is the maximum unsigned value of 6 bits?
5. Convert `10.0.0.1` into binary octets.

### Answers

1. `149`
2. `00101101`
3. `2⁵ = 32`
4. `2⁶ − 1 = 63`
5. `00001010.00000000.00000000.00000001`

---

**Next topic:** IPv4 addressing — Network ID, Host ID, address classes, and special addresses.
