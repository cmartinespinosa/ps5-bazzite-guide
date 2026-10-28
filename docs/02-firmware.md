# 2. Update the firmware to 13.60

Skip this step if your PS5 is already on 13.60.

!!! danger "Never update over the internet"
    Sony's online update installs the **latest** firmware, which the jailbreak doesn't support. Before connecting the PS5 to the internet, turn off automatic updates (see [step 4](04-ps5-settings.md)), and only update from USB with the exact file below.

## Prepare the USB stick

The stick must be formatted **exFAT** or **FAT32** and contain the file at `PS5/UPDATE/PS5UPDATE.PUP` (uppercase).

=== "macOS"

    Find the stick's disk number (e.g. `disk4`) with `diskutil list`, then:

    ```bash
    diskutil eraseDisk ExFAT PS5 MBRFormat disk4
    mkdir -p /Volumes/PS5/PS5/UPDATE
    cp PS5UPDATE.PUP /Volumes/PS5/PS5/UPDATE/PS5UPDATE.PUP
    sync
    md5 -q /Volumes/PS5/PS5/UPDATE/PS5UPDATE.PUP
    dot_clean -m /Volumes/PS5
    diskutil eject disk4
    ```

    !!! warning
        Double-check the disk number. `eraseDisk` on the wrong disk erases it.

=== "Windows"

    Format the stick as exFAT in File Explorer, create the folders `PS5\UPDATE` and copy the file into it as `PS5UPDATE.PUP`.

## Install from Safe Mode

1. **Fully power off** the PS5 (not rest mode).
2. Plug the stick into a rear USB-A port or the front USB-C port.
3. Hold the power button until the **second beep** (about 7 seconds). The PS5 starts in Safe Mode.
4. Connect the DualSense **with the cable** and press the PS button.
5. Choose **3. Update System Software → Update from USB Storage Device**.
6. Check that the screen says **13.60**, then confirm.

!!! danger
    Don't pick *Reset*, *Reinstall System Software* or *Rebuild Database* in Safe Mode.

When the console restarts, confirm the version in *Settings → System → System Software → Console Information*.
