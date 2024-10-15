
# Docker Compose - MySQL, MariaDB, and phpMyAdmin Setup

Este proyecto configura un entorno de bases de datos con MySQL, MariaDB y phpMyAdmin usando Docker Compose.

## Requisitos

- [Docker](https://www.docker.com/get-started) y [Docker Compose](https://docs.docker.com/compose/install/)
- Procesador compatible con arquitectura `amd64` o `arm64` (si utilizas un dispositivo ARM como un Mac con chip Apple M1/M2)

## Estructura del Proyecto

Este archivo `docker-compose.yml` configura tres servicios:

1. **MySQL** - Contenedor que utiliza la imagen `mysql:5.7`.
2. **MariaDB** - Contenedor que utiliza la última imagen de MariaDB.
3. **phpMyAdmin** - Herramienta de administración web para bases de datos MySQL y MariaDB.

## Cómo Usar

### Paso 1: Clonar el Repositorio

```bash
git clone <URL_DEL_REPOSITORIO>
cd practica-docker-compose
```

### Paso 2: Configurar las Variables de Entorno

Edita el archivo `docker-compose.yml` para ajustar las configuraciones de las bases de datos según tus necesidades:

```yaml
# Ejemplo de configuración
db:
  environment:
    MYSQL_ROOT_PASSWORD: yourpassword
    MYSQL_DATABASE: yourdatabase

db1:
  environment:
    MYSQL_ROOT_PASSWORD: ucatec
    MYSQL_DATABASE: your_database_name
    MYSQL_USER: your_username
    MYSQL_PASSWORD: your_password
```

### Paso 3: Ejecutar Docker Compose

Para iniciar los contenedores en segundo plano, ejecuta:

```bash
docker-compose up -d
```

### Paso 4: Nota sobre Compatibilidad con Arquitectura ARM

Si ves errores relacionados con la arquitectura, edita el archivo `docker-compose.yml` para forzar la compatibilidad con `amd64` en servicios específicos. Por ejemplo:

```yaml
# Ejemplo de compatibilidad
db:
  platform: linux/amd64
```

### Paso 5: Acceso a los Servicios

Una vez que los contenedores están en ejecución, puedes acceder a los servicios usando las siguientes URLs y puertos:

- **MySQL**: Disponible en `localhost:3306`
- **MariaDB**: Disponible en `localhost:3307`
- **phpMyAdmin**: Acceso desde tu navegador en [http://localhost:8080](http://localhost:8080)

### Paso 6: Detener y Eliminar los Contenedores

Para detener y eliminar los contenedores, ejecuta el siguiente comando:

```bash
docker-compose down
```

### Paso 7: Volúmenes Persistentes (Opcional)

Si deseas que los datos persistan entre reinicios de los contenedores, considera agregar volúmenes en el archivo `docker-compose.yml`. Por ejemplo:

```yaml
db:
  volumes:
    - ./mysql_data:/var/lib/mysql

db1:
  volumes:
    - ./mariadb_data:/var/lib/mysql
```

## Troubleshooting

- **Puertos en Uso**: Asegúrate de que los puertos especificados en el archivo `docker-compose.yml` estén libres. Si están en uso, modifica los puertos en el archivo.
- **Errores de Permisos en Linux**: Si encuentras errores de permisos, intenta ejecutar Docker Compose con `sudo`:

  ```bash
  sudo docker-compose up -d
  ```

- **Arquitectura Incompatible**: Si usas una arquitectura `arm64`, asegúrate de que todas las imágenes que uses sean compatibles. Agregar la línea `platform: linux/amd64` puede ayudar a forzar la compatibilidad.

Con estos pasos, deberías poder levantar tu entorno de MySQL, MariaDB y phpMyAdmin fácilmente. ¡Disfruta!
