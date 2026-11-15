# Computer Networking --- Day 2

## Binary Number System and IPv4 Address Representation

> **Source:** Transcription of the Day 2 handwritten notebook pages.
>
> The notes introduce binary numbers as the foundation for IP
> addressing, explain how bits represent decimal values, and show how an
> IPv4 address is written.

------------------------------------------------------------------------

## 1. Network Layer and IP Addressing

The notebook begins with the **Network Layer** and **IPv4 addressing**.

-   An **IP address** is a logical address used to identify a
    device/interface on an IP network.
-   IPv4 addresses contain **32 bits**.
-   The 32 bits are divided into **4 octets**.
-   Each octet contains **8 bits**.

``` text
IPv4 address = 32 bits

  8 bits       8 bits       8 bits       8 bits
+----------+----------+----------+----------+
| Octet 1  | Octet 2  | Octet 3  | Octet 4  |
+----------+----------+----------+----------+
```

An IPv4 address is commonly displayed in **dotted-decimal notation**:

``` text
200.202.63.247
```

Each decimal number represents one 8-bit octet.

------------------------------------------------------------------------

## 2. Binary Number System

The binary number system uses only two digits:

-   `0`
-   `1`

Each binary digit is called a **bit**.

Binary is a **base-2** number system. Each position represents a power
of 2.

### Binary place values

For an 8-bit number, read the place values from left to right:

  Bit position        7    6    5    4    3    2    1    0
  --------------- ----- ---- ---- ---- ---- ---- ---- ----
  Power of 2         2⁷   2⁶   2⁵   2⁴   2³   2²   2¹   2⁰
  Decimal value     128   64   32   16    8    4    2    1

``` text
128   64   32   16    8    4    2    1
  0    0    0    0    0    0    0    0
```

A bit set to `1` contributes its place value. A bit set to `0`
contributes nothing.

### Example: Convert binary `0111` to decimal

``` text
Binary:       0   1   1   1
Place value:  8   4   2   1

Calculation:  0 + 4 + 2 + 1 = 7
```

Therefore:

\[ (0111)*2 = (7)*{10} \]

### Example: Convert binary `1011` to decimal

\[ 1(2^3)+0(2^2)+1(2^1)+1(2^0) \]

\[ =8+0+2+1=11 \]

Therefore:

\[ (1011)*2=(11)*{10} \]

------------------------------------------------------------------------

## 3. Binary Values from 0 to 15

The notebook lists the 4-bit binary values:

    Decimal  4-bit binary
  --------- --------------
          0     `0000`
          1     `0001`
          2     `0010`
          3     `0011`
          4     `0100`
          5     `0101`
          6     `0110`
          7     `0111`
          8     `1000`
          9     `1001`
         10     `1010`
         11     `1011`
         12     `1100`
         13     `1101`
         14     `1110`
         15     `1111`

With `n` bits, the number of possible bit patterns is:

\[ 2\^n \]

For 4 bits:

\[ 2\^4=16 `\text{ patterns}`{=tex} \]

The values range from:

\[ 0 `\text{ to }`{=tex} 2\^n-1 \]

For 4 bits:

\[ 0 `\text{ to }`{=tex} 2\^4-1 = 15 \]

------------------------------------------------------------------------

## 4. Powers of 2

These powers are useful when converting binary values and calculating
address ranges.

  Power             Value
  ------- ---------------
  2⁰                    1
  2¹                    2
  2²                    4
  2³                    8
  2⁴                   16
  2⁵                   32
  2⁶                   64
  2⁷                  128
  2⁸                  256
  2¹⁶              65,536
  2²⁴          16,777,216
  2³²       4,294,967,296

**Important formulas**

-   Number of patterns using `n` bits: `2ⁿ`
-   Maximum unsigned value using `n` bits: `2ⁿ − 1`
-   Minimum unsigned value: `0`

### Example: Maximum value of an 8-bit octet

\[ 2\^8-1=256-1=255 \]

So an 8-bit octet can represent decimal values from **0 to 255**.

------------------------------------------------------------------------

