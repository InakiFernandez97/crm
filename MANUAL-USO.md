# Manual de Uso - CRM/ERP

## Tabla de Contenidos

1. [Introducción](#introducción)
2. [Requisitos del Sistema](#requisitos-del-sistema)
3. [Instalación con Laragon](#instalación-con-laragon)
4. [Configuración Inicial](#configuración-inicial)
5. [Estructura del Proyecto](#estructura-del-proyecto)
6. [Módulos Disponibles](#módulos-disponibles)
7. [Guía de Desarrollo con Laragon](#guía-de-desarrollo-con-laragon)
8. [Mantenimiento y Copias de Seguridad](#mantenimiento-y-copias-de-seguridad)
9. [Solución de Problemas](#solución-de-problemas)
10. [Índice de Archivos SQL](#índice-de-archivos-sql)

---

## Introducción

Este CRM/ERP es una solución empresarial completa construida con PHP moderna que proporciona funcionalidades para gestionar:

- **Clientes y Contactos**: Gestión centralizada de información de clientes
- **Ventas**: Leads, propuestas, presupuestos, órdenes y facturas
- **Proyectos**: Seguimiento de tareas, proyectos y sprints
- **Recursos Humanos**: Asistencia, licencias y control horario
- **Soporte**: Sistema de tickets y base de conocimiento
- **Finanzas**: Gestión de pagos, suscripciones y gastos
- **Integraciones**: Stripe, PayPal, Google API, Microsoft API

---

## Requisitos del Sistema

### Mínimos Recomendados

| Requisito | Versión/Especificación |
|-----------|------------------------|
| PHP | 8.1 o superior |
| MySQL | 5.7 o superior (8.0+ recomendado) |
| Extensiones PHP requeridas | - mysqli<br>- cURL<br>- mbstring<br>- intl<br>- json<br>- mysqlnd<br>- xml<br>- gd<br>- zlib |
| Espacio en disco | Mínimo 500 MB |
| Memoria RAM | Mínimo 2 GB (4 GB recomendado) |
| Servidor Web | Apache 2.4+ con mod_rewrite habilitado |

### Software Recomendado para Desarrollo

- **Laragon**: Para un entorno local completo
- **Visual Studio Code**: Editor de código
- **Composer**: Gestor de dependencias PHP
- **Git**: Control de versiones

---

## Instalación con Laragon

### Paso 1: Preparar Laragon

1. **Descargar e instalar Laragon** desde [laragon.org](https://laragon.org)
2. **Ejecutar Laragon** como administrador
3. **Verificar que Apache y MySQL estén activos** (indicadores verdes en la interfaz)

### Paso 2: Clonar o Descargar el CRM

```bash
# Opción 1: Usando Git
cd C:\laragon\www
git clone <URL-DEL-REPOSITORIO> crm

# Opción 2: Descargar ZIP
# Extraer en C:\laragon\www\crm
```

### Paso 3: Crear la Base de Datos

1. **Abrir Laragon** y hacer clic en **Database** (phpMyAdmin)
2. **Crear nueva base de datos**:
   - Nombre: `crm` (o el nombre que prefiera)
   - Colación: `utf8mb4_unicode_ci`

### Paso 4: Elegir Tipo de Instalación

#### Opción A: Instalación Limpia (Para Nuevo CRM)

1. **Acceder al instalador** en navegador:
   ```
   http://crm.test/install
   ```

2. **Completar el formulario de instalación**:
   - **Host de Base de Datos**: `localhost`
   - **Usuario de BD**: `root`
   - **Contraseña de BD**: (dejar vacío en Laragon)
   - **Nombre de BD**: `crm` (el que creó)
   - **Prefijo de BD**: `crm_` (opcional)
   - **Nombre del Administrador**: Nombre completo
   - **Email del Administrador**: Email válido
   - **Contraseña del Administrador**: Contraseña segura
   - **Código de Compra**: Verificar documentación

3. **Hacer clic en "Instalar"** y esperar a que se complete

#### Opción B: Cargar Base de Datos Propia (Para Desarrollo Local)

Si ya tienes un backup de tu BD:

1. **Copiar tu archivo SQL a la raíz del proyecto**:
   ```
   C:\laragon\www\crm\nplanet_crm.sql
   ```
   (o con el nombre que prefiera)

2. **Abrir phpMyAdmin** en Laragon:
   - Hacer clic en **Database**
   - Ir a **Importar**

3. **Seleccionar tu archivo SQL**:
   - Elegir el archivo: `nplanet_crm.sql`
   - Hacer clic en **Ejecutar**

4. **Esperar a que se importe** la BD completa

5. **Configurar la conexión** en `app/Config/Database.php`:
   - Verificar que coincidan host, usuario, contraseña y nombre de BD

6. **Acceder a** `http://crm.test` con tus credenciales existentes

### Paso 5: Acceder a la Aplicación

Una vez completada la instalación:

```
URL: http://crm.test
```

**Si usaste instalador limpio**:
- Email: El proporcionado durante la instalación
- Contraseña: La establecida durante la instalación

**Si cargaste BD propia**:
- Email y contraseña: Las de tu BD actual

---

## Estructura del Proyecto

```
crm/
├── app/                          # Código de la aplicación
│   ├── Config/                   # Archivos de configuración
│   ├── Controllers/              # Controladores de lógica
│   ├── Models/                   # Modelos de datos
│   ├── Views/                    # Vistas (HTML/PHP)
│   ├── Libraries/                # Librerías personalizadas
│   ├── Helpers/                  # Funciones auxiliares
│   └── Database/                 # Migraciones y seeds
├── system/                       # Framework base
├── assets/                       # Recursos estáticos
│   ├── css/                      # Estilos
│   ├── js/                       # Scripts JavaScript
│   ├── bootstrap/                # Bootstrap framework
│   └── images/                   # Imágenes
├── files/                        # Almacenamiento de archivos
│   ├── profile_images/           # Imágenes de perfil
│   ├── project_files/            # Archivos de proyectos
│   └── temp/                     # Archivos temporales
├── install/                      # Instalador
├── plugins/                      # Plugins personalizados
├── writable/                     # Directorio con permisos de escritura
│   ├── cache/                    # Caché de aplicación
│   ├── logs/                     # Logs del sistema
│   ├── session/                  # Sesiones
│   └── uploads/                  # Cargas de usuarios
├── index.php                     # Punto de entrada
├── README.md                     # Índice de documentación
├── README-TECNICO.md             # Documentación técnica
└── README-COMERCIAL.md           # Documentación comercial
```

---

## Módulos Disponibles

### 1. **Gestión de Clientes**
- Registro y perfiles de clientes
- Grupos de clientes
- Contactos asociados
- Historial de interacciones

### 2. **Gestión de Leads y Ventas**
- Seguimiento de leads
- Estados y fuentes de leads
- Propuestas y presupuestos
- Órdenes de compra
- Facturas y pagos

### 3. **Gestión de Proyectos**
- Creación y seguimiento de proyectos
- Tareas con prioridades
- Estados de progreso
- Asignación de equipo
- Timeline e hitos

### 4. **Gestión de Contratos**
- Plantillas de contratos
- Gestión de contratos activos
- Versionado de documentos
- Control de fechas de vencimiento

### 5. **Recursos Humanos**
- Control de asistencia
- Gestión de licencias
- Control de horarios
- Nóminas (si está incluido)

### 6. **Sistema de Tickets**
- Registro de incidencias
- Categorización y priorización
- Base de conocimiento
- Chat de soporte

### 7. **Finanzas**
- Gestión de gastos
- Categorías de gasto
- Reportes financieros
- Integraciones de pago (Stripe, PayPal)

### 8. **Administración**
- Configuración general
- Gestión de usuarios y permisos
- Copias de seguridad
- Plugins y extensiones
- Logs del sistema

---

## Guía de Desarrollo con Laragon

### Configuración del Entorno de Desarrollo

#### 1. Iniciar Laragon

1. Abrir **Laragon**
2. Verificar que **Apache** y **MySQL** estén activos (indicadores verdes)
3. El proyecto está disponible en `http://crm.test`

#### 2. Abrir el Proyecto en VS Code

1. En **Visual Studio Code**: 
   - `File` → `Open Folder`
   - Seleccionar `C:\laragon\www\crm`

2. **Extensiones recomendadas**:
   - PHP Intelephense (para autocompletado de PHP)
   - Thunder Client (para pruebas de API)
   - GitLens (para control de versiones)

#### 3. Flujo de Desarrollo

El desarrollo es simple:

```
1. Realizar cambios en:
   - Controladores: app/Controllers/
   - Modelos: app/Models/
   - Vistas: app/Views/
   - Helpers/Librerías: app/Helpers/ y app/Libraries/

2. Actualizar en navegador:
   http://crm.test

3. Ver logs de errores:
   writable/logs/log-*.log
```

#### 4. Control de Versiones con Git

Usa Git para versionar tu código:

```bash
# En terminal de Laragon o PowerShell
git add .
git commit -m "Descripción del cambio"
git push origin main
```

**Importante**: El archivo `.gitignore` protege automáticamente:
- Credenciales de base de datos
- Configuración sensible
- Archivos temporales y caché
- Logs del sistema

**No hacer commit de**:
- `app/Config/Database.php` (contiene credenciales)
- `app/Config/App.php` (contiene clave de encriptación)
- Carpeta `writable/` (archivos temporales)
- Carpeta `files/` (datos de usuarios)

---


## Mantenimiento y Copias de Seguridad

### Copias de Seguridad Automáticas

1. Ir a **Configuración** → **Administración** → **Backup**
2. Hacer clic en **"Crear Copia de Seguridad"**
3. Descargar archivo `.sql` generado

### Copias de Seguridad Manuales

**Base de Datos**:
```bash
# Desde línea de comandos en Laragon Terminal
mysqldump -u root crm > backup_crm_YYYY-MM-DD.sql

# Restaurar desde backup
mysql -u root crm < backup_crm_YYYY-MM-DD.sql
```

**Archivos**:
```bash
# Comprimir todo el proyecto
tar -czf crm_backup_YYYY-MM-DD.tar.gz crm/

# En Windows (usando 7-Zip)
# Click derecho → 7-Zip → Agregar a archivo
```

### Actualización del Sistema

1. **Respaldar completamente** (BD y archivos)
2. **Descargar actualización** desde la fuente
3. **Realizar actualización** siguiendo instrucciones de release notes
4. **Probar funcionalidades críticas** después de actualizar
5. **Revisar logs** para errores

---

## Solución de Problemas

### Problema: Error de conexión a base de datos

**Soluciones**:
1. Abrir phpMyAdmin y verificar que la BD existe
2. Verificar usuario y contraseña en configuración
3. Reiniciar servicio MySQL en Laragon
4. Verificar que el archivo `crm.sql` fue importado

### Problema: Permisos insuficientes para cargar archivos

**Soluciones**:
```bash
# En Laragon Terminal
chmod -R 777 files/
chmod -R 777 writable/
```

### Problema: Session no persiste

**Soluciones**:
1. Verificar permisos en `writable/session/`
2. Revisar configuración de sesión en `app/Config/Session.php`
3. Limpiar sesiones antiguas:
   ```bash
   rm -rf writable/session/*
   ```

### Problema: Timeout en operaciones largas

**Soluciones**:
1. Aumentar `max_execution_time` en `php.ini`:
   ```ini
   max_execution_time = 300
   ```
2. Aumentar `memory_limit`:
   ```ini
   memory_limit = 256M
   ```

---


---

## Soporte y Recursos

- **Documentación Técnica**: Ver [README-TECNICO.md](README-TECNICO.md)
- **Documentación Comercial**: Ver [README-COMERCIAL.md](README-COMERCIAL.md)
- **Logs de Sistema**: `writable/logs/`
- **Panel de Administración**: `http://crm.test/admin`

---

**Última actualización**: Abril 2026  
**Versión del Manual**: 1.0
