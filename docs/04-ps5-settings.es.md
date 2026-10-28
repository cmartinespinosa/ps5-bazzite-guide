# 4. Ajustes de la PS5

Aplica esto en la PS5 **antes del primer arranque de Linux**. Vuelve a aplicarlos si alguna vez restableces los ajustes de la consola.

| Ajuste | Valor | Por qué |
|--------|-------|---------|
| *Ajustes → Sistema → Ahorro de energía → Funciones disponibles en modo reposo → **Suministrar energía a los puertos USB*** | **Siempre** | **Obligatorio.** El loader pone la PS5 en modo reposo antes de arrancar Linux; el USB de arranque tiene que seguir alimentado. |
| *Ajustes → Sistema → HDMI → **Activar enlace de dispositivo HDMI*** | **Desactivado** | **Obligatorio.** Si no, la TV puede despertar o molestar a la consola durante el paso de modo reposo (pantalla negra). |
| *Ajustes → Sistema → Software del sistema → **Actualización y ajustes del software del sistema*** | Descarga e instalación automáticas **desactivadas** | Recomendado. Evita que Sony actualice por encima de 13.60. |
| *Ajustes → Sistema → Software del sistema → **Informar automáticamente de errores del software del sistema*** | **Desactivado** | Recomendado. |

## Instala el SSD M.2

Si aún no lo has hecho, apaga la PS5, desenchúfala y monta el SSD M.2 en la ranura de expansión ([guía de Sony](https://www.playstation.com/es-es/support/hardware/ps5-m2-ssd/)). Enciende y **deja que la PS5 lo formatee** cuando te lo pida. Linux añade su propia partición después.
