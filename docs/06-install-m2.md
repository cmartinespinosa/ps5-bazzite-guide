# 6. First Linux boot and install to the M.2

The first boot runs Bazzite **from the USB stick**. You only use it to copy Bazzite onto the M.2, so keep it minimal: Wi-Fi and SSH, nothing else. Don't install games here.

## 6.1 Boot Linux from the stick

1. Restart the PS5 and [jailbreak it](03-jailbreak.md).
2. From your computer, send the loader to port 9021:

    ```bash
    nc -w 5 <PS5_IP> 9021 < ps5-linux-loader-v35.elf
    ```

3. The loader finds the boot files on the stick and puts the PS5 into rest mode. Watch the light bar:
    - **orange blinking** → wait →
    - **orange solid** → wait **another 5–10 seconds** →
    - press the PS5's **power button**.
4. A **white** light means Linux is booting.

!!! note "Be patient"
    The first boot shows a **black screen for about 5 minutes**. Then Bazzite's setup wizard appears at 1080p: language, Wi-Fi, Steam login.

    When the wizard reboots, the PS5 goes back to its normal system. That's expected: **every Linux reboot lands in PS5 OS**. Jailbreak and send the loader again.

    After that, a **grey screen with a cursor** in the top-left corner for a few minutes is also normal: Steam is starting.

## 6.2 Connect over SSH

SSH is on by default. User **`ps5`**, password **`ps5`**.

1. Find the Linux IP address: Steam → *Settings → Internet*, or your router's device list. This guide calls it `<LINUX_IP>`.
2. From your computer:

    ```bash
    ssh ps5@<LINUX_IP>
    ```

3. Optional, to avoid typing the password: `ssh-copy-id ps5@<LINUX_IP>`.

## 6.3 Copy the image to the PS5

The M.2 installer needs the uncompressed image **on the PS5**. Copy the three parts over and unpack them there:

```bash
scp ps5-bazzite-deck-v1.3.1.img.7z.00* ps5@<LINUX_IP>:Downloads/
```

Then, on the PS5 (over SSH):

```bash
cd ~/Downloads
sha256sum ps5-bazzite-deck-v1.3.1.img.7z.00*
7z x -y ps5-bazzite-deck-v1.3.1.img.7z.001
```

You get `~/Downloads/ps5-bazzite-deck.img`. Over Wi-Fi the copy runs at about 10 MB/s, so allow 15–20 minutes.

## 6.4 Add a Linux partition to the M.2

Get the [ps5-linux-tools](https://github.com/ps5-linux/ps5-linux-tools), build them and run `m2_init`:

```bash
git clone https://github.com/ps5-linux/ps5-linux-tools ~/ps5-linux-tools
cd ~/ps5-linux-tools
make
lsblk /dev/nvme0n1
sudo ./m2_init
```

Expected: **`Successfully added Linux partition to m2.`** A new partition `nvme0n1p1` appears.

## 6.5 Install Bazzite on the M.2

Become root and mount the stick's boot partition:

```bash
sudo -i
mkdir -p /boot/efi
umount /boot/efi 2>/dev/null
mount LABEL=boot /boot/efi
```

Run the installer:

```bash
cd /var/home/ps5/ps5-linux-tools
./m2_install.sh --install /var/home/ps5/Downloads/ps5-bazzite-deck.img
```

It formats the M.2 partition (label `bazzite-deck-m2`) and copies ~12 GB. **There's no progress output**: it looks frozen but isn't. It took me 2–5 minutes. It ends with **`Installation complete.`**

Point the boot config at the M.2:

```bash
sed -i 's/root=LABEL=bazzite-deck /root=LABEL=bazzite-deck-m2 /' /boot/efi/cmdline.txt
cat /boot/efi/cmdline.txt
sync
```

Check that the line now contains **`root=LABEL=bazzite-deck-m2`**.

!!! danger "Always `sync`"
    The boot partition is FAT32. If you power off right after editing a file without `sync`, the file can end up **empty** and Linux won't boot.

## 6.6 Boot from the M.2

1. In Steam: *Power → **Shut Down*** (never *Restart*).
2. Power on the PS5, jailbreak, send the loader, wait for solid orange, press power.

Bazzite now runs from the M.2. It's a **fresh install**, so you'll see the setup wizard again, the IP address may change and the password is back to `ps5`. Carry on with [First boot setup](07-first-boot.md).
