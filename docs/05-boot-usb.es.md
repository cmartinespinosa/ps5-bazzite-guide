# 5. Grabar el USB de arranque

La imagen de Bazzite se graba directamente en el pendrive. Crea dos particiones:

- `boot` (FAT32): kernel, initrd, `cmdline.txt`, `vram.txt`. La PS5 siempre arranca desde aquí.
- `bazzite-deck`: un primer sistema Linux temporal. Lo usarás una vez para instalar Bazzite en el M.2.

!!! danger
    Grabar la imagen borra todo el pendrive. Revisa bien el nombre del disco antes de ejecutar `dd`.

## macOS

1. Comprueba las tres partes (ver [Requisitos](01-requirements.md#check-the-image-files)).
2. Busca el pendrive (p. ej. `disk4`):

    ```bash
    diskutil list external
    ```

3. Mira el tamaño **descomprimido** de la imagen (la *última* línea `Size =`; en la v1.3.1 eran 25.165.824.000 bytes):

    ```bash
    7zz l -slt ps5-bazzite-deck-v1.3.1.img.7z.001 | grep '^Size'
    ```

4. Descomprime y graba de una vez, directamente al dispositivo raw (`rdisk` es mucho más rápido que `disk`):

    ```bash
    diskutil unmountDisk disk4
    7zz x -so ps5-bazzite-deck-v1.3.1.img.7z.001 | sudo dd of=/dev/rdisk4 bs=4m
    sync
    ```

    A mí me tardó unos 6 minutos a ~74 MB/s. No hay barra de progreso; pulsa **Ctrl+T** para ver el progreso de `dd`.

5. Expulsa:

    ```bash
    diskutil eject disk4
    ```

## Windows / Linux

Descomprime el archivo `.001` con 7-Zip (coge `.002` y `.003` automáticamente) para obtener `ps5-bazzite-deck.img` y grábalo con Rufus o balenaEtcher (Windows) o `dd` (Linux). *No he probado este camino.*

## Enchúfalo

Enchufa el pendrive en uno de los **puertos USB-A traseros** de la PS5 y déjalo ahí para siempre.
