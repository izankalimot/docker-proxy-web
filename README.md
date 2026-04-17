# 🚀 docker-proxy-hub

Este proyecto implementa una infraestructura web robusta y escalable utilizando **Docker Compose**. Cuenta con un servidor **Nginx** configurado como **Proxy Inverso**, encargado de realizar **Balanceo de Carga** (Round Robin) y gestión de **Caché de contenido estático** sobre dos servidores web en segundo plano.

---

## 🏗️ Arquitectura del Sistema

El sistema se compone de tres servicios principales:

1.  **Proxy (Nginx)**: Actúa como punto de entrada (puerto `8080`). Balancea el tráfico entre los servidores web y cachea las respuestas para mejorar el rendimiento.
2.  **web1 (Nginx Alpine)**: Servidor web de alta disponibilidad que sirve la cartelera de películas.
3.  **web2 (Nginx Alpine)**: Réplica del servidor web1 para escalabilidad y redundancia.

---

## 📋 Requisitos Previos

Asegúrate de tener instalado en tu sistema:
- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)
- [Git](https://git-scm.com/)

---

## 🚀 Instalación y Uso

### 1. Clonar el repositorio
Abre una terminal y clona este proyecto desde GitHub:

```bash
git clone https://github.com/[TU_USUARIO]/docker-proxy-hub.git
cd docker-proxy-hub
```

### 2. Desplegar los contenedores
Levanta la infraestructura completa con un solo comando:

```bash
docker compose up -d
```

### 3. Acceder a la Web
Una vez desplegado, abre tu navegador y accede a:
👉 `http://localhost:8080`

---

## 🛠️ Verificación de Funcionalidades

### ⚖️ Balanceo de Carga (Round Robin)
Para comprobar que el tráfico se reparte entre los dos servidores:
1. Abre una terminal y observa los logs: `docker compose logs -f web1 web2`
2. Refresca la web (usa `Ctrl + F5` para evitar el caché del navegador).
3. Verás en los logs cómo las peticiones se alternan entre `web1-1` y `web2-1`.

### ⚡ Caché de Contenido
Nginx está configurado para almacenar en caché las imágenes y archivos estáticos. Puedes verificarlo de dos formas:
- **Cabeceras HTTP**: Realiza una petición con `curl.exe -I http://localhost:8080`. Busca la cabecera `X-Proxy-Cache`.
    - `MISS`: El archivo no estaba en caché y se pidió al servidor.
    - `HIT`: El archivo se sirvió instantáneamente desde el caché del proxy.
- **Tiempos de respuesta**: Las segundas cargas de la página serán significativamente más rápidas.

---

## 📸 Documentación y Capturas
En la carpeta `/capturasdocumentacion` encontrarás:
- 📑 **PDF de verificación**: Explicación detallada de las pruebas realizadas.
- 🖼️ **Capturas de pantalla**: Evidencias visuales del balanceo de carga y el estado del caché.

---

## 🎞️ Créditos
Infraestructura diseñada y configurada por **Izan**, utilizando Docker, Nginx y una cuidada selección de clásicos del cine.
