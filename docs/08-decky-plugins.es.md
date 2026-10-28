# 8. Decky Loader y plugins

[Decky Loader](https://github.com/SteamDeckHomebrew/decky-loader) añade un menú de plugins al menú de acceso rápido de Steam.

## Instala Decky Loader

Bazzite trae un comando para ello. Por SSH:

```bash
ujust setup-decky install
```

Un aviso de `chcon` al final es inofensivo. Luego reinicia Steam para que aparezca Decky (el menú de apagado del mando no tiene *Reiniciar Steam*):

```bash
systemctl --user restart gamescope-session-plus@ogui-steam.service
```

Abre el menú de acceso rápido (botón **`...`**, o **PS + X** en el DualSense, o **Ctrl + 2** en un teclado). El nuevo **icono de enchufe** es Decky.

## Activa el modo desarrollador

Los plugins de abajo no están en la tienda de Decky, así que se instalan desde las opciones de desarrollador:

1. Decky (icono de enchufe) → **icono de engranaje** (ajustes).
2. *General* → **Developer mode: On**.

Aparece una sección nueva, *Developer*, en los ajustes de Decky.

## Panel de Control (ventilador y GPU)

[Panel de Control](https://github.com/Hooandee/panel-de-control), de Hooandee, soporta la PS5 desde la v0.78.0: frecuencia de la GPU, temperatura del chip y **temperatura objetivo del ventilador** (cuatro modos o manual).

1. Descarga `Panel.de.Control.zip` de la [última release](https://github.com/Hooandee/panel-de-control/releases) en la PS5 (Modo escritorio → navegador → `~/Downloads`).
2. Ajustes de Decky → *Developer* → **Install Plugin from ZIP File** → *Browse* → elige el ZIP → *Install*.

O por SSH:

```bash
cd /tmp
curl -fLo pdc.zip https://github.com/Hooandee/panel-de-control/releases/latest/download/Panel.de.Control.zip
sudo unzip -oq pdc.zip -d ~/homebrew/plugins/
sudo systemctl restart plugin_loader
```

Ábrelo desde Decky → *Panel de Control* → sección del ventilador. *TDP: unsupported* es normal en la PS5. El plugin se actualiza solo más adelante.

!!! tip "Calor"
    Un usuario contó que su PS5 se apagó con tres pitidos tras horas con un juego exigente, probablemente por sobrecalentamiento. Desde la v1.5.1 el objetivo del ventilador por defecto es el de la propia consola (~80 °C). Yo vi ~57 °C en reposo y ~81 °C jugando a Elden Ring.

## PS5 Bazzite Updater (actualizaciones con un clic) {#ps5-bazzite-updater-one-click-updates}

[PS5 Bazzite Updater](https://github.com/cmartinespinosa/decky-ps5-bazzite-updater) es un plugin que hice yo. Te avisa cuando sale una versión nueva de PS5 Bazzite Deck, muestra las notas de la versión y puede instalarla y apagar la consola por ti.

1. Ajustes de Decky → *Developer* → **Install Plugin from URL**.
2. Escribe:

    ```
    https://github.com/cmartinespinosa/decky-ps5-bazzite-updater/releases/latest/download/decky-ps5-bazzite-updater.zip
    ```

3. *Install* y confirma. Decky avisa de que se ejecuta como **root**: lo necesita para instalar kernels.

**PS5 Updates** aparece entonces en la lista de plugins. Puedes volver a desactivar el modo desarrollador. Ver [Actualizar Bazzite](10-updating.md).
