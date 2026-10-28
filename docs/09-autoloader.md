# 9. One-click autoloader

Without this, every boot means: jailbreak in the browser, then send the loader from a computer. [WebKit Autoloader](https://github.com/itsPLK/ps5-webkit-autoloader) by itsPLK adds a PS5 app that runs the jailbreak **and** the Linux loader in one go. No computer needed.

## 1. Put the loader on the USB stick

The autoloader looks for a `ps5_autoloader` folder on USB first. From Bazzite, `/boot/efi` is the stick's boot partition. Copy the loader `.elf` to the PS5 (e.g. with `scp` into `~/Downloads`), then over SSH:

```bash
sudo mkdir -p /boot/efi/ps5_autoloader
sudo cp ~/Downloads/ps5-linux-loader-v35.elf /boot/efi/ps5_autoloader/
printf "ps5-linux-loader-v35.elf\n" | sudo tee /boot/efi/ps5_autoloader/autoload.txt
sync
```

`autoload.txt` lists the payloads to send, one per line. Only the Linux loader goes in here.

## 2. Install the autoloader app

1. Shut down Bazzite, power on the PS5 and [jailbreak it](03-jailbreak.md).
2. Send the installer:

    ```bash
    nc -w 10 <PS5_IP> 9021 < webkit-autoloader-installer_v0.6.1.elf
    ```

3. Expected: *WebKit Autoloader v0.6.1 cached successfully!* and *App installed.*
4. Restart the PS5 once.

## Daily use

1. Power on the PS5.
2. Open the **WebKit Autoloader** app from the home screen, right away, with no other app open.
3. Wait for the **solid orange** light, wait 5–10 seconds, press **power**.
4. Play.
5. Steam → *Power → **Shut Down***.

!!! note "It doesn't always work the first time"
    My first runs hung (at *Starting…* and at *Kernel: checking aio groups*). Restarting the PS5 and trying again fixed it. See [Troubleshooting](11-troubleshooting.md).

!!! tip "Idea: USB in = Linux, USB out = PS5 homebrew"
    The autoloader reads the USB's `ps5_autoloader` before the one in `/data`. In theory, you can keep a different homebrew setup in `/data/ps5_autoloader` and get it just by unplugging the stick. *I haven't tested this.*
