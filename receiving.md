# Table of Contents

1. [Legal Considerations for Signal Reception](#legal-considerations-for-signal-reception)
    - Can Listen To
    - Cannot Legally Listen To
2. [Configuring SDR Sharp (SDR#) for First Reception (Windows) and Capturing AM/FM Signals](#configuring-sdr-sharp-sdr-for-first-reception-windows-and-capturing-amfm-signals)
3. [Replicating the Same Actions in SDR Sharp with GNURadio Through Flowgraph Creation](#Replicating-the-Same-Actions-in-SDR-Sharp-with-GNURadio-Through-Flowgraph-Creation)
4. [Aircraft Tracking with ADS-B on Kali Linux](#aircraft-tracking-with-ads-b-on-kali-linux)
5. [Receiving and Decoding NOAA Weather Satellites, APRS, and POCSAG using SDRSharp](Receiving-and-Decoding-NOAA-Weather-Satellites,-APRS,-and-POCSAG-using-SDRSharp)

# Legal Considerations for Signal Reception

In this section, we will explore how to use an RTL-SDR to receive and analyze various types of signals. Here's a minimal breakdown of the bands your **RTL-SDR** can and **cannot** legally listen to:

#### ✅ Can Listen To:
- **Aviation Band (108 MHz – 137 MHz)**: Legal to listen to aircraft communications.
- **Amateur Radio Bands**: Legal to listen to (1.8 MHz to 1.9 MHz, 14 MHz to 14.35 MHz, etc.).
- **Emergency Services Bands (150 MHz – 174 MHz, 450 MHz – 470 MHz)**: Legal to listen to first responder communications.
- **Commercial Radio (AM 530 – 1700 kHz, FM 88 – 108 MHz)**: Legal to listen to public AM/FM radio stations.
- **CB Radio Band (27 MHz)**: Legal to listen to CB radio.
- **UHF and VHF Bands (300 MHz – 3 GHz)**: Legal to listen to private, business, and some public safety communications.
- **Broadcasting Bands**: Legal to listen to AM, FM, and TV broadcasts.
- **Wi-Fi and Bluetooth Bands (2.4 GHz – 5 GHz)**: Legal to listen to signals, but intercepting data may violate privacy laws.

#### ⚠️ Cannot Legally Listen To:
- **Military Frequencies (225 MHz – 400 MHz)**: Restricted, illegal to listen to most military communication.
- **Cellular Bands (700 MHz – 2.7 GHz)**: Illegal to listen to mobile phone communications due to privacy laws.
- **Encrypted/Private Communications**: Illegal to intercept encrypted or private signals.

Stay within legal bounds, especially regarding restricted or private bands.

---

## Configuring SDR Sharp (SDR#) for First Reception (Windows) and Capturing AM/FM Signals

1. Click on the hamburger symbol for a dropdown menu.
2. Go to Source and select the 'RTL-SDR USB'
3. Now you can start receiving signals

![image](https://github.com/user-attachments/assets/e05791c6-8fc2-4344-8fdf-1436294a372f)


When you click the play button on the top bar, the receiver will activate, producing a lot of noise (so be sure to lower the volume). You'll also see a waterfall display of incoming data:

![image](https://github.com/user-attachments/assets/062c544d-65d0-41f9-be4b-9d899e6c7515)


You can adjust the controls on the right, such as **Zoom**, **Contrast**, **Range**, and **Offset**, to fine-tune the display and help isolate a clearer signal. Each control allows you to optimize the view by adjusting the frequency range, contrast level, or shifting the signal for better clarity.

This was very interesting because I was able to tune into an FM radio station that was playing Imagine Dragons, haha:

![image](https://github.com/user-attachments/assets/b81d865a-836c-4d55-b0b4-cce71283c54b)


In **SDR#**, you can improve clarity by adjusting a few key settings. First, tweak the **RF Gain** and **IF Gain** to find the right balance—too high can cause distortion, too low can weaken the signal. Use **bandpass filters** to focus on the frequency range of interest and reduce unwanted noise.

For clearer audio, adjust the **audio volume** and, if needed, the **equalizer** to emphasize certain frequencies. The **Zoom** and **Contrast** on the waterfall help you focus on the signal visually, while adjusting the **Range** and **Offset** can help center the signal.

Lastly, ensure your antenna is properly positioned, as better placement can significantly improve signal reception.

In the bottom left corner, where I adjusted the RF Gain to 28dB, this gave me a really clear reading on the radio station (I removed the audio for content redistribution and fair-use reasons):

https://github.com/user-attachments/assets/aa65e024-1be1-41f7-9887-4f509ab55299

---

## Replicating the Same Actions in SDR Sharp with GNURadio Through Flowgraph Creation

⚠️ **Note:** Everything I am doing is configured with an RTL-SDR, which is significantly weaker than a HackRFOne device. The RTL-SDR has a more limited frequency range and lower power output, so using larger values for cutoff frequency and transition width might result in weaker signal strength or poor performance. It's important to adjust these settings according to the capabilities of your RTL-SDR hardware.

To start with naming our project, adding an author, if desired click the `Options` variable block that runs Python code to execute our flowgraphs and add in the following details for yourself if you want the aesthetic add-on.

You can do this by right-clicking and selecting properties, whenever we are editing a block you can double-click or follow that method for setting values on these blocks:

![image](https://github.com/user-attachments/assets/0bc8a94c-84da-45b3-860c-ef72829f444a)


See below for my changes:

![image](https://github.com/user-attachments/assets/904959f9-6d9e-49ee-a8c7-64dfe8ac66bc)


That will reflect in the graph later displaying a graph title, author, etc.

For the variable block in the graph named `samp_rate` change it's value to `2e6` (2 MHz):

![image](https://github.com/user-attachments/assets/6135f2c1-1214-4a4d-83f3-3a61100712c7)


Drag a variable block into the graph, name it `center_freq` and put that value to `104.5e6` (104.5 MHz):

![image](https://github.com/user-attachments/assets/b1cc0130-4056-4934-adec-1a01a9ee9fe5)


For actually connecting the RTL-SDR device to the GNU Radio software, we will proceed with the following -> Underneath `Sources` we want to take an `Osmocom Source`:

![image](https://github.com/user-attachments/assets/2b310929-7217-4dd5-95fb-051665985a37)


Key Features of the Osmocom Source Block:
- Acts as a receiver for **RTL-SDR and other supported SDRs**.
- Allows setting **frequency, sample rate, gain, and other parameters**.
- Provides real-time data from the SDR hardware to GNU Radio for further processing.

We are going to change the values to use our variables above and reduce the RF gain to zero:

![image](https://github.com/user-attachments/assets/e4d5e90c-6d21-4190-ae3e-c756c5fa0525)


Now we can add an (optional) low pass filter, the **Low-Pass Filter** removes high-frequency noise, allowing only lower-frequency signals to pass through, offering the following benefits:
- **Noise reduction**: Cleans up the signal by removing unwanted frequencies.
- **Clearer data**: Makes it easier to detect and decode relevant signals (e.g., FM radio).
- **Improved performance**: Enhances accuracy for analysis or decoding, like FM signal decoding.

![image](https://github.com/user-attachments/assets/5c38c0f1-cdc8-4e9e-b610-82b8bef4d7f2)


Notice we're making our first connection between blocks, we refer to these as digital signals. A digital signal is just a sequence of numbers that streams from one block to another.

We are going to setup the cutoff frequency as `100e3` (100 kHz) and the transition width to `10e3` (10 kHz):

![image](https://github.com/user-attachments/assets/c603c85c-9a62-47f0-9057-dbb7ab7389f2)


Now drag from the `Modulators` tab a `WBFM Receive` block and connect the low-pass filter to the WBFM Receive block:

![image](https://github.com/user-attachments/assets/be4036ce-bfe2-480d-a017-e578a56fa0d8)


For the **WBFM Receive** block, follow these settings:
1. **Quadrature Rate**: Set this to **`2e6` (2 MHz)**. This is the same as your sample rate from the **Osmocom Source**.
2. **Audio Decimation**: Set this to **`10`**. This is a common value to decimate the signal to an audio frequency range (48 kHz) after demodulation.

Now we will drag in an Audio Sink from `Audio` and connect it to the WBFM Receive block, then set the sample rate (as an integer `int`) to `48000`:

![image](https://github.com/user-attachments/assets/7e49b336-2df3-4f5e-bda9-feb342f2828f)


If the **Audio Sink** block is asking for an integer, you should enter **48000** (the sample rate in Hz, as an integer).

At this point we will add a `QT GUI Sink Block` from the `Instrumentation` > `QT` tab into our graph:

![image](https://github.com/user-attachments/assets/c4743d7a-3411-42fe-ad29-57971d41c499)


Connect the QT GUI Sink:
- Connect the output of the **WBFM Receive** block (after demodulating the FM signal) to the **QT GUI Sink** block. This allows you to visualize the FM audio signal.

Then you're going to set the `sample_rate` to `480000` to match the audio output, set the `center_frequency` to `center_freq` to match up, and change the `type` to float then click apply:

![image](https://github.com/user-attachments/assets/68f0bfa8-e988-4ac5-8505-ab03e488e25a)


⚠️ **Warning:** If you're hearing static or noise instead of a clear FM signal, it may be due to incorrect frequency, low signal strength, or improper filtering. Adjust the center frequency, low-pass filter, and gain settings until you achieve a clear audio output.

Now we can run the flowgraph by executing where `Run` is on the top navigation bar:

![image](https://github.com/user-attachments/assets/7601128c-5b91-4c36-8c23-977b8d04b62b)


When you run the flowgraph on the station `104.5 FM` you should hear whatever it has going on:

![image](https://github.com/user-attachments/assets/3a55f295-31fb-405e-bf4e-4f4bc10d126c)


You can also see the waterfall of the incoming data if you click other tabs:

![image](https://github.com/user-attachments/assets/9835bd9d-a489-4857-8b8c-b3289784c7ab)


We can add a volume slider to the reception graph by dragging and dropping the **QT GUI Range** block from the **QT GUI** tab. Then, adjust the following properties:
1. **Start**: This is the initial value of the slider (where it starts when you first run the flowgraph). Set it to `0.0` for mute (minimum volume).
2. **Stop**: This defines the maximum value of the slider. Set it to `2.0` for double the volume (maximum volume).
3. **Step**: This determines how much the slider adjusts with each tick. Set it to `0.1` for smoother volume control.

![image](https://github.com/user-attachments/assets/da4c12fb-a6d0-458b-a378-fd34a3af3353)


The **QT GUI Range** block by itself doesn't have connectors, because it's just a control element that adjusts values directly. To control the volume, we need to multiply the output audio signal by the value from the **QT GUI Range** block.

### Steps to Add Volume Control Using QT GUI Range:

1. **Add a Multiply Block**:
    - From the **Blocks** tab, drag the **Multiply Const** block (it's located in the **Math Operators** section).
    - This block will multiply the audio signal by the value from the **QT GUI Range**.
2. **Connect QT GUI Range to Multiply Block**:
    - The **QT GUI Range** block outputs a float value. Connect this output to the **constant** input of the **Multiply Const** block.
    - This will control the multiplication factor for the audio signal.

![image](https://github.com/user-attachments/assets/d851a224-b0d4-457b-808c-feed2ea98c1e)


 Connect the Blocks
1. **Connect the Output of Osmocom Source** to the **WBFM Receive** block.
2. **Connect the Output of WBFM Receive** to the **Multiply Const** block.
3. **Connect the Output of Multiply Const** to the **Audio Sink** block.

![image](https://github.com/user-attachments/assets/4d82ceb3-bbe9-42ed-a215-a078a6515159)


Now when we execute our flowgraph we have an audio slider:

![image](https://github.com/user-attachments/assets/a2990f6b-ee39-4217-afa4-8bd454f8f7dd)

As you can see, GNU Radio is quite different from tools like SDR Sharp, where everything is pre-built. In GNU Radio, you build the functionality yourself, giving you more control. While it takes more effort, this flexibility is powerful. As a next step, adding a frequency slider and an RF Gain slider would be beneficial for improving signal quality and further customizing the experience. This would allow for better tuning and a deeper understanding of how SDRs work.

---


## **Aircraft Tracking with ADS-B on Kali Linux**

In Kali Linux, we will use **dump1090**, which is a popular software to decode ADS-B signals. We will retrieve this from the GitHub page of the tool creator directly [GitHub](https://github.com/flightaware/dump1090):
```bash
git clone https://github.com/flightaware/dump1090.git
```

This is what you will receive when you clone that Git repo:

![image](https://github.com/user-attachments/assets/35b95a42-c168-4561-a76e-41ce003e8f67)


You should be able to build the installation locally by typing and submitting `make` in the terminal.

Then you can query the tool for help in order to see all switches:
```bash
┌──(root㉿kali)-[/home/kali/dump1090]
└─# ./dump1090 --help 
-----------------------------------------------------------------------------
| dump1090 ModeS Receiver                               dump1090-fa unknown |
| build options:                                                            |
-----------------------------------------------------------------------------
--device-type <type>     Select SDR type (default: none)

      ifile-specific options (use with --ifile)

--ifile <path>           read samples from given file ('-' for stdin)
--iformat <type>         set sample format (UC8, SC16, SC16Q11)
--throttle               process samples at the original capture speed
...
```


Now that **dump1090** is installed, you can start listening to **1090 MHz**, the frequency used by aircraft transmitting ADS-B signals. Tune your RTL-SDR to 1090 MHz (ADS-B Frequency).

1. **Connect your RTL-SDR** device to your Kali Linux machine.

2. Run **dump1090** to begin receiving and decoding ADS-B signals:
```bash
dump1090 --device-type rtl --gain -10 --lat <latitude> --lon <longitude> --interactive # You can omit latitude and longtitude
```

Explaining the command line arguments:
- **`--device-type rtl`**: Tells **dump1090** to use your RTL-SDR device.
- **`--gain -10`**: Sets the gain to a default value (you can adjust it if necessary).
- **`--lat <latitude>` and `--lon <longitude>`**: Sets your location to enhance accuracy (optional).
- **`--interactive`**: Opens an interactive mode that shows aircraft data in your terminal.

3. If you want to view the aircraft on a map in your browse locally, use the following command to enable a web interface to reach at your localhost with port 8080:
```bash
dump1090 --net --net-http-port 8080 --interactive
```

Once **dump1090** is running, you'll see a display with real-time aircraft data. The data includes:
- **Aircraft positions** (latitude and longitude).
- **Flight details** such as altitude, speed, and heading.
- A **live feed of aircraft** near you.
- The data is continuously updated, and if you are using the web interface, you'll see a real-time map.

You should be able to navigate to `http://localhost/dump1090/gmap.html` to see:

![image](https://github.com/user-attachments/assets/9d6ba3d4-7b86-420a-b6bb-a6a626cc4e7d)


Now you should have been able to successfully set up **ADS-B reception** on **Kali Linux** using **RTL-SDR**. You can now track aircraft in real-time, decode ADS-B signals, and visualize them on a map using **dump1090** or **Virtual Radar Server**.

This setup is ideal for beginners exploring software-defined radio (SDR) and aircraft tracking. As you gain more experience, you can experiment with additional configurations and features.


---

## Receiving and Decoding NOAA Weather Satellites, APRS, and POCSAG using SDRSharp


This section explains how to use **SDRSharp (SDR#)** with an **RTL-SDR** or similar software-defined radio to receive and decode data and provided demonstration videos:
- **NOAA Weather Satellites (APT)** – for weather images
- **APRS (Automatic Packet Reporting System)** – for amateur radio location and messaging
- **POCSAG (Pager Messages)** – for receiving pager transmissions

**Resources for NOAA, APRS, POCSAG:**
- [WXtoImg](https://wxtoimgrestored.xyz/)
- [Direwolf APRS Software](https://github.com/wb2osz/direwolf)
- [PDW Pager Decoder](http://www.g4hfq.co.uk/pdw/index.html)
- [Multimon-NG](https://github.com/EliasOenal/multimon-ng)
- [VB-Cable](https://vb-audio.com/Cable/)

---

## **1. NOAA Weather Satellites (APT) Decoding**

NOAA satellites transmit Automatic Picture Transmission (**APT**) signals at 137 MHz. These signals can be decoded into weather images.

See here for a video demonstration on the following task [Watch Video Here](https://www.youtube.com/watch?v=ACq0Kq5rVU4)

**Requirements**
    - **SDRSharp** (for signal reception)
    - **WXtoImg** (for decoding weather images)
    - **VB-Cable** (to route audio from SDR# to WXtoImg)

**What is VB-Cable?**

**VB-Cable** is a virtual audio cable that allows you to route audio from one application to another. In this setup, it is used to send the received NOAA APT audio from **SDRSharp** to **WXtoImg** for decoding.

**Setup & Steps**:
1. Open **SDRSharp** and configure:
    - **Mode**: WFM (Wide FM)
    - **Bandwidth**: 30-40 kHz
    - **Frequency**:
        - **NOAA 15** → 137.62 MHz
        - **NOAA 18** → 137.91 MHz
        - **NOAA 19** → 137.10 MHz
    - Enable **Correct IQ** (if using RTL-SDR)
2. Install and configure **VB-Cable**:
    - Set SDRSharp’s audio output to **VB-Cable Input**.
    - In WXtoImg, set the audio input to **VB-Cable Output**.
3. In **WXtoImg**, enable **Auto Processing** and wait for a satellite pass.
4. Once a satellite passes, WXtoImg will generate a weather image.

Receiving **NOAA Weather Satellites (APT)** transmissions **requires timing** because the satellites **move in polar orbits** and are only overhead for a limited time during each pass.

**How to Time a Satellite Pass**

1. **Use a Satellite Tracking Tool**:
    - Websites: [Heavens Above](https://www.heavens-above.com/), [N2YO](https://www.n2yo.com/)
    - Software: **Gpredict** (Linux/Windows), **Orbitron**
    - Mobile Apps: **ISS Detector**, **SatSat**
2. **Find Your Next Pass**:
    - Enter your **location (latitude/longitude)** into the tracker.
    - Check for NOAA **15, 18, or 19** satellites.
    - Look for a pass with **high elevation** (preferably 30°+ for good reception).
3. **Be Ready at the Right Time**:
    - Passes usually last **10-15 minutes**.
    - Start listening **a few minutes before AOS (Acquisition of Signal)**.
    - End when the satellite moves below the horizon (**LOS - Loss of Signal**).

**Why Timing Matters**
- The **satellite constantly moves**, so you need to track when it's **above your location**.
- If you try to receive signals when it’s below the horizon, you won’t get anything.
- Higher passes provide **better signal strength** and **clearer images**.

---

## **2. APRS (Automatic Packet Reporting System) Decoding**

APRS is a digital communication protocol for real-time information sharing over amateur radio.

See here for a video demonstration on the following task [Watch Video Here](https://www.youtube.com/watch?v=CfnrrJwwNU8) using RTL_FM and Multimon-ng on a Linux operating system.

**Requirements**
    - **SDRSharp** (to receive signals)
    - **Direwolf** or **Multimon-NG** (for decoding APRS packets)
    - **VB-Cable** (to route audio from SDR# to decoder)

**What is VB-Cable’s Role?**

VB-Cable acts as a bridge to transfer received APRS audio from **SDRSharp** to **Direwolf** or **Multimon-NG**, which then decode the APRS packets.

Steps for an alternative method using Direwolf:
1. Open **SDRSharp** and configure:
    - **Mode**: NFM (Narrow FM)
    - **Bandwidth**: 12-15 kHz
    - **Frequency**: 144.39 MHz (North America APRS frequency)
2. Install and configure **VB-Cable**:
    - Set SDRSharp’s audio output to **VB-Cable Input**.
    - In Direwolf, configure the audio input to **VB-Cable Output**.
3. Run the following command in **Direwolf**:
```bash
direwolf -c sdr.conf -r 48000
```

The software will start decoding **APRS messages** (e.g., GPS locations, weather reports).

---

## **3. POCSAG (Pager) Decoding**

POCSAG is a digital paging protocol used in many regions to send pager messages.

See here for a video demonstration on the following task [Watch Video Here](https://www.youtube.com/watch?v=A2v1IIVqnZk) provided by Tech Minds to walk you through it.

**Requirements**
    - **SDRSharp** (to receive signals)
    - **PDW (Windows)** or **Multimon-NG (Linux)** (for decoding POCSAG)
    - **VB-Cable** (to route audio from SDR# to decoder)

**How VB-Cable is Used**

VB-Cable is used to send the received POCSAG signal audio from **SDRSharp** to **PDW or Multimon-NG**, which then decode the messages.

**Setup & Steps**:
1. Open **SDRSharp** and configure:
    - **Mode**: NFM (Narrow FM)
    - **Bandwidth**: 12.5 kHz
    - **Frequency**: Scan **152-165 MHz** for active pager signals.
2. Install and configure **VB-Cable**:
    - Set SDRSharp’s audio output to **VB-Cable Input**.
    - In PDW or Multimon-NG, configure the audio input to **VB-Cable Output**.
3. In **PDW**, set **Signal Input** to **Soundcard** and adjust settings.
4. The decoder will start displaying pager messages in real-time.

---


