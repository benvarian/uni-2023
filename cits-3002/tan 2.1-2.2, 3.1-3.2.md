
- defines the electrical, timing and other interfaces by which bits are sent as signals over channels 
- foundation on which the network is built 
- 3 kinds of transmission media 
	- guided or wired 
	- wireless 
	- satellite 

# 2.1 guided transmission media 

## 2.1.1 persistent storage 
- basically saying that the cost of phyiscally storing media on drives in this day in age is still going to be cheaper and genereally faster than uploading it to the cloud 

## 2.1.2 twisted pairs 
- consits of two insulated copper wires, around 1mm thick 
- two parrallel wires constitute a fine antenna when the wires are twisted, the waves from different twists cancel out, so the wire radiates less effectively 
- a signal is usually carried as the difference in voltage between the two wires in the pair 
- transmitting the signnal as the difference between the two voltage levels, as opposed to an absoloute voltage provides better immunity to external noise because the noise tends to affect the voltage travelling through both wires in the same way, leaving the differential relatively unchanged 
- bandwith depends on the thickness of the wire and the distance travelled 

# 2.2 wireless transmission

## 2.2.1 the electromagnetic spectrum 
- when electrons move, they create eletromagnetic waves that can propagate through space
- the number of oscillations per second of a wave is called its frequency, f, and is measures in Hz
- the distance between two consecutive maxima is called the wavelength, which is universlaly designated by the greek letter $\lambda$ 
- in a vacum, all electromagnetic waves travel at the same speed, no matter their frequency 
- this speed usually called the speed of light, c, is approximately 3 x 10^8 m/sec, or about 1 foot (30 cm) per nanosecond 

## 2.2.2 frequency hopping spread spectrum 
- a transmitter hops from frequency to frequency hundreds of times per second 
- popular in military as hard to detect and impossible to jam 
- also offers good resistance to fading due to signals taking different paths from source to destination and interfering after recombining 

## 2.2.3 direct sequence spread spectrum 
- uses a code sequence to spread the data signal over a wider frequency band 
- widely used commercially as a spectrally efficient way to let multiple signals share the same frequency band 
- can tolerate interference and fading becuase only a fraction of the desired signal is lost 

## 2.2.4 ultra-wideband communcation 
- sends a series of low-energy rapid pulses, varying their carrier frequencies to communcate information
- the rapid transitions lead to a signal that is spread hinly over a very wide frequency band 
- defined as signals that have a bandwith of at least 500 MHz or at least 20% of the center frequency of their frequency band 
- with this much bandwith, UWB has the potential to communcate at several hundred megabits per second 

# data link layer 

## 3.1 data link layer design issues 
- uses the services of the physical layer below it to send and receive bits over communication channels that may lose data 
- has a number of functions that include 
	- providing a well defined service interface to the network layer 
	- framing sequences of bytes as self-contained segments 
	- detecting and correcting transmission errors 
	- regulating the flow of data so that slow receivers are not swamped by fast senders 
- to accomplish these goals, the layer takes the packets it gets from the network layer and encapsulates them into frames for transmission 
- each frame contains a frame header, a payload field for holding the packet and a frame trailer 
- frame management forms the heart of what the data link layer does 

### 3.1.1 services provided to the network layer 
- function of the data link layer is to provide services to the network layer 
- principal service of the link layer is transferring data from the network layer on the source machine to the network layer on the destination machine 
- on the source machine is an entity, call it a process, in the network layer that passes packets to the data link layer for transmission to the destination 
- the job of the data link layer is to transmit the data to the destination machine so they can be handed over to the network layer there 
- three reasonable possibilites that we will consider in turn are 
	- unacknowledged connectionless service 
		- having the source machine send independent frames to the destination machine without having the destination machine acknowledge them 
		- appropriate for real-time traffic, such as voice or video in which late data is worse than bad data 
	- acknowledgd connectionless service 
		- there are still no logical connections used, but each frame sent is invididually acknowledged
		- in this way the sender knows whether a frame has arrived correctly or been lost 
		- if it hasnt arrived within a specified time interval, it can be sent again 
		- good for unreliable channels such as wireless systems 
	- acknowledged connection-oriented service 
		- source and destination machines establish a connection before any data is transferred 
		- each frame sent over the connection is numbered and the data link layer guarantees that each frame sent is indeed received 
		- guarantees that each frame is received exactly once and that all frames are received in the right order 
		- provides a reliable bit stream 
		- appropriate over long, unreliable links such as satellite channel or long distance telephone circuit
