# Screenshots — pendiente de capturar

Esta carpeta aloja las capturas que referencian las guías de `docs/ops/role-*.md` y `admin-index.md`. A fecha de hoy (2026-04-19) las guías están escritas pero sin screenshots — se capturarán en una iteración posterior.

## Captura pendiente por guía

Formato sugerido: PNG, 1440×900 mínimo, zoom nativo. Anonimizar datos sensibles (emails, teléfonos, nombres de clubes reales) antes de subir.

### role-owner.md / role-admin.md
- [ ] `team-invite-modal.png` — modal de invitar con secciones "Añadir extras" y "Quitar del rol".
- [ ] `team-member-edit.png` — editar rol y overrides de un miembro existente.
- [ ] `pool-table.png` — tabla del pool con filtros y botón asignar.
- [ ] `clubs-panel-activos.png` — tab Activos del panel clubes.
- [ ] `clubs-panel-renovaciones.png` — tab Renovaciones con botón "Ya contactado".
- [ ] `create-club-modal.png` — modal "Crear club".
- [ ] `convert-lead-button.png` — botón "Convertir prospecto → Club" en un lead WON.
- [ ] `prospects-list.png` — listado de prospectos con botón "Convertir en lead".
- [ ] `marketing-meembly-tab.png` — tab Meembly con drafts + botón "Abrir en IG + marcar publicado".
- [ ] `marketing-clubs-tab.png` — tab "Para clubes" con selector de club y acciones approve/propose.
- [ ] `support-drafts.png` — bandeja de drafts con aprobar/rechazar/editar.
- [ ] `support-kb.png` — knowledge base editable.
- [ ] `audit-log.png` — log de auditoría del equipo.
- [ ] `instances-list.png` — listado SPA/MPS/PM/YVR con estado y errores.
- [ ] `targets-edit.png` — edición de objetivos por persona y periodo.

### role-manager.md
- [ ] `home-manager.png` — home vista Manager (KPIs equipo, sin tile pool).
- [ ] `pipeline-manager.png` — Kanban con filtros owner y prioridad.
- [ ] `activity-feed-manager.png` — feed global del equipo.
- [ ] `pending-tray-manager.png` — bandeja de pendientes con scope equipo.
- [ ] `metrics-manager.png` — ranking por comercial.
- [ ] `clubs-manager.png` — panel clubes tal como lo ve Manager (los tres tabs).

### role-postventa.md
- [ ] `home-postventa.png` — home vista Postventa con card "n/4 slots".
- [ ] `lead-detail-postventa.png` — detalle de lead: identity + deal + timeline + composer (sin pestañas WA/IG).
- [ ] `composer-email-upsell.png` — composer Email con plantilla "Meembly upsell" seleccionada y nota de Cc automático a Pablo.
- [ ] `pending-tray-postventa.png` — bandeja de pendientes incluyendo un recordatorio D+14 generado por cron.
- [ ] `release-lead-button.png` — botón "Devolver al pool" en detalle.
- [ ] `waiting-list.png` — listado de leads en espera con vencidos.
- [ ] `gmail-connect.png` — ajustes email / OAuth Google.

### role-venta.md
- [ ] `home-venta.png` — home vista Venta con card "n/4 slots" y tile Clubes.
- [ ] `lead-detail-venta.png` — detalle de lead con composer completo (email + WA + IG + llamada).
- [ ] `composer-whatsapp.png` — composer con pestaña WhatsApp.
- [ ] `composer-instagram.png` — composer con pestaña Instagram DM.
- [ ] `create-club-from-won.png` — botón "Crear club" desde un lead WON.

### role-viewer.md
- [ ] `home-viewer.png` — home Viewer (todo read-only).
- [ ] `pipeline-viewer.png` — Kanban sin permisos de mover.
- [ ] `sidebar-viewer.png` — sidebar con entradas reducidas.

### onboarding-comercial.md
- [ ] `invite-email.png` — email de invitación con magic link.
- [ ] `gmail-connect.png` — OAuth Google en Ajustes → Email (ya listado arriba; reutilizar).
- [ ] `lead-first-contact.png` — detalle de lead en primer contacto, con composer abierto en Email.
- [ ] `lead-lifecycle.png` — diagrama del ciclo `NEW → CONTACTED → QUALIFIED → DEMO → PROPOSAL → WON/LOST` (puede ser ilustración o screenshot del pipeline Kanban).
- [ ] `demo-flow.png` — diagrama del guion de demo (ilustración, no screenshot).
- [ ] `dashboard-cliente-home.png` — home de un dueño dentro de Meembly (lado cliente, `/dashboard`) con sidebar completo. Anonimizar datos reales.

## Cómo capturar

1. Preparar una cuenta de demo con datos anonimizados (script `scripts/seed-demo-crm.ts`).
2. Abrir cada pantalla con el rol correspondiente (tienen que ser 5 sesiones distintas o impersonar vía DB manualmente).
3. Capturar a 1440×900 o superior.
4. Revisar que no aparezcan emails reales, IGs de clubes reales, precios ajenos al demo, etc.
5. Guardar aquí con el nombre exacto indicado.
6. Enlazar desde la guía correspondiente sustituyendo referencias de texto (`Sidebar → Marketing → Tab Meembly`) por `![alt](./screenshots/marketing-meembly-tab.png)`.

## Responsable

Samuel decide cuándo se capturan. Probable slot: post-demo, cuando el estado esté congelado y no cambie 3 veces a la semana.
