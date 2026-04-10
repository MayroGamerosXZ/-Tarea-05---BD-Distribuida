# 🚕 MoveFast - Sistema Distribuido de Viajes Compartidos

MoveFast es una simulación de arquitectura de software a nivel empresarial inspirada en el backend de plataformas como Uber. Este proyecto demuestra la implementación práctica de microservicios, enrutamiento geográfico, particionamiento de bases de datos (Sharding) y tolerancia a particiones de red (Teorema CAP).

## 🚀 Características Principales

* **Sharding Geográfico Lógico:** La base de datos (SQL Server) segmenta las transacciones por código de país (`GT`, `MX`, `US`) aislando la carga de trabajo regional.
* **API Gateway Inteligente:** Construido con FastAPI, actúa como enrutador principal y evalúa la disponibilidad de los nodos antes de procesar una transacción.
* **Tolerancia a Fallos (Teorema CAP):** Prioriza la Consistencia y Tolerancia a Particiones (CP). Si un nodo geográfico cae, la API rechaza peticiones locales con un HTTP 503 (Service Unavailable) para evitar corrupción de datos, mientras el resto del mundo sigue operando.
* **Interfaz Asíncrona:** Una aplicación de escritorio cliente nativa construida en Python (CustomTkinter) que se comunica fluidamente con el backend mediante hilos (threading) para evitar bloqueos en la UI.

## 🛠️ Tecnologías Utilizadas

* **Frontend:** Python 3, CustomTkinter, Requests.
* **Backend / API:** Python 3, FastAPI, Uvicorn, PyODBC.
* **Base de Datos:** Microsoft SQL Server 2022.
* **Infraestructura:** Docker & Docker Compose.

---

## ⚙️ Requisitos Previos

Antes de ejecutar el proyecto, asegúrate de tener instalado en tu sistema:
1. [Docker Desktop](https://www.docker.com/products/docker-desktop/) (Corriendo en segundo plano).
2. [Python 3.10+](https://www.python.org/downloads/).
3. Controladores ODBC 18 para SQL Server (Para la conexión de Python a la BD).

---

## 🏃‍♂️ Instrucciones de Instalación y Ejecución

### 1. Levantar el Backend (Docker)
Clona este repositorio, abre una terminal en la carpeta raíz del proyecto y ejecuta:
```bash
docker-compose up --build -d
```

### 2. Configurar la Base de Datos
Abre SQL Server Management Studio (SSMS) o Azure Data Studio.

Conéctate a localhost,1433 con el usuario sa y la contraseña configurada en tu docker-compose.yml.

Ejecuta el Mega Script Maestro (incluido en la carpeta /sql) para crear la base de datos movefast, las tablas transaccionales e insertar los usuarios de prueba.

### 3. Iniciar la Interfaz de Usuario (Cliente)
Abre una nueva terminal en tu computadora (fuera de Docker), instala las dependencias de Python y ejecuta la aplicación:

Bash
```
pip install customtkinter requests
python app_cliente.py
```
