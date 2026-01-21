# Manual de Instalación: WordPress en Ubuntu Server (AWS)
**Asignatura:** Aplicaciones Web | **Ciclo:** SMR

Este manual detalla los pasos para realizar una instalación mínima pero plenamente funcional de WordPress en una instancia EC2 de AWS.

---

## 1. Instalación del Stack LAMP
Actualizamos el sistema e instalamos Apache, MySQL y PHP con las extensiones necesarias para que WordPress pueda procesar imágenes y datos.

```bash
sudo apt update
sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql php-gd php-xml php-mbstring -y
```

## 2. Configuración de la Base de Datos

WordPress utiliza una base de datos MySQL para almacenar todo el contenido dinámico (entradas, usuarios, configuraciones).

```sql
sudo mysql

-- Creamos la base de datos para el sitio
CREATE DATABASE wp_datos;

-- Creamos el usuario local exclusivo para esta web
CREATE USER 'alumno'@'localhost' IDENTIFIED BY 'password';

-- Otorgamos permisos totales sobre la base de datos al usuario
GRANT ALL PRIVILEGES ON wp_datos.* TO 'alumno'@'localhost';

-- Aplicamos los cambios y cerramos
FLUSH PRIVILEGES;
EXIT;
```

## 3. Descarga y Preparación de Archivos

En este paso descargamos la última versión oficial de WordPress en español y la preparamos en el directorio raíz del servidor web. También ajustaremos los permisos de Linux para que Apache sea el "dueño" de los archivos.

```bash
cd /var/www/html
sudo wget https://es.wordpress.org/latest-es_ES.tar.gz
sudo tar -xvf latest-es_ES.tar.gz
sudo mv wordpress/* .
sudo rm -rf wordpress latest-es_ES.tar.gz index.html

# Cambio de propietario al usuario de Apache (www-data)
# Fundamental para que WordPress pueda instalar temas, plugins y subir imágenes
sudo chown -R www-data:www-data /var/www/html/
```

## 4. Finalización de la Instalación (Vía Web)

Una vez que el servidor Ubuntu tiene el stack LAMP y los permisos configurados, el resto del proceso se realiza de forma visual desde el navegador.

1.  **Obtén la IP Pública:** Ve al panel de control de AWS EC2, localiza tu instancia y copia la dirección "IPv4 pública".
2.  **Acceso inicial:** Escribe esa IP en la barra de direcciones de tu navegador. Debería aparecer el selector de idioma de WordPress.
3.  **Configuración de la base de datos:** Introduce los credenciales que creamos en el Paso 2:
    * **Nombre de la base de datos:** `wp_datos`
    * **Nombre de usuario:** `alumno`
    * **Contraseña:** `password` (o la que definieras en MySQL).
    * **Servidor de la base de datos:** `localhost`
    * **Prefijo de tabla:** `wp_`



4.  **Información del sitio:** Define el título de tu web y crea tu cuenta de **Administrador de WordPress** (estos datos son para entrar al panel `/wp-admin`, no los confundas con los de la base de datos).

---
