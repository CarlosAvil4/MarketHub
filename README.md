# MarketHub – Data Engineering Project

**End-to-end Data Engineering pipeline | Python · Pandas · SQL · SQLite · Power BI**

---

# Español

## Descripción del proyecto

MarketHub es un proyecto personal de Data Engineering enfocado en el diseño y desarrollo de un pipeline de datos de extremo a extremo, desde la extracción de información mediante una API hasta su transformación, almacenamiento y consumo analítico.

El proyecto utiliza datos de productos, usuarios y carritos de compra obtenidos de [DummyJSON](https://dummyjson.com/), simulando el escenario de un marketplace.

El objetivo principal es construir una arquitectura de datos organizada, implementar procesos ETL, garantizar la calidad de los datos y preparar un modelo analítico que permita obtener información relevante para el negocio.

## Arquitectura

El proyecto sigue una arquitectura Medallion:

**API → Bronze → Silver → Gold → SQLite → Power BI**

### 1. Bronze – Raw Data

- Extracción de información desde DummyJSON API.
- Implementación de solicitudes HTTP y paginación.
- Almacenamiento de las respuestas originales en formato JSON.
- Conservación de los datos de origen para su posterior procesamiento.

### 2. Silver – Cleaned and Transformed Data

- Transformación de los datos utilizando Python y Pandas.
- Limpieza y normalización de estructuras.
- Separación de entidades y relaciones en diferentes tablas.
- Validación de registros, claves, duplicados y valores inconsistentes.
- Almacenamiento en formato Parquet.

### 3. Gold – Analytical Data Model

- Construcción de un modelo dimensional orientado al análisis.
- Implementación de tablas de hechos y dimensiones.
- Definición de relaciones entre entidades.
- Validación de claves primarias y foráneas.
- Preparación de tablas analíticas para consultas y visualización.

### 4. Data Storage and Analytics

- Persistencia de las tablas Gold en SQLite.
- Consultas SQL para validar y analizar los datos.
- Conexión de la base de datos con Power BI.
- Construcción del modelo semántico y desarrollo de indicadores mediante DAX.

## Tecnologías utilizadas

| Tecnología | Aplicación |
|---|---|
| Python | Extracción y transformación de datos |
| Pandas | Manipulación y procesamiento de datos |
| Requests | Consumo de API REST |
| SQL | Consultas y análisis de datos |
| SQLite | Almacenamiento relacional |
| Parquet | Almacenamiento de datos procesados |
| Jupyter Notebook | Desarrollo y documentación del pipeline |
| Power BI | Modelado semántico y visualización |
| DAX | Desarrollo de medidas analíticas |
| Git & GitHub | Control de versiones |

## Modelo de datos Gold

El modelo analítico contiene ocho tablas:

**Tablas de hechos**
- `fact_cart_items`
- `fact_carts`
- `fact_product_reviews`

**Dimensiones**
- `dim_product`
- `dim_user`
- `dim_reviewer`
- `dim_date`

**Tabla puente**
- `bridge_product_tags`

El modelo permite analizar información desde diferentes perspectivas, incluyendo productos, categorías, usuarios, carritos y reseñas.

## Calidad de datos

Durante el desarrollo se implementaron validaciones para garantizar la consistencia del modelo:

- Identificación de registros duplicados.
- Validación de claves primarias y foráneas.
- Detección de valores nulos.
- Verificación de integridad referencial.
- Validación de importes, descuentos y cantidades.
- Reconciliación entre los totales de los carritos y sus líneas de detalle.

## Estructura del proyecto

```text
MarketHub/
│
├── data/
│   ├── bronze/
│   ├── silver/
│   ├── gold/
│   └── database/
│       └── markethub.db
│
├── notebooks/
│   ├── 01_extract.ipynb
│   ├── 02_transform_silver.ipynb
│   └── 03_build_gold.ipynb
│
├── logs/
├── sql/
├── src/
│
├── .gitignore
└── README.md
```

## Convenciones y consideraciones

- Los datos proceden de DummyJSON y son datos sintéticos.
- Para los análisis del proyecto, los carritos se interpretan como transacciones completadas dentro de un escenario simulado de marketplace.
- Se utiliza USD como convención monetaria para los análisis.
- Estas dos últimas decisiones son supuestos del proyecto y no afirmaciones sobre el comportamiento real de la API.
- Los datos personales y financieros presentes en la fuente no forman parte del modelo analítico Gold.

## Objetivos de aprendizaje

Este proyecto busca desarrollar y demostrar conocimientos en:

- Construcción de pipelines ETL.
- Ingestión de datos desde APIs REST.
- Procesamiento y transformación con Python.
- Modelado dimensional y arquitectura de datos.
- Calidad e integridad de datos.
- Consultas SQL.
- Almacenamiento estructurado.
- Integración de datos con herramientas de Business Intelligence.

## Estado del proyecto

**En desarrollo.**

El pipeline local Bronze, Silver y Gold está implementado. Las tablas analíticas están almacenadas en SQLite y se ha iniciado la integración con Power BI.

Como evolución futura se contempla explorar Microsoft Fabric, automatización y orquestación de pipelines, y mejoras en la arquitectura de procesamiento.

---

# English

## Project Overview

MarketHub is a personal Data Engineering project focused on designing and developing an end-to-end data pipeline, covering data extraction, transformation, storage, and analytical consumption.

The project uses product, user, and shopping cart data retrieved from [DummyJSON](https://dummyjson.com/), simulating a marketplace environment.

Its main objective is to build a structured data architecture, implement ETL processes, ensure data quality, and prepare an analytical model to support business insights.

## Architecture

The project follows a Medallion Architecture:

**API → Bronze → Silver → Gold → SQLite → Power BI**

### 1. Bronze – Raw Data

- Data extraction from the DummyJSON API.
- HTTP requests and pagination handling.
- Storage of original API responses in JSON format.
- Preservation of source data for further processing.

### 2. Silver – Cleaned and Transformed Data

- Data transformation using Python and Pandas.
- Data cleaning and structural normalization.
- Separation of entities and relationships into individual tables.
- Validation of records, keys, duplicates, and inconsistent values.
- Storage in Parquet format.

### 3. Gold – Analytical Data Model

- Development of a dimensional model for analytical purposes.
- Implementation of fact and dimension tables.
- Definition of relationships between entities.
- Primary and foreign key validation.
- Preparation of analytical datasets for querying and visualization.

### 4. Data Storage and Analytics

- Persistence of Gold tables in SQLite.
- SQL queries for data validation and analysis.
- Database integration with Power BI.
- Development of a semantic model and analytical measures using DAX.

## Technology Stack

| Technology | Purpose |
|---|---|
| Python | Data extraction and transformation |
| Pandas | Data manipulation and processing |
| Requests | REST API consumption |
| SQL | Data querying and analysis |
| SQLite | Relational data storage |
| Parquet | Processed data storage |
| Jupyter Notebook | Pipeline development and documentation |
| Power BI | Semantic modeling and visualization |
| DAX | Analytical measure development |
| Git & GitHub | Version control |

## Gold Data Model

The analytical model consists of eight tables:

**Fact Tables**
- `fact_cart_items`
- `fact_carts`
- `fact_product_reviews`

**Dimensions**
- `dim_product`
- `dim_user`
- `dim_reviewer`
- `dim_date`

**Bridge Table**
- `bridge_product_tags`

This model supports analysis across different business perspectives, including products, categories, users, shopping carts, and reviews.

## Data Quality

Several validation processes were implemented to ensure data consistency:

- Duplicate record detection.
- Primary and foreign key validation.
- Null value detection.
- Referential integrity checks.
- Amount, discount, and quantity validation.
- Reconciliation between shopping cart totals and their corresponding line items.

## Project Structure

```text
MarketHub/
│
├── data/
│   ├── bronze/
│   ├── silver/
│   ├── gold/
│   └── database/
│       └── markethub.db
│
├── notebooks/
│   ├── 01_extract.ipynb
│   ├── 02_transform_silver.ipynb
│   └── 03_build_gold.ipynb
│
├── logs/
├── sql/
├── src/
│
├── .gitignore
└── README.md
```

## Assumptions and Considerations

- Data is sourced from DummyJSON and is synthetic.
- For project analysis, shopping carts are interpreted as completed transactions within a simulated marketplace scenario.
- USD is used as the project's monetary convention.
- These two decisions are project assumptions and are not claims about the API's actual business semantics.
- Personal and financial information from the source is excluded from the Gold analytical model.

## Learning Objectives

This project aims to develop and demonstrate skills in:

- ETL pipeline development.
- REST API data ingestion.
- Python-based data processing and transformation.
- Dimensional modeling and data architecture.
- Data quality and integrity.
- SQL querying.
- Structured data storage.
- Data integration with Business Intelligence tools.

## Project Status

**In progress.**

The local Bronze, Silver, and Gold pipeline has been implemented. Analytical tables are stored in SQLite, and Power BI integration has started.

Future improvements include exploring Microsoft Fabric, pipeline automation and orchestration, and enhancements to the data processing architecture.
