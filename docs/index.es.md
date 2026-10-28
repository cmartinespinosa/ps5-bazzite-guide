# Guía PS5 Bazzite

Esta guía lleva una **PS5 base de serie** hasta **[PS5 Bazzite Deck](https://github.com/VivaLaVent/ps5-bazzite-deck)** (un Linux parecido a SteamOS) funcionando desde el SSD M.2 interno de la consola, con plugins de Decky, control de ventiladores, actualizaciones con un clic y soluciones a los problemas que me encontré.

Es exactamente el camino que seguí con mi consola en octubre de 2026. Todos los comandos se ejecutaron de verdad; cuando algo falló, la guía lo dice.

!!! warning "Lee esto primero"
    - Esto es **no oficial** y **bajo tu propia responsabilidad**. Un jailbreak puede inutilizar la consola o hacer que te baneen de PSN.
    - Necesitas un firmware compatible con el jailbreak. Esta guía usa el **13.60**. Si tu PS5 ya tiene un firmware más nuevo, para aquí: no se puede volver atrás.
    - El SSD M.2 que uses para Linux se borra.
    - El mérito es de quienes hicieron el trabajo de verdad: los autores del exploit Relapse, el proyecto [ps5-linux](https://github.com/ps5-linux), [el loader de rmux](https://github.com/rmuxwashere/ps5-linux-loader), [VivaLaVent](https://github.com/VivaLaVent/ps5-bazzite-deck), [itsPLK](https://github.com/itsPLK/ps5-webkit-autoloader) y [Hooandee](https://github.com/Hooandee/panel-de-control).

## Cómo funciona, en un minuto

1. La PS5 se libera desde su propio navegador web (el exploit **Relapse**).
2. Se envía a la PS5 un payload, el **loader de Linux**. Pone la consola en modo reposo y la despierta arrancando un kernel Linux desde un **pendrive USB**.
3. El pendrive solo guarda los archivos de arranque. El sistema en sí vive en el **SSD M.2**.
4. Bazzite arranca en la interfaz Big Picture / Steam Deck de Steam. Juegas con un DualSense como en una Steam Deck.
5. Cada vez que enciendes, repites los pasos 1–2. Una app **autoloader** lo reduce a un clic.

## Los pasos

| # | Paso | Tiempo |
|---|------|--------|
| 1 | [Requisitos](01-requirements.md) | — |
| 2 | [Actualizar el firmware a 13.60](02-firmware.md) | 20 min |
| 3 | [Jailbreak con Relapse](03-jailbreak.md) | 5 min |
| 4 | [Ajustes de la PS5](04-ps5-settings.md) | 5 min |
| 5 | [Grabar el USB de arranque](05-boot-usb.md) | 15 min |
| 6 | [Primer arranque de Linux e instalación en el M.2](06-install-m2.md) | 1 h |
| 7 | [Configuración del primer arranque](07-first-boot.md) | 15 min |
| 8 | [Decky Loader y plugins](08-decky-plugins.md) | 15 min |
| 9 | [Autoloader de un clic](09-autoloader.md) | 10 min |
| 10 | [Actualizar Bazzite](10-updating.md) | 10 min |
| 11 | [Solución de problemas](11-troubleshooting.md) | — |

## Mi equipo

- PS5 base (con lector, modelo de lanzamiento), firmware 13.60
- SSD NVMe M.2 de 1 TB con disipador
- Pendrive SanDisk 250 GB USB 3.2, siempre enchufado en un puerto USB-A trasero
- PS5 Bazzite Deck v1.5.1, Decky Loader v3.3.0
- Un Mac para prepararlo todo (se indican alternativas para Windows/Linux donde cambian)
