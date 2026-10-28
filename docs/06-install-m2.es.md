# 6. Primer arranque de Linux e instalación en el M.2

El primer arranque ejecuta Bazzite **desde el pendrive**. Solo lo usas para copiar Bazzite al M.2, así que hazlo mínimo: Wi-Fi y SSH, nada más. No instales juegos aquí.

## 6.1 Arranca Linux desde el pendrive

1. Reinicia la PS5 y [haz el jailbreak](03-jailbreak.md).
2. Desde tu ordenador, envía el loader al puerto 9021:

    ```bash
    nc -w 5 <PS5_IP> 9021 < ps5-linux-loader-v35.elf
    ```

3. El loader encuentra los archivos de arranque en el pendrive y pone la PS5 en modo reposo. Mira la barra de luz:
    - **naranja parpadeando** → espera →
    - **naranja fija** → espera **otros 5–10 segundos** →
    - pulsa el **botón de encendido** de la PS5.
4. Una luz **blanca** significa que Linux está arrancando.

!!! note "Ten paciencia"
    El primer arranque muestra una **pantalla negra durante unos 5 minutos**. Luego aparece el asistente de Bazzite a 1080p: idioma, Wi-Fi, inicio de sesión en Steam.

    Cuando el asistente reinicia, la PS5 vuelve a su sistema normal. Es lo esperado: **cada reinicio de Linux acaba en el sistema de la PS5**. Haz el jailbreak y envía el loader otra vez.

    Después, una **pantalla gris con un cursor** en la esquina superior izquierda durante unos minutos también es normal: Steam está arrancando.

## 6.2 Conéctate por SSH

SSH viene activado. Usuario **`ps5`**, contraseña **`ps5`**.

1. Averigua la IP de Linux: Steam → *Ajustes → Internet*, o la lista de dispositivos de tu router. En esta guía se llama `<LINUX_IP>`.
2. Desde tu ordenador:

    ```bash
    ssh ps5@<LINUX_IP>
    ```

3. Opcional, para no escribir la contraseña: `ssh-copy-id ps5@<LINUX_IP>`.

## 6.3 Copia la imagen a la PS5

El instalador del M.2 necesita la imagen descomprimida **en la PS5**. Copia las tres partes y descomprímelas allí:

```bash
scp ps5-bazzite-deck-v1.3.1.img.7z.00* ps5@<LINUX_IP>:Downloads/
```

Luego, en la PS5 (por SSH):

```bash
cd ~/Downloads
sha256sum ps5-bazzite-deck-v1.3.1.img.7z.00*
7z x -y ps5-bazzite-deck-v1.3.1.img.7z.001
```

Obtienes `~/Downloads/ps5-bazzite-deck.img`. Por Wi-Fi la copia va a unos 10 MB/s, así que cuenta con 15–20 minutos.

## 6.4 Añade una partición Linux al M.2

Descarga las [ps5-linux-tools](https://github.com/ps5-linux/ps5-linux-tools), compílalas y ejecuta `m2_init`:

```bash
git clone https://github.com/ps5-linux/ps5-linux-tools ~/ps5-linux-tools
cd ~/ps5-linux-tools
make
lsblk /dev/nvme0n1
sudo ./m2_init
```

Resultado esperado: **`Successfully added Linux partition to m2.`** Aparece una partición nueva, `nvme0n1p1`.

## 6.5 Instala Bazzite en el M.2

Hazte root y monta la partición de arranque del pendrive:

```bash
sudo -i
mkdir -p /boot/efi
umount /boot/efi 2>/dev/null
mount LABEL=boot /boot/efi
```

Ejecuta el instalador:

```bash
cd /var/home/ps5/ps5-linux-tools
./m2_install.sh --install /var/home/ps5/Downloads/ps5-bazzite-deck.img
```

Formatea la partición del M.2 (etiqueta `bazzite-deck-m2`) y copia ~12 GB. **No muestra progreso**: parece colgado pero no lo está. A mí me tardó 2–5 minutos. Termina con **`Installation complete.`**

Haz que el arranque apunte al M.2:

```bash
sed -i 's/root=LABEL=bazzite-deck /root=LABEL=bazzite-deck-m2 /' /boot/efi/cmdline.txt
cat /boot/efi/cmdline.txt
sync
```

Comprueba que la línea contiene ahora **`root=LABEL=bazzite-deck-m2`**.

!!! danger "Siempre `sync`"
    La partición de arranque es FAT32. Si apagas justo después de editar un archivo sin hacer `sync`, el archivo puede quedarse **vacío** y Linux no arrancará.

## 6.6 Arranca desde el M.2

1. En Steam: *Apagar → **Apagar*** (nunca *Reiniciar*).
2. Enciende la PS5, haz el jailbreak, envía el loader, espera la luz naranja fija y pulsa encendido.

Bazzite ya corre desde el M.2. Es una **instalación nueva**: verás otra vez el asistente, puede cambiar la IP y la contraseña vuelve a ser `ps5`. Sigue con la [configuración del primer arranque](07-first-boot.md).
