# Meembly Admin — Índice operacional

Guías por rol para el equipo interno Meembly. Si te preguntas quién eres, mira la tabla de abajo y abre tu guía.

**¿Acabas de entrar al equipo?** Empieza por [onboarding-comercial.md](./onboarding-comercial.md) — te lleva del día 1 al primer cierre real. Luego usa las guías por rol como referencia.

## Quién es quién

```mermaid
flowchart TB
    Owner["OWNER<br/>Samuel<br/>acceso total"]
    Admin["ADMIN<br/>Marta<br/>casi todo excepto tocar al Owner"]
    Manager["MANAGER<br/>Pablo<br/>supervisa equipo comercial"]
    Venta["VENTA<br/>closer interno Meembly<br/>embudo completo · cap 4"]
    Member["MEMBER = Postventa<br/>Roberto (SPA/MPS)<br/>D+0/D+14 · cap 4"]
    Viewer["VIEWER<br/>Luis y stakeholders<br/>todo read-only"]

    Owner --> Admin
    Admin --> Manager
    Manager --> Venta
    Manager --> Member
    Owner -.comparten métricas.-> Viewer

    classDef owner fill:#fbbf24,stroke:#b45309,color:#111
    classDef admin fill:#60a5fa,stroke:#1e40af,color:#fff
    classDef manager fill:#a78bfa,stroke:#5b21b6,color:#fff
    classDef venta fill:#f472b6,stroke:#9d174d,color:#fff
    classDef member fill:#34d399,stroke:#065f46,color:#111
    classDef viewer fill:#e5e7eb,stroke:#6b7280,color:#111

    class Owner owner
    class Admin admin
    class Manager manager
    class Venta venta
    class Member member
    class Viewer viewer
```

| Persona | Rol | Guía |
|---|---|---|
| Samuel Dávila | Owner | [role-owner.md](./role-owner.md) |
| Marta | Admin | [role-admin.md](./role-admin.md) |
| Pablo Salcedo | Manager | [role-manager.md](./role-manager.md) |
| Closers internos Meembly | Venta | [role-venta.md](./role-venta.md) |
| Roberto y comerciales externos SPA/MPS | Postventa (`MEMBER` en DB) | [role-postventa.md](./role-postventa.md) |
| Luis y otros stakeholders externos | Viewer | [role-viewer.md](./role-viewer.md) |

**Postventa vs Venta** — mismo nivel en el organigrama, diferentes canales:

- **Postventa** (`MEMBER`, renderizado como "Postventa"): comercial externo contratado vía SPA/MPS. Hace D+0 + D+14 sobre leads auto-sincronizados desde Odoo con tag `Postventa`. Solo puede usar **email + Ringover** — nunca WhatsApp ni IG (son recursos compartidos de Meembly).
- **Venta** (`VENTA`): closer interno de Meembly. Trabaja el embudo completo (frío → WON → club). Todos los canales abiertos (email, WA, IG, llamadas) + crea clubes directo al cerrar WON.

## Qué puede hacer cada rol (resumen)

