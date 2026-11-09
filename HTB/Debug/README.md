# Debug — Hack The Box Write-up

**Platform:** Hack The Box — CTF Try Out  
**Category:** Hardware  
**Challenge:** Debug  
**Difficulty:** Very Easy  
**Focus:** UART Analysis, Logic Analyzer, Digital Signal Decoding

---

## 1. Challenge Overview

Debug is a hardware security challenge that involves analysing captured digital signals to recover information transmitted through a serial communication interface.

Embedded systems frequently use serial communication to exchange information between microcontrollers, processors, sensors, and other hardware components.

During hardware debugging, logic analyzers are commonly used to capture these signals and examine the communication taking place between devices.

However, captured digital signals are not immediately readable. They must be interpreted using the correct communication protocol and configuration.

This challenge introduces the use of a logic analyzer to inspect digital communication and recover information encoded through UART (Universal Asynchronous Receiver-Transmitter).

The primary objective was to analyse the supplied logic capture, identify the serial communication, and reconstruct the challenge flag.

## 2. Understanding the Challenge Materials

### 2.1 Provided Capture

The original logic capture used during the investigation was:

```text
hw_debug.sal
```

The `.sal` extension is associated with Saleae Logic capture sessions.

The capture contains recorded digital signal information that can be opened and examined using Saleae Logic 2.

The important task was to identify which captured signal represented the serial communication and interpret its data correctly.

### 2.2 Tools Used

The investigation involved the following tools and techniques:

| Tool / Technique | Purpose |
|---|---|
| Saleae Logic 2 | Opening and examining the digital logic capture |
| Async Serial Analyzer | Decoding UART communication |
| UART | Interpreting the captured serial data |
| CSV Export | Preserving decoded information for further analysis |

## 3. Understanding UART Communication

Before analysing the capture, it is important to understand how UART works.

UART is an asynchronous serial communication protocol commonly used in embedded systems.

Unlike parallel communication, where multiple bits are transferred simultaneously, UART sends data one bit at a time over a serial connection.

A typical UART frame contains:

1. **Start bit:** Indicates the beginning of a data frame.
2. **Data bits:** Contains the transmitted information.
3. **Parity bit:** Optional error-detection information.
4. **Stop bit:** Indicates the end of the frame.

### 3.1 UART Frame Structure

For an 8-N-1 configuration, a frame contains:

| Component | Configuration |
|---|---|
| Start bit | 1 bit |
| Data bits | 8 bits |
| Parity | None |
| Stop bits | 1 bit |

The notation `8-N-1` means:

- 8 data bits
- N = No parity
- 1 stop bit

### 3.2 Baud Rate

The baud rate determines the signaling rate used for serial communication.

A decoder configured with an incorrect baud rate may produce unreadable characters, framing errors, or incorrect data.

Therefore, identifying the correct baud rate is an important part of UART analysis.

## 4. Investigation and Analysis

### 4.1 Opening the Logic Capture

The first step was to open the supplied `hw_debug.sal` file using Saleae Logic 2.

After loading the capture, the available digital channels could be examined.

A logic analyzer represents digital signals as transitions between logic LOW and logic HIGH states.

These transitions provide the timing information required to identify and decode serial communication.

### 4.2 Identifying the Serial Signal

The next step was to inspect the available channels and identify the signal carrying asynchronous serial communication.

UART communication can often be recognised by examining its characteristic start bits, data transitions, and idle state.

The selected signal was then used for protocol decoding.

### 4.3 Adding the Async Serial Analyzer

An Async Serial analyzer was added in Saleae Logic 2.

This analyzer interprets the captured digital waveform according to UART-style serial framing.

Instead of manually converting individual bits into characters, the protocol analyzer reconstructs the transmitted bytes.

This makes it easier to inspect the communication and identify meaningful output.

### 4.4 Configuring UART Parameters

The decoder was configured using the following settings recorded during the investigation:

| Parameter | Value |
|---|---|
| Protocol | Async Serial / UART |
| Baud rate | 115200 |
| Data bits | 8 |
| Parity | None |
| Stop bits | 1 |
| Format | 8-N-1 |

**Important:** The final working baud rate should be confirmed against the original capture and successful decoded output before treating this configuration as definitive.

Incorrect UART parameters can result in invalid decoded data.

### 4.5 Inspecting the Decoded Output

After configuring the analyzer, the decoded serial data was examined.

The objective was to identify readable information within the captured communication.

