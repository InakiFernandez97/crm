# Índice Comparativo de Archivos SQL

## Resumen Ejecutivo

| Aspecto | install/database.sql | nplanet_crm.sql |
|--------|----------------------|-----------------|
| **Tipo** | Base de datos template del instalador | Backup de BD de producción |
| **Prefijo tablas** | Sin prefijo (ej: `activity_logs`) | Prefijo `rise_` (ej: `rise_activity_logs`) |
| **Propósito** | Crear BD limpia para nuevas instalaciones | Datos reales con histórico completo |
| **Volumen de datos** | Solo estructura y datos iniciales | Datos de múltiples clientes y transacciones |
| **Uso recomendado** | Opción A: Instalación limpia | Opción B: Desarrollo con datos existentes |

---

## Tablas Incluidas en Ambos Archivos

### Módulo: Gestión de Actividades y Logs
- `activity_logs` - Registro de cambios realizados en el sistema
- `announcements` - Anuncios del sistema
- `notifications` - Notificaciones de eventos

### Módulo: Gestión de Asistencia
- `attendance` - Registro de entrada/salida de empleados
- `leave_applications` - Solicitudes de permiso
- `leave_types` - Tipos de permisos disponibles

### Módulo: Gestión de Clientes y Leads
- `clients` - Base de clientes
- `client_groups` - Grupos de clasificación de clientes
- `leads` - Prospectos/leads
- `lead_status` - Estados de los leads
- `lead_source` - Fuentes de origen de leads

### Módulo: Gestión de Proyectos
- `projects` - Proyectos activos
- `project_members` - Miembros asignados a proyectos
- `project_comments` - Comentarios en proyectos
- `project_files` - Archivos de proyecto
- `project_time` - Tiempo registrado en proyectos
- `project_status` - Estados de proyectos
- `project_settings` - Configuración por proyecto

### Módulo: Gestión de Tareas
- `tasks` - Tareas del sistema
- `task_status` - Estados de tareas (To Do, In Progress, Done)
- `task_priority` - Niveles de prioridad
- `checklist_items` - Items de checklist dentro de tareas
- `checklist_groups` - Grupos de checklists
- `checklist_template` - Plantillas de checklists

### Módulo: Invoices (Facturas)
- `invoices` - Facturas emitidas
- `invoice_items` - Líneas de factura
- `invoice_payments` - Pagos registrados
- `paypal_ipn` - Confirmaciones PayPal
- `stripe_ipn` - Confirmaciones Stripe

### Módulo: Estimates (Presupuestos)
- `estimates` - Presupuestos creados
- `estimate_items` - Líneas de presupuesto
- `estimate_requests` - Solicitudes de presupuesto
- `estimate_forms` - Formularios para solicitudes
- `estimate_comments` - Comentarios en presupuestos

### Módulo: Contracts (Contratos)
- `contracts` - Contratos firmados
- `contract_items` - Líneas de contrato
- `contract_templates` - Plantillas de contratos

### Módulo: Proposals (Propuestas)
- `proposals` - Propuestas comerciales
- `proposal_items` - Líneas de propuesta
- `proposal_templates` - Plantillas de propuestas

### Módulo: Órdenes
- `orders` - Órdenes de compra
- `order_items` - Líneas de orden
- `order_status` - Estados de órdenes

### Módulo: Gestión de Productos/Items
- `items` - Catálogo de productos
- `item_categories` - Categorías de productos

### Módulo: Gastos
- `expenses` - Registro de gastos
- `expense_categories` - Categorías de gastos

### Módulo: Tickets (Soporte)
- `tickets` - Tickets de soporte
- `ticket_comments` - Comentarios en tickets
- `ticket_templates` - Plantillas de tickets
- `ticket_types` - Tipos de tickets

### Módulo: Comunicación
- `messages` - Mensajes entre usuarios
- `posts` - Posts/publicaciones

### Módulo: Notas y Archivos
- `notes` - Notas del sistema
- `general_files` - Archivos generales
- `project_files` - Archivos de proyecto
- `file_category` - Categorización de archivos

### Módulo: Configuración General
- `company` - Datos de la empresa
- `users` - Usuarios del sistema
- `roles` - Roles y permisos
- `settings` - Configuraciones del sistema
- `payment_methods` - Métodos de pago
- `notification_settings` - Configuración de notificaciones

### Módulo: Calendarizaciones
- `events` - Eventos y recordatorios
- `milestones` - Hitos de proyectos

### Módulo: Sesiones y Seguridad
- `ci_sessions` - Sesiones de usuario
- `verification` - Códigos de verificación

### Módulo: Artículos y Help/Knowledge Base
- `help_articles` - Artículos de ayuda
- `help_categories` - Categorías de ayuda
- `article_helpful_status` - Ratings de útilidad

