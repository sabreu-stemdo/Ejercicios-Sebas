# EJERCICIO SERVIDOR WEB APACHE

### 1. Monta un servidor web Apache, carga un fichero `index.html` y comprueba que funciona correctamente en tu navegador.  

 

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

