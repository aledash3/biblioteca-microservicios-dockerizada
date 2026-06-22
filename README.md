# 🐳 Taller Docker Compose: Microservicios con FastAPI, PostgreSQL y Nginx

![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge\&logo=python\&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-0.115.0-009688?style=for-the-badge\&logo=fastapi\&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-13-4169E1?style=for-the-badge\&logo=postgresql\&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge\&logo=docker\&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-API%20Gateway-009639?style=for-the-badge\&logo=nginx\&logoColor=white)
![Microservices](https://img.shields.io/badge/Architecture-Microservices-orange?style=for-the-badge)

---

# 📌 Descripción General

Este repositorio contiene el desarrollo de una práctica académica basada en **Docker Compose**, **FastAPI**, **PostgreSQL** y **Nginx**, orientada a la implementación de una arquitectura de microservicios para una biblioteca virtual.

El sistema está compuesto por tres microservicios independientes:

* `books_service`: gestión de libros.
* `users_service`: gestión de usuarios.
* `orders_service`: gestión de órdenes y relación entre usuarios y libros.

Todos los servicios se ejecutan en contenedores Docker y se comunican mediante redes internas. La base de datos PostgreSQL se mantiene aislada del host, mientras que Nginx funciona como **API Gateway**, exponiendo un único punto de entrada para consumir los servicios.

El proyecto implementa **CRUD completo**, documentación interactiva con **Swagger UI**, persistencia mediante volúmenes y buenas prácticas de seguridad en la configuración de contenedores.

---

# 🎯 Objetivos

## Objetivo General

Implementar una arquitectura de microservicios usando FastAPI, PostgreSQL, Docker Compose y Nginx como API Gateway, aplicando buenas prácticas de despliegue, persistencia, aislamiento de servicios y gestión de variables de entorno.

## Objetivos Específicos

* Crear tres microservicios independientes para libros, usuarios y órdenes.
* Implementar operaciones CRUD para cada entidad principal.
* Configurar PostgreSQL como sistema de persistencia.
* Utilizar Docker Compose para orquestar todos los contenedores.
* Configurar Nginx como API Gateway para enrutar las solicitudes.
* Gestionar variables sensibles mediante un archivo `.env`.
* Utilizar volúmenes para conservar los datos de la base de datos.
* Implementar redes internas para reducir la exposición de servicios.
* Verificar el funcionamiento del sistema mediante `curl` y Swagger UI.
* Aplicar buenas prácticas de seguridad en contenedores.

---

# 🧱 Arquitectura del Sistema

La arquitectura implementada sigue un enfoque de microservicios, donde cada componente tiene una responsabilidad específica.

```text
Cliente / Navegador / curl
        |
        v
Nginx API Gateway :8080
        |
        v
Microservicios FastAPI
        |
        v
PostgreSQL
```

El único servicio expuesto al host es **Nginx**, mediante el puerto `8080`.

Los microservicios y PostgreSQL no exponen puertos directamente hacia el exterior, sino que se comunican mediante redes internas definidas en Docker Compose.

---

# 🗂️ Estructura del Proyecto

```text
└── 📁Taller_DockerCompose 
    └── 📁books_service
        ├── .dockerignore
        ├── app.py
        ├── Dockerfile
        ├── requirements.txt
    └── 📁nginx
        ├── nginx.conf
    └── 📁orders_service
        ├── .dockerignore
        ├── app.py
        ├── Dockerfile
        ├── requirements.txt
    └── 📁users_service
        ├── .dockerignore
        ├── app.py
        ├── Dockerfile
        ├── requirements.txt
    ├── .env
    ├── .gitignore
    ├── docker-compose.yml
    └── README.md
```

---

# 🛠️ Tecnologías Utilizadas

| Tecnología     | Uso                                            |
| -------------- | ---------------------------------------------- |
| Python 3.11    | Lenguaje de programación de los microservicios |
| FastAPI        | Framework para construir las APIs REST         |
| Uvicorn        | Servidor ASGI para ejecutar FastAPI            |
| PostgreSQL 13  | Base de datos relacional                       |
| Psycopg2       | Conector entre Python y PostgreSQL             |
| Docker         | Contenerización de servicios                   |
| Docker Compose | Orquestación multicontenedor                   |
| Nginx          | API Gateway y proxy inverso                    |
| Swagger UI     | Documentación interactiva de las APIs          |

---

# 🧩 Servicios del Proyecto

## 📚 Books Service

Microservicio encargado de gestionar libros.

Entidad principal:

```json
{
  "id": 1,
  "title": "El Principito",
  "author": "Antoine de Saint-Exupéry"
}
```

Endpoints principales:

| Método | Endpoint          | Descripción              |
| ------ | ----------------- | ------------------------ |
| GET    | `/api/books/`     | Lista todos los libros   |
| GET    | `/api/books/{id}` | Consulta un libro por ID |
| POST   | `/api/books/`     | Crea un nuevo libro      |
| PUT    | `/api/books/{id}` | Actualiza un libro       |
| DELETE | `/api/books/{id}` | Elimina un libro         |

---

## 👤 Users Service

Microservicio encargado de gestionar usuarios.

Entidad principal:

```json
{
  "id": 1,
  "name": "David Cruz",
  "email": "david@example.com"
}
```

Endpoints principales:

| Método | Endpoint          | Descripción                |
| ------ | ----------------- | -------------------------- |
| GET    | `/api/users/`     | Lista todos los usuarios   |
| GET    | `/api/users/{id}` | Consulta un usuario por ID |
| POST   | `/api/users/`     | Crea un nuevo usuario      |
| PUT    | `/api/users/{id}` | Actualiza un usuario       |
| DELETE | `/api/users/{id}` | Elimina un usuario         |

---

## 🧾 Orders Service

Microservicio encargado de gestionar órdenes y relacionar usuarios con libros.

Entidad principal:

```json
{
  "id": 1,
  "user_id": 1,
  "user_name": "David Cruz",
  "book_id": 1,
  "book_title": "El Principito",
  "quantity": 2,
  "created_at": "2026-06-22 18:00:00"
}
```

Endpoints principales:

| Método | Endpoint           | Descripción               |
| ------ | ------------------ | ------------------------- |
| GET    | `/api/orders/`     | Lista todas las órdenes   |
| GET    | `/api/orders/{id}` | Consulta una orden por ID |
| POST   | `/api/orders/`     | Crea una nueva orden      |
| PUT    | `/api/orders/{id}` | Actualiza una orden       |
| DELETE | `/api/orders/{id}` | Elimina una orden         |

---

# 🔐 Variables de Entorno

El proyecto utiliza un archivo `.env` para centralizar las variables de configuración.

Ejemplo:

```env
POSTGRES_DB=library_db
POSTGRES_USER=library_user
POSTGRES_PASSWORD=library_pass_2026

DB_HOST=db
DB_PORT=5432

NGINX_HOST_PORT=8080
```

> El archivo `.env` contiene información sensible y no debe subirse a repositorios públicos.

---

# 🌐 API Gateway con Nginx

Nginx actúa como punto único de entrada para los microservicios.

Rutas principales:

```text
/api/books
/api/users
/api/orders
```

Ejemplo de enrutamiento:

```text
http://localhost:8080/api/books/  ->  books_service:5000
http://localhost:8080/api/users/  ->  users_service:5000
http://localhost:8080/api/orders/ ->  orders_service:5000
```

---

# 🧪 Documentación Interactiva con Swagger UI

FastAPI genera documentación automática para cada microservicio.

URLs disponibles:

```text
http://localhost:8080/api/books/docs
http://localhost:8080/api/users/docs
http://localhost:8080/api/orders/docs
```

Desde estas interfaces se pueden probar visualmente los métodos:

* GET
* POST
* PUT
* DELETE

## Solución al error `/openapi.json`

Si Swagger UI muestra el error:

```text
Not Found /openapi.json
```

significa que la documentación está intentando buscar el archivo OpenAPI en una ruta incorrecta.

Como los servicios se consumen detrás de Nginx con prefijos como `/api/books`, `/api/users` y `/api/orders`, cada microservicio debe configurar Swagger para apuntar al OpenAPI correspondiente:

```python
@app.get("/docs", include_in_schema=False)
def custom_swagger_ui():
    return get_swagger_ui_html(
        openapi_url="/api/books/openapi.json",
        title="Books Service - Swagger UI"
    )
```

Cada servicio debe usar su propio prefijo:

```text
/api/books/openapi.json
/api/users/openapi.json
/api/orders/openapi.json
```

---

# ⚙️ Requisitos

## Software Necesario

* Docker
* Docker Compose
* Git
* Navegador web
* Terminal Linux

## Sistema Operativo de Referencia

El proyecto fue probado en Ubuntu con Docker Compose.

---

# 🚀 Ejecución del Proyecto

## 1. Clonar el repositorio

```bash
git clone <URL_DEL_REPOSITORIO>
cd Taller_DockerCompose
```

## 2. Crear archivo `.env`

Crear un archivo `.env` en la raíz del proyecto:

```env
POSTGRES_DB=library_db
POSTGRES_USER=library_user
POSTGRES_PASSWORD=library_pass_2026

DB_HOST=db
DB_PORT=5432

NGINX_HOST_PORT=8080
```

## 3. Construir y levantar los contenedores

```bash
sudo docker compose up --build -d
```

## 4. Verificar contenedores activos

```bash
sudo docker compose ps
```

Se espera observar los siguientes servicios activos:

```text
db
books_service
users_service
orders_service
nginx
```

---

# 🔬 Pruebas con curl

## Verificar estado de los servicios

```bash
curl http://localhost:8080/api/books/health
curl http://localhost:8080/api/users/health
curl http://localhost:8080/api/orders/health
```

Respuesta esperada:

```json
{
  "service": "books_service",
  "status": "ok"
}
```

---

## 📚 Pruebas de Books Service

### Crear libro

```bash
curl -i -X POST http://localhost:8080/api/books/ \
  -H "Content-Type: application/json" \
  -d '{"title":"El Principito","author":"Antoine de Saint-Exupéry"}'
```

### Consultar libros

```bash
curl http://localhost:8080/api/books/
```

### Consultar libro por ID

```bash
curl http://localhost:8080/api/books/1
```

### Actualizar libro

```bash
curl -i -X PUT http://localhost:8080/api/books/1 \
  -H "Content-Type: application/json" \
  -d '{"title":"El Principito Actualizado","author":"Antoine de Saint-Exupéry"}'
```

### Eliminar libro

```bash
curl -i -X DELETE http://localhost:8080/api/books/1
```

> Si el libro tiene órdenes asociadas, el sistema devuelve `409 Conflict` para evitar inconsistencias.

---

## 👤 Pruebas de Users Service

### Crear usuario

```bash
curl -i -X POST http://localhost:8080/api/users/ \
  -H "Content-Type: application/json" \
  -d '{"name":"David Cruz","email":"david@example.com"}'
```

### Consultar usuarios

```bash
curl http://localhost:8080/api/users/
```

### Consultar usuario por ID

```bash
curl http://localhost:8080/api/users/1
```

### Actualizar usuario

```bash
curl -i -X PUT http://localhost:8080/api/users/1 \
  -H "Content-Type: application/json" \
  -d '{"name":"David Cruz Actualizado","email":"david.updated@example.com"}'
```

### Eliminar usuario

```bash
curl -i -X DELETE http://localhost:8080/api/users/1
```

> Si el usuario tiene órdenes asociadas, el sistema devuelve `409 Conflict` para evitar inconsistencias.

---

## 🧾 Pruebas de Orders Service

### Crear orden

```bash
curl -i -X POST http://localhost:8080/api/orders/ \
  -H "Content-Type: application/json" \
  -d '{"user_id":1,"book_id":1,"quantity":2}'
```

### Consultar órdenes

```bash
curl http://localhost:8080/api/orders/
```

### Consultar orden por ID

```bash
curl http://localhost:8080/api/orders/1
```

### Actualizar orden

```bash
curl -i -X PUT http://localhost:8080/api/orders/1 \
  -H "Content-Type: application/json" \
  -d '{"user_id":1,"book_id":1,"quantity":5}'
```

### Eliminar orden

```bash
curl -i -X DELETE http://localhost:8080/api/orders/1
```

---

# 🗄️ Verificación en PostgreSQL

Ingresar a PostgreSQL desde el contenedor:

```bash
sudo docker compose exec db psql -U library_user -d library_db
```

Listar tablas:

```sql
\dt
```

Consultar libros:

```sql
SELECT * FROM books;
```

Consultar usuarios:

```sql
SELECT * FROM users;
```

Consultar órdenes:

```sql
SELECT * FROM orders;
```

Salir de PostgreSQL:

```sql
\q
```

---

# 🛡️ Buenas Prácticas Aplicadas

El proyecto incorpora buenas prácticas de seguridad y mantenibilidad:

* Uso de archivo `.env` para variables de entorno.
* Exclusión del archivo `.env` mediante `.gitignore`.
* PostgreSQL sin exposición directa al host.
* Microservicios sin puertos públicos.
* Nginx como único punto de entrada.
* Redes internas para la comunicación entre servicios.
* Volumen persistente para PostgreSQL.
* Archivo `nginx.conf` montado en modo solo lectura.
* Uso de `.dockerignore` en cada microservicio.
* Contenedores de aplicación ejecutados con usuario no root.
* Separación de responsabilidades por microservicio.
* Validación de datos mediante Pydantic.
* CRUD completo para cada entidad.
* Documentación automática mediante Swagger UI.

---

# 🧬 Redes Docker

El archivo `docker-compose.yml` define tres redes:

```text
public_net
app_net
db_net
```

## public_net

Red utilizada por Nginx para publicar el API Gateway hacia el host.

## app_net

Red interna utilizada para comunicar Nginx con los microservicios.

## db_net

Red interna utilizada para comunicar los microservicios con PostgreSQL.

---

# 💾 Volúmenes Docker

El proyecto utiliza el volumen:

```text
postgres_data
```

Este volumen permite conservar los datos de PostgreSQL aunque los contenedores sean detenidos o recreados.

---

# ✅ Validación de Aislamiento

Los microservicios no deben estar disponibles directamente desde el host.

Este comando debería fallar:

```bash
curl http://localhost:5000/health
```

La entrada válida debe ser únicamente por Nginx:

```bash
curl http://localhost:8080/api/books/health
```

También se puede verificar que PostgreSQL no está expuesto observando la salida de:

```bash
sudo docker compose ps
```

Solo Nginx debería mostrar un puerto publicado:

```text
0.0.0.0:8080->80/tcp
```

---

# 🧰 Comandos Útiles

## Ver logs generales

```bash
sudo docker compose logs
```

## Ver logs por servicio

```bash
sudo docker compose logs books_service
sudo docker compose logs users_service
sudo docker compose logs orders_service
sudo docker compose logs nginx
sudo docker compose logs db
```

## Detener contenedores sin borrar datos

```bash
sudo docker compose down
```

## Detener contenedores y borrar datos

```bash
sudo docker compose down -v
```

## Reconstruir completamente

```bash
sudo docker compose down
sudo docker compose up --build --force-recreate -d
```

---

# 🔬 Resultados Esperados

Al finalizar la ejecución y pruebas del proyecto se espera comprobar que:

* Los contenedores se ejecutan correctamente.
* PostgreSQL se encuentra en estado `healthy`.
* Nginx funciona como API Gateway.
* Las rutas `/api/books`, `/api/users` y `/api/orders` responden correctamente.
* Las operaciones CRUD funcionan en los tres microservicios.
* Los datos se almacenan de forma persistente en PostgreSQL.
* Los microservicios no están expuestos directamente al host.
* La base de datos no está expuesta públicamente.
* Swagger UI permite probar la API desde el navegador.

---

# 👨‍💻 Autor

**David Alejandro Cruz Palacios**

Carrera de Ciencias de la Computación
Universidad Politécnica Salesiana
Quito, Ecuador

---

# 📜 Licencia

Este proyecto fue desarrollado con fines académicos y educativos.

Todos los derechos pertenecen a su respectivo autor.
::: 
