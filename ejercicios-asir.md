# 1º ASIR  
## INSTALACIÓN DE SISTEMAS OPERATIVOS  

### Preguntas:  
- ¿Qué es un hipervisor? ¿Qué tipos de hipervisores existen?  
- ¿Qué es un Sistema Operativo y dónde está instalado?  
- ¿Qué significa LTS?  

### Instalación de sistemas operativos en un hipervisor:  
Elige un hipervisor (**VirtualBox** o **VMWare**) y realiza la instalación de los siguientes sistemas operativos en sus versiones **LTS**:  

- **Ubuntu Server**  
- **Ubuntu Desktop**  
- **Windows Server**

# EJERCICIOS DE ADMINISTRACIÓN LINUX  
## Monitorización de procesos existentes en el sistema  

### 1. Ejecuta el comando `xeyes`  
```bash
xeyes
```

### 2. ¿Qué PID tiene el proceso `xeyes`? ¿Cuál es su proceso padre? ¿Cuál es el PID del proceso padre?

Para encontrar el **PID** de `xeyes`:  

```bash
pgrep xeyes
ps aux | grep xeyes
```

Para obtener el proceso padre:
```bash
ps -p <PID_de_xeyes> -o comm
```

Para obtener el PID del proceso padre:
```bash
ps -o ppid= -p <PID_de_xeyes>
```

### 3. ¿Cuántos procesos hay en ejecución en el sistema?
```bash
ps -e | wc -l
```

### 4. ¿Cuántos procesos son del usuario root? (Muchos /Pocos)
```bash
ps -U root | wc -l
```


### 5. Descubre la jerarquía de procesos de su usuario. (Pista pstree) Buscar en man.
```bash
Pstree –u <usuario>
```

### 6. Utilizando el comando top, averiguar cuál es el proceso que más tiempo de CPU ha consumido.
```bash
Ejecuta el comando top y pulsa P
```

### 7. Utilizando el comando top, averigüe cuál es el proceso que más espacio de memoria ha consumido
```bash
Ejecuta el comando top y pulsa M
```

### 8. ¿En qué fecha y hora arrancó el sistema?
```bash
Cat /proc/stat | grep btime
Date –d <resultado del comando de arriba>
-----
Uptime –s
```


# EJERCICIO SERVIDOR WEB APACHE

### 1. Monta un servidor web Apache, carga un fichero `index.html` y comprueba que funciona correctamente en tu navegador.  

### Pasos:  

1. **Instalar Apache**  
```bash
sudo apt install apache2
```
2. **Habilitar el servidor Apache en el firewall**  
```bash
sudo ufw allow apache
```
3. **Comprobar el estado del servidor Apache**
**  
```bash
sudo systemctl status apache2
```
4. **Ruta donde cargar documentos para mostrar en la web**  
```bash
/var/www/html
```
5. **Fichero de configuración apache**  
```bash
/etc/apache2
```
6. **Acceder a través de localhost/ip del servidor**  



# EJERCICIOS DE ADMINISTRACIÓN WINDOWS - (PowerShell  )

## 1. Crea un cmdlet de PowerShell llamado saludo1.ps1 
Define dos variables: `$nombre` y `$saludo`. Luego, muestra un mensaje en la consola con el saludo y el nombre.  

### Código:  
```powershell
# saludo1.ps1
# Definir las variables
$nombre = "Juan"
$saludo = "Hola"

# Mostrar el mensaje en la consola
Write-Host "$saludo, $nombre!"
```

## 2. Crea un cmdlet de PowerShell llamado saludo2.ps1
```powershell
# saludo2.ps1
param (
    [string]$nombre,
    [string]$saludo
)

# Mostrar el mensaje en la consola
Write-Host "$saludo, $nombre!"
```

## 3. Crea un cmdlet de PowerShell llamado saludo3.ps1
```powershell
# saludo3.ps1
# Solicitar el saludo al usuario
$saludo = Read-Host "Por favor, ingresa el saludo"

# Solicitar el nombre al usuario
$nombre = Read-Host "Por favor, ingresa el nombre"

# Mostrar el mensaje en la consola
Write-Host "$saludo, $nombre!"
```

## 4. Crea un cmdlet de PowerShell que realice operaciones aritméticas entre dos números

