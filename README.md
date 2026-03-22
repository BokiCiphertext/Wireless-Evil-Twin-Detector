# Wireless-Evil-Twin-Detector
A python based Wireless Intrusion Detection System (WIDS) for identifying rogue access points.

### **How I Built It**
* **Language:** Python with the Scapy library.
* **Hardware:** Realtek 802.11n Adapter (WA04).
* **The Fix:** I resolved a virtualization error ('ioctl(SIOCGIFINDEX) failed') by configuring a custom USB Filter in virtualBox.

### **Usage**
1. Put card in Monitor Mode: 'sudo airmon-ng start wlan0'
2. Run script: 'sudo python3 evil_twin_detector.py'

### **Python Code**

from scapy.all import *

seen_wifi = {}

def find_evil_twin(packet):
    if packet.haslayer(Dot11Beacon):
        
        name = packet[Dot11Elt].info.decode(errors="ignore")
        mac_address = packet[Dot11].addr2

        if name not in seen_wifi:
            seen_wifi[name] = mac_address
            print(f"[+] Found New WiFi: {name} (MAC: {mac_address})")
        
        else:
            if seen_wifi[name] != mac_address:
                print(f"\n[!!!] ALERT: EVIL TWIN DETECTED!")
                print(f"The WiFi '{name}' is being broadcast by two different devices!")
                print(f"First MAC: {seen_wifi[name]}")
                print(f"Second (Suspicious) MAC: {mac_address}\n")
                
print("--- Scanning for Evil Twins... Press Ctrl+C to stop ---")
sniff(iface="wlan0", prn=find_evil_twin, store=0)
