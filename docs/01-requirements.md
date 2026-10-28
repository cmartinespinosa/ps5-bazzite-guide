# 1. Requirements

## Hardware

- [ ] **A base PS5** (disc or digital) on firmware **13.60 or lower**. Check in *Settings → System → System Software → Console Information*: in a string like `26.01-12.70.00.01`, the middle part (`12.70`) is the firmware.
- [ ] **An NVMe M.2 SSD** for Linux, ideally with a heatsink. It must meet [Sony's M.2 requirements](https://www.playstation.com/en-us/support/hardware/ps5-m2-ssd/) (PCIe 4.0). It will be erased. 1 TB is plenty.
- [ ] **A USB stick, 32 GB or more** (the image unpacks to 25.2 GB). It stays plugged into the PS5 forever, so a small, fast one is ideal. I used a SanDisk 250 GB USB 3.2.
- [ ] **A DualSense and its USB cable** (Safe Mode needs the cable).
- [ ] **A computer** to download and flash files. This guide uses macOS; Windows/Linux notes are included.
- [ ] Optional: a USB keyboard and mouse, handy for the Linux desktop.
- [ ] Wi-Fi works out of the box. Ethernet is not needed.

!!! note "Displays"
    The PS5's HDMI chip only outputs standard TV modes: 1080p60/120, 1440p60 (1440p120 on some models) and 2160p60. **Ultrawide (21:9) is not possible.** On my 3440×1440 monitor the best mode is 2560×1440 @ 60 Hz.

## Downloads

Grab these on your computer before you start.

| What | Where | Notes |
|------|-------|-------|
| **Firmware 13.60** | [darthsternie.net](https://darthsternie.net/ps5-firmwares/) → *Official Firmwares* → 13.60.00 | Pick the **Update** PUP (~1.25 GB), **not the Recovery one** (~1.40 GB, wipes the console). Only needed if you're below 13.60. |
| **PS5 Bazzite Deck image** | [VivaLaVent/ps5-bazzite-deck releases](https://github.com/VivaLaVent/ps5-bazzite-deck/releases) | The three files `ps5-bazzite-deck-vX.Y.Z.img.7z.001`, `.002`, `.003`. Skip the `-update.tar.xz`, `.patch` and `.diff` files. I used v1.3.1, then updated. |
| **Linux loader** | [rmuxwashere/ps5-linux-loader releases](https://github.com/rmuxwashere/ps5-linux-loader/releases) | `ps5-linux-loader-v35.elf` (v3.5), the loader VivaLaVent's README recommends. |
| **WebKit Autoloader** | [itsPLK/ps5-webkit-autoloader releases](https://github.com/itsPLK/ps5-webkit-autoloader/releases) | `webkit-autoloader-installer_v0.6.1.elf`. Optional, for one-click boot ([step 9](09-autoloader.md)). |

### Check the firmware file

The 13.60 Update PUP is exactly 1,247,471,104 bytes with this MD5:

```bash
md5 -q PS5UPDATE.PUP
# 06a74efce009503170b7add7fecfeb36
```

You can also compare its SHA256 with [MewX's firmware list](https://github.com/MewX/ps5-official-firmware-list).

### Check the image files

Compare each part with the SHA256 published on the release page:

```bash
shasum -a 256 ps5-bazzite-deck-v*.img.7z.00*
```

## Tools on the computer

=== "macOS"

    ```bash
    brew install sevenzip
    ```

    `diskutil`, `dd`, `nc` and `ssh` are built in.

=== "Windows"

    [7-Zip](https://www.7-zip.org/) to unpack the image, [Rufus](https://rufus.ie/) or [balenaEtcher](https://etcher.balena.io/) to flash it, and a netcat build (or the [PS5 Payload Sender](https://github.com/search?q=ps5+payload+sender) tools) to send `.elf` files. *Not tested by me.*

=== "Linux"

    `p7zip`, `dd`, `netcat` and `ssh` from your package manager. *Not tested by me.*
