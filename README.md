# Guía para Implementar MariaDB y MongoDB con Docker Compose

## Objetivo
Vamos a crear dos proyectos que usarán contenedores Docker para ejecutar bases de datos **MariaDB** y **MongoDB**. Cada proyecto tendrá su propia configuración para que podamos ejecutarlos de manera independiente.

## Requisitos
- **Docker**: Para crear y administrar contenedores.
- **Docker Compose**: Para gestionar múltiples contenedores a la vez.

Si aún no tienes Docker instalado, puedes hacerlo desde [aquí](https://www.docker.com/products/docker-desktop).

---

## Parte 1: Configuración del Proyecto MariaDB

### 1. Crear Estructura de Carpetas
Primero, necesitamos crear una carpeta donde estarán todos los archivos de configuración de MariaDB.

Ejecuta los siguientes comandos en la terminal:

```bash
mkdir mariadb_apellido_nombre
cd mariadb_apellido_nombre
touch docker-compose.yml .env .env.example .gitignore README.md
```
- `mkdir mariadb_apellido_nombre`: Crea la carpeta para el proyecto.
- `cd mariadb_apellido_nombre`: Entra en la carpeta creada.
- `touch` crea los archivos necesarios para el proyecto:
  - `docker-compose.yml`: Contendrá la configuración de Docker Compose.
  - `.env` y `.env.example`: Archivos para las variables de entorno.
  - `.gitignore`: Definirá qué archivos no deben ser subidos a GitHub.
  - `README.md`: Proporcionará instrucciones para los usuarios.

### 2. Escribir el Archivo `docker-compose.yml`
En este archivo se define cómo será creado el contenedor de MariaDB:

```yaml
version: '3'
services:
  mariadb:
    image: mariadb:latest
    container_name: mariadb_container
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
    ports:
      - "3306:3306"
    volumes:
      - mariadb_data:/var/lib/mysql
volumes:
  mariadb_data:
```

**Explicación**:
- **version**: Indica la versión de Docker Compose.
- **services**: Define los servicios a levantar. En este caso, `mariadb`.
- **image**: Especifica la imagen de MariaDB a utilizar.
- **environment**: Variables que serán configuradas desde el archivo `.env`.
- **ports**: Mapea el puerto `3306` del contenedor al `3306` del host.
- **volumes**: Define dónde se almacenarán los datos de MariaDB para persistencia.

### 3. Configurar el Archivo `.env`
El archivo `.env` contendrá las variables de entorno necesarias para MariaDB:

```bash
MYSQL_ROOT_PASSWORD=rootpassword
MYSQL_DATABASE=testdb
MYSQL_USER=user
MYSQL_PASSWORD=userpassword
```
**Nota**: Este archivo contiene información sensible, por eso no lo subiremos a GitHub.

### 4. Crear un Ejemplo `.env.example`
El archivo `.env.example` servirá como referencia para otros usuarios:

```bash
MYSQL_ROOT_PASSWORD=example_rootpassword
MYSQL_DATABASE=example_db
MYSQL_USER=example_user
MYSQL_PASSWORD=example_password
```
![image](https://github.com/user-attachments/assets/03254a58-fced-4cc1-b805-160f8a1248d0)


### 5. Configurar el Archivo `.gitignore`
En `.gitignore`, agrega la siguiente línea para evitar que se suba el archivo `.env` a GitHub:

```gitignore
.env
```

### 6. Crear el Archivo `README.md`
Este archivo explicará cómo configurar el proyecto:

```markdown
# MariaDB Docker Setup

## Prerequisites
- Docker
- Docker Compose

## Setup Instructions

1. Clone the repository.
2. Navigate to the `mariadb_apellido_nombre` folder.
3. Create a `.env` file based on `.env.example`.
4. Run the following command to start the MariaDB service:
   ```bash
   docker-compose up -d
   ```

## Connecting to MariaDB

- Host: `localhost`
- Port: `3306`
- Username and password are set in the `.env` file.

![alt text](image-1.png)

## Verifying the Service
Use a MySQL client like MySQL Workbench to connect to the MariaDB instance.
```

---

## Parte 2: Configuración del Proyecto MongoDB

### 1. Crear Estructura de Carpetas
Crea una carpeta para MongoDB y los archivos necesarios:

```bash
mkdir mongodb_apellido_nombre
cd mongodb_apellido_nombre
touch docker-compose.yml .env .env.example .gitignore README.md
```

### 2. Escribir el Archivo `docker-compose.yml`
El archivo `docker-compose.yml` para MongoDB será:

```yaml
version: '3'
services:
  mongodb:
    image: mongo:latest
    container_name: mongodb_container
    environment:
      MONGO_INITDB_ROOT_USERNAME: ${MONGO_INITDB_ROOT_USERNAME}
      MONGO_INITDB_ROOT_PASSWORD: ${MONGO_INITDB_ROOT_PASSWORD}
    ports:
      - "27017:27017"
    volumes:
      - mongodb_data:/data/db
volumes:
  mongodb_data:
```

**Explicación**:
- **environment**: Las variables `MONGO_INITDB_ROOT_USERNAME` y `MONGO_INITDB_ROOT_PASSWORD` son necesarias para la configuración inicial del usuario administrador de MongoDB.
- **ports**: El puerto `27017` se mapea para que podamos acceder a MongoDB desde el host.

### 3. Configurar el Archivo `.env`
En el archivo `.env`, agrega:

```bash
MONGO_INITDB_ROOT_USERNAME=mongoadmin
MONGO_INITDB_ROOT_PASSWORD=adminpassword
```

### 4. Crear un Ejemplo `.env.example`
El archivo `.env.example` para MongoDB se verá así:

```bash
MONGO_INITDB_ROOT_USERNAME=example_admin
MONGO_INITDB_ROOT_PASSWORD=example_password
```
![alt text](<Captura de pantalla 2024-09-30 162501.png>)

### 5. Configurar el Archivo `.gitignore`
Añade `.env` al archivo `.gitignore` para que no se suba a GitHub:

```gitignore
.env
```
![alt text](image.png)

### 6. Crear el Archivo `README.md`
Añade las instrucciones de configuración en el archivo `README.md`:

```markdown
# MongoDB Docker Setup

## Prerequisites
- Docker
- Docker Compose

## Setup Instructions

1. Clone the repository.
2. Navigate to the `mongodb_apellido_nombre` folder.
3. Create a `.env` file based on `.env.example`.
4. Run the following command to start the MongoDB service:
   ```bash
   docker-compose up -d
   ```

## Connecting to MongoDB

- Host: `localhost`
- Port: `27017`
- Username and password are set in the `.env` file.

![alt text](<Captura de pantalla 2024-09-30 162550.png>)

![alt text](<Captura de pantalla 2024-09-30 162411.png>)
