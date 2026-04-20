# Guía del Viewer — stakeholders externos (Luis Escobar y similares)

Eres un stakeholder externo con acceso de lectura al panel de Meembly Admin. Ves prácticamente todo lo que hace el equipo — leads, deals, actividad, métricas, clubes — pero no editas nada. Tu rol está pensado para reportings, seguimiento de inversores, asesoramiento externo, etc.

Si buscas algo concreto, empieza por el [índice](./admin-index.md).

## Qué ves al entrar

URL: `/admin`.

- **Home**: KPIs generales del equipo (sin filtros), pipeline MRR global, métricas.
- **Sidebar**: Home · Buscar · Mis leads · En espera · Pendientes · Pipeline · Actividad · Métricas · Soporte · Objetivos · Instancias · Ajustes.
  - **No ves**: Pool, Prospectos, Clubes (panel), Marketing, Equipo, Auditoría.

Tu scope es **todo sin filtro** (igual que Owner/Admin en lectura) — no te restringen a un subconjunto de leads.

## Lo que puedes hacer (todo read-only)

### Leads · Deals · Actividad

- **Mis leads / En espera / Pendientes**: listados completos de todo el equipo.
- **Pipeline**: Kanban con todos los deals, sin permiso de mover.
- **Actividad**: feed global de todo lo que ha hecho el equipo — emails, WA, IG, llamadas, notas, stage changes.
- **Buscar**: búsqueda global.

No puedes editar lead/deal, no puedes asignar, no puedes mover stages. Todos los botones de acción aparecen deshabilitados o directamente no se renderizan.

### Pendientes

Puedes ver qué leads tienen actividad entrante sin atender. **No puedes** marcarlas como gestionadas (gate `crm.activities.send` no lo tienes) — es decisión de quien trabaja el lead.

### Métricas

Sidebar → **Métricas**. KPIs globales, rankings, objetivos vs. real. Ideal para reporting.

### Objetivos

Sidebar → **Objetivos**. Ves los objetivos que Marta/Samuel han fijado. No los editas.

### Soporte (read-only)

Sidebar → **Soporte**. Conversaciones + analytics. **No** apruebas drafts, **no** editas KB. Útil para hacerte una idea del volumen y calidad de soporte a clubes.

### Instancias Odoo

Sidebar → **Instancias**. Ves SPA, MPS, PM, YVR con su estado. No editas credenciales ni desactivas instancias.

## Qué NO puedes hacer

Todo lo que implique tocar algo:

- **Editar leads, deals, actividades**.
- **Enviar comunicaciones** (email/WA/IG/llamadas): tu rol no incluye `crm.activities.send`.
- **Asignar leads**, ver pool, ver prospectos.
- **Panel de clubes**: no tienes `clubs.view`. Si necesitas salud de clientes, pídele a Marta un reporte.
- **Marketing, Equipo, Auditoría**: nada.
- **Ajustes del equipo** (aunque ves "Ajustes" en el sidebar, las subsecciones están gateadas y la mayoría no te dejan entrar).

## Cómo escalar

- **Necesitas un reporte que no puedes extraer desde métricas**: a Marta o Samuel. Normalmente preparan un export ad-hoc.
- **Quieres acceso a una sección que no ves** (p.ej. panel Clubes): al Owner (Samuel) — él decide si te añade `clubs.view` como override puntual.
- **Algo se ve raro o inconsistente**: a Samuel.

## Lecturas complementarias

- Plan de roles v2: [docs/plan-roles-crm-v2.md](../plan-roles-crm-v2.md).
- [admin-index.md](./admin-index.md) — índice por tarea, te lleva directo a la sección de otra guía si necesitas contexto.
