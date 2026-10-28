# 10. Updating Bazzite

PS5 Bazzite Deck updates **in place**: no reflashing, your games and settings stay. An update replaces the kernel and modules; the script backs them up first.

Check your version:

```bash
cat /etc/ps5-bazzite-deck-version
```

(`uname -r` doesn't help: it stays `7.3.0` across releases.)

## Option A: the Decky plugin

With [PS5 Bazzite Updater](08-decky-plugins.md#ps5-bazzite-updater-one-click-updates) installed, you get a Steam notification when a new version is out. Open Decky → **PS5 Updates** → *Install and power off*. It downloads the update, checks its SHA256, runs the project's own `update.sh`, and powers off only if the script ends with `DONE`.

!!! note
    The full install-and-power-off flow hasn't been tested end to end through the plugin yet. If it fails, use option B and [open an issue](https://github.com/cmartinespinosa/decky-ps5-bazzite-updater/issues).

## Option B: by hand

Latest **stable** release, one command:

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/VivaLaVent/ps5-bazzite-deck/main/tools/update-latest.sh)
```

This only sees stable releases. For a **specific** version (for example a pre-release), set `V` and run:

```bash
V=v1.5.1
B=https://github.com/VivaLaVent/ps5-bazzite-deck/releases/download/$V
cd ~
curl -LO $B/ps5-bazzite-deck-$V-update.tar.xz
curl -LO $B/ps5-bazzite-deck-$V-update.tar.xz.sha256
sha256sum -c ps5-bazzite-deck-$V-update.tar.xz.sha256
tar xJf ps5-bazzite-deck-$V-update.tar.xz
bash ps5-bazzite-deck-$V-update/update.sh
```

The script backs up to `/var/lib/ps5-update-backup/<date>/`, ends with **`DONE`**, and prints an **undo command**. Copy it somewhere.

## After updating

1. **Shut down** (a new kernel needs a cold boot).
2. Boot with the loader or autoloader as usual. The first boot can stay black for a while.
3. You may need to re-pair the DualSense.

## Getting notified without the plugin

On GitHub, open [VivaLaVent/ps5-bazzite-deck](https://github.com/VivaLaVent/ps5-bazzite-deck) → *Watch → Custom → Releases*. Or subscribe to the [RSS feed](https://github.com/VivaLaVent/ps5-bazzite-deck/releases.atom).
