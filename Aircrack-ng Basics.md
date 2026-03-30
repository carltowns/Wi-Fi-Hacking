# Aircrack-ng Essentials

## AIRMON-NG

**Purpose:**
Enable/disable monitor mode on wireless interfaces.

### Basic Usage

* Show interface info:

kali@kali:~$ sudo airmon-ng

### Check for Interfering Processes

* List interfering services (e.g., NetworkManager):

kali@kali:~$ sudo airmon-ng check

* Stop/kill interfering processes:

kali@kali:~$ sudo airmon-ng check kill

### Start Monitor Mode

* Enable monitor mode:

kali@kali:~$ sudo airmon-ng start wlan0

* Start on a specific channel:

kali@kali:~$ sudo airmon-ng start wlan0 6


### Verify Monitor Mode

* Using `iw` (recommended):

kali@kali:~$ sudo iw dev wlan0mon info

* Using `iwconfig` (deprecated, less reliable):

kali@kali:~$ sudo iwconfig wlan0mon


### Debug / Verbose Output

* Verbose:

kali@kali:~$ sudo airmon-ng --verbose

* Debug:

kali@kali:~$ sudo airmon-ng --debug


### Stop Monitor Mode

kali@kali:~$ sudo airmon-ng stop wlan0mon

---

## AIRODUMP-NG

**Purpose:**
Capture and analyze wireless packets.

### Basic Usage

kali@kali:~$ sudo airodump-ng

### Sniffing Traffic

* Capture on a specific channel:

kali@kali:~$ sudo airodump-ng wlan0mon -c 6

### Targeted Capture

* Capture a specific AP and save output:

kali@kali:~$ sudo airodump-ng -c 3 --bssid 34:08:04:09:3D:38 -w cap1 wlan0mon

---

## AIREPLAY-NG

**Purpose:**
Packet injection and testing.

### Injection Test

* Set interface channel first:

kali@kali:~$ sudo airmon-ng start wlan0 3

* Run basic injection test:

kali@kali:~$ sudo aireplay-ng -9 wlan0mon

### Targeted Injection

* Against specific ESSID and BSSID:

kali@kali:~$ sudo aireplay-ng -9 -e wifissid -a 34:08:04:09:3D:38 wlan0mon

* Using another interface:

kali@kali:~$ sudo aireplay-ng -9 -i wlan1mon wlan0mon


---

## AIRCRACK-NG

**Purpose:**
Password cracking and performance testing.

### Benchmark Mode

kali@kali:~$ aircrack-ng -S

---

## AIRDECAP-NG

**Purpose:**
Remove wireless headers from capture files and filter out additional APs from the capture.

### Example

kali@kali:~$ sudo airdecap-ng -b 34:08:04:09:3D:38 testnet-01.cap

---

## AIRGRAPH-NG

**Purpose:**
Visualize wireless networks and client relationships.

### Setup

kali@kali:~$ mkdir graph
kali@kali:~$ cd graph
kali@kali:~$ wget http://standards-oui.ieee.org/oui.txt
kali@kali:~$ cd ..

### Graph Types

#### Clients-to-AP Relationship (CAPR)

* Shows client ↔ AP relationships
* Color codes:

  * Green = WPA
  * Yellow = WEP
  * Red = Open
  * Black = Unknown

kali@kali:~$ airgraph-ng -o Picture1.png -i dump-01.csv -g CAPR


#### Client Probe Graph (CPG)

* Shows client ↔ probed networks

kali@kali:~$ airgraph-ng -o Picture2.png -i dump-01.csv -g CPG

---

## EXTRA COMMAND

* Save capture in CSV format:

kali@kali:~$ airodump-ng -w test21MAR --output-format csv wlan0mon