The decoded output provided the information required to reconstruct the challenge flag.

The analysis also demonstrated why protocol identification and correct decoder configuration are important when investigating raw digital signals.

### 4.6 Preserving the Decoded Data

The decoded information could be exported into CSV format for further inspection.

The investigation also used a CSV capture named:

```text
debug_output.csv
```

Preserving decoded data separately makes it easier to search, filter, compare, and document relevant information without repeatedly analysing the original waveform.

## 5. Findings and Flag Reconstruction

The UART analysis revealed several fragments of the challenge flag.

The recovered fragments were:

**Fragment 1:**

```text
HTB{
```

**Fragment 2:**

```text
547311173_
```

**Fragment 3:**

```text
n37w02k_
```

**Fragment 4:**

```text
c0mp20m153d}
```

The fragments were assembled in their original order to reconstruct the complete flag.

### Reconstructed Flag

```text
HTB{547311173_n37w02k_c0mp20m153d}
```

This was the final result of the investigation.

## 6. Technical Concepts Learned

### 6.1 Logic Analyzers

A logic analyzer is an instrument used to capture and inspect digital signals over time.

It helps engineers understand communication between electronic components and investigate problems involving digital interfaces.

### 6.2 UART Communication

UART is widely used in embedded systems for serial communication.

Understanding its framing structure makes it possible to interpret captured digital signals and recover transmitted information.

### 6.3 Serial Protocol Decoding

Protocol analyzers convert raw signal transitions into readable data.

Correct configuration is essential because the decoder relies on timing and framing parameters to interpret the captured communication.

### 6.4 Baud Rate Configuration

The baud rate determines the timing of serial communication.

An incorrect setting can cause corrupted or unreadable output.

### 6.5 CSV Data Analysis

Exporting decoded data into CSV format provides another way to inspect the recovered information.

It allows the output to be preserved and reviewed independently of the original logic capture.

## 7. Key Learnings

This challenge provided practical exposure to hardware debugging and digital communication analysis.

My major takeaways were:

- Understanding how logic analyzers capture digital signals.
- Learning how UART communication transfers data serially.
- Understanding the structure of an 8-N-1 UART frame.
- Learning how to configure an Async Serial analyzer in Saleae Logic 2.
- Recognising the importance of correct baud-rate configuration.
- Understanding how raw digital waveforms can be converted into readable information.
- Learning how decoded data can be exported and preserved for further investigation.

## 8. Conclusion

Debug demonstrated how digital communication captured from embedded hardware can be analysed to recover meaningful information.

By examining the supplied Saleae Logic capture, identifying UART communication, configuring a serial protocol analyzer, and inspecting the decoded output, I was able to reconstruct the challenge flag.

The challenge reinforced the importance of understanding low-level communication protocols and using the appropriate debugging tools when investigating embedded systems.

It also highlighted how information that is not immediately readable in a digital waveform can become understandable through correct protocol analysis.

---

## 9. Future Reference — Quick Revision

| Item | Details |
|---|---|
| Challenge | Debug |
| Platform | Hack The Box |
| Category | Hardware |
| Original capture | `hw_debug.sal` |
| Decoded output | `debug_output.csv` |
| Main tool | Saleae Logic 2 |
| Protocol | UART / Async Serial |
| Recorded baud rate | 115200 |
| Data bits | 8 |
| Parity | None |
| Stop bits | 1 |
| Format | 8-N-1 |
| Main technique | Logic analyzer and UART decoding |
| Final result | Challenge flag reconstructed |

## 10. Evidence and Reproducibility

Recommended evidence to preserve alongside this writeup:

```text
Debug/
├── README.md
├── evidence/
│   └── debug_output.csv
└── screenshots/
    ├── 01-original-logic-capture.png
    ├── 02-digital-signal-channels.png
    ├── 03-uart-analyzer-configuration.png
    ├── 04-decoded-uart-output.png
    └── 05-flag-reconstruction.png
```

**Reproduction checklist:**

- [ ] Keep the original `hw_debug.sal` capture.
- [ ] Record the selected digital channel.
- [ ] Record the verified baud rate.
- [ ] Record the UART framing configuration.
- [ ] Preserve the decoded CSV output.
- [ ] Capture screenshots of the successful decoding.
- [ ] Verify the reconstructed flag against the challenge.

These details will make it easier to reproduce the analysis and understand the solution when revisiting the challenge in the future.
