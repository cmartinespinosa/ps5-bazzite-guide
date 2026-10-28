# 9. Autoloader de un clic

Sin esto, cada arranque significa: jailbreak en el navegador y luego enviar el loader desde un ordenador. [WebKit Autoloader](https://github.com/itsPLK/ps5-webkit-autoloader), de itsPLK, añade una app a la PS5 que hace el jailbreak **y** lanza el loader de Linux de una vez. Sin ordenador.

## 1. Pon el loader en el pendrive

El autoloader busca primero una carpeta `ps5_autoloader` en el USB. Desde Bazzite, `/boot/efi` es la partición de arranque del pendrive. Copia el `.elf` del loader a la PS5 (p. ej. con `scp` a `~/Downloads`) y luego, por SSH:

```bash
sudo mkdir -p /boot/efi/ps5_autoloader
sudo cp ~/Downloads/ps5-linux-loader-v35.elf /boot/efi/ps5_autoloader/
printf "ps5-linux-loader-v35.elf\n" | sudo tee /boot/efi/ps5_autoloader/autoload.txt
sync
```

`autoload.txt` lista los payloads que se envían, uno por línea. Aquí solo va el loader de Linux.

## 2. Instala la app del autoloader

1. Apaga Bazzite, enciende la PS5 y [haz el jailbreak](03-jailbreak.md).
2. Envía el instalador:

    ```bash
    nc -w 10 <PS5_IP> 9021 < webkit-autoloader-installer_v0.6.1.elf
    ```

3. Resultado esperado: *WebKit Autoloader v0.6.1 cached successfully!* y *App installed.*
4. Reinicia la PS5 una vez.

## Uso diario

1. Enciende la PS5.
2. Abre la app **WebKit Autoloader** desde la pantalla de inicio, enseguida, sin otras apps abiertas.
3. Espera la luz **naranja fija**, espera 5–10 segundos y pulsa **encendido**.
4. Juega.
5. Steam → *Apagar → **Apagar***.

!!! note "No siempre funciona a la primera"
    Mis primeros intentos se colgaron (en *Starting…* y en *Kernel: checking aio groups*). Reiniciar la PS5 y volver a probar lo solucionó. Ver [Solución de problemas](11-troubleshooting.md).

!!! tip "Idea: USB puesto = Linux, USB quitado = homebrew de PS5"
    El autoloader lee el `ps5_autoloader` del USB antes que el de `/data`. En teoría puedes guardar otra configuración homebrew en `/data/ps5_autoloader` y usarla solo con desenchufar el pendrive. *No lo he probado.*
