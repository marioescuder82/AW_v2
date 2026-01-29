# Práctica de WordPress  
## Aplicaciones Web – SMR  
### Creación de la web de un centro educativo (Twenty Twenty-Five)

---

## 1. Objetivos de la sesión
Al finalizar la sesión, el alumnado será capaz de:

- Crear páginas y entradas en WordPress.
- Diferenciar entre contenido y diseño.
- Modificar plantillas en temas de bloques.
- Crear una barra lateral mediante bloques.
- Organizar la navegación de un sitio web educativo.

---

## 2. Contexto de la práctica
Vamos a crear una web similar en estructura y diseño a la del instituto:

https://portal.edu.gva.es/46022622/

---

## 3. Preparación inicial
1. Accede al panel de administración (`/wp-admin`).
2. Comprueba que el tema **Twenty Twenty-Five** está activo.
3. En **Ajustes → Generales**:
   - Título del sitio: *IES Ejemplo SMR*
   - Descripción corta: *Web del centro educativo*

---

## 4. Creación de la página Inicio y modificación de la plantilla

### 4.1 Crear la página Inicio
1. Ve a **Páginas → Añadir nueva**.
2. Título: **Inicio**.
3. No añadas contenido todavía.

---

### 4.2 Editar la plantilla de la página
1. En la barra lateral derecha, pulsa sobre **Plantilla**.
2. Selecciona **Editar plantilla**.
3. Acepta el aviso indicando que los cambios afectarán a todas las páginas que usen esta plantilla.

> **Nota didáctica:**  
> Las plantillas definen la estructura general del sitio (cabecera, columnas, pie).  
> El contenido de cada página se inserta dentro de esa estructura.

---

### 4.3 Crear una estructura con barra lateral
1. Dentro del editor de la plantilla, inserta un bloque **Columnas**.
2. Configura:
   - Columna izquierda: 25 %
   - Columna derecha: 75 %
3. La columna izquierda actuará como **barra lateral**.

---

### 4.4 Crear el “menú lateral” con bloques
En la columna izquierda:

1. Inserta un bloque **Encabezado** con el texto:
   - *Novedades*
2. Añade un bloque **Lista** o **Navegación**.
3. Crea enlaces a:
   - Matrícula (página)
   - Puertas abiertas (entrada)
   - Libros de texto (entrada)

> **Nota:**  
> En los temas de bloques, los widgets tradicionales se sustituyen por bloques dentro de las plantillas.

---

### 4.5 Guardar la plantilla
1. Guarda los cambios de la plantilla.
2. Vuelve al editor de la página **Inicio**.

---

## 5. Creación del resto de páginas
Crea las siguientes páginas como **páginas normales**, sin jerarquía:

- Centro  
- Gestiones  
- Matrícula  
- Oferta formativa  
- ESO  
- Bachillerato  
- Ciclos Formativos  
- Otros estudios  
- Blog  

Todas usarán automáticamente la plantilla modificada.

---

## 6. Configuración de la página de inicio estática
1. Accede a **Ajustes → Lectura**.
2. En *Tu página de inicio muestra*, selecciona **Una página estática**.
3. Configura:
   - Página de inicio: *Inicio*
   - Página de entradas: *Blog*
4. Guarda los cambios.

---

## 7. Creación de las entradas del Blog
Desde **Entradas → Añadir nueva**, crea:

- **Puertas abiertas**
- **Libros de texto**

Añade un texto breve simulando una noticia del centro.

---

## 8. Creación del menú superior
1. Ve a **Apariencia → Menús**.
2. Crea un menú llamado **Menú superior**.
3. Añade las páginas:
   - Inicio  
   - Centro  
   - Gestiones  
   - Oferta formativa  
   - Blog  

### Organización del menú
Organiza los elementos arrastrándolos:
- *Matrícula* dentro de *Gestiones*
- *ESO*, *Bachillerato*, *Ciclos Formativos* y *Otros estudios* dentro de *Oferta formativa*

Asigna el menú a la ubicación principal del tema.

---

## 9. Comprobación final
Verifica que:

- La página **Inicio** se muestra como página principal.
- Existe una barra lateral con accesos directos.
- El menú superior está correctamente organizado.
- El Blog muestra las entradas creadas.
- La navegación es clara y funcional.

---

## 10. Cierre de la sesión
Reflexión final:

- Diferencias entre páginas, entradas, menús y plantillas.
- Ventajas de los temas de bloques frente a los temas clásicos.
- Dificultades encontradas durante la práctica.

**Próxima sesión:**  
Personalización visual del sitio: colores, tipografías, imágenes y cabecera.
