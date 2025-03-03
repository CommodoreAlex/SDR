# Exploring Software Defined Radios (SDR)

This project is designed as a learning experience for myself and others interested in working with **SDR hardware** and **software tools** to send, receive, and analyze wireless communication signals, particularly with the **RTL-SDR** device. We will explore the use of **SDR Sharp (SDR#)**, **GNU Radio**, and other software tools, each tailored for specific use cases outlined in this repository.

---
## **Table of Contents**

1. [Introduction to SDR](introduction.md)
2. [Setting Up SDR Hardware & Software](setting-up.md)
3. [Receiving and Analyzing Signals](receiving.md)
4. [Transmitting (Where Legally Permitted)](transmitting.md)

---
### Project Overview

This repository provides resources, guides, and experiments using **Software Defined Radios (SDR)** such as **RTL-SDR** along with software tools like **SDR Sharp (SDR#)**, **GNU Radio**, and other SDR applications. These tools help explore and understand wireless communications from a practical standpoint.

**Other learning objectives include:**
- Learn the fundamentals of Software Defined Radios
- Understand signal processing concepts and their applications
- Work hands-on with RTL-SDR hardware to receive and decode real-world signals
- Use tools like SDR Sharp, GNU Radio, and more for signal visualization and processing
- Engage in various wireless communication experiments and share findings

---
### Legal and Ethical Considerations

- Always adhere to local laws and regulations when working with SDR.
- Do not transmit on restricted frequencies without authorization.
- Respect privacy and ethical considerations when decoding signals.

---
### Required Hardware

- **[RTL-SDR Dongle](https://www.amazon.com/RTL-SDR-Blog-RTL2832U-Software-Defined/dp/B0BMKZCKTF?th=1)** (or equivalent SDR hardware)
- **Antennas** (for different frequency ranges):
    - [Wideband Antenna Kit](https://www.amazon.com/dp/B07X2LJ4HB?ref=ppx_yo2ov_dt_b_fed_asin_title)
    - [Telescopic Antenna](https://www.amazon.com/dp/B091C5Y8T7?ref=ppx_yo2ov_dt_b_fed_asin_title)
- **Computer** (Windows/Linux) with USB support

---
###  Required Software

- **[SDR Sharp](https://airspy.com/download/)** (Windows-based SDR software)
- **[GNU Radio](https://www.gnuradio.org/)** (for advanced signal processing)
- **Virtual Audio Cable** (for piping audio signals)
- **Additional plugins for decoding digital signals****

---
### Introduction to SDR

- **[What is SDR?](https://en.wikipedia.org/wiki/Software-defined_radio) How does it work?**
- **[Understanding frequency bands](https://en.wikipedia.org/wiki/Frequency_allocation) and [modulation](https://en.wikipedia.org/wiki/Modulation)**
- Key components of an SDR setup (RTL-SDR, antennas, adapters)
- Cost breakdown of your SDR components
- Signal strength concepts (modulation techniques, decibels, SNR)

Learn more in [INTRODUCTION.md](introduction.md).

---
### Setting Up SDR Hardware & Software

- Learn about SDR-relevant operating systems
- Setting up SDR Sharp and drivers (Airspy) for use in Windows
- Setting up GNU Radio for use in Linux and running `rtl_test`

Learn more in [SETTING-UP.md](setting-up.md).

---
### Receiving and Analyzing Signals

- **[AM/FM Radio reception](https://en.wikipedia.org/wiki/FM_broadcasting)**
- **[Aircraft tracking with ADS-B](https://en.wikipedia.org/wiki/Automatic_dependent_surveillance_%E2%80%93_broadcast)**
- NOAA Weather Satellite decoding
- **[Digital modes: APRS](https://en.wikipedia.org/wiki/Automatic_Packet_Reporting_System), [POCSAG](https://en.wikipedia.org/wiki/POCSAG)**

Learn more in [RECEIVING.md](receiving.md).

---
### Transmitting (Where Legally Permitted)

- Basics of SDR-based transmission
- **[Licensing requirements and regulations](https://en.wikipedia.org/wiki/Federal_Communications_Commission)** (for U.S. users)
- Discussion of theory regarding transmission with HackRF / LimeSDR

Learn more in [TRANSMITTING.md](transmitting.md).

---
## Additional Learning Resources and Inspiration

1. **Software Defined Radios Overview:**  
    Explore this insightful video by Random Teq, which provides an in-depth explanation of Software Defined Radios (SDRs) and visualizes many of the concepts discussed in this repository.
   
    [Watch the video here](https://www.youtube.com/watch?v=3PIi_BFulzA&list=PLhBFZf0L5I7rwR6-8cEr4FntgLIF6CTSG&index=1)
    
3. **Engaging Lecture from BSides Cape Town:**  
    A memorable and engaging lecture by Gerard de Jong from BSides Cape Town, which stands out not only for its humor but also for making complex content accessible. This lecture is one of the key resources that influenced this repository’s approach.
   
    [Watch the video here](https://www.youtube.com/watch?v=gMwciWchH3Q&list=PLhBFZf0L5I7rwR6-8cEr4FntgLIF6CTSG&index=2)
    
4. **Comprehensive Guide to SDR Hardware and Software:**  
    This informative video by Tech Minds covers a variety of hardware, receiver add-ons, antenna add-ons, and software that complement the SDR concepts explored in this repository.
   
    [Watch the video here](https://www.youtube.com/watch?v=nB6XQSEFwVA&list=PLhBFZf0L5I7rwR6-8cEr4FntgLIF6CTSG&index=3)

5. **Great Scott Gadgets HackRF Lesson's by Michael Ossmann:** This instructional set of 11 lessons are very comprehensive, covering an entire outline of tactics, techniques, and procedures relating to SDRs and digital signals processing.

    [Watch the video here](https://www.youtube.com/watch?v=BeeSN14JUYU&list=PLu0BPYzTjiHru1KmPThmbY-8rRm3EWvUQ)

6. **DRAGON OS FOCAL - The Software Defined Radio Toolbox:** This video by Tech Minds presents Dragon OS Focal, an operating system that is configured to be an asset to your SDR and digital signals processing research. This operating system packs up many relevant tools for ease of use in one place.
   
    [Watch the video here](https://www.youtube.com/watch?v=lTBtlGGf5KE)

Feel free to explore more insightful lectures and tutorials for free on YouTube to deepen your understanding and stay inspired!

----
