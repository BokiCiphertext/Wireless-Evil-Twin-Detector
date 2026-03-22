# Wireless-Evil-Twin-Detector
A python based Wireless Intrusion Detection System (WIDS) for identifying rogue access points.

### **How I Built It**
* **Language:** Python with the Scapy library.
* **Hardware:** Realtek 802.11n Adapter (WA04).
* **The Fix:** I resolved a virtualization error ('ioctl(SIOCGIFINDEX) failed') by configuring a custom USB Filter in virtualBox.

### **Usage**
1. Put card in Monitor Mode: 'sudo airmon-ng start wlan0'
2. Run script: 'sudo python3 evil_twin_detector.py'
