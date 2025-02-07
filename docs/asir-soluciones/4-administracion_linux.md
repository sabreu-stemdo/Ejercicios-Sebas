
# EJERCICIOS DE ADMINISTRACIÓN DE SSOO

## 1. Realizar un Shell Script que reciba 3 argumentos de programa y realice una operación matemática  
El script debe:  
- Controlar que los argumentos sean válidos.  
- Asegurar que la operación matemática es válida.  
- Evitar divisiones por cero.  
- Validar que el número de argumentos es 3.  

 
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
