# 3. Jailbreak with Relapse

Relapse is a browser-based exploit. You open it from the PS5's built-in **User's Guide** page, which is redirected to the exploit through a custom DNS server.

## Set the DNS

1. *Settings → Network → Settings → Set Up Internet Connection*.
2. Select your Wi-Fi network → *Advanced Settings*.
3. **DNS Settings: Manual**, Primary DNS: **`45.56.67.85`**.
4. Save.

!!! tip
    I keep this DNS permanently: it also blocks Sony's update servers, which protects you from an accidental firmware update.

## Run the exploit

1. Open *Settings → User's Guide, Health and Safety, and Other Information → User's Guide*.
2. The Relapse page loads. Check that it detects the right firmware.
3. Select **Jailbreak** and wait.
4. Success: a message saying **`elfldr is listening on port 9021`**. The PS5 now accepts `.elf` payloads on port 9021.

If it freezes or the console reboots, just try again. It's a timing race and often needs a second attempt. See [Troubleshooting](11-troubleshooting.md#relapse-hangs-at-checking-aio-groups).

## Find the PS5's IP address

*Settings → Network → Connection Status → View Connection Status*. Write down the **IPv4 address**. This guide calls it `<PS5_IP>`.

!!! warning "Linux path: keep it clean"
    For the Linux boot, jailbreak a **freshly restarted** PS5 and send **only** the Linux loader. Don't send kstuff, etaHEN or other homebrew payloads first: they're incompatible with the Linux loader and the console freezes instead of entering rest mode.
