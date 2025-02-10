---
course:
  - CSM 477
tags: 
last topic: Serial Communications
next topic: Transmission Media
note to self:
---

2025-02-09 20:25

# Intro To Data Communications

## Detailed Notes
### Data Communications
This concerns the transmission of digital messages to devices external to the message source.
**External Devices:** independently powered circuitry that exists beyond the chassis of a computer or other digital message source. 

### Communications Channel
A pathway over which information can be conveyed.
-Information is represented by individual data bits.
-The message source is the transmitter, and the destination id the receiver.
#### Channel Types:
- Simplex Channel: A channel whose direction is unchanging. Eg. Radio channel.
- Half-Duplex Channel: A single physical channel in which the signal may be reversed. Messages flow in two directions, but never at the same time. Eg. phone call, also used by centronics.
- Full-Duplex Channel: allows simultaneous message exchange in both directions. It consists of 2 simplex channels. The transmission rate of the reverse channel may be slower if it used only for flow control of the forward channel.

### Serial Communications
- Bit serial transmission conveys a message one bit at a time through a channel.
- Byte serial transmission conveys 8 bits at a time through 8 parallel channels. (Centronics printer interface is a case where byte-serial transmission is used.)
- **Examples:** 16 bit wide data bus to transfer data between a microprocessor and memory chips, when communicating with a timesharing system over a modem, only a single channel is available, and bit-serial transmission is required.

### Transmission Media


## Key Points
- **Rule:** The maximum permissible transmission rate of  a message is directly proportional to signal power and inversely proportional to channel noise.
- **Aim:** Provide the highest possible transmission rate at the lowest possible power with the least possible noise.
- Bit serial transmission is normally just called serial transmission and is the chosen communications method in many computer peripherals.

## Summary

-