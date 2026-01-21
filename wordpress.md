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

### 1.1 Activación del motor de reescritura (Rewrite)

Para que WordPress pueda generar URLs "limpias" o "amigables" (ej: `misitio.com/contacto` en lugar de `index.php?id=123`), debemos activar el módulo de reescritura de Apache. Sin este paso, la web solo funcionará en su página de inicio.

```bash
sudo a2enmod rewrite
```

> **Nota técnica para el alumno:** El comando `sudo a2enmod rewrite` instala la "capacidad" de redirección en el servidor (el motor), pero por seguridad Apache no la usará a menos que le demos permiso explícito en el archivo de configuración (ver Paso 4). 

Esta distinción es clave en administración de sistemas: una cosa es que el software esté **instalado** y otra que tenga **permisos** para actuar sobre una carpeta específica.

---

## 2. Configuración de la Base de Datos

WordPress utiliza una base de datos MySQL para almacenar todo el contenido dinámico (entradas, usuarios, configuraciones).

```sql
sudo mysql

-- Creamos la base de datos para el sitio
CREATE DATABASE wp_datos;

-- Creamos el usuario local exclusivo para esta web
CREATE USER 'alumno'@'localhost' IDENTIFIED BY 'SMR_2026';

-- Otorgamos permisos totales sobre la base de datos al usuario
GRANT ALL PRIVILEGES ON wp_datos.* TO 'alumno'@'localhost';

-- Aplicamos los cambios y cerramos
FLUSH PRIVILEGES;
EXIT;
```