# Análisis y esquema de mejoras — brote_buy

> Este documento es un esquema para decidir próximos pasos, no un compromiso de implementación. Cada
> ítem se aborda en una conversación/tarea futura, priorizado de mayor a menor impacto.

## Diagnóstico del estado actual

### Fortalezas
- **Producto ya completo y usable**: billeteras multi-moneda (ARS/USD), gastos por categoría,
  créditos en cuotas, deudas fijas, metas de ahorro con "cosecha", gamificación (XP, niveles, rachas,
  logros), import de resúmenes bancarios (CSV con mapeo de columnas), export/import de datos en JSON,
  cotización de dólar blue (automática o manual).
- **Cero infraestructura**: corre 100% en el navegador, sin costo de hosting ni backend que mantener.
- **UI cuidada**: tema oscuro, tipografía custom (Space Grotesk / JetBrains Mono), drag-and-drop para
  reordenar billeteras, undo de borrados, toasts, meta tags de PWA (`mobile-web-app-capable`, etc.).
- **Sanitización básica presente**: `esc()` escapa HTML de los datos ingresados por el usuario antes
  de insertarlos en el DOM (mitiga XSS por esa vía).

### Debilidades / riesgos
1. **Persistencia y sync frágiles.** Todo vive en `localStorage`: se pierde si el usuario borra el
   caché del navegador o cambia de dispositivo sin sincronizar. El sync entre dispositivos es un hack
   contra la API de GitHub Gists: requiere que el usuario genere un Personal Access Token de GitHub y
   lo pegue a mano en cada dispositivo, y ese token queda **guardado en texto plano en
   `localStorage`** (visible desde devtools, sin expiración gestionada por la app). No hay
   autenticación real: cualquiera con el token + el ID del gist accede a los datos financieros.
2. **Sin base de datos real.** El "modelo de datos" es un único objeto JS (`S`) serializado a JSON —
   no hay integridad referencial, no hay backups automáticos ni forma de auditar/recuperar historial
   con confianza más allá de lo que el usuario exporte manualmente.
3. **Archivo monolítico.** ~2850 líneas de HTML + CSS + JS mezcladas en un solo `index.html` — diffs
   de git enormes ante cualquier cambio chico, difícil de testear o de mostrar como código
   "profesional" en un portfolio.
4. **Sin tooling.** No hay `package.json`, build, linter ni tests — toda la lógica (cálculo de
   cuotas, conversión de moneda, XP/niveles) vive sin cobertura de pruebas.
5. **No usa el stack objetivo del workspace.** Tal como está, no sirve como pieza de portfolio que
   demuestre Node/TS + SQL — que es justamente la fortaleza real del usuario (SQL, diseño de bases de
   datos, integraciones) que este workspace busca canalizar hacia un stack moderno.

## Esquema priorizado de mejoras

### Tier 1 — bajo/medio esfuerzo, mejora inmediata
No tocan la lógica de negocio, son reorganización y piezas faltantes:

1. **Separar `index.html`** en `index.html` + `estilos.css` + `app.js` (o módulos JS por dominio:
   billeteras, gastos, créditos, metas, gamificación). Mismo comportamiento, código mantenible y con
   diffs razonables.
2. **Mitigar el riesgo del token de Gist** a corto plazo: como mínimo, dejar una advertencia visible
   en la UI de configuración sobre qué implica pegar un token ahí; a mediano plazo se resuelve de raíz
   con el Tier 2.
3. **Completar el PWA**: ya están los meta tags (`mobile-web-app-capable`, `theme-color`), pero falta
   el `manifest.json` y un service worker — sin eso, no es instalable ni funciona offline como app.

### Tier 2 — la mejora estrella
4. **Backend propio: Node.js/TypeScript (Express o Nest) + PostgreSQL**, con autenticación real
   (email+password o magic link) y endpoints REST para wallets, gastos, créditos, deudas y metas. El
   frontend (ya modularizado en el Tier 1) pasa a consumir esa API en vez de `localStorage` + Gist.
   - Resuelve de raíz el problema de sync/seguridad del Tier 1.2.
   - Es exactamente la pieza que el roadmap del workspace pide como "primer proyecto freelance real"
     (`../../.cloud/roadmap.md`, ítem 3: "dashboard con base de datos").
   - Aprovecha la experiencia real del usuario en SQL y diseño de bases de datos, sumando práctica
     concreta de Node/TS en el backend — el objetivo declarado del workspace.

### Tier 3 — pulido adicional
5. **Tests** de la lógica más sensible: cálculo de cuotas de crédito, conversión de moneda (ARS/USD
   con cotización blue), cálculo de XP/niveles/rachas.
6. **Evaluar migrar el frontend a React/Next** — opcional. El vanilla JS actual funciona bien; migrar
   solo si aporta valor de portfolio adicional o si el mantenimiento del frontend se vuelve un cuello
   de botella una vez conectado al backend.
7. **Deploy real**: frontend en Vercel/Netlify/GitHub Pages (gratis), backend + Postgres en
   Railway/Render (free-tier) — actualizar `../.cloud/infra/deploy.md` cuando se concrete.

## Cómo seguir
Este esquema queda anotado en `../.cloud/business/roadmap.md` (sección "Próximo") y en las tareas
activas de `../.claude/CLAUDE.md`. La ejecución de cada tier se coordina en conversaciones futuras —
no hay compromiso de fecha ni de orden estricto más allá de la priorización sugerida acá.
