# Changelog

Todas las modificaciones notables de este proyecto serán documentadas en este archivo.

El formato está basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/)
y este proyecto se adhiere a [Semantic Versioning](https://semver.org/lang/es/).

---

## [1.1.0] - 2026-11-15

### Añadido
* **Integración del plugin PHP Weathermap**:
  * Instalación del plugin con volumen persistente dedicado (`librenms_weathermap_plugin`).
  * Enrutamiento de configuraciones de mapas hacia `/data/weathermap` en almacenamiento persistente.
  * Automatización mediante demonio `crond` interno con ejecución de sondeo (`map-poller.php`) cada 5 minutos (`LIBRENMS_WEATHERMAP=true`, `LIBRENMS_WEATHERMAP_SCHEDULE=*/5 * * * *`).
  * Activación del editor visual en `/plugins/Weathermap/editor.php` para diagramas jerárquicos estilo NOC.
* **Documentación**:
  * Actualización de `README.md` con la guía de uso del editor Weathermap.

---

## [1.0.0] - 2026-11-15

### Añadido
* **Stack Docker Compose**:
  * Servicio `librenms` (Web UI Nginx + PHP-FPM) expuesto en el puerto configurable 8000.
  * Servicio `dispatcher` (Python Poller/Discovery asíncrono y Master Scheduler).
  * Servicio `db` con MariaDB 10.11 optimizado (`utf8mb4`, `lower_case_table_names=0`).
  * Servicio `redis` (Redis 7) para colas de tareas de sondeo y caché distribuido.
* **Archivos de Configuración**:
  * `.env.example`: Plantilla de variables de entorno para despliegue seguro sin exponer credenciales.
  * `.gitignore`: Exclusión estricta de `.env`, volúmenes locales y archivos temporales.
  * `docker-compose.yml`: Definición estructurada de servicios, redes internas y volúmenes persistentes.
* **Documentación (`README.md`)**:
  * Guía paso a paso de despliegue en **Windows (Docker Desktop)**.
  * Guía paso a paso de despliegue en **VPS / Servidor Linux (Ubuntu/Debian)** con configuración de firewall UFW y recomendaciones de producción.
  * Sección explicativa detallada sobre la pantalla de validación (`validate.php`) en arquitecturas de microservicios Docker (diferenciación entre contenedor Web y contenedor Dispatcher).
  * Guía de configuración SNMP para equipamiento de ISP: **MikroTik RouterOS**, **ZTE OLT (C300/C320/C600)** y **V-SOL OLT (V1600 Series)**.
  * Justificación de convivencia y sinergia con **Zabbix** y **Prometheus + Grafana**.
  * Hoja de ruta para futuras integraciones (**Oxidized**, **Weathermap**, **Grafana**).
* **Licencia**:
  * Inclusión de licencia de código abierto MIT en `LICENSE`.

### Corregido
* Corrección en el nombre de la imagen oficial de LibreNMS (`librenms/librenms` en lugar de errores de sintaxis).
* Estandarización de nombres de servicios en `docker-compose.yml` (`librenms` como nombre de servicio unificado).
* Configuración de la variable `base_url` en la base de datos de LibreNMS para resolver la advertencia de URL no específica.
