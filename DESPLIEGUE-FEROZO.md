# Despliegue Manual en Ferozo

Esta guía está pensada para un despliegue manual cuando el hosting no puede usar SSH o un flujo Git privado.

## Qué queda en el repositorio

- Código fuente de la aplicación.
- Plantillas de configuración seguras.
- Archivos de ejemplo para entorno.

## Qué no debes subir con valores reales

- Claves de base de datos.
- Clave de encriptación.
- Credenciales SMTP.
- Archivo `.env` real.

## Pasos de implementación

### 1. Subir el proyecto

1. Sube todo el contenido del repositorio al directorio raíz del sitio en Ferozo.
2. Verifica que `index.php` quede accesible desde la raíz del sitio.
3. Si el hosting te obliga a usar `public_html`, coloca el proyecto completo ahí o ajusta el document root para que apunte a la carpeta del proyecto.

### 2. Crear la base de datos

1. Crea una base de datos en el panel de Ferozo.
2. Crea un usuario de base de datos y asígnale permisos completos sobre esa base.
3. Anota estos datos:
   - Host
   - Usuario
   - Contraseña
   - Nombre de la base

### 3. Configurar el entorno

1. Copia `.env.example` a `.env`.
2. Edita `.env` con los datos reales del hosting.
3. Ajusta al menos estas claves:
   - `CI_ENVIRONMENT`
   - `app.baseURL`
   - `app.cookieDomain`
   - `app.encryption_key`
   - `database.default.hostname`
   - `database.default.username`
   - `database.default.password`
   - `database.default.database`

### 4. Importar la base de datos

1. Importa el archivo SQL del proyecto desde el panel de base de datos de Ferozo.
2. Si usas el instalador, valida que el prefijo de tablas coincida con el valor configurado.

### 5. Ajustar correo saliente

Si usarás SMTP, completa estos valores en `.env`:

- `email.protocol`
- `email.SMTPHost`
- `email.SMTPUser`
- `email.SMTPPass`
- `email.SMTPPort`
- `email.SMTPCrypto`

### 6. Permisos de escritura

Da permisos de escritura a:

- `writable/cache/`
- `writable/logs/`
- `writable/session/`
- `writable/uploads/`
- `files/temp/`
- `files/profile_images/`
- `files/project_files/`
- `files/timeline_files/`
- `files/general/`

### 7. Validación final

1. Abre el sitio en el navegador.
2. Comprueba inicio de sesión, carga de archivos y conexión con la base de datos.
3. Revisa `writable/logs/` si aparece algún error.

## Si prefieres hacerlo sin `.env`

También puedes editar directamente estas plantillas en el servidor:

- `app/Config/Database.php`
- `app/Config/App.php`
- `app/Config/Email.php`

## Nota importante

Después de configurar producción, no vuelvas a subir un `.env` real al repositorio público.