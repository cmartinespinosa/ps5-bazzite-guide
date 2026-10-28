# 8. Decky Loader and plugins

[Decky Loader](https://github.com/SteamDeckHomebrew/decky-loader) adds a plugin menu to Steam's Quick Access menu.

## Install Decky Loader

Bazzite has a built-in command for it. Over SSH:

```bash
ujust setup-decky install
```

A `chcon` warning at the end is harmless. Then restart Steam so Decky appears (the controller's power menu has no *Restart Steam*):

```bash
systemctl --user restart gamescope-session-plus@ogui-steam.service
```

Open the Quick Access menu (**`...`** button, or **PS + X** on the DualSense, or **Ctrl + 2** on a keyboard). A new **plug icon** is Decky.

## Turn on Developer mode

The plugins below aren't in the Decky store, so you install them from Decky's developer options:

1. Decky (plug icon) → **gear icon** (settings).
2. *General* → **Developer mode: On**.

A new *Developer* section appears in Decky's settings.

## Panel de Control (fan and GPU)

[Panel de Control](https://github.com/Hooandee/panel-de-control) by Hooandee supports the PS5 since v0.78.0: GPU clock, chip temperature and **fan target temperature** (four modes or manual).

1. Download `Panel.de.Control.zip` from the [latest release](https://github.com/Hooandee/panel-de-control/releases) onto the PS5 (Desktop Mode → browser → `~/Downloads`).
2. Decky settings → *Developer* → **Install Plugin from ZIP File** → *Browse* → pick the ZIP → *Install*.

Or over SSH:

```bash
cd /tmp
curl -fLo pdc.zip https://github.com/Hooandee/panel-de-control/releases/latest/download/Panel.de.Control.zip
sudo unzip -oq pdc.zip -d ~/homebrew/plugins/
sudo systemctl restart plugin_loader
```

Open it from Decky → *Panel de Control* → fan section. *TDP: unsupported* is normal on the PS5. The plugin updates itself later.

!!! tip "Heat"
    One user reported the PS5 shutting down with three beeps after hours of a demanding game, likely overheating. Since v1.5.1 the default fan target is the console's own (~80 °C). I saw ~57 °C idle and ~81 °C in Elden Ring.

## PS5 Bazzite Updater (one-click updates)

[PS5 Bazzite Updater](https://github.com/cmartinespinosa/decky-ps5-bazzite-updater) is a plugin I made. It tells you when a new PS5 Bazzite Deck version is out, shows the release notes, and can install it and power off for you.

1. Decky settings → *Developer* → **Install Plugin from URL**.
2. Enter:

    ```
    https://github.com/cmartinespinosa/decky-ps5-bazzite-updater/releases/latest/download/decky-ps5-bazzite-updater.zip
    ```

3. *Install* and confirm. Decky warns that it runs as **root**: it needs that to install kernels.

**PS5 Updates** then shows up in the plugin list. You can turn Developer mode off again. See [Updating Bazzite](10-updating.md).
