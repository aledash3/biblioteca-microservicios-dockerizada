# DockerCompose CRUD FastAPI + PostgreSQL + Nginx

Archivos modificados para implementar CRUD completo.

## Aplicar cambios

Copiar estos archivos sobre el proyecto original.

## Levantar

```bash
sudo docker compose down
sudo docker compose up --build -d
```

## Pruebas

```bash
curl http://localhost:8080/api/books/health
curl http://localhost:8080/api/users/health
curl http://localhost:8080/api/orders/health
```

## Swagger UI

- http://localhost:8080/api/books/docs
- http://localhost:8080/api/users/docs
- http://localhost:8080/api/orders/docs
