# CLAUDE.md — brote_buy

> Sigue la convención general del workspace en `../../.cloud/estructura.md` (raíz de `Entorno_Emprendedor`).

## Propósito del proyecto
**Brote 🌱 — Tu jardín financiero**: app de finanzas personales gamificada. Maneja billeteras
multi-moneda (ARS/USD con cotización dólar blue), gastos por categoría, créditos en cuotas, deudas,
metas de ahorro, e import de resúmenes bancarios (CSV). La capa de gamificación (XP, niveles, rachas,
logros) es el diferencial frente a un tracker de gastos convencional.

Frente: **Portfolio** — es la pieza que se adopta como el "proyecto freelance real" del roadmap del
workspace (`../../.cloud/roadmap.md`, ítem 3), pensada para demostrar el stack Node/TS + SQL de punta
a punta una vez que se implemente el backend (ver Tier 2 de `../docs/analisis-mejoras.md`).

## Stack
**Actual (se desvía del default del workspace):** un único `index.html` con HTML+CSS+JS inline, sin
build, sin `package.json`. Persistencia 100% client-side vía `localStorage`, con sync opcional entre
dispositivos mediante un hack contra la API de GitHub Gists (usa un Personal Access Token de GitHub
guardado en `localStorage`, pegado a mano por el usuario en cada dispositivo).

**Objetivo (default del workspace, pendiente de implementar):** Node.js/TypeScript (Express o Nest)
+ PostgreSQL como backend real con auth propia, sirviendo a este mismo frontend (o a una versión
modularizada de él). Ver el esquema priorizado completo en `../docs/analisis-mejoras.md`.

## Convenciones específicas
- Mientras no exista backend, cualquier cambio al modelo de datos vive en las funciones
  `defaultState()` / `normalizeState()` dentro del `<script>` de `index.html` — mantenerlas
  sincronizadas si se agregan campos nuevos al estado.
- `esc()` se usa para sanitizar todo dato de usuario antes de insertarlo como HTML (evita XSS) — no
  interpolar strings de usuario sin pasarlos por `esc()`.

## Tareas activas
- [ ] Tier 1 — separar `index.html` en HTML + CSS + JS propios (ver `../docs/analisis-mejoras.md`)
- [ ] Tier 1 — completar PWA real: `manifest.json` + service worker
- [ ] Tier 2 — backend Node/TS + Postgres para reemplazar el sync vía Gist (la mejora estrella)
- [ ] Tier 3 — tests, evaluar deploy real (frontend + backend)

## Contexto relevante
- El token de GitHub para el sync vía Gist se guarda **en texto plano en `localStorage`**
  (`SYNCKEY`), visible desde devtools y sin expiración gestionada por la app — riesgo de seguridad
  conocido, documentado en `../docs/analisis-mejoras.md`, a resolver reemplazando el mecanismo por un
  backend con auth real (Tier 2).
- La cotización de dólar (`fx`) tiene fuente "blue" (fetch automático) o manual — ver `fetchDollar()`
  en `index.html`.
- Versión actual del frontend: `v9.2` (ver `#appVersion` al pie del HTML).
