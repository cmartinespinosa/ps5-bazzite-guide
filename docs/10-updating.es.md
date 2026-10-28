# 10. Actualizar Bazzite

PS5 Bazzite Deck se actualiza **en el sitio**: sin volver a grabar nada, tus juegos y ajustes se mantienen. Una actualización sustituye el kernel y los módulos; el script hace antes una copia de seguridad.

Mira tu versión:

```bash
cat /etc/ps5-bazzite-deck-version
```

(`uname -r` no sirve: se queda en `7.3.0` en todas las versiones.)

## Opción A: el plugin de Decky

Con [PS5 Bazzite Updater](08-decky-plugins.md#ps5-bazzite-updater-one-click-updates) instalado, recibes una notificación de Steam cuando sale una versión nueva. Abre Decky → **PS5 Updates** → *Install and power off*. Descarga la actualización, comprueba su SHA256, ejecuta el propio `update.sh` del proyecto y apaga solo si el script termina con `DONE`.

!!! note
    El flujo completo de instalar y apagar todavía no se ha probado de principio a fin a través del plugin. Si falla, usa la opción B y [abre un issue](https://github.com/cmartinespinosa/decky-ps5-bazzite-updater/issues).

## Opción B: a mano

Última versión **estable**, un solo comando:

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/VivaLaVent/ps5-bazzite-deck/main/tools/update-latest.sh)
```

Solo ve versiones estables. Para una versión **concreta** (por ejemplo una pre-release), pon `V` y ejecuta:

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

El script hace la copia en `/var/lib/ps5-update-backup/<fecha>/`, termina con **`DONE`** e imprime un **comando para deshacer**. Guárdalo en algún sitio.

## Después de actualizar

1. **Apaga** (un kernel nuevo necesita un arranque en frío).
2. Arranca con el loader o el autoloader como siempre. El primer arranque puede quedarse en negro un rato.
3. Puede que tengas que volver a emparejar el DualSense.

## Enterarte de nuevas versiones sin el plugin

En GitHub, abre [VivaLaVent/ps5-bazzite-deck](https://github.com/VivaLaVent/ps5-bazzite-deck) → *Watch → Custom → Releases*. O suscríbete al [feed RSS](https://github.com/VivaLaVent/ps5-bazzite-deck/releases.atom).