| Área | Owner | Admin | Manager | Venta | Postventa | Viewer |
|---|:-:|:-:|:-:|:-:|:-:|:-:|
| Ver leads | Todos | Todos | Equipo comercial | Propios | Propios | Todos (read) |
| Editar leads | ✓ | ✓ | — | Propios | Propios | — |
| Asignar leads / ver pool | ✓ | ✓ | — | — | — | — |
| Pipeline (ver/mover) | ✓ / ✓ | ✓ / ✓ | Ver equipo | Ver propios / mover propios | Ver propios / mover propios | Ver / — |
| Enviar email / llamada | ✓ | ✓ | ✓ | ✓ | ✓ | — |
| Enviar WhatsApp | ✓ | ✓ | ✓ | ✓ | — | — |
| Enviar Instagram DM | ✓ | ✓ | ✓ | ✓ | — | — |
| Prospectos (pre-funnel) | ✓ | ✓ | — | — | — | — |
| Clubes (panel Activos/Onboarding/Renovaciones) | ✓ | ✓ | ✓ | ✓ | — | — |
| Crear club | ✓ | ✓ | — | ✓ | — | — |
| Customer Success (salud clientes) | ✓ | ✓ | ✓ | — | — | — |
| Marketing (proponer contenido a clubes, publicar Meembly) | ✓ | ✓ | — | — | — | — |
| Soporte — ver conversaciones | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Soporte — aprobar drafts, editar KB | ✓ | ✓ | — | — | — | — |
| Instancias Odoo (SPA/MPS/PM/YVR) — ver | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Instancias Odoo — gestionar | ✓ | ✓ | — | — | — | — |
| Equipo (invitar, cambiar rol, overrides) | ✓ | ✓ | — | — | — | — |
| Objetivos (ver/editar) | ✓ / ✓ | ✓ / ✓ | ✓ / — | ✓ / — | ✓ / — | ✓ / — |
| Métricas | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Auditoría (log del equipo Meembly) | ✓ | ✓ | — | — | — | — |
| Ajustes (Gmail personal) | ✓ | ✓ | ✓ | ✓ | ✓ | — |

El Owner puede dar permisos extra a personas concretas (add) o quitar permisos del bundle (deny) desde **Equipo → editar miembro**. Lo explica [role-owner.md](./role-owner.md).

### Permisos efectivos — cómo se calculan

```mermaid
flowchart LR
    Role([Rol del miembro<br/>OWNER/ADMIN/<br/>MANAGER/MEMBER/VIEWER]) --> Bundle[Bundle del rol<br/>permisos por defecto]
    Add([Permisos añadidos<br/>con override<br/>permissions]) --> Sum((( ∪ )))
    Bundle --> Sum
    Sum --> Sub((( \ )))
    Deny([Permisos retirados<br/>con override<br/>permissionsDeny]) --> Sub
    Sub --> Final[Permisos efectivos]

    style Final fill:#bbf7d0,stroke:#14532d,color:#111
    style Deny fill:#fca5a5,stroke:#991b1b,color:#111
    style Add fill:#dbeafe,stroke:#1e40af,color:#111
    style Bundle fill:#fde68a,stroke:#a16207,color:#111
```

Regla: **deny siempre gana**. Si un permiso está en el bundle del rol y también en `permissionsDeny`, queda denegado.

## ¿Cómo hago X? — Índice por tarea

