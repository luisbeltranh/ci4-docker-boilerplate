Markdown

# Boilerplate Docker + CodeIgniter 4 + Shield

Este es un boilerplate de desarrollo listo para usar que configura un entorno completo con Docker. Incluye Apache, PHP 8.1, MySQL 8.0, CodeIgniter 4, la librería de autenticación Shield y phpMyAdmin.

---
## ✨ Características

* ✅ **Entorno Dockerizado:** Todos los servicios corren en contenedores aislados orquestados con Docker Compose.
* ✅ **Servidor Web:** Apache, configurado para usar `public_html` como el directorio público.
* ✅ **PHP:** Versión 8.1 con las extensiones más comunes para CodeIgniter (`intl`, `mysqli`, `pdo_mysql`).
* ✅ **Base de Datos:** MySQL 8.0.
* ✅ **Framework:** CodeIgniter 4 en su última versión.
* ✅ **Autenticación:** Sistema de autenticación listo para usar con **CodeIgniter Shield**.
* ✅ **Gestor de Base de Datos:** Acceso visual a la base de datos a través de **phpMyAdmin**.

---
## 📋 Prerrequisitos

Antes de empezar, asegúrate de tener instalado en tu sistema:
* [Git](https://git-scm.com/)
* [Docker Desktop](https://www.docker.com/products/docker-desktop) (para Mac y Windows) o Docker Engine + Compose (para Linux).

---
## 🚀 Instalación y Puesta en Marcha

Sigue estos pasos para levantar el entorno de desarrollo.

### 1. Clonar el Repositorio
Clona este repositorio en tu máquina local y navega al nuevo directorio.

git clone [https://github.com/tu-usuario/tu-repositorio.git](https://github.com/tu-usuario/tu-repositorio.git) nuevo-proyecto
cd nuevo-proyecto

### 2. Configurar el Archivo de Entorno
Copia el archivo de entorno de ejemplo de CodeIgniter. Este archivo es ignorado por Git para proteger tus contraseñas y claves.

cp src/env src/.env
Luego, abre el archivo src/.env y configura las variables de la base de datos para que coincidan con las definidas en docker-compose.yml.

Ini, TOML

# src/.env

CI_ENVIRONMENT = development
app.baseURL = 'http://localhost'

# --- Database ---
database.default.hostname = mysql-db
database.default.database = mi_base_de_datos
database.default.username = mi_usuario
database.default.password = mi_contraseña
database.default.DBDriver = MySQLi

### 3. Construir y Levantar los Contenedores
Este comando construirá las imágenes personalizadas y pondrá en marcha todos los servicios en segundo plano.

docker-compose up -d --build

### 4. Instalar Dependencias de Composer
Ejecuta Composer dentro del contenedor para descargar CodeIgniter, Shield y todas las demás dependencias de PHP.

docker-compose exec php-apache composer install
### 5. Ejecutar las Migraciones
Este comando creará todas las tablas necesarias en la base de datos, incluyendo las del sistema de autenticación de Shield.

docker-compose exec php-apache php spark migrate
¡Listo! Tu entorno de desarrollo está completamente configurado y en funcionamiento.

💻 Uso del Entorno
🌐 Aplicación Web: http://localhost/

🗃️ Gestor de Base de Datos (phpMyAdmin): http://localhost:8081/

Para iniciar sesión en phpMyAdmin, usa las credenciales de la base de datos definidas en tu docker-compose.yml (mi_usuario, mi_contraseña).

🐳 Comandos Útiles de Docker
Iniciar el entorno:
docker-compose up -d

Detener el entorno:
docker-compose down

Verificar el estado de los contenedores:
docker-compose ps

Acceder a la terminal del contenedor de PHP/Apache (para usar php spark o composer):
docker-compose exec php-apache bash

Ver los logs (registros) en tiempo real:
docker-compose logs -f php-apache