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

## 4. Configuración del Servidor Web (Paso Crítico)

Por defecto, Apache viene configurado para ignorar cualquier instrucción de configuración local por motivos de seguridad. Sin embargo, WordPress necesita "reescribir" URLs para que funcionen los enlaces permanentes (ej: `/contacto` en lugar de `/?p=123`). 

Para permitir esto, debemos autorizar al servidor a leer el archivo de reglas oculto (`.htaccess`) que WordPress genera.

1.  **Abre el archivo de configuración** por defecto de Apache: 
    `sudo nano /etc/apache2/sites-available/000-default.conf`

2.  **Localiza la línea** `DocumentRoot /var/www/html` y añade justo debajo el siguiente bloque de código:

```apache
<Directory /var/www/html>
    AllowOverride All
</Directory>
```

> **¿Qué hace exactamente "AllowOverride All"?**
> Es la autorización que el administrador del servidor da a la aplicación web. 
> * **`None` (Configuración por defecto):** El servidor ignora cualquier archivo de configuración local (`.htaccess`) que encuentre en las carpetas del sitio.
> * **`All`:** El servidor tiene permiso para leer y aplicar las reglas de navegación que WordPress escribe automáticamente en su archivo `.htaccess`. 
>
> **Consecuencia en clase:** Si el alumno olvida cambiar este parámetro a `All`, la página de inicio cargará correctamente, pero al hacer clic en cualquier sección, noticia o menú, el servidor responderá con un **Error 404 Not Found**, ya que no sabrá cómo redirigir la petición internamente.



3.  **Reinicia el servicio Apache** para que el servidor cargue tanto el módulo de reescritura (`rewrite`) como la nueva política de permisos:
```bash
sudo systemctl restart apache2
```

## 5. Finalización de la Instalación (Vía Web)

Una vez que el servidor Ubuntu tiene el stack LAMP y los permisos configurados, el resto del proceso se realiza de forma visual desde el navegador.

1.  **Obtén la IP Pública:** Ve al panel de control de AWS EC2, localiza tu instancia y copia la dirección "IPv4 pública".
2.  **Acceso inicial:** Escribe esa IP en la barra de direcciones de tu navegador. Debería aparecer el selector de idioma de WordPress.
3.  **Configuración de la base de datos:** Introduce los credenciales que creamos en el Paso 2:
    * **Nombre de la base de datos:** `wp_datos`
    * **Nombre de usuario:** `alumno`
    * **Contraseña:** `SMR_2026` (o la que definieras en MySQL).
    * **Servidor de la base de datos:** `localhost`
    * **Prefijo de tabla:** `wp_`



4.  **Información del sitio:** Define el título de tu web y crea tu cuenta de **Administrador de WordPress** (estos datos son para entrar al panel `/wp-admin`, no los confundas con los de la base de datos).

---

## 6. Verificación y Checklist Final

Para asegurar que la instalación es plenamente funcional y cumple con los estándares de **Sistemas Microinformáticos y Redes**, el alumno debe comprobar:

* [ ] **Acceso Web:** ¿Carga el sitio al poner la IP? Si no carga, comprueba el **Security Group** de AWS (puerto 80 abierto).
* [ ] **Permisos de Escritura:** Intenta subir una imagen en `Medios > Añadir nuevo`. Si da error, revisa el comando `chown -R www-data:www-data`.
* [ ] **Enlaces Permanentes (Crítico):** Ve a `Ajustes > Enlaces permanentes`, selecciona **"Nombre de la entrada"** y guarda cambios. Navega por la web:
    * Si las páginas funcionan: El módulo `rewrite` y el `AllowOverride All` están **correctos**.
    * Si da Error 404: Revisa el archivo `000-default.conf` (Paso 4).
* [ ] **Seguridad:** ¿Has borrado el archivo `index.html` original de Apache para que no interfiera?



---
**Resultado esperado:** Al finalizar las 9 horas, el alumno debe disponer de un sitio WordPress donde pueda instalar temas (como Astra o GeneratePress) y crear contenido sin encontrar errores de permisos o de rutas.