
# EJERCICIOS DE DOCKER   

## 1. Crear un `docker-compose.yml` para desplegar `miapp` en Docker Swarm  

### Requisitos:  
- Servicio llamado `miapp`.  
- Imagen: `nahuic/miapp:v1`.  
- Seis réplicas distribuidas en todo el clúster.  
- Solo se detendrá en caso de fallo y esperará 10 segundos antes de reiniciar.  

 
```yaml
version: '3.8'
services:
  miapp:
    image: nahuic/miapp:v1
    deploy:
      replicas: 6  # Número de réplicas del servicio
      mode: replicated  # Modo de replicación
      restart_policy:
        condition: on-failure  # Solo reiniciar si falla
        delay: 10s  # Espera de 10 segundos entre reinicios
    networks:
      - default

networks:
  default:
    driver: bridge
```

## 2. Crear un docker-compose.yml para el servicio miotra a partir de un Dockerfile

### Requisitos:  
- Servicio llamado ``miotra``.
- Se usará una imagen construida desde un ``Dockerfile``.
- 10 réplicas con 1 contenedor por nodo.
- Se actualizarán 2 contenedores a la vez y si falla, se revierte al estado anterior.
- Se permitirán hasta 5 intentos fallidos antes de dar error.

### Pasos previos:
```bash
docker build -t miotra:latest .
```

 
```yaml
version: '3.8'
services:
  miotra:
    image: miotra:latest  # Utiliza la imagen que acabamos de construir
    deploy:
      replicas: 10  # Número de réplicas del servicio
      mode: replicated  # Modo de replicación
      placement:
        constraints:
          - node.role == worker  # Distribuir en nodos de trabajo
      update_config:
        parallelism: 2  # Se actualizan 2 contenedores a la vez
        delay: 10s  # Espera de 10 segundos entre actualizaciones
        failure_action: rollback  # Si falla la actualización, revertir al estado anterior
        max_failure_ratio: 0.5  # Permitir hasta un 50% de fallos antes de error
    networks:
      - default

networks:
  default:
    driver: bridge
```

## 3. Crear un docker-compose.yml para miprog con limitaciones de CPU y memoria

### Requisitos:  
- Imagen: miprog_img:1.0 desde Docker Hub.
- Límite de uso:
- Máximo: 30% CPU, 50MB RAM.
- Mínimo: 10% CPU, 30MB RAM.
- 20 réplicas con un máximo de 5 por nodo.
- Health check cada minuto, con 3 intentos y un inicio tras 20 segundos

 
```yaml
version: '3.8'
services:
  miprog:
    image: miprog_img:1.0
    deploy:
      replicas: 20
      mode: replicated
      placement:
        constraints:
          - node.role == worker
      max_replicas_per_node: 5
      resources:
        limits:
          cpus: '0.30'  # Limitar al 30% de CPU
          memory: 50M  # Limitar a 50MB de memoria
        reservations:
          cpus: '0.10'  # Reservar al menos 10% de CPU
          memory: 30M  # Reservar al menos 30MB de memoria
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8080/health"]
      interval: 1m
      retries: 3
      start_period: 20s
    networks:
      - default

networks:
  default:
    driver: bridge
```


## 4. Crear docker-compose.yml para miprog2 con volúmenes

### Requisitos:  
- Mismo servicio miprog_img:1.0.
- Volumen local datos asociado a /app/data.
- Solo se ejecutará en nodos administradores.
- 10 réplicas con máximo 2 por nodo.


 
```yaml
version: '3.8'
services:
  miprog2:
    image: miprog_img:1.0
    deploy:
      replicas: 10
      mode: replicated
      placement:
        constraints:
          - node.role == manager
      max_replicas_per_node: 2
    volumes:
      - datos:/app/data
    networks:
      - default

volumes:
  datos:
    driver: local

networks:
  default:
    driver: bridge

```

## 5. Crear docker-compose.yml para redis_y_tal con secreto externo

### Requisitos:  
- Servicio basado en la última imagen de Redis.
- Secreto externo llamado valle_secreto.
- 6 réplicas, una en cada nodo.
- Actualización de 2 contenedores a la vez.
- Si falla, se revierte al estado anterior.
- El tiempo máximo de espera para considerar un fallo es de 30s.


 
```yaml
version: '3.8'
services:
  redis_y_tal:
    image: redis:latest
    deploy:
      replicas: 6
      mode: replicated
      placement:
        constraints:
          - node.role == worker
      update_config:
        parallelism: 2
        failure_action: rollback
        max_failure_ratio: 0.5
        delay: 10s
        timeout: 30s
    secrets:
      - valle_secreto
    networks:
      - default

secrets:
  valle_secreto:
    external: true  # Define que el secreto es externo

networks:
  default:
    driver: bridge
```