---
layout: post
title: Hash algorithm
subtitle: hash algorithm
categories: algorithm
tags: [algorithm, hash]
---

# Hash Algorithm

## What is Hash Algorithm ?
---
* Function that matches random size of value to fixed size of value
* Hash Function must satisfy the definition of the function in mathematics

## 해시 알고리듬 분류
---
* (비암호학적) 해시 함수
* 암호학적 해시 함수

이 둘은 굳이 분류하자면 비암호학적 해시 함수이다.

* [CheckSum](#checksum)
* [Cyclic Redundancy Check, CRC](#cyclic-redundancy-check)

1. 임의 크기 -> 고정 크기
2. 결정론적 작동
이라는 해시 알고리듬의 정의를 만족한다
하지만 해시 알고리듬의 다른 속성은 조금 씩 달라짐

## Typical properties of hash algorithm ( 해시 알고리듬의 속성 )
---
* 효율성 (efficiency)
* 균일성 (uniformity)

### Uniformity of Hash Algorithm
	* A hash function with an even distribution have a high uniformity
	* Commonly, great hash algorithm should have high uniformity
	* Perfect hash algorithm : no hash conflict
		+ only possible if input value is very limited
	* [Chi-squared test](https://en.wikipedia.org/wiki/Chi-squared_test"chi-squared test")
		+ if the result is between `0.95 ~ 1.05`, uniform distribution hash function
	* How to increase uniformity
		+ Make a bucket number as an prime number (since it's using modulo operation)
		+ Design the hash function for perfect [avalanche effect](#avalanche)

#### Avalanche Effect <a name="avalanche"></a>
	* If an input is changed slightly, the output changes significantly
		+ desirable property of [cryptographic algorithms](#cryptographic-hash-function)
		+ hard to analogize the algorithm
	* Strict Avalanche Criterion, SAC
		+ if a single input bit flips, each of output bit changes with a 50% probability
		+ hash function with SAC is very likely to have an even distribution

#### Locality-sensitive hashing
	* Algorithm aimed to maximize the hash conflict instead of minimizing
	* Conflict should occur for data only with similar contents
	* Purpose to look for similar things in massive amounts of data
		+ searching spam mail, similar documents, etc

### Efficiency of Hash Algorithm
	* Usually prefer fast hash algorithm
	* Prefer quick access even if it waste more memory space
	* Prefer fast hash algorithm even with some conflicts occur
		+ hash conflict is rare
		+ even it happens, does not slow down much from O(1)
	* However, nowadays it's common to prefer hash functions that are difficult to accelerate in Hardware
		+ still prefer fast execution in Software
		+ related to [cryptographic hash algorithms](#cryptographic-hash-function)

### (Non-Cryptographic) Hash Function
---
	* Not secure to use as an cryptographically
	* Usage of unsecure hash function
		+ data store and search (Hash Table)
		+ [error detect occurred during data storage/transfer](#checksum)
		+ unique id creation
		+ etc
	* There are no such Hash functions which guarantee best result for every data type
	* Probabilistic algorithm exist which use different hash functions depending on the input value
		+ universal hashing
	* So it is important to use suitable hash function for certain purpose
1. Murmur
2. FNV-1, FNV-1a (difference is the order of XOR and multiplying prime number)
```c
/* FNV-1 Hash Function */
#define FNV_PRIME_32 16777619
#define FNV_OFFSERT_32 2166136261U
uint32_t FNV32(const char *str, uint32_t len) {

	uint32_t hash = FNV_OFFSERT_32;

	for(uint32_t i = 0; i < len; ++i) {s
		hash = hash * FNV_PRIME_32;
		hash = hash ^ str[i];
	}

	return hash;
}
```

#### Checksum
	* A small size of Data made by several data
		+ usually make a sum of every bytes in the data by a certain method
	* Similar with Hash Function
		+ output value size is fixed
	* Usage : Detect error occurred during data storage/transfer
		+ store Data with the result of checksum
		+ later, calculate checksum and compare with stored checksum
		+ if it's different, means error has been occurred
		+ credit card number, ISBN, etc
		+ check file if it's original file (no virus)
	* Usually doesn't cover data recovery (But some does e.g ECC)
##### Parity bit (Checksum)
	* Checksum adding additional 1 bit to binary data
	* Usually use bytes as an unit (7 bit data +  1 bit parity)
	* Even parity & Odd parity
		+ sum of the every bit including parity should be even or odd
<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-style:solid;border-width:0px;font-family:Arial, sans-serif;font-size:14px;overflow:hidden;
  padding:10px 5px;word-break:normal;}
.tg th{border-style:solid;border-width:0px;font-family:Arial, sans-serif;font-size:14px;font-weight:normal;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-baqh{text-align:center;vertical-align:top}
.tg .tg-c3ow{border-color:inherit;text-align:center;vertical-align:top}
.tg .tg-ml2k{border-color:inherit;color:#000000;text-align:center;vertical-align:top}
</style>
<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow" rowspan="2">Data</th>
    <th class="tg-c3ow" rowspan="2">Number of Bits</th>
    <th class="tg-c3ow" colspan="2">Data including Parity Bit</th>
  </tr>
  <tr>
    <td class="tg-c3ow">Odd Parity</td>
    <td class="tg-c3ow">Event Parity</td>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">000 0000</td>
    <td class="tg-c3ow">0</td>
    <td class="tg-c3ow"><span style="color:#FE0000">1</span>000 0000</td>
    <td class="tg-c3ow"><span style="color:#FE0000">0</span>000 0000<br></td>
  </tr>
  <tr>
    <td class="tg-c3ow">010 1100</td>
    <td class="tg-c3ow">3</td>
    <td class="tg-c3ow"><span style="color:#FE0000">0</span>010 1100</td>
    <td class="tg-ml2k"><span style="color:#FE0000">1</span>010 1100</td>
  </tr>
  <tr>
    <td class="tg-baqh">111 1111</td>
    <td class="tg-baqh">7</td>
    <td class="tg-baqh"><span style="color:#FE0000">0</span>111 1111</td>
    <td class="tg-baqh"><span style="color:#FE0000">1</span>111 1111</td>
  </tr>
</tbody>
</table>

|          |                | Data including Parity Bit | Data including Parity Bit |
|:--------:|:--------------:|:-------------------------:|:-------------------------:|
|   Data   | Number of Bits |         Odd Parity        |        Event Parity       |
| 000 0000 |        0       |         1000 0000         |         0000 0000         |
| 010 1100 |        3       |         0010 1100         |         1010 1100         |
| 111 1111 |        7       |         0111 1111         |         1111 1111         |


##### Cyclic Redundancy Check (Checksum)
	* Create checksum value by using modulo operation in polynomial
	* Easy to implement in binary hardware
		+ Latest CPU comes with the CRC-32C command
	* CRC's name changes depend on polynomial
	* Depend on leading coefficient of polynomial, number of bits used by CRC changes
		+ Each coefficient is 1 or 0
		+ leading coefficient is always 1 
			- e.g) $x^3 + x + 1$ => 011 (~~1011~~) , CRC-3-GSM (leading bit omitted)
```
CRC calculation example (CRC-3-GSM)
message = 10101001011001
1. Add 0 as (Number of polynomial bits - 1) which is 3, `10101001011001 000`
2. Calculate XOR bit operation, `10101001011001 000 ^ 1011 = 00011001011001 000`
3. Leave out the 0, and repeat #2 with bit 1 until every original bits become 0. (For this case, `110010111001 000 ^ 1011`)
4. `00000000000001 010 ^ 1011 = 00000000000000 001` is the checksum value

Validation test
1. Put checksum value at the end of the recieved message (`10101001011001-> 10101001011001 001`)
2. Repeat the same CRC calculation #2 and #3
3. If the result is 0, No error!
```
```java

```
https://en.wikipedia.org/wiki/Cyclic_redundancy_check

### Cryptographic hash function
---
	* An algorithm that's virtually impossible to find the original value in the hash value
		+ One-way function
		+ Requires a lot of mathematical knowledge
	* To find the original value, every combination should be tried (brute-force)
	* Usage
		+ integrity check of message or file
		+ digital signature creation or verfication
		+ password verfication
		+ proof-of-work (PoW)
			- make DoS hard in blockchain, etc
#### Properties of Cryptographic Hash Function
	* [pre-image resistance](#pre-image-resistance)
	* [second pre-image resistance](#second-pre-image-resistance)
	* [collision resistance](#collision-resistance)
##### Pre-image resistance
	* It should be hard to find original data from hash values.
		+ i.e) Original value shouldn't be store with hash value. Hacker might find some pattern with it.
	* This means that it should be difficult to see patterns from hash values
	* Hash value, the longer the better
##### Second pre-image resistance
	* It should be hard to find two different input with the same hash value.
		+ Case with Hash & input value
##### Collision resistance
	* It should be hard to find two different input with the same hash value.
		+ Case with no Hash & input value
	* Collision attack is easy compare to other resistance attack
		+ Viable collision attack is already found against MD5 and SHA-1

### How hacker find out password?
---
1. Rainbow Table
	+ Hash Table with common input with hash value
2. Brute-Force
3. Dictionary Attack
	+ Enter every word in a dictionary as a password

### How to prevent hacking?
---
There is no way to perfectly prevent hacking but can make it difficult.

1. Don't use well known passwords
	+ Can found the list of hacked passwords on the web
2. Force user to use long password
3. Send link or use other social login without saving a password

How to prevent Rainbow attack
1. Add Salt! (Visible to Hacker)
	+ Make a random string and put it behind the password before calculating hash value
	+ Put a random string in the DB
	+ Can't find the hash value in the rainbow table
	+ Hacker needs to try brute-force & dictionary attack for each password
2. Add Pepper! (Invisible to Hacker)
	+ Common string pasting to all passwords
	+ Don't save it in DB, only web server knows the value
	+ Since hacker doesn't have, almost every attack is worthless
	+ But, if when the web server memory gets hacked with the database, it won't be safe anymore.
