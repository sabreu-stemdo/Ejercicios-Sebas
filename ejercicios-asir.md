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
