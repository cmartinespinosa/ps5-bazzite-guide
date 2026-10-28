# 5. Flash the boot USB

The Bazzite image is written directly to the USB stick. It creates two partitions:

- `boot` (FAT32): kernel, initrd, `cmdline.txt`, `vram.txt`. The PS5 always boots from here.
- `bazzite-deck`: a first, temporary Linux system. You'll use it once to install Bazzite on the M.2.

!!! danger
    Flashing erases the whole stick. Double-check the disk name before running `dd`.

## macOS

1. Check the three parts (see [Requirements](01-requirements.md#check-the-image-files)).
2. Find the stick (e.g. `disk4`):

    ```bash
    diskutil list external
    ```

3. Find the **uncompressed** size of the image (the *last* `Size =` line; for v1.3.1 it was 25,165,824,000 bytes):

    ```bash
    7zz l -slt ps5-bazzite-deck-v1.3.1.img.7z.001 | grep '^Size'
    ```

4. Unpack and write in one go, straight to the raw device (`rdisk` is much faster than `disk`):

    ```bash
    diskutil unmountDisk disk4
    7zz x -so ps5-bazzite-deck-v1.3.1.img.7z.001 | sudo dd of=/dev/rdisk4 bs=4m
    sync
    ```

    This took about 6 minutes at ~74 MB/s on my stick. There's no progress bar; press **Ctrl+T** to see `dd`'s progress.

5. Eject:

    ```bash
    diskutil eject disk4
    ```

## Windows / Linux

Unpack the `.001` file with 7-Zip (it picks up `.002` and `.003` automatically) to get `ps5-bazzite-deck.img`, then flash it with Rufus or balenaEtcher (Windows) or `dd` (Linux). *I didn't test this path.*

## Plug it in

Plug the stick into one of the PS5's **rear USB-A ports** and leave it there for good.