```powershell
# operaciones_aritmeticas.ps1

# Solicitar los números al usuario
$numero1 = Read-Host "Por favor, ingresa el primer número"
$numero2 = Read-Host "Por favor, ingresa el segundo número"

# Convertir los valores a tipo numérico
$numero1 = [double]$numero1
$numero2 = [double]$numero2

# Realizar las operaciones aritméticas
$suma = $numero1 + $numero2
$resta = $numero1 - $numero2
$multiplicacion = $numero1 * $numero2
$division = if ($numero2 -ne 0) { $numero1 / $numero2 } else { "No se puede dividir por cero" }

# Mostrar los resultados en la consola
Write-Host "Suma: $suma"
Write-Host "Resta: $resta"
Write-Host "Multiplicación: $multiplicacion"
Write-Host "División: $division"
```

## 5. Crea un cmdlet de PowerShell que compare dos números
```powershell
# comparacion_numeros.ps1

# Solicitar los números al usuario
$numero1 = Read-Host "Por favor, ingresa el primer número entero"
$numero2 = Read-Host "Por favor, ingresa el segundo número entero"

# Convertir los valores a enteros
$numero1 = [int]$numero1
$numero2 = [int]$numero2

# Comparar los números
if ($numero1 -gt $numero2) {
    Write-Host "$numero1 es mayor que $numero2."
} elseif ($numero1 -lt $numero2) {
    Write-Host "$numero1 es menor que $numero2."
} else {
    Write-Host "$numero1 es igual a $numero2."
}

```

## 6. Crea un cmdlet de PowerShell que repita "FAP" según un número ingresado

```PowerShell
# fap_repeticiones.ps1

# Solicitar un número al usuario
$numero = Read-Host "Por favor, ingresa un número positivo"

# Convertir el valor a un número entero
$numero = [int]$numero

# Verificar si el número es positivo
if ($numero -le 0) {
    Write-Host "El número debe ser positivo. Inténtalo de nuevo."
} else {
    # Usar un bucle para mostrar "FAP" tantas veces como el número ingresado
    for ($i = 1; $i -le $numero; $i++) {
        Write-Host "FAP"
    }
}

```


## 7. Crea un cmdlet que valide un número entre 1 y 100
```PowerShell
# validar_numero.ps1

# Inicializar contador de errores
$errores = 0
$numero = 0

while ($true) {
    # Solicitar un número al usuario
    $numero = Read-Host "Por favor, ingresa un número entre 1 y 100"

    # Intentar convertir el valor a un número entero
    if ([int]::TryParse($numero, [ref]$null)) {
        $numero = [int]$numero

        # Verificar si el número está en el rango
        if ($numero -ge 1 -and $numero -le 100) {
            break
        } else {
            Write-Host "El número debe estar entre 1 y 100."
            $errores++
        }
    } else {
        Write-Host "Eso no es un número válido. Por favor, inténtalo de nuevo."
        $errores++
    }
}

# Evaluar el resultado
if ($errores -eq 0) {
    Write-Host "¡Campeón! Has ingresado un número válido a la primera."
} else {
    for ($i = 1; $i -le $errores; $i++) {
        Write-Host "¡Error! Intenta nuevamente."
    }
}
```

# EJERCICIOS DE ADMINISTRACIÓN DE SSOO

## 1. Realizar un Shell Script que reciba 3 argumentos de programa y realice una operación matemática  
El script debe:  
- Controlar que los argumentos sean válidos.  
- Asegurar que la operación matemática es válida.  
- Evitar divisiones por cero.  
- Validar que el número de argumentos es 3.  

### Código:  
```bash
#!/bin/bash

# Comprobar que se reciben exactamente 3 argumentos
if [ $# -ne 3 ]; then
    echo "No hay 3 argumentos. Saliendo."
    exit 1
fi

# Comprobar que el primer y tercer argumento son números
if ! [[ $1 =~ ^-?[[:digit:]]+$ ]] || ! [[ $3 =~ ^-?[[:digit:]]+$ ]]; then
    echo "No se introdujeron valores válidos. Saliendo."
    exit 1
fi

# Comprobar que el segundo argumento es una operación válida
if ! [[ $2 =~ ^[+\-*/^]$ ]]; then
    echo "No se introdujo una operación válida. Saliendo."
    exit 1
fi

# Realizar la operación matemática
case $2 in
    +) echo "Resultado de $1 + $3: $(( $1 + $3 ))" ;;
    -) echo "Resultado de $1 - $3: $(( $1 - $3 ))" ;;
    \*) echo "Resultado de $1 * $3: $(( $1 * $3 ))" ;;
    /) 
        if [ $3 -eq 0 ]; then
            echo "Error: División por cero no permitida. Saliendo."
            exit 1
        fi
        echo "Resultado de $1 / $3: $(( $1 / $3 ))"
        ;;
    ^) echo "Resultado de $1 ^ $3: $(($1 ** $3))" ;;
esac
```

