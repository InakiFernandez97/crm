# Informe Técnico del Sistema

## Arquitectura general

El proyecto está construido sobre PHP con una arquitectura modular. La organización principal del código se distribuye en controladores, vistas, modelos, configuración central, helpers, librerías y terceros.

La aplicación usa rutas explícitas, control de permisos por módulo y un sistema de hooks para extender comportamiento sin modificar el núcleo.

## Estructura funcional detectada

### Seguridad y acceso

- Login, signup y recuperación de acceso.
- Control de acceso por roles y permisos.
- Restricción por módulo.
- Restricción por IP.
- Reglas distintas para staff y clientes.

### Módulos de negocio

- Clientes, contactos y grupos.
- Leads, estados de leads y fuentes.
- Proyectos, tareas, prioridades y estados.
- Presupuestos, propuestas, contratos, órdenes y facturas.
- Pagos de facturas y suscripciones.
- Tickets, tipos de ticket y base de conocimiento.
- Gastos y categorías de gasto.
- Asistencia, licencias y control horario.
- Notas, mensajes, eventos, anuncios y timeline.
- Página pública, páginas internas y paneles de cliente y equipo.

### Administración

- Configuración general del sitio.
- Carga de logo, favicon e imagen de login.
- Personalización del tema y menús.
- Configuración de correo SMTP y Outlook.
- Prueba de correo.
- Copia de seguridad de base de datos.
- Configuración de módulos activos.
- Gestión de plugins.

### Integraciones

- Stripe.
- PayPal.
- Paytm.
- Google API.
- Microsoft API.
- Webhooks.
- GitHub y Bitbucket para actividad sobre tareas.

## Capacidades transversales

- Multilenguaje.
- Sistema de archivos temporales y permanentes.
- Carga de adjuntos e imágenes.
- Hooks para acciones de inserción, actualización y eliminación.
- Plugins instalables desde ZIP.
- Menús configurables por cliente o por usuario.

## Dependencias y soporte

- Procesamiento de correo y documentos.
- Librerías de terceros para PDF, Excel, imágenes y ZIP.
- Integración con editor enriquecido y UI basada en vistas del framework.

## Vacíos funcionales relevantes

### ERP

- No se ve núcleo contable completo.
- No se ve inventario con almacenes.
- No se ve compras ni proveedores.
- No se ve producción o manufactura.
- No se ve nómina.
- No se ve activo fijo ni depreciación.

### CRM

- No se ve automatización de marketing avanzada.
- No se ve omnicanalidad unificada.
- No se ve scoring o nurturing de leads.
- No se ve BI avanzado ni forecasting comercial profundo.

## Lectura técnica final

El sistema está bien modularizado y es extensible. Técnicamente puede crecer por plugins y hooks, pero su modelo de negocio principal sigue estando más cerca de una suite CRM y de gestión operativa que de un ERP completo.