## 5. Converting an 8-bit Binary Number to Decimal

Use the place values:

``` text
128  64  32  16   8   4   2   1
```

### Example 1: `10000000`

\[ 128=128 \]

### Example 2: `11000000`

\[ 128+64=192 \]

### Example 3: `11100000`

\[ 128+64+32=224 \]

### Example 4: `11110000`

\[ 128+64+32+16=240 \]

### Example 5: `11111000`

\[ 128+64+32+16+8=248 \]

### Example 6: `11111100`

\[ 128+64+32+16+8+4=252 \]

### Example 7: `11111110`

\[ 128+64+32+16+8+4+2=254 \]

### Example 8: `11111111`

\[ 128+64+32+16+8+4+2+1=255 \]

     Binary      Decimal
  ------------ ---------
   `10000000`        128
   `11000000`        192
   `11100000`        224
   `11110000`        240
   `11111000`        248
   `11111100`        252
   `11111110`        254
   `11111111`        255

------------------------------------------------------------------------

## 6. Fixed Bits and Possible Combinations

The notebook demonstrates how fixing some bits changes the number of
possible patterns.

For `n` total bits, if `k` bits are fixed, the remaining `n-k` bits can
vary.

\[ `\text{Possible combinations}`{=tex}=2\^{n-k} \]

### Example 1: 2 bits, with 1 bit fixed

If the first bit is fixed to `0`, the possible values are:

``` text
00
01
```

If the first bit is fixed to `1`:

``` text
10
11
```

There are:

\[ 2\^{2-1}=2 \]

patterns for each fixed first-bit value.

### Example 2: 3 bits, with 2 bits fixed

If the first two bits are fixed, the final bit can be either `0` or `1`.

``` text
00 -> 000, 001
01 -> 010, 011
10 -> 100, 101
11 -> 110, 111
```

There are:

\[ 2\^{3-2}=2 \]

possible patterns for each fixed 2-bit prefix.

------------------------------------------------------------------------

## 7. IPv4 Address Representation

An IPv4 address has 32 bits, arranged as four 8-bit octets.

### Example from the notebook

``` text
Decimal: 200.202.63.247
```

Each octet can be converted separately:

    Decimal octet  8-bit binary
  --------------- --------------
              200   `11001000`
              202   `11001010`
               63   `00111111`
              247   `11110111`

So the complete binary address is:

``` text
11001000.11001010.00111111.11110111
```

The dots separate the four octets.

### Address size

\[ 4 `\text{ octets}`{=tex}`\times 8`{=tex} `\text{ bits}`{=tex}=32
`\text{ bits}`{=tex} \]

The total number of possible IPv4 bit patterns is:

\[ 2\^{32}=4,294,967,296 \]

This is the total size of the IPv4 address space, not the number of
addresses available for ordinary host assignment.

------------------------------------------------------------------------

## 8. Quick Revision

  Concept                            Remember
  ---------------------------------- ------------------
  Binary base                        2
  Binary digits                      0 and 1
  One bit                            One binary digit
  One octet                          8 bits
  IPv4 address size                  32 bits
  IPv4 octets                        4
  Decimal range of one octet         0--255
  Patterns with `n` bits             2ⁿ
  Maximum unsigned value             2ⁿ − 1
  Combinations with `k` fixed bits   2ⁿ⁻ᵏ

------------------------------------------------------------------------

## 9. Practice Questions

1.  Convert binary `1010` to decimal.
2.  Convert binary `1111` to decimal.
3.  Write decimal 9 in 4-bit binary.
4.  Write decimal 13 in 4-bit binary.
5.  What is the maximum decimal value of an 8-bit octet?
6.  How many patterns can be represented using 5 bits?
7.  How many patterns are possible when 3 bits are used and 1 bit is
    fixed?
8.  Convert `11000000` to decimal.
9.  Convert `11111100` to decimal.
10. Convert each octet of `200.202.63.247` into 8-bit binary.
11. How many bits are present in an IPv4 address?
12. How many total bit patterns exist in a 32-bit address?

------------------------------------------------------------------------

*End of Day 2 notes.*
