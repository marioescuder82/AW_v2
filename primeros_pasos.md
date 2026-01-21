# Manual de Gestión y Diseño: WordPress en Ubuntu Server (AWS)
**Asignatura:** Aplicaciones Web | **Perfil:** Administrador de Sistemas (SMR)

Este manual comienza una vez que el stack LAMP y WordPress han sido instalados correctamente en el servidor.

---

## 1. ¿Qué es WordPress? (Breve Introducción)

WordPress es un **CMS** (*Content Management System*) de código abierto. Básicamente, es una aplicación web que permite gestionar una base de datos de contenidos (textos, imágenes, usuarios) y presentarlos mediante una capa de diseño (temas).

Para un alumno de SMR, es importante entender que WordPress separa:
* **Contenido:** Guardado en la base de datos MySQL.
* **Funcionalidad:** Gestionada por el núcleo de WordPress y los *Plugins*.
* **Apariencia:** Controlada por los *Temas*.

**Acceso al panel de control:**
Para administrar el sitio, debes añadir `/wp-admin` a la IP de tu servidor:
`http://TU_IP_PUBLICA/wp-admin`



---

## 2. Instalación de Temas: El caso de Bootscore

Un **Tema** es una colección de archivos que definen la estructura visual. En esta práctica utilizaremos **Bootscore**, un tema que integra el framework **Bootstrap 5**, permitiendo crear webs modernas y totalmente *responsive* (adaptables a móviles).

### Pasos para instalar Bootscore:

1.  **Descarga el tema:** Ve a la web oficial de [bootscore.me](https://bootscore.me/) y descarga el archivo `.zip` del tema principal.
2.  **Sube el archivo:**
    * En el escritorio de WordPress, ve a **Apariencia > Temas**.
    * Haz clic en el botón superior **Añadir nuevo**.
    * Haz clic en **Subir tema**.
    * Selecciona el archivo `.zip` descargado e instala.
3.  **Activa el tema:** Una vez terminada la subida, pulsa en **Activar**.



> **Nota técnica (SMR):** Si al subir el archivo recibes un error de "El archivo excede el tamaño máximo", recuerda que el límite se configura en el servidor Ubuntu editando el archivo `/etc/php/8.x/apache2/php.ini` (parámetros `upload_max_filesize` y `post_max_size`).

---

## 3. Personalización del Sitio

WordPress dispone de una herramienta de edición en vivo llamada **Personalizador**.

### Cómo acceder:
Dirígete a **Apariencia > Personalizar**. Verás un menú a la izquierda y una vista previa de tu web a la derecha.



### Secciones clave para configurar:

* **Identidad del sitio:** Aquí cambias el nombre de la web, el eslogan y el **Favicon** (icono que aparece en la pestaña del navegador).
* **Menús:** Permite crear la navegación principal. Bootscore suele usar la posición "Primary Menu" para la parte superior.
* **Ajustes de la página de inicio:** Por defecto, WordPress muestra las últimas noticias (Blog). Cámbialo a "Una página estática" para que parezca una web corporativa.
* **CSS Adicional:** Esta es la sección más potente para un administrador. Permite añadir código CSS para cambiar colores o fuentes sin editar los archivos del servidor.

---

## 4. Ejercicio Práctico: CSS en Bootscore

Bootscore usa las clases estándar de Bootstrap. Si quieres cambiar el color de la barra de navegación desde el panel de personalización, añade esto en **CSS Adicional**:

```css
/* Cambiar el color de fondo de la cabecera */
.navbar {
    background-color: #2c3e50 !important;
}

/* Cambiar el color del texto del logo/marca */
.navbar-brand {
    color: #ffffff !important;
}