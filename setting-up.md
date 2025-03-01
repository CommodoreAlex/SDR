# Setting Up SDR Hardware & Software

### Choosing an Operating System

For the best SDR experience, consider using an SDR-focused Linux distribution:

- **DragonOS** – A pre-configured Linux distro with SDR tools (recommended).
- **[Kali Linux](https://www.kali.org/)** – Includes `rtl-sdr` and other RF analysis tools.
- **[Pentoo](https://www.pentoo.ch/)** – A security-focused distro with SDR utilities.

If using Windows, follow the steps below for manual setup.

---

###  Setting Up SDR Hardware

To begin with SDR, you'll need the following hardware components:

|Component|Description|
|---|---|
|**RTL-SDR USB Dongle**|A low-cost software-defined radio receiver.|
|**Antenna**|Required to capture signals; varies by frequency range.|
|**USB Extension Cable**|Reduces interference by distancing the dongle from the computer.|
|**Filters (optional)**|Helps remove unwanted signals from strong nearby transmitters.|

 **Hardware Setup Steps**
1. **Connect the RTL-SDR or Airspy SDR to your computer’s USB port.**
2. **Attach the antenna** to the SDR dongle.
    - For better reception, consider using an external or rooftop antenna.
3. **Use a USB extension cable** to minimize electrical noise interference.
4. **Optional: Use a band-pass filter** if you’re in an area with strong interfering signals.

See what the device prior to connection to a computer looks like when completely built out:

![image](https://github.com/user-attachments/assets/9833faa8-5049-4e90-91d6-f89ae7f36ac3)


---

### Windows Setup using SDR Sharp

For a full video demonstration see this video: [Demonstration by Random Teq](https://www.youtube.com/watch?v=3PIi_BFulzA&list=PLhBFZf0L5I7rwR6-8cEr4FntgLIF6CTSG)

Download the **Airspy SDR# Software** from [Airspy’s website](https://airspy.com/download/):

![image](https://github.com/user-attachments/assets/91eb5998-1462-4b2a-a23b-e40281f89cca)


Unzip the contents of the folder to preferred location:

![image](https://github.com/user-attachments/assets/26646024-0daa-4411-b496-ad40dd3d4dff)


Click on `install-rtlsdr.bat` and waive Windows SmartScreen if necessary:

![image](https://github.com/user-attachments/assets/2ae80f23-6189-460d-81fd-b9973436f672)

You will be seeing a Windows command prompt appear:

![image](https://github.com/user-attachments/assets/1e7f4461-94d0-401e-a765-66a4975aa3e0)


You will notice that the file `zadig` appears inside of this Window. You want to click it:

![image](https://github.com/user-attachments/assets/2808d6de-cb98-4733-9593-cfa405020cdd)

Once you start the `zadig` application a Window will appear. You should now connect the USB device to your computer, where it will populate in the Window as `Bulk-In, Interface (Interface 0)`:

![image](https://github.com/user-attachments/assets/7914fd47-0b76-41e3-baa0-17df2da8373a)


If you go to Options > List All Devices: you will see a bunch of devices you could theoretically choose. We are going to ensure we're using our device.

**At this point we should click on 'Install Driver'.** Then you can close this application:

![image](https://github.com/user-attachments/assets/03384adb-6c06-4379-bf96-da320c5b43a3)


At this point go and open the SDRSharp application from within your file explorer window.

You may be required to install `dotnet8` or `dotnet9` at this time from: [Dotnet8](https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-desktop-8.0.13-windows-x86-installer?cid=getdotnetcore)

Then when you open the application you will see the following window:

![image](https://github.com/user-attachments/assets/10d9a6f4-12fd-4f56-84a1-3435f5d78495)

If you're going to be using Windows, your setup is now complete and we will configure for first-reception in the next file. 

If you're intending on using BOTH, continue on the Linux side to install GNURadio. That tool will come up later.

---

#### **Linux Setup (Using GNU Radio)**

**GNU Radio** is an open-source **software-defined radio (SDR) framework** that provides a collection of signal processing blocks for implementing radio systems. It allows users to design, simulate, and deploy real-world wireless communication applications using **software instead of dedicated hardware**.

 **Key Features:**
- **Graphical Interface (GRC):** GNU Radio Companion (GRC) provides a drag-and-drop interface for building SDR applications without coding.
- **Python & C++ Support:** You can develop signal processing applications programmatically in Python or C++.
- **Wide Hardware Support:** Works with SDR devices like **RTL-SDR, HackRF, USRP, BladeRF, Airspy**, and more.
- **Real-time Signal Processing:** Used for radio communications, radar, satellite signals, and even security research.
- **Extensible & Modular:** Includes built-in DSP (digital signal processing) blocks, but you can create custom ones.

 **Common Use Cases:**
- Signal analysis and demodulation
- Wireless protocol development (AM/FM, GSM, LTE, etc.)
- Spectrum monitoring and radio astronomy
- Amateur radio experiments
- Reverse engineering wireless signals

**Install Dependencies and Tools [Wiki for GNURadio](https://wiki.gnuradio.org/index.php/InstallingGR)**
```bash
sudo apt-get update
sudo apt-get install gnuradio
```

You can start GNU Radio from the command line with:
```bash
gnuradio-companion
```

This is the application we'll be using for the Linux side of receiving information with these SDRs:

![image](https://github.com/user-attachments/assets/21cef109-7a85-46b2-9a0d-46a70a75f35b)


**Test the Device Connection** with `rtl_test`:
```bash
sudo apt install rtl-sdr -y
rtl_test
```

When you use **`rtl_test`** with **GNU Radio**, it serves as a utility to gather and display information about the connected **RTL-SDR** device. Essentially, it helps you verify that the **RTL-SDR hardware** is correctly recognized and provides key details that may be useful for your radio system configuration in GNU Radio.

**What `rtl_test` Does in the GNU Radio Context:**
1. **Detects RTL-SDR Devices:**
    - It checks if your RTL-SDR device is connected and accessible by the system.
2. **Displays Hardware Information:**
    - Lists important data such as:
        - **Model** (e.g., RTL-SDR v3)
        - **Serial number** (if available)
3. **Helpful for Troubleshooting:**
    - If your RTL-SDR device isn't behaving as expected in GNU Radio, running `rtl_test` gives you quick feedback to ensure it's properly connected and detected by your system. This helps confirm if there are any issues with the device or the drivers.

**How It Relates to GNU Radio:**
- After confirming the device's status via `rtl_test`, you can confidently use it within **GNU Radio** for signal processing tasks. The blocks within GNU Radio (such as the **RTL-SDR source block**) will rely on this confirmation to interact with the hardware, enabling you to process SDR signals in real time.

Running `rtl_test` should give an output like:
```bash
Found 1 device(s):
  0: Realtek RTL2838UHIDIR (USB)
     - Sample Rate Range: 1.024 MHz to 3.2 MHz
     - Serial Number: 00000001
```

This confirms that the RTL-SDR device is ready for use in GNU Radio.

---

