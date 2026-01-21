# Manual de Instalación: WordPress en Ubuntu Server (AWS)
**Asignatura:** Aplicaciones Web | **Ciclo:** SMR

Este manual detalla los pasos para realizar una instalación mínima pero plenamente funcional de WordPress en una instancia EC2 de AWS.

---

## 1. Instalación del Stack LAMP
Actualizamos el sistema e instalamos Apache, MySQL y PHP con las extensiones necesarias para que WordPress pueda procesar imágenes y datos.

``````bash
sudo apt update
sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql php-gd php-xml php-mbstring -y

### 1.1 Activación del motor de reescritura (Rewrite)

Para que WordPress pueda generar URLs "limpias" o "amigables" (ej: `misitio.com/contacto` en lugar de `index.php?id=123`), debemos activar el módulo de reescritura de Apache. Sin este paso, la web solo funcionará en su página de inicio.

``````bash
sudo a2enmod rewrite