# ITEA-Steroid Pocket-NIC — releases

Ready-to-install builds of **ITEA-Steroid Pocket-NIC**, a field network appliance
for IT technicians running on a Raspberry Pi Zero 2 W. The source code is private;
this repository only publishes installable packages.

## Install

1. Flash **Raspberry Pi OS Lite (64-bit)** with Raspberry Pi Imager. In the
   Imager settings set a hostname (e.g. `itea-steroid`), a user and password,
   your Wi-Fi and country, and enable SSH.
2. Boot the Pi, connect with SSH, and run:

   ```sh
   curl -fsSL https://github.com/smoke-detector/ITEA-Steroid-releases/releases/latest/download/get.sh | sudo sh
   ```

3. Open `http://<hostname>.local` in a browser and create the admin password.

Run the same command again at any time to upgrade; settings and files are kept.
To install a specific version: `curl -fsSL …/get.sh | sudo ITEA_VERSION=v0.1.0 sh`.

## Setup hotspot

When the Pi has no working Wi-Fi it starts its own hotspot:

- SSID `ITEA-Steroid`, password `ITEAdvisors` (the password can be changed in the dashboard)
- Dashboard at `http://100.64.0.1`
- Clients get an address only (no gateway), so a phone keeps its own internet

![Join the setup hotspot](hotspot-qr.svg)

## What the installer does

Installs the required Debian packages (NetworkManager, nmap, lldpd, tftpd-hpa,
vsftpd, samba, cloudflared, …), creates a restricted service account, installs
the `itea-nic` program and its systemd services, and enables the dashboard on
port 80. Each download is checked against `SHA256SUMS` before installing.
