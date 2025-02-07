# EJERCICIOS DE ADMINISTRACIÓN WINDOWS - (PowerShell  )

## 1. Crea un cmdlet de PowerShell llamado saludo1.ps1 
Define dos variables: `$nombre` y `$saludo`. Luego, muestra un mensaje en la consola con el saludo y el nombre.  

 
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