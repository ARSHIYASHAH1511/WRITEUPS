@'

\# Debug - Hack The Box



\*\*Platform:\*\* Hack The Box  

\*\*Category:\*\* Hardware  

\*\*Challenge:\*\* Debug



\## 1. Overview



This challenge involved analyzing a digital logic capture to recover information transmitted through a serial communication interface.



The investigation focused on understanding the captured signals and decoding the UART communication.



\## 2. Tools Used



\- Saleae Logic 2

\- UART / Async Serial protocol analyzer

\- CSV output for decoded signal data



\## 3. Capture File



The original logic capture used during the investigation was:



`hw\_debug.sal`



The capture was examined in Saleae Logic 2.



\## 4. UART Configuration



The serial decoder was configured with the following settings:



| Parameter | Value |

|---|---|

| Protocol | Async Serial / UART |

| Baud rate | 115200 |

| Data bits | 8 |

| Parity | None |

| Stop bits | 1 |

| Format | 8-N-1 |



\## 5. Analysis Process



1\. Open the logic capture in Saleae Logic 2.

2\. Inspect the available digital signal channels.

3\. Identify the signal carrying serial communication.

4\. Add an Async Serial analyzer.

5\. Configure the decoder using the UART settings above.

6\. Inspect the decoded output.

7\. Export or preserve the decoded data for further analysis.



Add your actual channel selection, decoded output, and observations here.



\## 6. Findings



Document the decoded messages and explain how they contribute to solving the challenge.



\## 7. Flag



Add the verified challenge flag here after confirming it.



\## 8. Lessons Learned



\- Understanding asynchronous serial communication

\- Configuring UART protocol analyzers

\- Analyzing digital logic captures

\- Exporting and examining decoded serial data



\## 9. Evidence



Screenshots and supporting analysis files belong in the `screenshots` and `evidence` directories.

'@ | Set-Content -Encoding UTF8 "HTB\\Debug\\README.md"

