# 7. Configuración del primer arranque

## Cambia la contraseña por defecto

Todo el mundo conoce `ps5` / `ps5`, y SSH está activado. Cámbiala ya:

```bash
ssh -t ps5@<LINUX_IP> passwd
```

La nueva contraseña necesita **al menos 8 caracteres** (las más cortas fallan con `BAD PASSWORD`).

Opcionalmente, vuelve a copiar tu clave SSH (se perdió con la reinstalación):

```bash
ssh-copy-id ps5@<LINUX_IP>
```

## Pantalla

Steam → *Ajustes → Pantalla*:

- **Rango RGB: Completo** (lo recomienda el README de PS5 Bazzite Deck).
- **Resolución**: elige tu mejor modo. 2560×1440 a 60 Hz es lo máximo en un monitor 1440p; el ultrapanorámico no está disponible (ver [Requisitos](01-requirements.md#hardware)).

## Empareja el DualSense por Bluetooth

1. Steam → *Ajustes → Bluetooth*.
2. Con el mando apagado, mantén **PS + Create** hasta que la luz parpadee rápido.
3. Selecciónalo en la lista.

!!! note
    En la v1.3.x, emparejarlo con Linux rompía el emparejamiento con el sistema de la PS5 (había que volver a emparejarlo con cable). Desde la v1.4 Linux usa su propia dirección Bluetooth, así que el mando sigue emparejado con los dos.

## Cómo apagar

Usa siempre Steam → *Apagar → **Apagar***. **Reiniciar** te devuelve al sistema de la PS5 y necesitarás el loader otra vez.

Desde la v1.4.1 también tienes **Suspender**: una pulsación corta del botón de encendido pausa el juego (luz naranja) y otra pulsación corta lo despierta. Ahorra poca energía, porque la GPU sigue encendida.
