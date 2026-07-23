# NURA Cells — Cuestionarios

Formularios web (HTML autónomos, bilingües ES/EN) para el sistema de captación y postventa de **NURA Cells**.

## Contenido
| Archivo | Qué es |
|---|---|
| [`cuestionario_candidatura.html`](cuestionario_candidatura.html) | Formulario "¿Eres candidato?" — captura leads y los envía al CRM con su tag de audiencia (dolor crónico / anti-aging). |
| [`encuesta_satisfaccion_nps.html`](encuesta_satisfaccion_nps.html) | Encuesta de satisfacción post-tratamiento con NPS (0–10) y estrellas. |
| [`index.html`](index.html) | Página de inicio con enlaces a ambos formularios. |

## Configuración (antes de usar)
Cada formulario envía los datos por webhook. Abre el archivo y reemplaza la constante:

```js
const WEBHOOK_URL = "PEGAR_URL_WEBHOOK_GHL_AQUI";
```

por la URL del **Inbound Webhook** de tu Workflow en GoHighLevel
(GHL → Automation → nuevo Workflow → Trigger *Inbound Webhook* → copiar URL).
Mientras no se configure, el formulario funciona en modo demo (muestra el envío en la consola del navegador).

## Publicar en línea (GitHub Pages, gratis)
1. En este repo: **Settings → Pages**.
2. En *Build and deployment* → *Source*: **Deploy from a branch**.
3. Branch: **main**, carpeta **/ (root)** → **Save**.
4. En 1–2 minutos tus formularios quedan en:
   - `https://<usuario>.github.io/nura-cuestionarios/cuestionario_candidatura.html`
   - `https://<usuario>.github.io/nura-cuestionarios/encuesta_satisfaccion_nps.html`

## Privacidad
Estos formularios **no almacenan datos**: solo los reenvían al CRM. No incluyen datos de pacientes. El expediente clínico vive de forma interna en Google Drive de NURA.

## Licencia
Copyright (C) 2026 NURA Cells.

Este proyecto está licenciado bajo la **GNU Affero General Public License v3.0 o posterior (AGPL-3.0-or-later)** — ver el archivo [`LICENSE`](LICENSE).

Puedes usar, estudiar y modificar el código, pero **cualquier versión distribuida o desplegada (incluso como servicio web) debe liberar su código fuente bajo la misma licencia**. Se distribuye sin garantía.

---
Parte del *Sistema Automatizado NURA* · Guadalajara, México · ¡Vive la experiencia NURA!
