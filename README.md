<!---
{
  "depends_on": [],
  "author": "Stephan Bökelmann",
  "first_used": "2025-03-31",
  "keywords": ["transmission", "signal", "bit", "bitrate"]
}
--->

# Signal Encoding

## 1) Introduction
Think of a picture in your mind. 
If you want to communicate this to someone else, it's neccessary to search for a common medium, that you can manipulate and your recepient can observe. 
This can be a piece of paper that you draw on, your hands with which you wave or the air-pressure which they can sense with their ears. 
When it comes to machine-to-machine communication, this holds also true.

---

Imagine you are standing at a lake. 
Across the lake, there is another person you want to communicate with. 
You shout and shout, but you can't hear each others voices. 
A great engineer comes along, hands you a super-fast waterpump and shows you well near by to manipulate the waterheight in the lake.
Your partner gets a yardstick that he sticks vertically into the water of the lake to measure the waterheight. 
Additionally you both get translation tables, that convert each letter of the alphabet in a series of five consecutive waterlevels.
The table tells you the following:

> We call each letter a letter.
> We call each combination of 5 consecutive bits a symbol.
> Each message contains exactly 10 symbols.
> If a message has less than 10 symbols the last symbols get stuffed with whitespace.
> Each message is prefixed with a sequence of low-low-low-high-low called start-sequence.
> The receiver has to syncronize his stopwatch with the high-level-length of the start-sequence.
> The lenght of a level may change from message to message, but never within the message.
> This LLLHL not part of any symbol.
> The channel is always low when no message is being send.


| Zeichen        | H/L-Code | Binär  |
|----------------|-----------|--------|
| A              | LLLLL     | 00000  |
| B              | LLLLH     | 00001  |
| C              | LLLHH     | 00011  |
| Start-Sequence | LLLHL     | 00010  |
| D              | LLHLL     | 00100  |
| E              | LLHLH     | 00101  |
| F              | LLHHL     | 00110  |
| G              | LLHHH     | 00111  |
| H              | LHLLL     | 01000  |
| I              | LHLLH     | 01001  |
| J              | LHLHL     | 01010  |
| K              | LHLHH     | 01011  |
| L              | LHHLL     | 01100  |
| M              | LHHLH     | 01101  |
| N              | LHHHL     | 01110  |
| O              | LHHHH     | 01111  |
| P              | HLLLL     | 10000  |
| Q              | HLLLH     | 10001  |
| R              | HLLHL     | 10010  |
| S              | HLLHH     | 10011  |
| T              | HLHLL     | 10100  |
| U              | HLHLH     | 10101  |
| V              | HLHHL     | 10110  |
| W              | HLHHH     | 10111  |
| X              | HHLLL     | 11000  |
| Y              | HHLLH     | 11001  |
| Z              | HHLHL     | 11010  |
| Space          | HHLHH     | 11011  |

With these rules, you can now send messages to your opposite, by filling the lake with more water, or pumping it out!

### 1.1) Further Readings and Other Sources

- **Claude Shannon – "A Mathematical Theory of Communication"**  
  The foundational paper that introduced the concept of information theory and formalized communication channels.

- **Brian W. Kernighan & Rob Pike – "The Practice of Programming"**  
  Contains practical insights into how data is structured and transmitted, with emphasis on clear representation and protocols.

- **Andrew S. Tanenbaum – "Computer Networks"**  
  A comprehensive resource for understanding network layers, encoding schemes, and data transmission principles.

- **Simon Singh – "The Code Book"**  
  A popular science book on the history of codes and encoding, perfect for building intuition and appreciation of symbolic systems.

- **Ben Eater – [YouTube: "How computers send data"]**  
  A highly visual and beginner-friendly explanation of bit-level communication and encoding schemes.  
  → https://www.youtube.com/watch?v=3EN8CWhOZiU


## 2) Tasks

1. **Decode a Message**: Given the sequence `LLLHL LLHLL HLHLL HLHHL HLHLH LLLLH`, decode it using the symbol table provided.
![exercise waveform](https://maxclerkwell.github.io/svg_storage/fundamentals/waveforms/exercise_message_01.wavedrom.svg)

2. **Design a Message**: Encode the message `HELLO` using the H/L-Code, including the correct start-sequence and padding with `Space` if needed.
3. **Detect Invalid Symbols**: Check the sequence `LLLHL LLLLH LLHLL LLLHL` and identify which symbols are valid and which one(s) violate the constraints.
4. **Modify a Symbol**: Choose any symbol from the table and create a new version by flipping a single bit. Check whether the new code remains valid (i.e. does not become the start-sequence).
5. **Channel State Analysis**: If no message is transmitted, what is the expected level on the channel?
6. **Design Your Own Encoding Rule**: Propose a new forbidden pattern (e.g. `HHLLH`) and list which existing symbols would become invalid under this rule.

## 3) Questions
1. How does the continuous low-level help the receiver understanding messages?
2. If each level in the symbol lasts 5 seconds, how long does it take to transmit one full message (including start-sequence and 10 symbols)?
3. How many full messages can be transported over this channel per minute?
4. What parameters could an engineer change about the general system to increase the message-throughput?
5. Explain why it would take infinite power to change the water-level from low to high instantaneously.

## 4) Advice
Communication is not just about sending data — it's about ensuring the receiver can make sense of it.  
Whether you're flipping water levels, sending voltage pulses, or transmitting bits across fiber optics, clarity, structure, and timing are key.  
So when designing or analyzing any signal encoding system, always ask yourself:

> Can the receiver know *when* to listen, *what* to listen for, and *how* to interpret it?

Mastering this mindset will not only help you understand communication systems, but also make you a better programmer, engineer, and thinker.