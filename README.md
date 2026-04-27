<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=32&duration=3000&pause=1000&color=1F3864&center=true&vCenter=true&width=700&lines=SQL+Dictionary+Architect;Documenta+tu+BD+en+segundos;Potenciado+con+IA+%F0%9F%A4%96" alt="Typing SVG" />

<br/>

![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)
![CustomTkinter](https://img.shields.io/badge/CustomTkinter-UI-blue?style=for-the-badge&logo=python&logoColor=white)
![Groq](https://img.shields.io/badge/Groq-LLaMA%203.3-orange?style=for-the-badge&logo=groq&logoColor=white)
![Excel](https://img.shields.io/badge/Output-Excel%20.xlsx-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)
![License](https://img.shields.io/badge/Licencia-MIT-green?style=for-the-badge)

<br/>

> **Genera diccionarios de datos profesionales en Excel** desde una base de datos en vivo o desde archivos SQL, enriquecidos automáticamente con inteligencia artificial (Groq · LLaMA 3.3).

</div>

---

## ✨ ¿Qué hace este proyecto?

**SQL Dictionary Architect** es una aplicación de escritorio con interfaz gráfica que automatiza por completo la documentación de bases de datos relacionales. Conecta a tu BD (o carga un archivo `.sql`), presiona un botón, y obtienes un archivo Excel prolijo con:

- 📋 **Una hoja por tabla** — nombre físico, PK, FK, columnas, tipos de dato y descripciones
- 📑 **Hoja ÍNDICE** — listado general de todas las tablas con su descripción
- 🔗 **Hoja de Relaciones** — relaciones entre tablas (1:1, 1:N, N:M) generadas por IA
- 📊 **Hoja de Índices** — índices recomendados para optimizar consultas, generados por IA

---

## 🗂️ Estructura del proyecto

```
extractor.py
│
├── GroqEnricher        # Llama a la API de Groq (LLaMA 3.3) para documentar tablas y generar relaciones
├── SQLFileParser       # Parsea archivos .sql / backups y extrae la estructura DDL
├── ExcelGenerator      # Crea y formatea el archivo Excel de salida
└── DataDictApp         # Interfaz gráfica principal (CustomTkinter)
```

---

## 🚀 Flujo de funcionamiento

```
┌──────────────────────────────────────────────────────────────┐
│                   SQL Dictionary Architect                   │
└──────────────────┬───────────────────────────────────────────┘
                   │
        ┌──────────▼──────────┐
        │  ¿Fuente de datos?  │
        └──────────┬──────────┘
                   │
       ┌───────────┴───────────┐
       │                       │
┌──────▼──────┐         ┌──────▼──────┐
│  Conexión   │         │  Archivo    │
│  a BD viva  │         │  .sql /     │
│  (SQLAlch.) │         │  .backup    │
└──────┬──────┘         └──────┬──────┘
       │                       │
       └──────────┬────────────┘
                  │
        ┌─────────▼──────────┐
        │  Extracción de     │
        │  tablas, PK y FK   │
        └─────────┬──────────┘
                  │
        ┌─────────▼──────────┐        ┌─────────────────────┐
        │  ¿IA activada?     │──Sí───▶│  Groq · LLaMA 3.3   │
        └─────────┬──────────┘        │  - Descripción tabla │
                  │ No                │  - Nombre lógico col.│
                  │                   │  - Claves únicas     │
                  │                   │  - Observaciones     │
                  │◀──────────────────│  - Relaciones        │
                  │                   │  - Índices           │
                  │                   └─────────────────────┘
        ┌─────────▼──────────┐
        │  Generación Excel  │
        │  (openpyxl)        │
        └─────────┬──────────┘
                  │
        ┌─────────▼──────────┐
        │  📁 diccionario    │
        │     .xlsx listo    │
        └────────────────────┘
```

---

## 🎨 Formato del Excel generado

El Excel utiliza un sistema de colores para identificar el rol de cada columna de un vistazo:

| Color | Significado |
|:---:|---|
| 🟦 Azul oscuro (`#1F3864`) | Encabezado de sección |
| 🟨 Amarillo (`#FFF2CC`) | Clave Primaria — **PK** |
| 🟩 Verde (`#E2EFDA`) | Clave Foránea — **FK** |
| 🟧 Naranja (`#FCE4D6`) | PK y FK simultáneamente — **PK/FK** |
| 🟦 Azul claro (`#D9E1F2`) | Etiqueta de metadato |

---

## ⚙️ Motores de base de datos soportados

| Motor | Puerto por defecto | Driver SQLAlchemy |
|---|:---:|---|
| **PostgreSQL** | 5432 | `postgresql+psycopg2` |
| **MySQL** | 3306 | `mysql+pymysql` |
| **MariaDB** | 3306 | `mysql+pymysql` |
| **Oracle Database** | 1521 | `oracle+cx_oracle` |

> También soporta archivos `.sql`, `.backup` y `.dump` de PostgreSQL, MySQL y MariaDB.

---

## 📦 Instalación

**1. Clona el repositorio**
```bash
git clone https://github.com/tu-usuario/sql-dictionary-architect.git
cd sql-dictionary-architect
```

**2. Instala las dependencias**
```bash
pip install customtkinter openpyxl sqlalchemy groq
```

> Dependencias adicionales según tu motor de BD:
> ```bash
> pip install psycopg2-binary   # PostgreSQL
> pip install pymysql           # MySQL / MariaDB
> pip install cx_Oracle         # Oracle
> ```

**3. Ejecuta la aplicación**
```bash
python extractor.py
```

---

## 🤖 Configuración de IA (Groq)

El enriquecimiento con IA es **opcional**. Si lo activas, necesitas una API Key gratuita de Groq:

1. Regístrate en [console.groq.com](https://console.groq.com)
2. Genera una API Key (`gsk_...`)
3. En la aplicación, activa el switch **"Activar IA"** e ingresa tu key

El modelo utilizado es **`llama-3.3-70b-versatile`**. Para cambiar a otro modelo en el futuro, edita la constante en `GroqEnricher`:

```python
class GroqEnricher:
    MODEL = "llama-3.3-70b-versatile"  # ← cambia aquí
```

---

## 🗺️ FIXED_MAPS — Nombres predefinidos

Para columnas de nomenclatura estándar en tu organización (como campos de auditoría), puedes pre-definir su nombre lógico y descripción en el diccionario `FIXED_MAPS`, evitando que la IA las procese innecesariamente:

```python
FIXED_MAPS = {
    "created_at": ("Fecha Creación", "Fecha y hora de creación del registro. DEFAULT NOW()."),
    "audit_ip":   ("Dirección IP",   "IP del terminal del operador."),
    # Añade tus propias columnas aquí...
}
```

---

## 📁 Archivos de salida

El archivo Excel generado contiene las siguientes hojas:

```
📊 diccionario.xlsx
├── ÍNDICE                    ← Listado general de todas las tablas
├── NOMBRE_TABLA_1            ← Detalle de columnas, PK, FK y metadatos
├── NOMBRE_TABLA_2
├── ...
├── RELACIONES ENTRE TABLAS   ← Generado por IA
└── ÍNDICES DE LA BASE DE DATOS ← Generado por IA
```

---

## 🛠️ Tecnologías utilizadas

| Librería | Uso |
|---|---|
| `customtkinter` | Interfaz gráfica moderna |
| `openpyxl` | Generación y formato del archivo Excel |
| `sqlalchemy` | Conexión e inspección de bases de datos |
| `groq` | Cliente oficial de la API de Groq (IA) |
| `re` / `json` | Parseo de archivos SQL y respuestas JSON |
| `threading` | Procesamiento en segundo plano sin congelar la UI |

---

## 📄 Licencia

Este proyecto está bajo la licencia **MIT**. Consulta el archivo `LICENSE` para más detalles.

---

<div align="center">

Hecho por **Smit BZ** · 2026

</div>
