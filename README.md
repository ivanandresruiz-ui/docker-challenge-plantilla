# Docker Challenge — Repositorio plantilla
Ivan Andres Ruiz - 2460978

Este repositorio contiene una aplicación Flask ya implementada y un evaluador para el taller. Tu tarea es crear `Dockerfile` y `docker-compose.yml`.

1. Lee `ENUNCIADO.md`.
2. Crea los dos archivos requeridos en la raíz.
3. No modifiques `app.py`, `requirements.txt` ni el evaluador.
4. Sube el proyecto a tu repositorio individual de GitHub.
5. Revisa la pestaña **Actions** para consultar las pruebas.

Estructura final: añade `Dockerfile` y `docker-compose.yml` a los archivos existentes.

No subas tokens, contraseñas reales ni otros secretos. El workflow es una ayuda de verificación; el docente también revisará el repositorio y tu comprensión.

## Mi solución

**Repositorio:** https://github.com/ivanandresruiz-ui/docker-challenge-plantilla

### 1. Dockerfile
Se utilizó `python:3.11-slim` como imagen base, `/app` como directorio de trabajo y se instalaron las dependencias de requirements.txt. La aplicación Flask se ejecuta en el puerto 5000.

### 2. Docker Compose
Se configuraron dos servicios:
- **web:** ejecuta Flask y publica el puerto 5000.
- **db:** utiliza PostgreSQL 16 para almacenar las tareas.

### 3. Comunicación entre servicios
La variable DATABASE_URL utiliza el hostname `db` porque Docker Compose permite la comunicación entre servicios mediante sus nombres dentro de la red interna. No se utiliza `localhost` porque apuntaría al propio contenedor Flask.

### 4. Persistencia
Se creó el volumen nombrado `postgres_data`, montado en `/var/lib/postgresql/data`. Al ejecutar `docker compose down` sin `-v`, los contenedores se eliminan, pero el volumen conserva los datos.

### 5. Pruebas realizadas
- docker compose config: configuración validada.
- docker compose ps: servicios web y db activos.
- GET /health: conexión con PostgreSQL correcta.
- GET /tasks: consulta de tareas correcta.
- POST /tasks: registro de Mi primera tarea correcto.
