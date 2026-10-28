# 11. Troubleshooting

## Boot

### Relapse hangs at "checking aio groups"

The jailbreak (in the browser or the autoloader) stops at *Kernel: checking aio groups*, or the page stops responding. It's a timing race. Answer *Yes* to stop the page, restart the PS5 and try again. It works more often right after power-on, with no other app open.

### The PS5 only beeps and won't turn on

After a hung autoloader, the console may refuse to start. **Unplug the power cable for 30 seconds**, plug it back in, power on.

### Back in the PS5 system after the loader (blue blinking light)

You pressed the power button before the orange light went **solid**. Send the loader again, wait for solid orange, then **5–10 more seconds**.

### Every Linux reboot lands in the PS5 system

Expected. Use *Shut Down*, never *Restart*.

### Grey screen with a mouse cursor

Steam is starting. Wait a few minutes. If it lasts more than 10 minutes, hold power for 10 seconds and boot again.

### Black screen after editing `cmdline.txt`

Restore the backup if you made one, and always `sync` before powering off:

```bash
sudo cp /boot/efi/cmdline.txt.bak /boot/efi/cmdline.txt && sync && sudo poweroff
```

If Linux won't boot at all, plug the USB stick into a computer and fix `cmdline.txt` on its `boot` partition.

!!! danger "Don't use the 40 CU unlock"
    Adding `amdgpu.ps5_cu_unlock=3` to `cmdline.txt` gave me a black screen and GPU crashes (`ring gfx timeout`, `GPU Recovery Failed`). Your console may differ, but mine didn't take it.

## Games

### Elden Ring / Sekiro stuck at ~40 fps

Even at 720p, with the GPU barely used. The cause is the Proton version, not the hardware. **Force Proton 9**: in Steam, game → *Properties → Compatibility* → *Force a specific Steam Play compatibility tool* → **Proton 9**. Sekiro then runs at 60.

Try Proton 9 first for any FromSoftware game, or any game that runs worse than it should.

### Elden Ring stuck on an endless loading spinner

Happened with Proton 11.0. Switch to Proton 9 (or Experimental).

### Games quit to the Steam menu after ~10 minutes

Seen in RoboCop: Rogue City and Fatekeeper. The system log shows an amdgpu `page fault … PERMISSION_FAULTS` from `gamescope`, then `ring gfx_0.0.0 timeout`, then gamescope aborts. It's a kernel GPU driver bug, not the game.

- v1.5.0 includes a GPU fix for this. v1.5.1 still lists it as a known issue, so **update to the latest version**.
- If it still happens, run this right after a crash and share the output with the project (see the [PS5 Bazzite Deck README](https://github.com/VivaLaVent/ps5-bazzite-deck) for where):

    ```bash
    ps5-report
    ```

## Other

### `passwd` says BAD PASSWORD

Use at least 8 characters.

### Decky doesn't show up

Restart the Steam session over SSH:

```bash
systemctl --user restart gamescope-session-plus@ogui-steam.service
```

### Undo an update

`update.sh` printed an undo command when you updated. Backups are in `/var/lib/ps5-update-backup/`.