- when connection oriented services is used, transfers go through three distinct phases 
	- connection is established by having both sides initialise variables and counters needed to keep track of which frames have been received and which ones have not 
	- one or more frames are actually transmitted 
	- the connection is released, freeing up the variables, buffers and other resources used to maintian the connection 

### 3.1.2 framing 
- physical layer accepts a raw bit stream and attempts to deliver it to the desitnation 
- if the channel is noisy, as it is for most wireless and some wired links, the physical layer will add some redundancy to its signals to reduce the bit error rate to a tolerable level 
- it is up to the dat link layer to detect errors and if necessary, correct errors 
- usual approach is for the data link layer to break up the bit stream into discrete frames, compute a short token called a checksum for each frame and include the checksum in the frame when it is transmitted 
- when a frame arrives at the destination, the receiver recomputes the checksum based on the received frame
- if the newly computed checksum if different from the one contained in the frame, the data link layer knows that an error has occured and takes steps to deal with it 
- breaking up the bit stream into frames is more difficult than it first appears, a good design must make it easy for a receiver to find the start of new frames while using little of the channel bandwidth, four methods 
	- byte count 
		- uses a field in the header to specify the number of bytes in the frame 
		- when the data link layer at the destination sees the byte count, it knows how many bytes follow and hence where the end of the frame is 
		- the reason this method generally isnt used by iteself is because the part of memeory storing how many bytes follow can become corrupted and introduce many problems with recontacting the original sender and wrecking packets in teh process
	- flag bytes with byte stuffing 
		- gets around the problem of resynchronisation after an error by having each frame start and end with speical bytes 
		- often the same byte, called a flag byte, is used as both the starting and ending delimiter 
		- two consecutive flag bytes indicate the end of one frame and the start of the next 
		- thus, if the receiver ever loses synchronisation it can just search for two flag bytes to find the end of the current frame and the start of the next frame
		- **one way to solve this problem is to have the senders data link layer insert a special escape byte just before each accidental flag byte in the data, thus a framing flag byte can be distinguished from one in the data by the absence or presence of an escape byte before it. the data link layer on the receiving end removes the escape bytes before giving the data to the network layer, this is called byte stuffing** 
	- flag bits with byte stuffing 
		- framing can also be done at a bit level, so frames can contain an arbitrary number of bits made up of units of any size 
		- developed for the once popular HDLC (high level data link control)
		- each frame begins and ends with a special bit pattern, 01111110 or 0x7E.
		- whenever the senders data link layer encounters five consecutive 1s in the data, it automatically stuffs a 0 bit into the outgoing bit stream 
		- this bit stuffing is analogous to byte stuffing, in which an escape byte is stuffed into the outgoing character stream before a flag byte in the data
		- also ensures a minimum density of transitions that help the physical layer maintain synchronisation 
		- when the reciever sees five consecutive incoming 1 bits, followe dby a 0 bit, it automatically destuffs the 0 bit.
		- **with bit stuffing the boundary between two frames can be unambiguously recognised by the flag pattern. Thus if the receiver loses track of where it is, all it has to do is scan the input for flag sequences, since they can only occur at frame boundaries and never within the data**
		- **side effect is that the length of a frame now depends on the contents of the data it carries, for instance if there are no flag bytes in the data, 100 bytes might be carried in a frame of rougly 100 bytes **
	- physical layer coding violations 
		- use a shortcut from the physical layer 
		- we know that the enconding of bits as signals often includes redundancy to help the receiver
		- this redundancy means that some signals will not occur in regular data 
		- for example 
			- in the 4B/5B line code 4 data bits are mapped to 5 signal bits to ensure sufficient bit transitions
			- this means that 16 out of the 32 signal possibilities are not used 
			- can use some resevered signals to indicate the start and end of frames 
		- in effect we are using coding violations (invalid characters) to delimit frames 
		- **the beautiy of this scheme is that because they are reserved signals, it is easy to find the start and and of frames and there is no need to stuff the data** 

### 3.1.3 error control 
- how to make sure all frames are eventually delivered to the network layer at the destination and in the proper order 
- assume that the receiver can tell whether a frame that it receives contains correct or faulty information 
- it might be fine for the sender to just keep outputtig frames without regard to whether they were arriving properly, but for reliable connection oriented service it would not be fine at all
- the usual wya to ensure reliable delivery is to privde the sender with some feedback about what is happening at the other end 
- typically, the protocol calls for the reciever to send back speicals control frames bearing positive or negaitve acknowledgements about the incoming frames. if the sender receives a positive acknowledged about a frame, it knowns the frame has arrived safely. a negative acknowledgement means that something has gone wrong and the frame must be transmitted again 
- it should be clear that a protocol in which the sender transmits a frame and them waits for an acknowledgement, positive or negative, will hang forever if a frame is ever lost due to, malfunctioning hardware or a fulity communication channel 
- possibly dealt with by introducing timers into the data link layer, 
	- when the sender transmitys a frame, it genreally also starts a timer, 
	- the timer is set to expire after an interval long enough for a frame to reach the destination, be processed there and have the acknowledgement propagate back to the sender 
