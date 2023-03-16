
- The go-back-N protocol wastes bandwidth on retransmitted frames if the error rate is high.
- he receiver can buffer all received frames (up to some limit) and simply wait for the bad frame to be retransmitted.
- The _sender's window size_ corresponds to the number of frames transmitted by not yet received - it varies, grows and shrinks, over time.
- The _receiver's window size_ corresponds to the number of frames that the receiver is willing to receive - it too varies over time, and is always ≥ 1.
- ![[Screenshot 2023-03-16 at 12.02.12 pm.png]]