# ITEA-Steroid Pocket-NIC — releases

Ready-to-install builds of **ITEA-Steroid Pocket-NIC**, a field network appliance
for IT technicians running on a Raspberry Pi Zero 2 W. The source code is private;
this repository only publishes installable packages.

## Default passwords

Everything uses the same published default so a new unit works straight away.
**None of these are forced to change**, but change them if the device will sit on a
network you do not control.

| What | Default | Change it |
|---|---|---|
| Dashboard login | `admin` / `ITEAdvisors` | Dashboard → System → Admin password |
| SSH / console login | `itea` / `ITEAdvisors` (you set this in Raspberry Pi Imager, see below) | Dashboard → System → Pi login password |
| Setup hotspot Wi-Fi | `ITEA-Steroid` / `ITEAdvisors` | Dashboard → System → Setup hotspot |
| Access point Wi-Fi | `ITEA-Steroid-AP` / `ITEAdvisors` | Dashboard → Network mode |

## Install

1. Open **Raspberry Pi Imager** and choose **Raspberry Pi OS Lite (64-bit)**. In the
   OS customisation settings enter:
   - Hostname: `itea-steroid`
   - Username: `itea` and password: `ITEAdvisors`
   - Your Wi-Fi name, password and country
   - Services → enable SSH (password authentication)
2. Boot the Pi, connect with SSH (`ssh itea@itea-steroid.local`, password `ITEAdvisors`), and run:

   ```sh
   curl -fsSL https://github.com/smoke-detector/ITEA-Steroid-releases/releases/latest/download/get.sh | sudo sh
   ```

3. Open `http://itea-steroid.local` and sign in with `admin` / `ITEAdvisors`.

The installer never changes the Pi's own password; it uses whichever user you created
in Imager. Run the same command again at any time to upgrade; settings and files are
kept. To install a specific version:
`curl -fsSL …/get.sh | sudo ITEA_VERSION=v0.2.0 sh`.

## Setup hotspot

When the Pi has no working Wi-Fi it starts its own hotspot:

- SSID `ITEA-Steroid`, password `ITEAdvisors`
- Dashboard at `http://100.64.0.1`
- Clients get an address only (no gateway), so a phone keeps its own internet

![Join the setup hotspot](hotspot-qr.svg)

## What it does

Wi-Fi setup with hotspot fallback, an access-point mode that shares the Ethernet
uplink, an Ethernet DHCP-server mode, ping/traceroute/DNS/Nmap/Wake-on-LAN tools,
LLDP/CDP/FDP discovery, a browser serial console, TFTP/SFTP/FTP/SMB file transfer in
a fixed-size area that cannot fill the OS, USB storage, a virtual DVD drive for ISO
images, Cloudflare Tunnel from a pasted token, an HDMI status screen and a GPIO
Wi-Fi reset jumper.

## What the installer does

Installs the required Debian packages (NetworkManager, nmap, lldpd, tftpd-hpa,
vsftpd, samba, cloudflared, kernel headers, …), creates a restricted service account,
installs the `itea-nic` program and its systemd services, and enables the dashboard on
port 80. Each download is checked against `SHA256SUMS` before installing.

## Support the project

ITEA-Steroid is free. If it saves you time, you can donate:
**[Donate via Stripe](https://donate.stripe.com/eVq6oz0LU7ucgX19KE57W00)** (also
available as a QR code in the dashboard under System).