- normall the frame will be correctly received and the acknowledgement will get back before the timer runs, in which case the timer will be cancelled 
- however if the either the ogirignal frame or the acknowledgement is lost, the timer will go off, alerting the sender to a potential problem 
- **to prevnent from the reciever accepting the same frames multiple times, it is necessary to assign sequence numbers to outgoing frames, so that the receiver can distinguish retransmissions from originals**

### 3.1.3 flow control 
- what to do with a sender that systematically wants to transmit frames faster than the reciver can accept them?
- basically how to control the output of data from say a super duper fast server to a slower mobile device 
- feedback based flow control 
	- receiver sends back information to the sender giving it permission to send more data, or at least telling the sender how the receiver is doing 
- rate based flow control 
	- the protocol has a built-in mechanism that limits the rate at which senders may transmit data, without using feedback from the receiver 

# 3.2 error detection and correction 

## 3.2.1 error correcting codes 
- examine four different error-correcting codes 
	- hamming codes 
	- binary convolutional codes 
	- reed-solomon codes 
	- low-density parity check codes 
- all add redundancy to the information that is sent 
- a frame consists of m data bits, and r redundant bits 
- in a block code the r check bits are computed solely as a function of the m data bits which they are associated, as though the m bits were looked up in a large table to find their correspodning r check bits 
- in a systematic code, the m data bits are sent directly, along with their check bits, rather than being encoded themselves before they are sent 
- in a linear code, the r check bits are computed as a linear function of the m data bits. exclusive or (xor) or modulo 2 addition is a popular choice. this means that encoding can be done with operations such as matrix multiplications or simple logic circuits 
- let the total length of a block be n (ie n = m + r). we will describe this as an (n, m) code. an n-bit unit containing data and check bits is referred to as an n-bit codeword. 
- the code rate is teh fraction used in practive vary widely. they might be 1/2 for a noisy chanel, in which case half of the received information in redundant, or close to 1 for a high-quality channel
- to understand how errors are handled, it is necessary to first look closely at what an error really is.
	- given any two codewords that may be transmitted or received 
	- 10001001 and 10110001
	- is is possible to determine how corresponding bits differ. In this case 3 bits differ. 
	- **to determine how many bits differ, just XOR the two codewords and count the number of 1 bits in the result.**
	- for example 
	- ![[Screenshot 2023-04-08 at 9.48.48 pm.png]]
- the number of bit positions in which two codewords differ is called the hamming distance, its significance is that if two codewords are a hamming distance 'd' apart, it will require 'd' single bit errors to convert one into the other 
- to reliably detect d errors, you need a distance d + 1 code because with such a code there is no way that d single bit errors can change a valid codeword into another valid codeword. when the receiver sees an illegal code word, it can tell that a transmission erorr has occured. 
- to correct d errors, you need a distance 2d + 1 code because that way the legal codewords are so far apart that even with d changes the original codeword is still closer than any other codeword. This means the original codeword can be uniquely determined based on nhte assumption that a larger number of errors are less likely 
- as a simple example of an error-correcting code, consider a code with only four valid codewords 
	- 0000000000, 0000011111, 1111100000, and 1111111111
	- this code has a distance of 5, which means that it can correct double errors or detect quadruple errors. if the codeword 0000000111 arrives and we expect only single or double bit errors, the receiver will know that the original must have been 0000011111. if however a triple error changes 0000000000 to 000000111, the error will not be corrected properly.
- imagine that we want to design a code with m message bits and r check bits that will allow all single errors to be corrected. each of the $2^m$ legal messages has n illegal codewords at a distance of 1 from it. these are formed by systematically inverting each of the n bits in the n-bit codeword formed from it. thus each of the $2^m$ legal messages required n + 1 bit patterns dedicated to it. since the total number of bit patterns is $2^n$, we must have (n + 1)$2^m$ ≤ $2^n$ using n = m + r, this requirement becomes 
	- m + r + 1 ≤ $2^r$ 
	- given m this puts a lower limit on the number of check bits needed to correct single errors 
