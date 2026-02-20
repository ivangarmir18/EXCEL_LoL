# LoL-MetaScraper: Competitive Intelligence ETL & Scraper

## 📌 Descripción General

**LoL-MetaScraper** es un sistema automatizado de inteligencia competitiva basado en la extracción de datos en tiempo real (Web Scraping). Funciona como un motor de soporte analítico diseñado para optimizar la toma de decisiones mediante estadística pura (Winrates, Banrates, Sinergias y Counters).

El sistema extrae, normaliza e inyecta métricas dinámicas directamente en una base de datos en la nube (Google Sheets), que actúa como cerebro estratégico del usuario final.

> **🤖 Nota sobre el desarrollo asistido por IA:**
> La concepción del proyecto, el diseño de la arquitectura ETL, la lógica de normalización de datos y el flujo de trabajo (desde la extracción hasta el volcado en Sheets) son de mi autoría. Para la redacción de la sintaxis pura de Python y la construcción ágil de la interfaz gráfica, me he apoyado en Inteligencia Artificial. Mi rol en este proyecto es el de **Arquitecto de Software y Datos**, enfocándome en resolver el problema y estructurar la solución algorítmica de forma eficiente.

## ⚙️ Arquitectura del Sistema (ETL & GUI)

El proyecto utiliza una arquitectura de procesamiento en segundo plano con interfaz gráfica asíncrona:

### 1. Interfaz Gráfica (GUI) y Concurrencia
* **Dashboard Tkinter:** Interfaz de usuario completa con visor de métricas en tiempo real (`Treeview`), barra de progreso y consola de *logs*.
* **Procesamiento Asíncrono:** Uso de `threading` y `queue` para aislar el proceso pesado de *scraping* del hilo principal de la interfaz, garantizando una experiencia de usuario fluida sin cuelgues.

### 2. Extract (Web Scraping Híbrido)
* **Motor Selenium Optimizado:** Configuración del WebDriver con argumentos *anti-bot* (`AutomationControlled`) y bloqueo de carga de imágenes para maximizar la velocidad de respuesta.
* **Parseo HTML con BeautifulSoup:** Una vez que Selenium resuelve el DOM, BeautifulSoup extrae eficientemente las tablas de *counters* y *winrates*.
* **Manejo de Excepciones Dinámico:** Lógica de reintentos y mapeo predictivo de URLs (`SLUG_MAPPING`) para campeones con nomenclaturas irregulares.

### 3. Transform (Data Cleaning)
* **Normalización de Strings:** Estandarización de nombres extraídos de la web (limpieza de caracteres especiales y espacios) para que coincidan unívocamente con la nomenclatura de la base de datos de destino (`OUTPUT_NORMALIZATION`).

### 4. Load (Google Sheets API)
* **Integración con GSpread:** Conexión mediante Service Accounts de Google Cloud (`credentials.json`) para lectura y escritura masiva mediante Pandas DataFrame.
* **Auto-Backup de Seguridad:** El sistema clona automáticamente la hoja de destino en la nube (`worksheet.duplicate`) creando un respaldo con *timestamp* antes de sobrescribir cualquier dato en producción.

## 🛠️ Stack Tecnológico
* **Lenguaje:** Python 3.8+
* **Frontend:** `tkinter`, `ttk`
* **Scraping:** `selenium`, `webdriver_manager`, `beautifulsoup4`
* **Procesamiento y API:** `pandas`, `gspread`
* **Concurrencia:** `threading`, `queue`

## 🚀 Instalación y Despliegue

1. Clonar el repositorio.
2. Asegurar la instalación de las dependencias requeridas (ver `requirements.txt`).
3. **Configuración de Google Cloud (CRÍTICO):**
   * Obtener el archivo JSON de credenciales de una Service Account (Google Cloud Platform).
   * Renombrarlo a `credentials.json` y ubicarlo en la raíz del proyecto.
   * Otorgar permisos de "Editor" en el Google Sheet al email de la Service Account.
4. Ejecutar el proyecto mediante el archivo `launcher.bat` (que automatiza el inicio) o lanzando `python update_lol_data.py`.

---
*Desarrollado por Iván García Miranda.*
