# 3. Jailbreak con Relapse

Relapse es un exploit que funciona en el navegador. Lo abres desde la página de la **Guía del usuario** de la PS5, que se redirige al exploit gracias a un servidor DNS personalizado.

## Configura el DNS

1. *Ajustes → Red → Ajustes → Configurar conexión a internet*.
2. Selecciona tu red Wi-Fi → *Ajustes avanzados*.
3. **Ajustes de DNS: Manual**, DNS primario: **`45.56.67.85`**.
4. Guarda.

!!! tip
    Yo dejo este DNS de forma permanente: además bloquea los servidores de actualización de Sony, lo que te protege de una actualización de firmware accidental.

## Ejecuta el exploit

1. Abre *Ajustes → Guía del usuario, salud y seguridad y otra información → Guía del usuario*.
2. Se carga la página de Relapse. Comprueba que detecta el firmware correcto.
3. Selecciona **Jailbreak** y espera.
4. Éxito: un mensaje que dice **`elfldr is listening on port 9021`**. La PS5 ya acepta payloads `.elf` en el puerto 9021.

Si se congela o la consola reinicia, vuelve a intentarlo. Es una carrera de tiempos y a menudo necesita un segundo intento. Ver [Solución de problemas](11-troubleshooting.md#relapse-hangs-at-checking-aio-groups).

## Averigua la IP de la PS5

*Ajustes → Red → Estado de la conexión → Ver estado de la conexión*. Apunta la **dirección IPv4**. En esta guía se llama `<PS5_IP>`.

!!! warning "Camino Linux: que esté limpia"
    Para arrancar Linux, haz el jailbreak con la PS5 **recién reiniciada** y envía **solo** el loader de Linux. No envíes antes kstuff, etaHEN ni otros payloads homebrew: son incompatibles con el loader de Linux y la consola se congela en vez de entrar en modo reposo.
