# Alerta de convocatorias · Click+Clack

Revisa una vez al día las páginas de convocatorias de cooperación internacional, gobierno nacional y fundaciones que le interesan al equipo de alianzas de Click+Clack, y avisa cuáles cambiaron y qué apareció.

**Tablero:** https://juanjose-muri.github.io/alerta-convocatorias-click/

SECOP II no se vigila aquí (carga con JavaScript y se consulta por NIT): esa parte se hace aparte con Croma.

## Cómo funciona

1. Un flujo de GitHub Actions corre `scripts/revisar.py` una vez al día (programado a las 6:00 a. m. hora de Colombia; GitHub puede correrlo horas después).
2. El script descarga cada página de `fuentes.txt`, saca el texto visible línea por línea y lo compara con la revisión anterior (`data/textos/`).
3. Si aparecieron o desaparecieron líneas, lo anota en `data/cambios.json`, actualiza `data/estado.json` y el RSS (`data/feed.xml`), y abre un aviso (issue) en el repo, que llega por correo a quien lo siga.
4. Si una página no responde, las demás siguen. Cada corrida queda en `data/corrida.json`.
5. Los lunes y miércoles, Claude lee `data/cambios.json`, cruza con el barrido de SECOP y entrega un reporte filtrado por lo que le sirve a Click.

## Agregar o quitar páginas

Edita `fuentes.txt`: una página por línea, `Nombre | dirección`. Si una página cambia mucho por cosas que no importan, agrega palabras al final (`Nombre | dirección | educación, convocatoria`) y solo se comparan las líneas que las tengan.

No sirve para páginas que piden iniciar sesión, que cargan todo con JavaScript o que bloquean robots.

Para correr la revisión a mano: pestaña **Actions** → **Revisar convocatorias** → **Run workflow**.

Para no recibir avisos por correo, cambia `AVISOS_GITHUB: "si"` por `"no"` en `.github/workflows/revisar.yml`.

## Crédito

Adaptado de la [Alerta de convocatorias](https://github.com/Estado-X/alerta-convocatorias-colombia) de Estado X (licencia MIT), a su vez inspirada en [changedetection.io](https://github.com/dgtlmoon/changedetection.io), de dgtlmoon (licencia Apache-2.0). Las convocatorias y los datos son de cada entidad.
