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