- this theoretical lower limit can in fact be achieved using a method due to hamming. in hamming codes the bits of the codeword are numbered consecutively, starting with bit 1 at the left end, bit 2 to its immediate right, and so on. the bits that are powers of 2 (1,2,4,8,16 etc) are check bits. the rest (3,5,6,7,9, etc) are filled up with the m data bits. 
- example of hamming code correcting a single bit error 
	- ![[Screenshot 2023-04-08 at 10.21.50 pm.png]]
- this construction gives a code with a hamming distance of 3, which means that it can correct single errors (or detect double errors). 
- when a codewords arrives, the reciver redoes the check bit computations including the values of the received check bits. we call these the **check results**
- if the check bits are correct then, for even parity sums, each check result should be zero. in this case, the codeword is accepted as valid 
- if the check results are not all zero, and error has been detected. the set of check results form the error syndome that is used to inpoint and correct the error. 
- in fig 3.6 above, a single bit error has occured on the channel so the check results are 0,1,0,1 for k = 8,4,2,1. 
- this gives a syndrome of 0101 or 5. by the design of this scheme, this means that the fifth bit is in error. flipping the incorrect bit and discarding the check bits gives the correct message of an ASCII 'A'.

## 3.2.2 error detecting codes 
- used on wireless links 
- noisy and error prone 
- examine 3 different error-detecing codes, all linear, systematic block codes 
	- parity 
		- a single parity bit is appended to the data 
		- the parity bit is chosen so that the number of 1 bits is even (or odd)
		- doing this is the equivalent to computing the even patity bit as the modulo 2 sum or XOR of the data bits 
		- example 
			- 1011010 is sent in even parity, a bit is added to the end to make it 10110100.
			- with odd parity 1011010 becomes 10110101.
		- a code with a single parity bit has a distance of 2, since any single bit error produces a codeword with the wrong parity, this means that it can detect single bit errors 
		- example 
			- consider a channel on which errors are isolated and the error rate is $10^{-6}$ per bit 
			- typical lan links provide bit error rates of $10^{-10}$. 
			- block size is 1000 bits, to provide error correction for 1000 bit blocks, we know that 10 check bits are needed. thus a megabit of data would require 10,000 check bits 
		- the total overhead for the error detection and retransmission method is only 2001 bits per megabit of data, versus 10,000 bits for a hamming code.
		- one of the main problems with parity bits is that if lots of the data is corrupted then the accuracy rate will drop to 0.5.
		- the odds can be improved considerably if each block to be sent is regarded as a rectangular martrix n bits wide and k bits high, now if we compute and send one parity bit for each row, up to k-bit errors will be reliably detected as long as there is at most one error per row.
		- **theres a better way than above which is called interleaving**
			- compute a parity bit for each of the n columns and send all the data as k rows, sending the rows from top to bottom and the bits in each row from left to right in the usual manner 
			- at the last row we send the n parity bits
			- this transmission order is shown for n = 7 and k = 7
			- ![[Screenshot 2023-04-10 at 11.42.53 am.png]]
			- general technique to convert a code that detects isolated errors into a code that detects burst errors 
	- checksums 
		- a group of check bits associated with a message, regardless of how the bits are calculated 
		- usually placed at the end of the message, as the complement of the sum function 
		- this way errors may be detected by summing the entire received codeword, both data bits and checksum, if the result comes out to 0 it means no error has been received 
		- the 16-bit checksum used on all internet packets are part of the ip protocol
		- sum of the message bits divided into 16-bit words 
		- because this method operates on words rather than on bits, errors that leave the parity unchanged can still alter the sum and be detected 
		- this algorithm gives a more uniform coverage of the data by the checksum bits. otherwise two high-order bits can be added, overflow and be lost without changing the sum
		- the internet checksum, is efficient and simple but provides weak protection in some cases percisely because it is a simple sum. 
		- **doesnt detect the deletion or addition of zero data, nor swapping parts of the message, provides weak protection against message splices in which parts of the two packets are put together**
		- a better choice is fletchers checksum, 
			- includes a positional component, adding the product of the data and its positoin to the running sum. 
			- provides stronger detection of changes in the position of data 
	- cyclic redundancy checks (CRCs)
		- based upon treating bit strings as representations of polynomial with coefficicents of 0 and 1 only 
		- a k-bit frame is regarded as the coefficient list for a polynomial with k terms, ranging from $x^{k-1}$ to $x^0$. said to be to the degree of k - 1. the high order bit is the coefficient of $x^{k-1}$, the next bit is the coefficient of $x^{k-2}$, and so on.
		- example 
			- 110001 has 6 bts and thus represents a six-term polynomial with coefficients: 1,1,0,0,0,1 
			- ![[Screenshot 2023-04-10 at 11.59.00 am.png]]
---

