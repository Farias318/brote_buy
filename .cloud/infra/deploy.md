# Despliegue — brote_buy

## Proveedor
Todavía **no está desplegado**. Es un `index.html` estático (sin build, sin dependencias), así que
por ahora alcanza con free-tier estático:

- **Corto plazo (frontend actual tal cual):** Vercel, Netlify o GitHub Pages — cualquiera sirve para
  un HTML estático, elegir el que ya se use en otros proyectos del workspace por consistencia.
- **Cuando se implemente el Tier 2 de `../../docs/analisis-mejoras.md`** (backend Node/TS + Postgres):
  sumar Railway o Render (free-tier) para backend + base de datos, manteniendo el frontend en el
  proveedor estático elegido arriba.

## Checklist antes de desplegar
- [ ] Variables de entorno cargadas en el proveedor (ver `.env.example`) — hoy no aplica, no hay backend
- [ ] Build corre sin errores en local — hoy no aplica, no hay build
- [ ] Base de datos migrada / seed cargado si aplica — hoy no aplica
- [ ] Dominio o subdominio configurado
- [ ] CI/CD (si aplica) corriendo en cada push a main

## URL de producción
<!-- Completar cuando esté desplegado -->
