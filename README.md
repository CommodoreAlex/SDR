# Exploring Software Defined Radios (SDR)

This project is designed as a learning experience for myself and others interested in working with SDR hardware and software tools to send, receive, and analyze wireless communication signals.

---
## **Table of Contents**

1. [Overview](#project-overview)
2. [Legal & Ethical Considerations](#legal-and-ethical-considerations)
3. [Required Hardware](#required-hardware)
4. [Required Software](#required-software)
5. [Introduction to SDR](#introduction-to-sdr)
6. [Setting Up SDR Hardware & Software](#setting-up-sdr-hardware-and-software)
7. [Receiving and Analyzing Signals](#receiving-and-analyzing-signals)
8. [Transmitting (Where Legally Permitted)](#transmitting-where-legally-permitted)
9. [Advanced Topics](#advanced-topics)
10. [Additional Learning Resources and Inspiration](#additional-learning-resources-and-inspiration)

---
### Project Overview

This repository provides resources, guides, and experiments using **Software Defined Radios (SDR)** such as **RTL-SDR** and software tools like **SDR# (SDR Sharp)** to explore and understand wireless communications.

 **Other learning objectives include:**
- Learn the fundamentals of Software Defined Radios
- Understand signal processing concepts
- Work with hardware like RTL-SDR to receive and decode signals
- Use software tools like SDR Sharp, GNU Radio, and other SDR applications
- Conduct hands-on experiments with real-world wireless signals
- Document findings and share knowledge with others

---
### Legal and Ethical Considerations

- Always adhere to local laws and regulations when working with SDR.
- Do not transmit on restricted frequencies without authorization.
- Respect privacy and ethical considerations when decoding signals.
- Do not attempt to decrypt any encrypted data received, unless given explicit permission to do so by the transmitter to avoid potential legal and LIKELY consequences. 

---
### Required Hardware

- **[RTL-SDR Dongle](https://www.amazon.com/RTL-SDR-Blog-RTL2832U-Software-Defined/dp/B0BMKZCKTF?th=1)** (or equivalent SDR hardware)
- **Antennas** (for different frequency ranges):
    - [Wideband Antenna Kit](https://www.amazon.com/dp/B07X2LJ4HB?ref=ppx_yo2ov_dt_b_fed_asin_title)
    - [Telescopic Antenna](https://www.amazon.com/dp/B091C5Y8T7?ref=ppx_yo2ov_dt_b_fed_asin_title)
- **Computer** (Windows/Linux/macOS) with USB support

---
###  Required Software

- **[SDR Sharp](https://airspy.com/download/)** (Windows-based SDR software)
- **[GNU Radio](https://www.gnuradio.org/)** (for advanced signal processing)
- **[GQRX](https://www.gqrx.dk/)** (Linux/macOS SDR application)
- **Virtual Audio Cable** (for piping audio signals)
- **Additional plugins for decoding digital signals****

---
### Introduction to SDR

- **[What is SDR?](https://en.wikipedia.org/wiki/Software-defined_radio) How does it work?**
- **[Understanding frequency bands](https://en.wikipedia.org/wiki/Frequency_allocation) and [modulation](https://en.wikipedia.org/wiki/Modulation)**

Learn more in [INTRODUCTION.md](introduction.md).

---
### Setting Up SDR Hardware & Software

- Installing drivers and setting up RTL-SDR
- Configuring SDR Sharp for first reception
- Exploring SDR signal visualization

Learn more in [SETTING-UP.md](setting-up.md).

---
### Receiving and Analyzing Signals

- **[FM Radio reception](https://en.wikipedia.org/wiki/FM_broadcasting)**
- **[Aircraft tracking with ADS-B](https://en.wikipedia.org/wiki/Automatic_dependent_surveillance_%E2%80%93_broadcast)**
- NOAA Weather Satellite decoding
- **[Digital modes: APRS](https://en.wikipedia.org/wiki/Automatic_Packet_Reporting_System), [POCSAG](https://en.wikipedia.org/wiki/POCSAG)**

Learn more in [RECEIVING.md](receiving.md).

---
### Transmitting (Where Legally Permitted)

- Basics of SDR-based transmission
- **[Licensing requirements and regulations](https://en.wikipedia.org/wiki/Federal_Communications_Commission)** (for U.S. users)
- Using HackRF / LimeSDR for transmission experiments

Learn more in [TRANSMITTING.md](transmitting.md).

---
### Advanced Topics

- Reverse engineering unknown signals
- **[Using GNU Radio for signal processing](https://en.wikipedia.org/wiki/GNU_Radio)**
- Security implications of SDR

Learn more in [ADVANCED.md](advanced.md).

---
## Additional Learning Resources and Inspiration

1. **Software Defined Radios Overview:**  
    Explore this insightful video by Random Teq, which provides an in-depth explanation of Software Defined Radios (SDRs) and visualizes many of the concepts discussed in this repository.  
    [Watch the video here](https://www.youtube.com/watch?v=3PIi_BFulzA&list=PLhBFZf0L5I7rwR6-8cEr4FntgLIF6CTSG&index=1)
    
2. **Engaging Lecture from BSides Cape Town:**  
    A memorable and engaging lecture by Gerard de Jong from BSides Cape Town, which stands out not only for its humor but also for making complex content accessible. This lecture is one of the key resources that influenced this repository’s approach.  
    [Watch the video here](https://www.youtube.com/watch?v=gMwciWchH3Q&list=PLhBFZf0L5I7rwR6-8cEr4FntgLIF6CTSG&index=2)
    
3. **Comprehensive Guide to SDR Hardware and Software:**  
    This informative video by Tech Minds covers a variety of hardware, receiver add-ons, antenna add-ons, and software that complement the SDR concepts explored in this repository.  
    [Watch the video here](https://www.youtube.com/watch?v=nB6XQSEFwVA&list=PLhBFZf0L5I7rwR6-8cEr4FntgLIF6CTSG&index=3)
	
4. **Great Scott Gadgets HackRF Lesson's by Michael Ossmann:**
	This instructional set of 11 lessons are very comprehensive, covering an entire outline of tactics, techniques, and procedures relating to SDRs and digital signals processing.
	[Watch the video here](https://www.youtube.com/watch?v=BeeSN14JUYU&list=PLu0BPYzTjiHru1KmPThmbY-8rRm3EWvUQ)

6. **DRAGON OS FOCAL - The Software Defined Radio Toolbox:**
	This video by Tech Minds presents Dragon OS Focal, an operating system that is configured to be an asset to your SDR and digital signals processing research. This operating system packs up many relevant tools for ease of use in one place.
	[Watch the video here](https://www.youtube.com/watch?v=lTBtlGGf5KE)

Feel free to explore more insightful lectures and tutorials for free on YouTube to deepen your understanding and stay inspired!

----
