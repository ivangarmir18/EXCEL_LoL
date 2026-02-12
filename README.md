
```markdown
# 🎮 LoL-MetaScraper: Competitive Intelligence Dashboard

![Python](https://img.shields.io/badge/Python-3.9%2B-blue?style=for-the-badge&logo=python) ![Selenium](https://img.shields.io/badge/Selenium-Web%20Scraping-43B02A?style=for-the-badge&logo=selenium) ![Google Sheets](https://img.shields.io/badge/Google%20Sheets-Live%20Dashboard-34A853?style=for-the-badge&logo=google-sheets) ![Status](https://img.shields.io/badge/Status-Meta%20Dependent-orange?style=for-the-badge)

## 📋 Descripción General

**LoL-MetaScraper** es un sistema automatizado de **Inteligencia Competitiva** para League of Legends. Su objetivo no es solo mostrar datos, sino actuar como un **Coach Virtual** que ayuda a tomar decisiones de *drafting* (selección de campeones) basadas en estadística pura y el meta actual.

El sistema funciona mediante una arquitectura híbrida: un **motor de scraping** en Python que extrae datos en tiempo real de webs de análisis (winrates, banrates, counters) y los inyecta en una **Hoja de Cálculo Maestra (Google Sheets)** donde se cruzan con criterios estratégicos personalizados (sinergias, dificultad, composición de equipo).

> **La Filosofía:** Los datos ganan partidas. Este sistema elimina la subjetividad ("creo que este campeón es bueno") y la reemplaza por evidencia ("este campeón tiene un 52% de WR y hace counter a su toplaner").

## 🏗 Arquitectura del Sistema

El flujo de datos está diseñado para que el usuario interactúe principalmente con el Excel, mientras el script trabaja en segundo plano.

```text
├── 📂 root
│   ├── 📜 update_lol_data.py    # Core: Script de Scraping (Selenium + BeautifulSoup)
│   ├── 📜 launcher.bat          # Ejecutable: Actualización en un clic
│   ├── 📜 credentials.json      # Seguridad: Llave de acceso a Google Cloud API
│   └── 📊 [Google Sheet]        # DASHBOARD: El cerebro real del sistema (Cloud)

```

## 🚀 Características Clave

### 1. Extracción de Datos en Tiempo Real (ETL)

* Utiliza **Selenium** para navegar dinámicamente y extraer datos frescos del parche actual.
* Resuelve automáticamente inconsistencias de nombres (ej. *Wukong* vs *MonkeyKing*) mediante un sistema de mapeo de `slugs`.

### 2. El Dashboard (Google Sheets) como UI

El script alimenta un Google Sheet diseñado específicamente para el análisis estratégico. El valor real reside en cómo se visualizan estos datos:

* **Cálculo de "Score" Compuesto:** No solo mira el Winrate. Combina Winrate + Counter Pick + Sinergia de equipo.
* **Filtrado por Roles:** Permite ver rápidamente qué *Support* es el mejor estadísticamente para tu *ADC*.
* **Detección de "OPs" Ocultos:** Cruza datos de *Low Pickrate* con *High Winrate* para encontrar joyas ocultas del meta.

### 3. Automatización Total

* Sin necesidad de tocar código. El usuario ejecuta `launcher.bat` y el sistema abre el navegador, actualiza la base de datos y cierra el proceso.

---

## 🛠️ Instalación y Configuración

### Prerrequisitos

* Python 3.8 o superior.
* Google Chrome instalado (para el WebDriver).

### 1. Clonar el Repositorio

```bash
git clone [https://github.com/tuusuario/lol-metascraper.git](https://github.com/tuusuario/lol-metascraper.git)
cd lol-metascraper

```

### 2. Instalación de Dependencias

El script gestiona sus librerías, pero puedes instalarlas manualmente:

```bash
pip install pandas selenium gspread oauth2client webdriver-manager beautifulsoup4

```

### 3. Configuración de Google Cloud (Credenciales)

El sistema necesita permiso para escribir en tu Hoja de Cálculo.

1. Obtén un archivo de credenciales JSON de una Service Account de Google Cloud.
2. **Renómbralo a `credentials.json**`.
3. Colócalo en la carpeta raíz del proyecto.

> **Nota:** Asegúrate de compartir tu Google Sheet con el email de la Service Account (ej: `bot@project-name.iam.gserviceaccount.com`) y darle permisos de "Editor".

---

## ⚡ Cómo Usar

1. **Ejecuta `launcher.bat**`: Verás una ventana de consola y el navegador abriéndose brevemente.
2. **Espera el mensaje de éxito**: El script procesará campeón por campeón.
3. **Abre tu Google Sheet**: Los datos en la pestaña "CRUDO" se habrán actualizado.
4. **Analiza en la pestaña "HOJA BUENA"**: Tus fórmulas y tablas dinámicas ahora reflejan el estado real del juego hoy.

---

## 📊 Lógica de Decisión

El sistema prioriza campeones basándose en la siguiente jerarquía de valor:

1. **Counter Directo:** ¿El campeón anula mecánicamente al rival?
2. **Winrate Global:** ¿El campeón está fuerte en el parche actual (>51%)?
3. **Sinergia:** ¿Encaja con la composición de mi equipo (ej. *Wombo Combo*)?

---

## ⚠️ Disclaimer

Este proyecto cumple con los términos de servicio de las APIs utilizadas y no inyecta código en el cliente del juego. Es una herramienta de análisis externa.
**League of Legends** es una marca registrada de Riot Games, Inc.

---

*Desarrollado por Iván García Miranda*

```

