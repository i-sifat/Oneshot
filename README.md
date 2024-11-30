## Setup

### Termux (Android)

**Note**: Root access is required.

#### Installation
1. **Install Requirements**:
    ```bash
    termux-setup-storage
    pkg install -y root-repo
    pkg install -y git tsu python wpa-supplicant pixiewps iw openssl
    ```
2. **Clone Repository**:
    ```bash
    git clone --depth 1 https://github.com/i-sifat/Oneshot OneShot
    ```
3. **Run**:
    ```bash
    sudo python OneShot/oneshot.py -i wlan0 --iface-down -K
    ```

---

## Usage
```bash
python3 oneshot.py <arguments>
```

### Required Arguments:
- `-i`, `--interface=<wlan0>`: Specify the interface to use.

### Optional Arguments:
- `-b`, `--bssid=<mac>`: Specify target AP BSSID.
- `-p`, `--pin=<wps pin>`: Use a specific PIN (4/8 digits or string).
- `-K`, `--pixie-dust`: Run Pixie Dust attack.
- `-B`, `--bruteforce`: Launch online brute force attack.
- `--push-button-connect`: Initiate WPS push-button connection.

### Advanced Options:
- `-d`, `--delay=<n>`: Set delay between pin attempts (default: 0).
- `-w`, `--write`: Save AP credentials on success.
- `-F`, `--pixie-force`: Force Pixiewps to brute force full range.
- `-X`, `--show-pixie-cmd`: Display Pixiewps command.
- `--vuln-list=<filename>`: Use custom vulnerable device list (`vulnwsc.txt`).
- `--iface-down`: Bring the interface down after execution.
- `-l`, `--loop`: Continuously run.
- `-r`, `--reverse-scan`: Reverse scan order (for small displays).
- `--mtk-wifi`: Activate/deactivate MediaTek Wi-Fi drivers (for Android MediaTek SoCs).
- `-v`, `--verbose`: Enable verbose output.

---

## Usage Examples

### Pixie Dust Attack on a Specific BSSID:
```bash
sudo python3 oneshot.py -i wlan0 -b 00:90:4C:C1:AC:21 -K
```

### Scan for Networks and Start Pixie Dust Attack:
```bash
sudo python3 oneshot.py -i wlan0 -K
```

### Online WPS Brute Force:
```bash
sudo python3 oneshot.py -i wlan0 -b 00:90:4C:C1:AC:21 -B -p 1234
```

### WPS Push Button Connection:
```bash
sudo python3 oneshot.py -i wlan0 --pbc
```

---

## Troubleshooting

### Error: *RTNETLINK answers: Operation not possible due to RF-kill*
Run:
```bash
sudo rfkill unblock wifi
```

### Error: *Device or resource busy (-16)*
- Disable Wi-Fi in system settings.
- Kill the Network Manager.
- Use the `--iface-down` flag.

### Issue: *Disappearing `wlan0` Interface on Android (MediaTek SoC)*
Run OneShot with:
```bash
--mtk-wifi
```

---
---

# OneShot

A powerful tool to perform [Pixie Dust attacks](https://forums.kali.org/showthread.php?24286-WPS-Pixie-Dust-Attack-Offline-WPS-Attack) and other WPS-related operations without requiring monitor mode.

---

## Overview

**OneShot** simplifies WPS attacks and Wi-Fi network scanning by integrating various tools, including Pixie Dust and 3WiFi.

### Key Features:
- **Pixie Dust attack**: Exploit WPS vulnerabilities without monitor mode.
- **Offline WPS PIN generation**: Leverages [3WiFi](https://3wifi.stascorp.com/wpspin) for PIN generation.
- **Online WPS brute force**: Run exhaustive PIN-based WPS attacks.
- **Wi-Fi scanner**: Highlights networks vulnerable to attacks (requires `iw`).

---

## Requirements
- Python 3.6+
- [Wpa supplicant](https://www.w1.fi/wpa_supplicant/)
- [Pixiewps](https://github.com/wiire-a/pixiewps)
- [iw](https://wireless.wiki.kernel.org/en/users/documentation/iw)

---

## Special Thanks
- **rofl0r**: Original implementation.
- **Monohrom**: Testing, bug fixes, and ideas.
- **Wiire**: Development of Pixiewps.
