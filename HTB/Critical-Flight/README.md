# Critical Flight — Hack The Box Write-up

**Platform:** Hack The Box — CTF Try Out  
**Category:** Hardware  
**Challenge:** Critical Flight  
**Difficulty:** Very Easy  
**Focus:** PCB Analysis, Gerber Files, Hardware Reverse Engineering

---

## 1. Challenge Overview

Critical Flight is a hardware security challenge that introduces the analysis of printed circuit board (PCB) design files.

A PCB provides the physical electrical connections between components in an electronic system. These connections are represented through conductive copper traces, pads, and other structures distributed across different board layers.

In multilayer PCB designs, the complete circuit cannot always be understood by examining a single layer. Internal copper layers can contain routing information that is not visible from the top or bottom of the board.

This challenge involves inspecting Gerber files associated with a PCB design, examining relevant copper layers, and recovering information concealed within the board's design.

The primary objective was to investigate the supplied hardware design files and reconstruct the challenge flag.

## 2. Understanding the Challenge Materials

### 2.1 Provided Files

The challenge archive was:

```text
hw_critical_flight.zip
```

The archive contained Gerber files associated with the `HadesMicro` PCB design.

Gerber files are widely used in PCB manufacturing. They describe individual layers of a circuit board using graphical primitives such as lines, flashes, and regions.

Different Gerber files represent different aspects of the board, including:

- Copper layers
- Solder mask layers
- Silkscreen layers
- Board outlines
- Internal copper routing

### 2.2 Important Gerber Files

Two files were particularly relevant during the investigation:

| File | Layer | Purpose |
|---|---|---|
| `HadesMicro-B_Cu.gbr` | Bottom Copper | Represents conductive features on the bottom copper layer |
| `HadesMicro-In1_Cu.gbr` | Internal Copper 1 | Represents conductive features on an internal PCB layer |

**Why are these layers important?**

A multilayer PCB can distribute electrical connections across several copper layers.

The bottom copper layer represents routing on the underside of the board, while an internal copper layer represents conductive structures inside the PCB.

Examining these layers independently can reveal information that may be difficult to recognise when looking at the board as a single image.

## 3. Tools and Techniques

The investigation involved the following concepts and techniques:

### 3.1 Gerber File Inspection

Gerber files were examined to understand the board's graphical structure and identify relevant copper-layer information.

### 3.2 PCB Layer Analysis

Individual copper layers were treated as separate sources of information rather than assuming that the complete board could be understood from one view.

### 3.3 Copper Trace Examination

Copper traces represent electrical connections between different parts of a PCB.

Examining their arrangement can help identify routing patterns and unusual structures.

### 3.4 Hardware Reverse Engineering

Hardware reverse engineering involves studying an existing electronic design to understand its structure, behaviour, and implementation.

In this challenge, the focus was on interpreting PCB design artifacts rather than analysing a running software application.

## 4. Investigation and Analysis

### 4.1 Extracting the Challenge Archive

The first step was to obtain the supplied challenge archive:

```text
hw_critical_flight.zip
```

The archive contained the Gerber files required for the investigation.

The files were identified by their names and layer designations.

### 4.2 Identifying the Relevant Layers

After examining the available Gerber files, attention was focused on:

```text
HadesMicro-B_Cu.gbr
HadesMicro-In1_Cu.gbr
```

The file naming convention was useful in understanding the layer assignments:

- `B_Cu` refers to bottom copper.
- `In1_Cu` refers to internal copper layer 1.

These layers were examined separately to investigate the information represented in each.

### 4.3 Examining the Bottom Copper Layer

The first relevant file was:

```text
HadesMicro-B_Cu.gbr
```

This file represents the bottom copper layer of the PCB.

The layer was inspected for relevant graphical information and patterns.

The investigation recovered the following flag fragment:

```text
HTB{533_7h3_1nn32_w02k1n95
```

This fragment represented the first part of the challenge flag.

### 4.4 Examining the Internal Copper Layer

The second relevant file was:

```text
HadesMicro-In1_Cu.gbr
```

This file represents the first internal copper layer.

The layer was examined independently to identify the remaining information.

The following fragment was recovered:

```text
_0f_313c720n1c5#$@}
```

This fragment contained the remaining part of the flag.

### 4.5 Reconstructing the Flag

The two recovered fragments were combined in their original order.

**Fragment 1 — Bottom Copper:**

```text
HTB{533_7h3_1nn32_w02k1n95
```

**Fragment 2 — Internal Copper 1:**

```text
_0f_313c720n1c5#$@}
```

Combining both fragments produced the complete challenge flag.

This was the key finding of the investigation.

## 5. Technical Explanation

### 5.1 What Are Gerber Files?

Gerber is a standard format used to communicate PCB manufacturing information.

A Gerber file describes a two-dimensional representation of a particular PCB layer.

It can contain graphical instructions representing:

- Lines and tracks
- Circular pads
- Copper regions
- Apertures
- Other manufacturing features

A PCB design typically consists of several individual Gerber files, each corresponding to a particular layer.

### 5.2 Why Inspect Individual Copper Layers?

Multilayer PCBs contain conductive structures on different physical layers.

Some connections are routed on the outer surfaces, while others are placed inside the board.

Looking at the complete PCB may make certain patterns difficult to distinguish.

Inspecting each layer separately allows an investigator to:

1. Understand the physical arrangement of conductive features.
2. Identify unusual routing patterns.
3. Examine individual copper structures.
4. Compare information across multiple layers.
5. Investigate patterns that may not be obvious in a combined representation.

### 5.3 Hardware Reverse Engineering Perspective

This challenge demonstrates that hardware design files are useful sources of information during security investigations.

Even without interacting with a physical circuit board, it is possible to examine its design artifacts and recover information represented within its layout.

This is an important aspect of hardware forensics and reverse engineering.

## 6. Final Flag

**Challenge:** Critical Flight

**Status:** Successfully solved

```text
HTB{533_7h3_1nn32_w02k1n95_0f_313c720n1c5#$@}
```

## 7. Key Learnings

This challenge helped reinforce several important hardware security concepts.

### Technical Learnings

- Understanding the purpose and structure of Gerber files.
- Identifying PCB layers using their file naming conventions.
- Understanding the difference between bottom and internal copper layers.
- Examining PCB design artifacts independently.
- Recognising the importance of copper routing during hardware analysis.
- Recovering information distributed across multiple hardware design layers.

### Security Learnings

- Hardware design files can contain information relevant to security investigations.
- Analysing individual PCB layers can reveal details that are not immediately obvious.
- Hardware reverse engineering is not limited to physical devices; design files can also provide valuable evidence.
- Understanding the underlying hardware implementation is an important part of a broader security assessment.

## 8. Conclusion

Critical Flight provided practical
