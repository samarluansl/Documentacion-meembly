# Guía del Manager — Pablo

Tu rol está pensado para dirigir al equipo comercial desde arriba: ves todo lo que hacen los Members (Roberto y los que vengan), pero no tocas el pool, no asignas leads y no gestionas el equipo. Esa responsabilidad es del Admin (Marta) o del Owner (Samuel).

Si buscas una tarea concreta, empieza por el [índice](./admin-index.md).

## Qué ves al entrar

URL: `/admin`.

- **Home**: KPIs del equipo — "En espera (equipo)", "Pipeline MRR" (global, no solo el tuyo), métricas globales. No ves el tile "Pool sin asignar".
- **Sidebar**: Home · Buscar · Mis leads · En espera · Pendientes · Pipeline · Actividad · Métricas · Clubes · Soporte · Objetivos · Instancias · Ajustes.
  - **No ves**: Pool, Prospectos, Marketing, Equipo, Auditoría.

## Cómo funciona tu "scope"

El scope es el filtro silencioso que el sistema aplica a tus queries. Tú ves:

- **Leads, deals y actividad de todos los Members del equipo** (Roberto y los que vengan).
- **Lo que tengas asignado a ti directamente** (si acaso).

No ves leads asignados a otro Manager, Admin, Owner o Viewer. Tampoco ves leads sin asignar (pool) — para eso habría que darte `pool.view` con un override explícito.

Scope aplicado en:

- `/admin/dashboard/leads` (Mis leads) — personalmente verás los tuyos, pero en los listados generales y en `/leads/waiting`, `/leads/pending`, `/deals`, `/activity`, `/search` verás también lo del equipo.
- Pipeline Kanban — todos los deals del equipo.
- Actividad (feed) — todas las actividades del equipo.

Owner/Admin/Viewer pasan sin filtro (ven todo). Member solo ve lo suyo.

## Tu trabajo diario

### Pipeline y actividad del equipo

Sidebar → **Pipeline**.

Kanban con los deals del equipo (NEW → CONTACTED → QUALIFIED → DEMO → PROPOSAL → WON/LOST). Filtros: owner (filtrar por Roberto en concreto, por ejemplo), prioridad A/B/C, instancia Odoo, monto mínimo/máximo.

Tú **no puedes mover deals** (gate `crm.deals.write` no lo tienes). Solo observas y envías feedback al Admin o al Member.

Sidebar → **Actividad** — feed global con cada email enviado, WA, IG, llamada, nota, stage change de todo el equipo. Útil para ver qué ha hecho Roberto hoy sin tener que abrir cada lead.

### Pendientes del equipo

Sidebar → **Mis leads → Pendientes**. Lista leads con actividad entrante sin atender de todo el equipo. Te sirve como semáforo: si ves que Roberto acumula pendientes, ya sabes por dónde empujar.

Tú puedes **marcar actividades como gestionadas** (gate `crm.activities.send` sí lo tienes) pero, por norma, eso lo hace el comercial que trabaja el lead.

### Métricas

Sidebar → **Métricas**. KPIs globales del equipo — leads trabajados, deals cerrados, MRR, tasa de conversión por stage, ranking por comercial, objetivos vs. real.

Todos los roles ven métricas sin filtro (decisión del plan v2). Si un objetivo necesita tu validación, tú lo lees — editar objetivos es del Admin.

### Panel clubes

Sidebar → **Clubes**. Ves los tres tabs completos:

- **Activos**: clubes en producción (nombre, ciudad, deporte, manager, integraciones, instancia Odoo, fecha creación).
- **Onboarding**: score y checklist de clubes nuevos.
- **Renovaciones**: clubes con renovación próxima (90 días).

**No puedes** crear clubes nuevos ni convertir leads a clubes — eso es Admin/Owner.

### Customer Success (absorbido en Clubes)

`/admin/dashboard/customer-success` redirige a Clubes → tab Onboarding. La información antigua sigue viva, solo que unificada con el panel de clubes.

### Buscar

Sidebar → **Buscar**. Búsqueda global por nombre de club, email, teléfono, IG handle. El resultado está filtrado por tu scope — solo ves leads del equipo (o tuyos).

### Soporte (read-only)

Sidebar → **Soporte**. Ves conversaciones, drafts, analytics, knowledge base. **No puedes aprobar** drafts, ni rechazarlos, ni editar la KB (gate `support.manage` no lo tienes). Si ves algo raro, escalas a Marta o Samuel.

### Actividades — enviar comunicaciones

Como Manager puedes **enviar** email / WhatsApp / IG / registrar llamadas (gate `crm.activities.send`). Útil cuando tienes que entrar a un lead concreto a reforzar. El ownership sigue siendo del Member al que está asignado — tú quedas registrado en el log como quien envió la actividad.

### Conectar tu Gmail personal

Ajustes → Email. OAuth con Google para que los emails que mandes desde el CRM salgan desde tu cuenta. Pasos iguales que para cualquier miembro.

## Qué NO puedes hacer

- **Asignar leads** del pool a comerciales (gate `crm.leads.assign` — Owner/Admin only).
- **Ver el pool** (gate `pool.view` — Owner/Admin only). Si necesitas ver leads sin asignar para tomar decisiones, pídele a Marta que los reparta o que te dé `pool.view` como override temporal.
- **Editar leads o deals**: no tienes `crm.leads.write` ni `crm.deals.write`. Si detectas un dato erróneo o un deal mal valorado, escalas al Member o al Admin.
- **Ver prospectos** (gate `prospects.view`). Son pre-funnel; cuando un prospecto se convierte en lead aparece en tu scope.
- **Ver marketing** (gate `marketing.admin`). No es parte de tu rol — el marketing lo gestionan Samuel y Marta.
- **Gestionar equipo** (invitar, desactivar, cambiar roles, editar overrides). Eso es Admin/Owner.
- **Ver auditoría del equipo** (gate `audit.view`). Si necesitas saber quién hizo qué, se lo pides a Marta.

### Nota sobre detalle de leads de Members

Cuando abres un lead que está asignado a Roberto (no a ti), puede que la página de detalle te devuelva "Este lead no es tuyo". Es una inconsistencia conocida entre el scope de la **lista** y el scope de la **página de detalle** — el detalle hoy solo deja entrar a Owner/Admin o al Member propietario. Si te topas con ella y necesitas el detalle, hay dos vías: pedirle a Marta que te abra el lead (puede hacer lo que sea), o abrirlo como Viewer temporal (impracticable día a día). Está en el backlog para homologar.

## Cómo escalar

- **Lead mal asignado o perdido**: a Marta (Admin). Ella libera y reasigna.
- **Objetivos no cuadran**: a Marta o Samuel. Tú los lees, ellos los editan.
- **Detalle de un lead de Roberto que no puedes abrir**: a Marta para que te lo enseñe o cambie puntualmente el scope.
- **Decisión sobre un prospecto o un marketing push**: a Marta/Samuel.

## Lecturas complementarias

- [role-admin.md](./role-admin.md) — qué hace Marta que tú no.
- [role-member.md](./role-member.md) — el día a día de Roberto, para entender qué supervisas.
- Plan de roles v2: [docs/plan-roles-crm-v2.md](../plan-roles-crm-v2.md).