### Trabajar un lead
- Recibir uno del pool → [Postventa §Flujo 1](./role-postventa.md#flujo-1--recibir-un-lead-del-pool) · [Venta §Flujo](./role-venta.md#flujo-completo-lead-frío--club-activo) · [Admin §Repartir pool](./role-admin.md#repartir-el-pool)
- Mover stage (NEW → CONTACTED → QUALIFIED → DEMO → PROPOSAL) → [Postventa §Flujo 2](./role-postventa.md#flujo-2--trabajar-el-lead-hasta-cerrarlo)
- Cerrar lead (WON / LOST) → [Postventa §Flujo 2](./role-postventa.md#flujo-2--trabajar-el-lead-hasta-cerrarlo)
- Devolver lead al pool → [Postventa §Devolver al pool](./role-postventa.md#devolver-un-lead-al-pool)
- Ver mis slots (n/4) → [Postventa §Cap de 4 leads](./role-postventa.md#cap-de-4-leads)
- Enviar email / llamada (Postventa) → [Postventa §Composer](./role-postventa.md#composer-envía-comunicaciones-sin-salir-del-lead)
- Enviar email / WA / IG / llamada (Venta) → [Venta §Canales](./role-venta.md#canales-que-tienes)
- Mandar email "Meembly upsell" D+14 → [Postventa §Flujo D+0/D+14](./role-postventa.md#flujo-d0--d14-tu-ritmo-estándar)

### Comercial desde arriba (Manager/Admin/Owner)
- Ver actividad del equipo → [Manager §Pipeline y actividad](./role-manager.md#pipeline-y-actividad-del-equipo)
- Métricas / ranking → [Manager §Métricas](./role-manager.md#métricas)
- Editar objetivos comerciales → [Admin §Objetivos](./role-admin.md#objetivos) · [role-owner.md](./role-owner.md)

### Equipo
- Invitar comercial nuevo → [Admin §Invitar](./role-admin.md#invitar-a-alguien-al-equipo)
- Ajustar permisos a una persona (add/deny) → [Owner §Overrides](./role-owner.md#overrides-add--deny)
- Cambiar rol de un miembro → [Owner §Cambiar rol](./role-owner.md#cambiar-el-rol-de-alguien)
- Desactivar miembro → [Admin §Desactivar](./role-admin.md#desactivar-un-miembro)

### Clubes
- Ver clubes activos / salud / renovaciones → [Manager §Panel clubes](./role-manager.md#panel-clubes) · [Admin §Panel clubes](./role-admin.md#panel-clubes-activos--onboarding--renovaciones)
- Crear un club nuevo desde admin → [Admin §Crear club](./role-admin.md#crear-un-club-nuevo)
- Convertir un lead ganado en club → [Admin §Convertir lead](./role-admin.md#convertir-un-lead-ganado-en-club)

### Prospectos (pre-funnel)
- Registrar prospecto B2B → [Admin §Prospectos](./role-admin.md#prospectos-pre-funnel)
- Convertir prospecto en lead → [Admin §Prospectos](./role-admin.md#prospectos-pre-funnel)

### Marketing
- Aprobar y publicar post Meembly (IG propio) → [Admin §Marketing Meembly](./role-admin.md#marketing-meembly-publicación-manual-desde-admin)
- Proponer contenido a un club cliente → [Admin §Marketing clubes](./role-admin.md#marketing-proponer-contenido-a-un-club)

### Soporte
- Aprobar / editar / rechazar un draft de IA → [Admin §Soporte](./role-admin.md#soporte-aprobar-drafts-de-ia)
- Añadir corrección a la KB → [Admin §Soporte](./role-admin.md#soporte-aprobar-drafts-de-ia)
- Ver conversaciones (read-only) → [Viewer §Soporte](./role-viewer.md#soporte-read-only)

### Infraestructura
- Conectar tu Gmail personal (para enviar emails desde tu identidad) → [Admin §Gmail](./role-admin.md#conectar-tu-gmail-personal) · [Postventa §Gmail](./role-postventa.md#conectar-tu-gmail-personal)
- Revisar instancias Odoo con error → [Admin §Instancias](./role-admin.md#instancias-odoo) · [Owner](./role-owner.md)
- Ver auditoría del equipo → [Admin §Auditoría](./role-admin.md#auditoría) · [Owner](./role-owner.md)

### Notificaciones pendientes
- Ver leads con actividad entrante sin atender → [Postventa §Pendientes](./role-postventa.md#pendientes-bandeja-de-actividad-entrante) · [Manager §Pendientes](./role-manager.md#pendientes-del-equipo)
- Marcar una actividad como gestionada → idem

## Convenciones

- **Meembly** = app de cliente (dueños de clubes). URL: `/[locale]/dashboard/...`.
- **Meembly Admin** = este panel interno. URL: `/[locale]/admin/...`.
- Todas las guías asumen que has entrado en `/admin` y que tu sesión está activa.
- Si ves "Acceso restringido" y crees que es un error, escalas al Owner (Samuel).

## Screenshots

Los screenshots de cada pantalla viven en `docs/ops/screenshots/`. Si un screenshot está desactualizado o falta, abre un issue o avisa a Samuel.

## ¿Quieres cambiar algo en estas guías?

Editar directamente en `docs/ops/*.md` y proponer cambios como PR. El owner de estas guías es Samuel.
