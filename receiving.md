# Receiving and Analyzing Signals

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

## ## **Aircraft Tracking with ADS-B on Kali Linux**

 **Step-by-Step Guide for Setting Up ADS-B Reception:**

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


