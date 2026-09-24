# NURA Cells — Cuestionarios

Formularios web (HTML autónomos, bilingües ES/EN) para el sistema de captación y postventa de **NURA Cells**.

## Contenido
| Archivo | Qué es |
|---|---|
| [`cuestionario_candidatura.html`](cuestionario_candidatura.html) | Formulario "¿Eres candidato?" — captura leads y los envía al CRM con su tag de audiencia (dolor crónico / anti-aging). |
| [`encuesta_satisfaccion_nps.html`](encuesta_satisfaccion_nps.html) | Encuesta de satisfacción post-tratamiento con NPS (0–10) y estrellas. |
| [`index.html`](index.html) | Página de inicio con enlaces a ambos formularios. |
| [`seguimiento_resultados.html`](seguimiento_resultados.html) | **Cuestionario de seguimiento de resultados (PROM)**, a los 30, 90 y 180 días del tratamiento. Cinco pasos, con autoguardado. **No se enlaza desde el índice a propósito**: se abre solo desde el enlace personal que el CRM le manda a cada paciente, y sin ese enlace no funciona. |

## Configuración (antes de usar)

**No todos los formularios se configuran igual**, y la diferencia importa.

### `seguimiento_resultados.html` — envío directo al Apps Script

Manda al `/exec` del Apps Script, que escribe la hoja `Resultados` del libro y de ahí espeja a la
ficha del contacto en el CRM. Se editan dos constantes:

```js
appsScriptUrl: 'PEGAR_URL_EXEC_DEL_APPS_SCRIPT',
tokenProm:     'PEGAR_NURA_TOKEN_PROM',
```

**Sí, el token queda a la vista en un archivo público, y está pensado.** No es el token del CRM sino
uno propio, que el Apps Script **confina** a la ruta de resultados y rechaza con 403 en cualquier
otra. Con él a la vista, lo peor que alguien puede hacer es un renglón falso en la hoja de
resultados —el mismo riesgo que ya se acepta porque el enlace del paciente es adivinable—, y nunca
tocar el CRM ni la contabilidad. **Si algún día ese token sirviera para algo más, la decisión entera
deja de sostenerse.**

Sin configurar, `CONFIG.destino` vale `'demo'` y el formulario **rechaza el envío** en vez de fingir
que salió bien: un archivo sin configurar nunca debe mostrarle «¡Gracias!» a un paciente cuyas
respuestas no fueron a ningún lado.

### Los otros dos — webhook del CRM

```js
const WEBHOOK_URL = "PEGAR_URL_WEBHOOK_GHL_AQUI";
```

Se sustituye por la URL del **Inbound Webhook** del Workflow correspondiente
(GHL → Automation → nuevo Workflow → Trigger *Inbound Webhook* → copiar URL). Mientras no se
configure, funcionan en modo demo e imprimen el envío en la consola del navegador.

## Publicar en línea (GitHub Pages, gratis)
1. En este repo: **Settings → Pages**.
2. En *Build and deployment* → *Source*: **Deploy from a branch**.
3. Branch: **main**, carpeta **/ (root)** → **Save**.
4. En 1–2 minutos tus formularios quedan en:
   - `https://<usuario>.github.io/Nura-Cuestionarios/cuestionario_candidatura.html`
   - `https://<usuario>.github.io/Nura-Cuestionarios/encuesta_satisfaccion_nps.html`

> **El nombre del repositorio distingue mayúsculas en la URL.** Es `Nura-Cuestionarios`, con las dos
> iniciales en mayúscula: `nura-cuestionarios` devuelve 404.

## `nura-health/` — cuestionarios de NURA Health

Los 5 cuestionarios del sistema de planes de **NURA Health** (nutrición y entrenamiento) y su índice
interno. **No se editan aquí**: la fuente es `NURA HEALTH/03_CUESTIONARIOS/` y se copian con
`node 02_ARNES/publicar_cuestionarios.js`, que se niega a copiar si las pruebas no están en verde.

- Envían al `/exec` del pipeline de NURA Health (`NH_ENDPOINT`), **no** al CRM ni al Apps Script de
  seguimiento.
- Mientras quede un `[PENDIENTE]` legal o la URL de marcador, **no envían** y muestran la franja
  «CUESTIONARIO NO OPERATIVO». Está hecho a propósito (`NURA HEALTH/05_DOCS/CANDADOS.md`).
- No se enlazan desde el `index.html` de la raíz.

URL: `https://alancastro1997-cloud.github.io/Nura-Cuestionarios/nura-health/<archivo>.html` (distingue mayúsculas).

## Privacidad

Hay que distinguir dos cosas que antes este archivo decía fundidas en una.

**NURA no almacena nada aquí.** El sitio es estático: no hay servidor, no hay base de datos, no hay
analítica y no se carga un solo recurso de terceros —ni fuentes web, ni CDN—. Nada de lo que escriba
un paciente llega a este sitio; los formularios solo reenvían al CRM. El expediente clínico vive de
forma interna en el Google Drive de NURA.

**Pero el navegador del paciente sí guarda un borrador**, y solo en el cuestionario de seguimiento.
Para que nadie pierda lo contestado si se cierra la pestaña, las respuestas se guardan **en el propio
dispositivo** hasta que se envían, y se borran en cuanto el envío sale bien. Con dos excepciones que
importan:

- **La descripción de un efecto no esperado nunca se guarda**, ni siquiera en el dispositivo. Es texto
  libre y un relato puede identificar a alguien sin llevar un solo nombre; un teléfono se presta.
- El borrador es por paciente y por momento, así que la evaluación de los 90 días no puede abrir la de
  los 30.

> La frase anterior de esta sección —*"estos formularios no almacenan datos"*— dejó de ser cierta en
> el instante en que existió el autoguardado. Se corrigió en el mismo commit que lo introdujo. Una
> garantía que el texto afirma y el código no cumple es un defecto, no una imprecisión.

## Licencia
Copyright (C) 2026 NURA Cells.

Este proyecto está licenciado bajo la **GNU Affero General Public License v3.0 o posterior (AGPL-3.0-or-later)** — ver el archivo [`LICENSE`](LICENSE).

Puedes usar, estudiar y modificar el código, pero **cualquier versión distribuida o desplegada (incluso como servicio web) debe liberar su código fuente bajo la misma licencia**. Se distribuye sin garantía.

---
Parte del *Sistema Automatizado NURA* · Guadalajara, México · ¡Vive la experiencia NURA!
