## textbook readings
![[tan 2.1-2.2, 3.1-3.2]]

![[kr 5.1-5.2]]
## reponsibilities of the physical and data link layers 
- unlike other adjacent layers, its not possible to simply replace an implementation of one layer with another 
- Physical layer responsibilities 
	- provide the physical topology of the network 
	- provide the transfer medium 
	- encode data into a transmission signal supported by the medium 
	- decode data into a transmission signal supported by the medium 
	- generate or amplified re-transmitted signals along the medium 
	- monitors transmission errors 
	- detects arriving signal levels to synchronise speed and timing 
- Data link layer responsibilites 
	- construct data frames using the format of the physical layer 
	- calculates cyclic redundancy codes (crc) information 
	- checks for arriving errors using crc information 
	- initiates and arbitrates and passing device addresses in data 
	- acknowledges receipt of a frame
	- retransmits data if there is an error 

## metrics of network measurement 
- latency or propagation delay is the amount of time it takes for the first bit to reach its destination
- Round time trip (RTT) is twice the latency, the time for one bit to travel to the destination, and the first bit in reply to return 
- Bandwith is the number of bits that can be fit through a network connection, per unit time. bandwith has been related to frequency within the medium 
- Throughput is usually the measured number of bits per second, while bandwith is the nominal (peak) number of bits per second possible, high bandwith does not imply low latency, you can braodcast many mbps over a satellite connection, but it will take hundreds of milliseconds to arrive 
- Example 
	- a car can carry 4 people to bunbury in 2 hours, thus the bandwith is 2 people p/h
	- a bus can take 60 passengers and arrive in 2 hours 
	- thus the bandwith is 30 people p/h, but the latency is still 2 hours 
- ![[Screenshot 2023-03-08 at 10.20.21 am.png]]

