# Roadmap — brote_buy

## Hecho
- Frontend funcional completo (v9.2): billeteras multi-moneda, gastos, créditos en cuotas, deudas,
  metas de ahorro, gamificación (XP/niveles/rachas/logros), import de resúmenes bancarios,
  export/import de datos, cotización dólar blue.

## En curso
- Integración del proyecto a la convención estructural del workspace (`.claude/`, `.cloud/`, `docs/`,
  `README.md`) y armado del esquema de mejoras (ver `../../docs/analisis-mejoras.md`).

## Próximo
- **Tier 1**: separar `index.html` en HTML + CSS + JS propios; documentar/mitigar el riesgo del
  token de GitHub en `localStorage`; completar PWA real (`manifest.json` + service worker).
- **Tier 2 (la mejora estrella)**: backend propio Node.js/TypeScript + PostgreSQL con auth real,
  reemplazando el sync vía GitHub Gist — la pieza que convierte a `brote_buy` en la demostración
  end-to-end del stack Node/TS + SQL del workspace.
- **Tier 3**: tests, evaluar deploy real (frontend + backend), evaluar migrar frontend a React/Next
  si se justifica.

Detalle completo del diagnóstico y de cada tier en `../../docs/analisis-mejoras.md`.
