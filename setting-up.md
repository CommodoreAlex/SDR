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

### Setting Up Airspy SDR SHARP

#### Windows Setup

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

1. **Install Dependencies and Tools**
```bash
sudo apt install airspy-tools gnuradio # Debian/Ubuntu
```

1. **Test the Device Connection**

```bash
airspy_info
```

1. **Start Using GNU Radio**
    - **GNU Radio** is a powerful open-source toolkit for signal processing. It offers an extensive range of capabilities for SDR applications.
    - Launch **GNU Radio Companion** (GRC), which provides a graphical interface to design signal processing flowgraphs.
    - Create a new flowgraph and use the **RTL-SDR Source** or **Airspy Source** block to start receiving signals.
    - For more advanced configurations and visualizations, explore GNU Radio's built-in modules or add external blocks for custom needs.


---

## Exploring SDR Signal Visualization

- Use the **waterfall display** to identify signal patterns and frequencies.
- Adjust **gain settings** for better reception.
- Experiment with different **modulation types** (AM, FM, SSB, etc.) to hear various signals.

For a streamlined SDR setup, **DragonOS** is highly recommended, as it comes pre-installed with SDR tools like **GQRX, CubicSDR, GNURadio**, and more.