## the physical layer and transmission errors 
![![//#^Table1]]
- rates of transmission errors are described by their probability of occuring, or by their expected bit-error-rate
- transmission errors usually occur in bursts and are caused by
	- thermal noise 
	- distorted frequency 
	- crosstalk between adjacent wires 

## how data is placed in frames
- simple timing gaps between frames cannot be used as all hardware devices run at slightly different speeds, resulting in skewing if time is relied upon
- to overcome synchronisation problems, special byte sequences are often used to prefix and suffix the data 
- as these special byes may themselves be required data we must escape their special meaning 
- this process is termed byte stuffing, use DLE = $020_8$, STX = $002_8$, ETX = $003_8$ 
- a lower level approach, bit-stuffing, overcomes the reliance on using the ASCII codes. each frame is not enveloped in pairs of "flag" patterns 01111110.
- if this flag pattern appears in the data, the stuffed sequence 011111010 is transmitted


## phase encoding of signals 
- a digital signal is a sequence of discrete, discontinuous pulses, or signal elements 
- if all signal elements have the same (voltage) sign, they are termed unipolar 
- the modulation rate of a LAN is the number of signal elements (transmitted) per second, or the baud rate 
- to correctly interpret a signal, the receiver must know the time of each signal element and the expected voltage levels of the bits 0 and 1
- the 2 simplest encoding schemes are the:
	- non-return to zero level (NRZ-L) and
	- non-return to zero inverted (NRZ-I)
- NRZ-I is an example of differential encoding in which the signal transition, rather than the signal level indicated the value of each bit 
- biphase encoding, ensures that there will be a transition in the middle of each bit 
- with tranditional manchester encoding the mid-bit transition provides a clocking mechanism 
- with differential manchester the mid-bit transition provides the clocking and the initial transition provides the data 
- **biphase encoding schemes have at least one transition per bit time, thus the meximum modulation rate , or baud rate, is twice that for NRZ-L and NRZ-I**

## error detection and correction 
- data may be modified so that errors can either be:
	- detected
		- you can only tell that the data is wrong
	- corrected
		- something went wrong and you can fix it then continue with more data 
- correction is required where communication must be simplex, but correction is expensive.
- a good example of its need is between earth and inter-planetary spacecraft. error correction by the reveiver is referred to as forward error correction, whereas re-transmission schemes are referred to as reverse error correction
- codewords are constructed consisting of both data and check bits 
- the hamming distance between two codewrods consists of the number of bit posistions in which they differ
- the difference is performed modulo-2 or exclusive-or:
- **the numuber of 1s that occur is the hamming distance**
	- ![[Screenshot 2023-03-08 at 11.12.01 am.png]]
- the hamming distance of a code is the minimum hamming distance between any two words in that code
- to detect: δ errors, a distance of δ + 1 is required
- eg: to detect 1 bit in error requires that there is no word with a distance of 1 from the valid word 
- to correct: δ errors, a distance of 2 δ + 1 is required so that even with δ errors, the damaged codeword is the closest to one valid codeword. 

## hammings correction of single-bit errors 
- say that a single transmission consists of m bits for the message, and r bits of seemingly redundant information 
- thus transmit n = m + r bits when transmiting a message 
- the question is "how much more information do we need to transmit so that the receiver can correct errors"
- each of the 2^m possible message words has n illegal code words which are a distance 1 from it. therefore each message word requires n + 1 distinct bits (1 legal one, and n illegal ones)
- richard hamming developed a method which achieves the lower bound of
	- m + r + 1 <= $2^r$ 
- each bit that has the position of a power of 2 {1,2,4,8,...} is a check bit and forces the parity of some collection of bits including itself, parity may be forced to be either even or odd
- example 
	- 3 = 2 + 1 
	- 7 = 4 + 2 + 1
	- 11 = 8 + 2 + 1
- when a codeword is received at the other end, we must check and possibly correct it 
- to correct it when it arrives 
	1. start a counter at 0.
	2. examine and check bit in position {1,2,4,8} to see if it has the correct parity 
	3. if not, add k to c 
	4. when all check bits have been examined, and counter c is 0, the the codeword is correct. Otherwise, the incorrect bit is in position c
- example
	- ![[Screenshot 2023-03-08 at 12.24.30 pm.png]]

## cyclic redundancy codes (CRCs)
- the extra bits used to detect errors are called checksum bits 

### polynomial codes
- a ploynomial is represented by a bit string with 1 for each power represented in the ploynomial, and 0 otherwise 
- eg: $x^4$ + $x^3$ + 1 is represented as 11001 
- ploynomial arithmetic is performed modulo-2 or exclusive-or 
- ![[Screenshot 2023-03-08 at 12.41.21 pm.png]]
- both the sender and receiver agree on a generator polynomial, G(x), with high and low order bits 1.
- the message, M, is also interpreted as a polynomial 
- the checksum, when calculated, is appended to the message so that (m + checksum), known as the transmission T(x), is divisible by G(x)
- on arrival we simply check that the received transmsission is divisislbe by G(x).
- what types or errors can and cannot be detexted with CRCs?
	- let the error bits in $T_arrived$ (x) be E(x). each bit in E(x) corresponds to a bit that has been invereted. if there are k 1 bits in E(x), then there have been k single-bit errors 
	- then due to the properties of the modulo-2 arithmetic:
	- ![[Screenshot 2023-03-08 at 12.45.31 pm.png]]
	- we notice that if G(x) divides E(x), then errors can go by undetected 
- important results 
	- if G(x) has two or more terms all single bit errors can be detected 
	- to detect double errors, G(x) must not be divisible by. (x^k + 1) for k up to some maximum frame length 
	- to detect an odd number of errors, G(x) should contain (x+1) as a factor 
	- polynomials of degree r will detect all burst errors of <= r bits

## some standard polynomial codes 
- 16 bit checksums catch
	- all single and double bit errors 
	- all errors with an odd number of bits 
	- all burst errors ≤ 16 bits long
	- 99.997% of burst errors = 17 bits 
	- 99.998% of burst errors ≥ 18 bits 
- ![[Screenshot 2023-03-08 at 12.50.58 pm.png]]