## 2. Realizar un Shell Script que gestione un fichero de datos
El script debe:  
- Verificar si el fichero existe y mostrar sus permisos.
- Permitir al usuario ingresar 5 nombres y apellidos, eliminando espacios intermedios.

### Código: 
```bash
#!/bin/bash

echo -n "Introduce el nombre de un fichero que tendrá los datos: "
read fichero

# Verificar si el fichero existe
if ! [ -e "./$fichero" ]; then
    echo "Fichero no encontrado en la ruta actual."
    exit 1
fi

# Mostrar los permisos del fichero
echo "Permisos de $fichero: $(ls -l "$fichero" | awk '{print $1}')"

# Guardar 5 nombres y apellidos en el fichero
for ((i=1; i<=5; i++))
do
    echo -n "Introduce el nombre de la persona nº$i: "
    read nombre
    nombre=$(echo "$nombre" | tr -d ' ')

    echo -n "Introduce el primer apellido de la persona nº$i: "
    read apellido1
    apellido1=$(echo "$apellido1" | tr -d ' ')

    echo -n "Introduce el segundo apellido de la persona nº$i: "
    read apellido2
    apellido2=$(echo "$apellido2" | tr -d ' ')

    echo "$i:$nombre:$apellido1:$apellido2" >> $fichero
done
```

## 3. Realizar un Shell Script que consulte un fichero de datos
El script debe:  
- Permitir al usuario buscar un nombre en un fichero.
- Guardar la consulta con fecha y hora en un fichero general.

### Código: 
```bash

#!/bin/bash

echo -n "¿Nombre del fichero del que se va a leer los datos?: "
read fichero

# Verificar si el fichero existe
if ! [ -e "./$fichero" ]; then
    echo "Fichero no encontrado."
    exit 1
fi

echo -n "¿Nombre a buscar dentro del fichero de datos?: "
read nombre

# Crear el fichero de consultas si no existe
if ! [ -e "./consultas.txt" ]; then
    touch consultas.txt
    echo "Fichero 'consultas.txt' creado."
    echo -e "Nº Nombre Apellido1 Apellido2 Fecha Hora" > consultas.txt
fi

# Buscar el nombre y guardar la consulta con la fecha y hora
awk -F':' -v valor="$nombre" '{
    if ($2 == valor) {
        printf "%-6s %-15s %-15s %-15s %-12s %-8s\n",$1,$2,$3,$4,strftime("%Y-%m-%d"),strftime("%H:%M")
    }
}' "$fichero" >> consultas.txt

# Alinear la salida con column -t
column -t consultas.txt > consultas_temp.txt && mv consultas_temp.txt consultas.txt
echo "Consulta registrada en 'consultas.txt'."


```


## 4. Realizar un Shell Script que guarde consultas en directorios estructurados
El script debe:  
- Crear un directorio Consultas y dentro subdirectorios por fecha.
- Guardar cada consulta en un archivo separado con el nombre del usuario buscado.

### Código: 
```bash
#!/bin/bash

# Crear el directorio "Consultas" si no existe
if [ -d "./Consultas" ]; then
    echo "El directorio 'Consultas' ya existe."
else
    mkdir -p "./Consultas"
    echo "Directorio 'Consultas' creado."
fi

# Crear un subdirectorio con la fecha actual
if [ -d "./Consultas/$(date +%F)" ]; then
    echo "El directorio con la fecha '$(date +%F)' ya existe."
else
    mkdir -p "./Consultas/$(date +%F)"
    echo "Directorio con la fecha '$(date +%F)' creado."
fi

echo -n "¿Nombre del fichero del que se va a leer los datos?: "
read fichero

# Verificar si el fichero de datos existe
if ! [ -e "./$fichero" ]; then
    echo "Fichero no encontrado."
    exit 1
fi

echo -n "¿Nombre a buscar dentro del fichero de datos?: "
read nombre

# Crear el archivo de consulta si no existe
ruta_fichero="./Consultas/$(date +%F)/$nombre.txt"
if ! [ -e "$ruta_fichero" ]; then
    touch "$ruta_fichero"
    echo "Fichero '$nombre.txt' creado."
    echo -e "Nº Nombre Apellido1 Apellido2 Hora" > "$ruta_fichero"
fi

# Guardar la consulta en el archivo correspondiente
awk -F':' -v valor="$nombre" '{
    if ($2 == valor) {
        printf "%-6s %-15s %-15s %-15s %-8s\n",$1,$2,$3,$4,strftime("%H:%M")
    }
}' "$fichero" >> "$ruta_fichero"

# Alinear la salida con column -t
column -t "$ruta_fichero" > "${ruta_fichero}_temp" && mv "${ruta_fichero}_temp" "$ruta_fichero"

echo "Consulta registrada en '$ruta_fichero'."

```



