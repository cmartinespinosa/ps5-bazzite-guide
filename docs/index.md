# PS5 Bazzite Guide

This guide takes a **stock base PS5** all the way to **[PS5 Bazzite Deck](https://github.com/VivaLaVent/ps5-bazzite-deck)** (a SteamOS-like Linux) running from the console's internal M.2 SSD, with Decky plugins, fan control, one-click updates and fixes for the problems I ran into.

It's the exact path I followed on my own console in October 2026. Every command here was run for real; where something failed, the guide says so.

!!! warning "Read this first"
    - This is **unofficial** and **at your own risk**. Jailbreaking can brick a console or get it banned from PSN.
    - You need a firmware the jailbreak supports. This guide uses **13.60**. If your PS5 is already on a newer firmware, stop here: you can't go back.
    - The M.2 SSD you use for Linux gets erased.
    - Credit goes to the people who did the real work: the Relapse exploit authors, the [ps5-linux](https://github.com/ps5-linux) project, [rmux's loader](https://github.com/rmuxwashere/ps5-linux-loader), [VivaLaVent](https://github.com/VivaLaVent/ps5-bazzite-deck), [itsPLK](https://github.com/itsPLK/ps5-webkit-autoloader) and [Hooandee](https://github.com/Hooandee/panel-de-control).

## How it works, in one minute

1. The PS5 is jailbroken from its built-in web browser (the **Relapse** exploit).
2. A **Linux loader** payload is sent to the PS5. It puts the console into rest mode and wakes it up running a Linux kernel from a **USB stick**.
3. The USB stick only holds the boot files. The system itself lives on the **M.2 SSD**.
4. Bazzite boots into Steam's Big Picture / Steam Deck interface. You play with a DualSense like on a Steam Deck.
5. Every time you power on, you repeat steps 1–2. An **autoloader** app turns that into one click.

## The steps

| # | Step | Time |
|---|------|------|
| 1 | [Requirements](01-requirements.md) | — |
| 2 | [Update the firmware to 13.60](02-firmware.md) | 20 min |
| 3 | [Jailbreak with Relapse](03-jailbreak.md) | 5 min |
| 4 | [PS5 settings](04-ps5-settings.md) | 5 min |
| 5 | [Flash the boot USB](05-boot-usb.md) | 15 min |
| 6 | [First Linux boot and install to the M.2](06-install-m2.md) | 1 h |
| 7 | [First boot setup](07-first-boot.md) | 15 min |
| 8 | [Decky Loader and plugins](08-decky-plugins.md) | 15 min |
| 9 | [One-click autoloader](09-autoloader.md) | 10 min |
| 10 | [Updating Bazzite](10-updating.md) | 10 min |
| 11 | [Troubleshooting](11-troubleshooting.md) | — |

## My setup

- Base PS5 (disc, launch model), firmware 13.60
- 1 TB NVMe M.2 SSD with heatsink
- SanDisk 250 GB USB 3.2 stick, permanently plugged into a rear USB-A port
- PS5 Bazzite Deck v1.5.1, Decky Loader v3.3.0
- A Mac to prepare everything (Windows/Linux alternatives are noted where they differ)
