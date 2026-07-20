# brote_buy — Brote 🌱

App de finanzas personales gamificada: billeteras multi-moneda (ARS/USD), gastos por categoría,
créditos en cuotas, deudas, metas de ahorro, e import de resúmenes bancarios, con XP/niveles/rachas/
logros como capa de gamificación.

## Demo
<!-- Link a producción, cuando esté desplegado (ver .cloud/infra/deploy.md) -->

## Stack
**Se desvía del default del workspace por ahora.** Es un único `index.html` con HTML+CSS+JS inline,
sin build ni dependencias. Persistencia vía `localStorage`, con sync opcional entre dispositivos a
través de un hack contra la API de GitHub Gists (ver riesgos y plan de reemplazo por un backend
Node/TS + PostgreSQL en [docs/analisis-mejoras.md](docs/analisis-mejoras.md)).

## Cómo correr en local
No requiere instalación: abrir `index.html` directamente en el navegador (o servirlo con cualquier
servidor estático, ej. `npx serve .`).

## Estructura
Este proyecto sigue la convención definida en `.cloud/estructura.md` del workspace
`Entorno_Emprendedor`. Ver también:
- [.claude/CLAUDE.md](.claude/CLAUDE.md) — contexto del proyecto para el agente.
- [docs/analisis-mejoras.md](docs/analisis-mejoras.md) — diagnóstico y esquema priorizado de mejoras.
- [.cloud/business/roadmap.md](.cloud/business/roadmap.md) — roadmap del proyecto.