# EJERCICIOS DE ADMINISTRACIÓN - Escritorio Remoto y SSH  

## 4. Configurar un escritorio remoto con Terminal Server  
El cliente se conectará a través de la red a una máquina con Windows que tiene el puerto **3389** con el servicio **Terminal Server** habilitado.  

### a. Configuración del Servidor (Windows)  

1. **Abrir el Administrador de Servicios**  
   - Presiona `Windows + R`, escribe `services.msc` y presiona `Enter`.  
   - Busca el servicio **Servicios de Escritorio Remoto** y verifica que está en ejecución.  

2. **Activar Escritorio Remoto**  
   - Ve a `Sistema` → `Configuración de Escritorio Remoto`.  
   - Abre `Panel de control` → `Seguridad y Sistema` → `Permitir acceso remoto`.  
   - Marca la opción:  
     ```plaintext
     Permitir conexiones remotas a este equipo
     ```  
     Esto permitirá que otros equipos se conecten remotamente.  

3. **Deshabilitar el firewall de Windows**  
   - Esto es necesario para permitir la conexión remota sin restricciones.  

---

### b. Configuración del Cliente  

1. **Abrir el Cliente de Escritorio Remoto**  
   - Ejecuta `Conexión a Escritorio Remoto`.  
   - Ingresa la dirección **IP del servidor** (la IP pública si accedes desde Internet).  
   - Conéctate usando las credenciales del usuario configurado en el servidor.  

---

## 5. Conectar a una máquina Ubuntu Desktop mediante SSH con MOBAXterm  

### Pasos:  

1. **Descargar e instalar MOBAXterm**  
   - Puedes descargarlo desde su sitio web oficial: [MOBAXterm](https://mobaxterm.mobatek.net/)  

2. **Conectarse a Ubuntu Desktop por SSH**  
   - Abre MOBAXterm.  
   - En la barra superior, selecciona **"Session" → "SSH"**.  
   - Introduce la dirección IP de la máquina Ubuntu Desktop.  
   - Especifica el usuario y la contraseña cuando lo solicite.  

3. **Confirmar la conexión**  
   - Si la conexión es exitosa, aparecerá el prompt de la terminal de Ubuntu en MOBAXterm.  



# EJERCICIOS DE ADMINISTRACIÓN DE ACTIVE DIRECTORY (AD DS)  

## 1. Creación automatizada de usuarios en AD DS a partir de un archivo CSV  
Se ha decidido crear el **AD DS de la FIFA-2018**, donde:  
- Cada usuario representa un **jugador**.  
- Cada **club** será un grupo en Active Directory.  
- Se utilizará **PowerShell** para importar los usuarios desde un archivo CSV y asignarlos a sus respectivos grupos.  

### Código:  
```powershell
Import-Module ActiveDirectory

# Ruta del archivo CSV
$csvPath = "C:\ruta\a\jugadores.csv"
$jugadores = Import-Csv -Path $csvPath

foreach ($jugador in $jugadores) {
    # Definir el nombre de usuario
    $username = $jugador.Username
    
    # Crear el usuario en AD
    New-ADUser -Name "$($jugador.FirstName) $($jugador.LastName)" `
        -GivenName $jugador.FirstName `
        -Surname $jugador.LastName `
        -SamAccountName $username `
        -UserPrincipalName "$username@FIFA18.com" `
        -Path "OU=Jugadores,DC=FIFA18,DC=com" `
        -AccountPassword (ConvertTo-SecureString $jugador.Password -AsPlainText -Force) `
        -Enabled $true

    # Asignar el usuario al grupo del club
    $grupo = $jugador.Club
    if (Get-ADGroup -Filter {Name -eq $grupo}) {
        Add-ADGroupMember -Identity $grupo -Members $username
    } else {
        Write-Host "El grupo '$grupo' no existe."
    }
}
```

# EJERCICIOS DE DOCKER   

## 1. Crear un `docker-compose.yml` para desplegar `miapp` en Docker Swarm  

### Requisitos:  
- Servicio llamado `miapp`.  
- Imagen: `nahuic/miapp:v1`.  
- Seis réplicas distribuidas en todo el clúster.  
- Solo se detendrá en caso de fallo y esperará 10 segundos antes de reiniciar.  

### Código:  
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

### Código:  
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

### Código:  
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


### Código:  
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


### Código:  
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