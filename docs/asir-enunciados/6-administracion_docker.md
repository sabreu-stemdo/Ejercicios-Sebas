
# EJERCICIOS DE DOCKER   
---

## 1. Crear un `docker-compose.yml` para desplegar `miapp` en Docker Swarm  

### Requisitos:  
- Servicio llamado `miapp`.  
- Imagen: `nahuic/miapp:v1`.  
- Seis réplicas distribuidas en todo el clúster.  
- Solo se detendrá en caso de fallo y esperará 10 segundos antes de reiniciar.  


## 2. Crear un docker-compose.yml para el servicio miotra a partir de un Dockerfile

### Requisitos:  
- Servicio llamado ``miotra``.
- Se usará una imagen construida desde un ``Dockerfile``.
- 10 réplicas con 1 contenedor por nodo.
- Se actualizarán 2 contenedores a la vez y si falla, se revierte al estado anterior.
- Se permitirán hasta 5 intentos fallidos antes de dar error.


## 3. Crear un docker-compose.yml para miprog con limitaciones de CPU y memoria

### Requisitos:  
- Imagen: miprog_img:1.0 desde Docker Hub.
- Límite de uso:
- Máximo: 30% CPU, 50MB RAM.
- Mínimo: 10% CPU, 30MB RAM.
- 20 réplicas con un máximo de 5 por nodo.
- Health check cada minuto, con 3 intentos y un inicio tras 20 segundos


## 4. Crear docker-compose.yml para miprog2 con volúmenes

### Requisitos:  
- Mismo servicio miprog_img:1.0.
- Volumen local datos asociado a /app/data.
- Solo se ejecutará en nodos administradores.
- 10 réplicas con máximo 2 por nodo.


## 5. Crear docker-compose.yml para redis_y_tal con secreto externo

### Requisitos:  
- Servicio basado en la última imagen de Redis.
- Secreto externo llamado valle_secreto.
- 6 réplicas, una en cada nodo.
- Actualización de 2 contenedores a la vez.
- Si falla, se revierte al estado anterior.
- El tiempo máximo de espera para considerar un fallo es de 30s.
