# 1. Requisitos

## Hardware {#hardware}

- [ ] **Una PS5 base** (con lector o digital) con firmware **13.60 o inferior**. Compruébalo en *Ajustes → Sistema → Software del sistema → Información de la consola*: en una cadena como `26.01-12.70.00.01`, la parte del medio (`12.70`) es el firmware.
- [ ] **Un SSD NVMe M.2** para Linux, mejor con disipador. Debe cumplir los [requisitos de M.2 de Sony](https://www.playstation.com/es-es/support/hardware/ps5-m2-ssd/) (PCIe 4.0). Se borrará. Con 1 TB sobra.
- [ ] **Un pendrive USB de 32 GB o más** (la imagen descomprimida ocupa 25,2 GB). Se queda enchufado en la PS5 para siempre, así que uno pequeño y rápido es lo ideal. Yo usé un SanDisk 250 GB USB 3.2.
- [ ] **Un DualSense y su cable USB** (el modo seguro necesita el cable).
- [ ] **Un ordenador** para descargar y grabar archivos. Esta guía usa macOS; hay notas para Windows/Linux.
- [ ] Opcional: un teclado y ratón USB, útiles para el escritorio de Linux.
- [ ] El Wi-Fi funciona de serie. No hace falta cable de red.

!!! note "Pantallas"
    El chip HDMI de la PS5 solo saca modos de TV estándar: 1080p60/120, 1440p60 (1440p120 en algunos modelos) y 2160p60. **Ultrapanorámico (21:9) no es posible.** En mi monitor 3440×1440 el mejor modo es 2560×1440 a 60 Hz.

## Descargas

Descarga esto en tu ordenador antes de empezar.

| Qué | Dónde | Notas |
|-----|-------|-------|
| **Firmware 13.60** | [darthsternie.net](https://darthsternie.net/ps5-firmwares/) → *Official Firmwares* → 13.60.00 | Elige el PUP de **Update** (~1,25 GB), **no el de Recovery** (~1,40 GB, borra la consola). Solo si estás por debajo de 13.60. |
| **Imagen de PS5 Bazzite Deck** | [Releases de VivaLaVent/ps5-bazzite-deck](https://github.com/VivaLaVent/ps5-bazzite-deck/releases) | Los tres archivos `ps5-bazzite-deck-vX.Y.Z.img.7z.001`, `.002`, `.003`. Ignora los `-update.tar.xz`, `.patch` y `.diff`. Yo usé la v1.3.1 y luego actualicé. |
| **Loader de Linux** | [Releases de rmuxwashere/ps5-linux-loader](https://github.com/rmuxwashere/ps5-linux-loader/releases) | `ps5-linux-loader-v35.elf` (v3.5), el loader que recomienda el README de VivaLaVent. |
| **WebKit Autoloader** | [Releases de itsPLK/ps5-webkit-autoloader](https://github.com/itsPLK/ps5-webkit-autoloader/releases) | `webkit-autoloader-installer_v0.6.1.elf`. Opcional, para arrancar con un clic ([paso 9](09-autoloader.md)). |

### Comprueba el archivo de firmware

El PUP de Update 13.60 ocupa exactamente 1.247.471.104 bytes y tiene este MD5:

```bash
md5 -q PS5UPDATE.PUP
# 06a74efce009503170b7add7fecfeb36
```

También puedes comparar su SHA256 con la [lista de firmwares de MewX](https://github.com/MewX/ps5-official-firmware-list).

### Comprueba los archivos de la imagen {#check-the-image-files}

Compara cada parte con el SHA256 publicado en la página de la release:

```bash
shasum -a 256 ps5-bazzite-deck-v*.img.7z.00*
```

## Herramientas en el ordenador

=== "macOS"

    ```bash
    brew install sevenzip
    ```

    `diskutil`, `dd`, `nc` y `ssh` vienen de serie.

=== "Windows"

    [7-Zip](https://www.7-zip.org/) para descomprimir la imagen, [Rufus](https://rufus.ie/) o [balenaEtcher](https://etcher.balena.io/) para grabarla, y una versión de netcat (o las herramientas [PS5 Payload Sender](https://github.com/search?q=ps5+payload+sender)) para enviar archivos `.elf`. *No lo he probado.*

=== "Linux"

    `p7zip`, `dd`, `netcat` y `ssh` desde tu gestor de paquetes. *No lo he probado.*