### Módulo: Sistema
- `labels` - Etiquetas generales
- `custom_fields` - Campos personalizados
- `custom_field_values` - Valores de campos personalizados
- `custom_widgets` - Widgets personalizados
- `dashboards` - Dashboards de usuario
- `team` - Equipos
- `team_member_job_info` - Información laboral de miembros
- `social_links` - Enlaces a redes sociales
- `pages` - Páginas estáticas
- `likes` - "Me gusta" en comentarios
- `pin_comments` - Comentarios fijados
- `taxes` - Impuestos configurados
- `to_do` - Lista de tareas personales

---

## Diferencias Principales

### Estructura de Nombres
- **install/database.sql**: Nombres de tabla sin prefijo
  ```
  CREATE TABLE `activity_logs` (...)
  CREATE TABLE `clients` (...)
  ```

- **nplanet_crm.sql**: Nombres de tabla con prefijo `rise_`
  ```
  CREATE TABLE `rise_activity_logs` (...)
  CREATE TABLE `rise_clients` (...)
  ```

### Cantidad de Registros

| Categoría | install/database.sql | nplanet_crm.sql |
|-----------|----------------------|-----------------|
| **Clientes** | 260 registros de prueba | 10,579 clientes reales |
| **Usuarios** | 1 usuario admin | Múltiples usuarios activos |
| **Datos históricos** | Mínimos (demo) | Completos (producción) |
| **Transacciones** | Datos de ejemplo | Histórico completo |

### Datos de Ejemplo

**install/database.sql** incluye:
- 42 plantillas de email predefinidas
- Configuraciones por defecto del sistema
- Datos de prueba para demostración
- Usuarios y clientes de ejemplo

**nplanet_crm.sql** incluye:
- Datos reales de la operación
- Múltiples sesiones de usuario autenticadas
- Histórico completo de transacciones
- Configuración actual del negocio

---

## Casos de Uso

### Usar install/database.sql (Opción A - Instalación Limpia)
✅ Primera instalación del sistema
✅ Crear ambiente de testing limpio
✅ Demostración a nuevos clientes
✅ Investigación y desarrollo
✅ Ambiente de staging controlado

**Ventajas:**
- Base de datos limpia sin datos históricos
- Menor tamaño de archivo
- Mejor para entrenamiento
- Performance inicial óptima

### Usar nplanet_crm.sql (Opción B - Datos Existentes)
✅ Desarrollo con datos reales
✅ Testing con escenarios reales
✅ Migración entre ambientes
✅ Análisis de datos históricos
✅ Replicación de problemas de producción

**Ventajas:**
- Datos reales para pruebas
- Histórico completo disponible
- Réplica exacta de producción
- Mejores reportes y análisis

---

## Ubicación de Archivos

```
crm/
├── install/
│   └── database.sql          ← Template del instalador (opción limpia)
├── nplanet_crm.sql           ← Backup de producción (con datos reales)
└── MANUAL-USO.md             ← Instrucciones de instalación
```

---

## Proceso de Importación

### Para install/database.sql
```sql
-- Crear base de datos
CREATE DATABASE crm_nuevo;
USE crm_nuevo;

-- Importar estructura e datos iniciales
SOURCE /ruta/a/install/database.sql;
```

### Para nplanet_crm.sql
```sql
-- Crear base de datos
CREATE DATABASE crm_desarrollo;
USE crm_desarrollo;

-- Importar datos de producción
SOURCE /ruta/a/nplanet_crm.sql;
```

---

## Información Técnica

### Codificación de Caracteres
- **Ambos archivos**: UTF-8 compatible
- **Colaciones**: utf8_unicode_ci (es_ES compatible)

### Tipos de Motor
- **Ambos archivos**: InnoDB (transaccional)
- **Soporte**: Transacciones, foreign keys, integridad referencial

### Versión de MySQL/MariaDB
- **Mínimo requerido**: MySQL 5.7 / MariaDB 10.2
- **Recomendado**: MariaDB 10.11+ o MySQL 8.0+

---

## Estadísticas Comparativas

| Métrica | install/database.sql | nplanet_crm.sql |
|---------|----------------------|-----------------|
| Tablas | ~85 | ~85 (con prefijo rise_) |
| Registros totales | ~300 aprox | 10,000+ |
| Tamaño estimado | < 1 MB | Variable según datos |
| Tiempo importación | < 1 segundo | 2-5 segundos |
| Datos de usuario | Mínimos | Completos |
| Histórico completo | ✗ No | ✓ Sí |

---

## Notas Importantes

⚠️ **PRECAUCIÓN**: 
- Ambas opciones son válidas según el caso de uso
- El instalador NO sobrescribe datos si la BD existe
- Mantener backups de ambas versiones
- Testing recomendado antes de usar en producción

📋 **RECOMENDACIONES**:
- Opción A para desarrollo inicial y testing limpio
- Opción B para replicar problemas de producción
- Combinar ambas en diferentes máquinas virtuales
- Rotación automática de backups de Opción B

---

**Última actualización**: Abril 2026
**Versión del documento**: 1.0
