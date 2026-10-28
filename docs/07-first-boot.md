# 7. First boot setup

## Change the default password

Everyone knows `ps5` / `ps5`, and SSH is on. Change it right away:

```bash
ssh -t ps5@<LINUX_IP> passwd
```

The new password needs **at least 8 characters** (shorter ones fail with `BAD PASSWORD`).

Optionally copy your SSH key again (it was lost with the reinstall):

```bash
ssh-copy-id ps5@<LINUX_IP>
```

## Display

Steam → *Settings → Display*:

- **RGB range: Full** (recommended by the PS5 Bazzite Deck README).
- **Resolution**: pick your best mode. 2560×1440 @ 60 Hz is the highest on a 1440p monitor; ultrawide isn't available (see [Requirements](01-requirements.md#hardware)).

## Pair the DualSense over Bluetooth

1. Steam → *Settings → Bluetooth*.
2. With the controller off, hold **PS + Create** until the light bar blinks fast.
3. Select it in the list.

!!! note
    On v1.3.x, pairing with Linux broke the pairing with the PS5 system (cable needed to re-pair). From v1.4 Linux uses its own Bluetooth address, so the controller stays paired with both.

## How to power off

Always use Steam → *Power → **Shut Down***. A **Restart** sends you back to the PS5 system, and you'll need the loader again.

From v1.4.1 you also get **Sleep**: a short press on the power button pauses the game (orange light), another short press wakes it up. It saves little power, because the GPU stays on.
