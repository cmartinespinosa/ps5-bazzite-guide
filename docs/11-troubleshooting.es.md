# 11. Solución de problemas

## Arranque

### Relapse se cuelga en "checking aio groups" {#relapse-hangs-at-checking-aio-groups}

El jailbreak (en el navegador o en el autoloader) se para en *Kernel: checking aio groups*, o la página deja de responder. Es una carrera de tiempos. Responde *Sí* para detener la página, reinicia la PS5 y vuelve a intentarlo. Funciona mejor justo después de encender, sin otras apps abiertas.

### La PS5 solo pita y no enciende

Tras un cuelgue del autoloader, la consola puede negarse a arrancar. **Desenchufa el cable de corriente 30 segundos**, vuelve a enchufarlo y enciende.

### De vuelta en el sistema de la PS5 tras el loader (luz azul parpadeando)

Pulsaste el botón de encendido antes de que la luz naranja estuviera **fija**. Envía el loader otra vez, espera la naranja fija y luego **5–10 segundos más**.

### Cada reinicio de Linux acaba en el sistema de la PS5

Es lo esperado. Usa *Apagar*, nunca *Reiniciar*.

### Pantalla gris con un cursor de ratón

Steam está arrancando. Espera unos minutos. Si dura más de 10 minutos, mantén pulsado el botón de encendido 10 segundos y vuelve a arrancar.

### Pantalla negra tras editar `cmdline.txt`

Restaura la copia si hiciste una, y haz siempre `sync` antes de apagar:

```bash
sudo cp /boot/efi/cmdline.txt.bak /boot/efi/cmdline.txt && sync && sudo poweroff
```

Si Linux no arranca de ninguna forma, enchufa el pendrive a un ordenador y arregla `cmdline.txt` en su partición `boot`.

!!! danger "No uses el desbloqueo de 40 CU"
    Añadir `amdgpu.ps5_cu_unlock=3` a `cmdline.txt` me dio pantalla negra y cuelgues de la GPU (`ring gfx timeout`, `GPU Recovery Failed`). Tu consola puede ser distinta, pero la mía no lo aguantó.

## Juegos

### Elden Ring / Sekiro atascados a ~40 fps

Incluso a 720p, con la GPU casi sin uso. La causa es la versión de Proton, no el hardware. **Fuerza Proton 9**: en Steam, juego → *Propiedades → Compatibilidad* → *Forzar el uso de una herramienta de compatibilidad de Steam Play* → **Proton 9**. Sekiro pasa a ir a 60.

Prueba primero Proton 9 con cualquier juego de FromSoftware, o con cualquier juego que vaya peor de lo que debería.

### Elden Ring se queda en un icono de carga infinito

Pasó con Proton 11.0. Cambia a Proton 9 (o Experimental).

### Los juegos se cierran al menú de Steam tras ~10 minutos

Visto en RoboCop: Rogue City y Fatekeeper. El log del sistema muestra un `page fault … PERMISSION_FAULTS` de amdgpu desde `gamescope`, luego `ring gfx_0.0.0 timeout`, y gamescope se cierra. Es un bug del driver de GPU del kernel, no del juego.

- La v1.5.0 incluye un arreglo de GPU para esto. La v1.5.1 todavía lo lista como problema conocido, así que **actualiza a la última versión**.
- Si sigue pasando, ejecuta esto justo después del cierre y comparte el resultado con el proyecto (ver el [README de PS5 Bazzite Deck](https://github.com/VivaLaVent/ps5-bazzite-deck) para saber dónde):

    ```bash
    ps5-report
    ```

## Otros

### `passwd` dice BAD PASSWORD

Usa al menos 8 caracteres.

### Decky no aparece

Reinicia la sesión de Steam por SSH:

```bash
systemctl --user restart gamescope-session-plus@ogui-steam.service
```

### Deshacer una actualización

`update.sh` imprimió un comando para deshacer cuando actualizaste. Las copias están en `/var/lib/ps5-update-backup/`.
