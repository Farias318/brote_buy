# Propuesta de valor — brote_buy

## Problema que resuelve
Llevar el control de plata personal (billeteras en distintas monedas, gastos del día a día, tarjetas
en cuotas, deudas fijas y metas de ahorro) en un solo lugar, sin planillas ni apps genéricas que no
manejan bien el contexto argentino (ARS/USD, dólar blue). El enganche viene de la gamificación
(XP, niveles, rachas, logros, "jardín" que crece) para que llevar el registro no se abandone al
segundo mes, que es el problema típico de las apps de finanzas personales.

## Para quién
Hoy: uso personal. Como pieza de portfolio, el público es doble — reclutadores técnicos evaluando
código presentable, y potenciales clientes freelance que buscan un dashboard con datos + backend
propio (ver `../../.cloud/negocio.md` de la raíz del workspace).

## Diferencial
- Gamificación real integrada al flujo financiero (no es un tracker plano de gastos).
- Maneja multi-moneda con cotización dólar blue automática, algo que la mayoría de las apps
  genéricas de finanzas no contempla para el mercado argentino.
- Import de resúmenes bancarios (CSV) para no cargar todo a mano.
- Hoy funciona 100% sin backend ni costo de hosting — el diferencial de portfolio será mostrar la
  migración prolija a un backend real (Node/TS + Postgres) sin perder esa base ya funcional.

## Llamado a la acción
Como portfolio: que quien lo vea pruebe la demo y note tanto el producto terminado (frontend) como
la arquitectura backend una vez implementada (Tier 2 de `../../docs/analisis-mejoras.md`).
