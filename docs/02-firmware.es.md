# 2. Actualizar el firmware a 13.60

Sáltate este paso si tu PS5 ya está en 13.60.

!!! danger "Nunca actualices por internet"
    La actualización online de Sony instala el firmware **más reciente**, que el jailbreak no soporta. Antes de conectar la PS5 a internet, desactiva las actualizaciones automáticas (ver [paso 4](04-ps5-settings.md)) y actualiza solo por USB con el archivo exacto de abajo.

## Prepara el pendrive

El pendrive debe estar formateado en **exFAT** o **FAT32** y contener el archivo en `PS5/UPDATE/PS5UPDATE.PUP` (en mayúsculas).

=== "macOS"

    Busca el número de disco del pendrive (p. ej. `disk4`) con `diskutil list` y luego:

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
        Revisa bien el número de disco. `eraseDisk` sobre el disco equivocado lo borra.

=== "Windows"

    Formatea el pendrive en exFAT desde el Explorador, crea las carpetas `PS5\UPDATE` y copia dentro el archivo como `PS5UPDATE.PUP`.

## Instalar desde el modo seguro

1. **Apaga del todo** la PS5 (no modo reposo).
2. Enchufa el pendrive en un USB-A trasero o en el USB-C frontal.
3. Mantén pulsado el botón de encendido hasta el **segundo pitido** (unos 7 segundos). La PS5 arranca en modo seguro.
4. Conecta el DualSense **con el cable** y pulsa el botón PS.
5. Elige **3. Actualizar el software del sistema → Actualizar desde un dispositivo de almacenamiento USB**.
6. Comprueba que en pantalla pone **13.60** y confirma.

!!! danger
    No elijas *Restablecer*, *Reinstalar el software del sistema* ni *Reconstruir base de datos* en el modo seguro.

Cuando la consola reinicie, confirma la versión en *Ajustes → Sistema → Software del sistema → Información de la consola*.
