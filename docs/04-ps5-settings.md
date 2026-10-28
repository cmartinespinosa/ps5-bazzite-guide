# 4. PS5 settings

Apply these on the PS5 **before the first Linux boot**. Re-apply them if you ever reset the console's settings.

| Setting | Value | Why |
|---------|-------|-----|
| *Settings → System → Power Saving → Features Available in Rest Mode → **Supply Power to USB Ports*** | **Always** | **Required.** The loader puts the PS5 in rest mode before booting Linux; the boot USB must stay powered. |
| *Settings → System → HDMI → **Enable HDMI Device Link*** | **Off** | **Required.** Otherwise the TV can wake or disturb the console during the rest-mode step (black screen). |
| *Settings → System → System Software → **System Software Update and Settings*** | Auto download and auto install **off** | Recommended. Stops Sony from updating past 13.60. |
| *Settings → System → System Software → **Report System Software Errors Automatically*** | **Off** | Recommended. |

## Install the M.2 SSD

If you haven't yet, power off the PS5, unplug it and fit the M.2 SSD in the expansion slot ([Sony's guide](https://www.playstation.com/en-us/support/hardware/ps5-m2-ssd/)). Power on and **let the PS5 format it** when asked. Linux adds its own partition later.
