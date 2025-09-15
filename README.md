# UC-AV-QOS-Automated
Real-Time, Multi-Vendor UC/AV Network QoS Automation for Cisco & Netgear Switches



# Real-Time Multi-Vendor UC/AV Network QoS Automation

Real-Time, Multi-Vendor UC/AV Network QoS Automation for Cisco & Netgear Switches. Monitors NVX, Biamp, Q-SYS, Teams, Zoom, AVB, and Multicast traffic and applies QoS dynamically. Logs metrics automatically for auditing and optimization.

---

## Overview

This Python script automates **Quality of Service (QoS) management** for audio/video and unified communications (UC) networks. It is designed for **live, production-ready deployments** across both **Cisco and Netgear switches**.

### Key Features

* Real-time detection of UC/AV traffic: **NVX, Biamp, Q-SYS, Teams, Zoom**
* Supports **AVB and Multicast streams**
* Fully dynamic **QoS application/removal** on Cisco and Netgear switches (via CLI or SNMP)
* Multi-threaded polling for **simultaneous device detection**
* Automatic logging of metrics to **CSV for auditing and historical analysis**
* User-friendly interactive setup (one-time configuration)
* Exception handling for stable operation in production
* Fully auto-installs required Python packages:

  * `netmiko`, `requests`, `rich`, `getpass`, `argparse`, `msal`, `scapy`, `pysnmp`, `pandas`

---

## Supported Devices

| Device / Protocol     | Detection Method                  | QoS Support       |
| --------------------- | --------------------------------- | ----------------- |
| NVX (Crestron)        | XiO Cloud API                     | Cisco/Netgear     |
| Biamp (Tesira/Devio)  | REST API                          | Cisco/Netgear     |
| Q-SYS                 | REST API                          | Cisco/Netgear     |
| Teams (MTR endpoints) | Microsoft Graph API               | Cisco/Netgear     |
| Zoom                  | Zoom REST API                     | Cisco/Netgear     |
| Multicast             | SNMP counters                     | Cisco/Netgear     |
| AVB                   | Interface packet sniffing (Scapy) | Cisco/Netgear     |

---

## Installation

1. **Clone the repository:**

```bash
git clone https://github.com/Khal1d-waheed/UC-AV-QOS-Automated.git

cd uc-av-qos-automation
```

2. **Run the script:**

```bash
python3 uc_av_qos.py
```

> The script will automatically install any missing dependencies.

---

## Setup / Configuration

* **Interactive prompts:** Upon first run, the script asks for:

  * Switch IP, username, and password
  * Total number of ports
  * Port mapping for each supported device (optional: leave blank if not present)
  * Polling interval, jitter threshold, packet loss threshold
  * API tokens for NVX, Teams, Zoom, Biamp, Q-SYS (optional)

* **Dynamic Operation:** After initial setup, all UC/AV devices are monitored continuously, and QoS policies are applied/removed automatically based on real-time metrics.

---

## Logging & Metrics

* All real-time metrics are logged automatically to:

```
logs/metrics.csv
```

* Metrics include per-device:

  * Jitter (ms)
  * Latency (ms)
  * Packet Loss (%)
* Historical logging allows auditing and QoS optimization trends.

---

## How It Works

1. The script polls all configured devices and streams for activity.
2. Metrics (latency, jitter, packet loss) are collected in real-time.
3. QoS policies are dynamically applied to ports on Cisco or Netgear switches based on thresholds.
4. Multithreading ensures multiple devices are polled simultaneously without delays.
5. All actions and metrics are logged for auditing and rollback.

---

## System Requirements

* Python 3.9+
* Network access to switches (SSH/SNMP)
* API access for NVX, Biamp, Q-SYS, Teams, Zoom if live metrics are needed
* Windows/Linux/macOS terminal

---

## Example Output

```
Device      Status             QoS Applied
NVX         ACTIVE (5,6)       EF_QOS
BIAMP       IDLE               -
TEAMS       ACTIVE (10)        UC_HIGH
AVB         ACTIVE (7)         EF_HIGH
```

Metrics CSV (`logs/metrics.csv`) contains:

| Timestamp           | Device | Jitter | Latency | Packet Loss | QoS Applied |
| ------------------- | ------ | ------ | ------- | ----------- | ----------- |
| 2025-09-14 18:00:01 | NVX    | 4      | 12      | 0           | EF\_QOS     |

---

## Notes

* The script supports **dynamic detection** and **optional devices** — leave a device blank during setup if it is not present in your environment.
* Fully production-ready for live deployments with rollback and error handling.
* Both **Cisco and Netgear** QoS are fully supported via CLI or SNMP.

