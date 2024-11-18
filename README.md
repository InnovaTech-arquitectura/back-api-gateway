# Configuración de Kong en Modo Declarativo y Configuración Multi-Nodo

Este proyecto configura **Kong API Gateway** en modo declarativo con una configuración multi-nodo, junto con monitoreo adicional mediante **cAdvisor**.

## Contenido
- [Descripción General](#descripción-general)
- [Requisitos Previos](#requisitos-previos)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Servicios y Rutas en Kong](#servicios-y-rutas-en-kong)
- [Configuración Multi-Nodo](#configuración-multi-nodo)
- [Monitoreo con cAdvisor](#monitoreo-con-cadvisor)
- [Instrucciones de Uso](#instrucciones-de-uso)
- [Notas Importantes sobre Entornos](#notas-importantes-sobre-entornos)
- [Resolución de Problemas](#resolución-de-problemas)

## Descripción General

La configuración incluye:
- **Kong API Gateway** en modo declarativo.
- **Nodos Múltiples de Kong** para balanceo de carga y redundancia.
- **cAdvisor** para monitorear métricas de los contenedores.

La configuración declarativa se define en el archivo `kong.yml`, que incluye servicios, rutas, plugins y consumidores.

## Requisitos Previos

Antes de desplegar esta configuración, asegúrate de tener:
- Docker y Docker Compose instalados.
- Los puertos `8000`, `8001`, `8002`, `8003` y `8085` disponibles en tu máquina anfitriona.

## Estructura del Proyecto
├── docker-compose.yml # Configuración de Docker Compose 
├── kong.yml # Configuración declarativa para Kong 
└── README.md # Documentación (este archivo)


## Servicios y Rutas en Kong

El archivo `kong.yml` incluye:
- **Plugins**: Configuración de los plugins `file-log`, `cors` y `prometheus`.
- **Consumidores**: Gestión de consumidores con autenticación JWT.
- **Servicios y Rutas**:
  - Configuración de múltiples APIs para `users-api`, `inventory-api`, `support-api` y `ecommerce-api`.
  - Soporte para métodos GET, POST, PUT, PATCH, DELETE y OPTIONS con rutas basadas en expresiones regulares.

## Configuración Multi-Nodo

El entorno incluye:
- **Nodo 1**: Proxy en el puerto `8000`, API de Administración en el puerto `8001`.
- **Nodo 2**: Proxy en el puerto `8002`, API de Administración en el puerto `8003`.

Ambos nodos comparten la configuración declarativa definida en `kong.yml`.

## Monitoreo con cAdvisor

`cAdvisor` permite monitorear el uso de recursos de los contenedores y está disponible en el puerto `8085`.

## Instrucciones de Uso

1. **Clonar el Repositorio**:
   ```bash
   git clone <url-del-repositorio>
   cd <carpeta-del-repositorio>
   docker-compose up --build
   ```

Acceder a los Nodos de Kong:

Proxy (Nodo 1): http://localhost:8000
API de Administración (Nodo 1): http://localhost:8001
Proxy (Nodo 2): http://localhost:8002
API de Administración (Nodo 2): http://localhost:8003
Monitorear con cAdvisor:

Abre http://localhost:8085 en un navegador.
Probar el Gateway: Usa herramientas como curl o Postman para interactuar con los servicios y rutas configurados.

Notas Importantes sobre Entornos
El archivo kong.yml incluye las direcciones IP de los servicios configurados. Estas IPs deben ser actualizadas dependiendo del entorno de despliegue (producción, pruebas, desarrollo).


