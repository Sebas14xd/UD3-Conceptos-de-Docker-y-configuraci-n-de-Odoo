# Conceptos de Docker

## 1. ¿Qué hacen los comandos de Docker vistos?

- `docker pull`: descarga la imagen de Odoo
- `docker pull postgres`: descarga la imagen de PostgreSQL
- `docker run`: crea e inicia un contenedor
- `docker ps`: muestra los contenedores en ejecución
- `docker stop`: detiene un contenedor
- `docker start`: inicia un contenedor detenido
- `docker compose up -d`: inicia Odoo y PostgreSQL en segundo plano
- `docker compose down`: detiene y elimina los contenedores del proyecto

## 2. ¿Qué significan los bloques del archivo `compose.yml`?

- `services`: define los servicios Odoo y PostgreSQL
- `image`: indica la imagen que se utiliza
- `ports`: permite acceder a Odoo mediante el puerto 8069
- `environment`: configura variables como usuarios y contraseñas
- `depends_on`: establece que Odoo depende del servicio de PostgreSQL
- `volumes`: conserva los datos de Odoo y la base de datos
- `secrets`: permite gestionar contraseñas de forma más segura

## 3. ¿Qué es una imagen?

Es una plantilla que contiene lo necesario para ejecutar una aplicación

## 4. ¿Qué es un contenedor?

Es una instancia de una imagen en ejecución

## 5. ¿Qué es un volumen?

Es un espacio de almacenamiento que permite conservar los datos aunque se elimine un contenedor

## 6. ¿Cómo mejorar la eficiencia y la seguridad?

- **Eficiencia:** utiliza imágenes, elimina dependencias innecesarias y limitar el consumo de memoria y CPU
- **Archivo `.env`:** guarda la configuración en variables para no escribirla directamente en `compose.yml`
- **Docker Secrets:** guarda contraseñas en archivos secretos y utiliza variables como `POSTGRES_PASSWORD_FILE` y `PASSWORD_FILE`
- **Seguridad:** utiliza contraseñas robustas, actualizar las imágenes y evitar publicar el puerto de PostgreSQL

## Configuración de Odoo con Docker

### 1. Diferencias entre `compose.yml` y `odoo.conf`

- `compose.yml`: configura los contenedores, los puertos, los volúmenes y las variables
- `odoo.conf`: configura opciones propias de Odoo, como la ruta de los módulos, los parámetros de conexión a la base de datos

#### ¿Qué es más seguro?

- Para las contraseñas Docker Secrets

#### ¿Qué es más práctico para desarrollar en local?

- usar `compose.yml` para los servicios y archivos `odoo.conf` local para los ajustes de desarrollo

### 2. ¿Cuál es la configuración de producción y cuál la de desarrollo?

- **Producción:** está pensada para usuarios reales. Tiene seguridad reforzada, copias de seguridad y parámetros de rendimiento
- **Desarrollo:** modifica módulos, ver errores y probar cambios.

#### ¿Cómo configurar ambas opciones en `compose.yml`?

- **Producción:** `docker compose up -d`
- **Desarrollo:** `docker compose -f docker-compose.yml -f compose.dev.yml up -d`

### 3. ¿Qué directorios de Odoo podemos guardar en el repositorio?

- `addons`: sí, porque contiene los módulos y el código del desarrollo
- `filestore`: no, porque contiene archivos adjuntos de los usuarios y datos que deben conservarse
- `sesiones`: no, porque contiene información temporal de las sesiones de los usuarios

## Puesta en marcha

```bash
docker compose up -d
```

Después entra en http://localhost:8069 y crea la base de datos **odoo** (contraseña maestra: la de `admin_passwd` en `config/odoo.conf`).
