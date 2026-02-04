# Manual de Prácticas: WordPress (Tema Twenty Twenty-Five)
**Módulo:** Aplicaciones Web (SMR)
**Tema Activo:** Twenty Twenty-Five (Full Site Editing)

Este manual guía al alumno a través de la configuración básica, edición y gestión de plugins en un entorno de WordPress moderno utilizando el editor del sitio.

---

## 1. Edición de Menús (Navegación)
En el tema *Twenty Twenty-Five*, los menús se gestionan desde el Editor del Sitio, no desde la antigua sección de "Apariencia > Menús".

1. Dirígete a **Apariencia > Editor**.
2. En el menú lateral, haz clic en **Navegación**.
3. Pulsa el icono del **lápiz (Editar)** para modificar el menú actual.
4. Para añadir un nuevo enlace:
   - Haz clic en el icono **(+)** dentro del bloque de navegación.
   - Escribe el nombre de la página que quieres enlazar o pega una URL.
5. **Importante:** Haz clic en **Guardar** (arriba a la derecha) dos veces para confirmar los cambios.

---

## 2. Crear una página con todas las entradas (Blog)
Configuración para que una página actúe como "feed" de noticias automático.

1. Ve a **Páginas > Añadir nueva**.
2. Titúlala **"Blog"** (o "Noticias") y **déjala vacía**. Publícala.
3. Ve a **Ajustes > Lectura**.
4. En la sección *Tu página de inicio muestra*, selecciona **Una página estática**.
   - **Portada:** (Tu página de inicio).
   - **Página de entradas:** Selecciona la página **"Blog"** que creaste.
5. Guarda los cambios.

---

## 3. Editor de código: Añadir Google Maps (iFrame)
Cómo insertar código HTML externo (iframe) manipulando el código fuente de una página.

1. Ve a **Google Maps**, busca una ubicación, pulsa "Compartir" > "Insertar un mapa" y copia el código HTML.
2. En WordPress, edita la página donde quieres el mapa.
3. Haz clic en los **tres puntos verticales (⋮)** en la esquina superior derecha de la pantalla.
4. Selecciona **Editor de código** (cambiarás de visual a código HTML puro).
5. Pega el código del iframe en la posición deseada.
6. Vuelve al menú de tres puntos y selecciona **Editor visual** para ver el resultado.

---

## 4. Personalizar CSS del Menú
Añadir estilos personalizados globales para cambiar la apariencia de los ítems de navegación.

1. Ve a **Apariencia > Editor**.
2. Haz clic en el icono de **Estilos** (el círculo dividido en blanco y negro arriba a la derecha).
3. Haz clic en los tres puntos **(⋮)** del panel de Estilos y elige **CSS adicional**.
4. Pega el siguiente código para poner un fondo gris claro a los elementos del menú:

```css
/* Estilo para items de navegación en Twenty Twenty-Five */
.wp-block-navigation-item {
    background-color: lightgray; /* Color de fondo */
    margin-right: 5px;           /* Separación entre botones */
    padding: 5px 10px;           /* Espacio interior */
    border-radius: 4px;          /* Bordes redondeados */
}
```

5. Guarda los cambios.

---

## 5. Instalación y Uso de Plugins

Para instalar cualquiera de los siguientes complementos, debes ir siempre a **Plugins > Añadir nuevo**, buscar el nombre exacto, hacer clic en **Instalar ahora** y posteriormente en **Activar**.

### A. WPFront Scroll Top
*Objetivo: Añadir una flecha flotante para que el usuario pueda volver arriba de la página automáticamente.*

1. Instala y activa el plugin **"WPFront Scroll Top"**.
2. Ve al menú de configuración en **Ajustes > Scroll Top**.
3. Marca la casilla **Enabled** (Habilitado).

4. Desplázate hasta el final de la página y haz clic en **Guardar cambios** (deja el resto de valores por defecto).
5. **Comprobación:** Abre tu página web, haz scroll hacia abajo y verifica que aparece el botón en la esquina inferior derecha.

### B. TablePress
*Objetivo: Crear tablas de datos fácilmente e insertarlas en cualquier página.*

1. Instala y activa el plugin **"TablePress"**.
2. En la barra lateral izquierda, haz clic en **TablePress > Añadir nueva tabla**.
3. Escribe el nombre de la tabla (ej. "Lista de Alumnos"), define el número de filas y columnas, y pulsa **Añadir tabla**.
4. Rellena las celdas con la información deseada.
5. Haz clic en **Guardar cambios**.
6. **Importante:** En la parte superior de esa misma pantalla, localiza el campo "Shortcode" (tendrá un aspecto como `[table id=1 /]`) y cópialo.

7. Ve a la página donde quieras mostrar la tabla y edítala.
8. Añade un bloque nuevo tipo **Shortcode** (o un Párrafo) y pega el código `[table id=1 /]`.
9. Actualiza la página para ver la tabla.

### C. All-in-One WP Migration
*Objetivo: Aprender a hacer copias de seguridad (Backup) y restaurar el sitio en caso de error.*

1. Instala y activa el plugin **"All-in-One WP Migration"**.

**Paso 1: Exportar la web (Copia de Seguridad)**
2. Ve a **All-in-One WP Migration > Exportar**.
3. Haz clic en el botón **Exportar a** y selecciona la opción **Archivo**.

4. El plugin empaquetará tu sitio. Cuando termine, haz clic en el botón verde parpadeante **Descargar** y guarda el archivo `.wpress` en tu ordenador.

**Paso 2: Simulación de desastre (Ejercicio)**
5. Ve a la sección **Páginas** de WordPress.
6. **Borra** algunas páginas que hayas creado (envíalas a la papelera y, opcionalmente, vacía la papelera). Ahora tu web está "rota" o incompleta.

**Paso 3: Restaurar la web**
7. Ve a **All-in-One WP Migration > Importar**.
8. Arrastra el archivo `.wpress` que descargaste en el paso 1 al recuadro de importación.
9. Aparecerá una advertencia indicando que **la base de datos y los archivos serán sobrescritos**. Haz clic en **Proceder**.
10. Al finalizar, haz clic en **Finalizar**.
    * *Nota:* Es muy probable que WordPress te cierre la sesión. Deberás entrar de nuevo con tu usuario y contraseña habituales.
    * *Resultado:* Las páginas que borraste habrán reaparecido.