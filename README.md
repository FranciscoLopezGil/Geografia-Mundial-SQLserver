# 🌍 World Database Project

Este proyecto contiene un modelo de base de datos relacional diseñado en SQL Server para almacenar información geopolítica y lingüística de los países del mundo.

## 📌 Estructura

La base de datos está compuesta por las siguientes tablas:

- **continents**: Lista de continentes, que contiene el ID y el nombre del continente.
- **countries**: Información sobre los países, incluyendo su nombre, población, y otros detalles relevantes.
- **capitals**: Información de las capitales de cada país.
- **languages**: Idiomas del mundo, con detalles como nombre y nombre nativo.
- **country_continents**: Relación entre países y continentes, indicando el continente principal de cada país.
- **country_languages**: Relación entre países e idiomas, especificando los idiomas hablados en cada país.


Además, incluye claves primarias y foráneas para mantener la integridad referencial.

## 🗺️ Diagrama Entidad-Relación
```
continents (continent_id PK, name)
        ▲
        │
country_continents (country_id PK, continent_id PK, is_primary)
        │
        ▼
countries (country_id PK, name, population, etc.)
   ▲             ▲
   │             │
capitals    country_languages (country_id PK, language_id PK, is_primary, percentage)
(country_id FK)           │
                          ▼
                     languages (language_id PK, name, native_name, etc.)
```
## 🚀 ¿Cómo usar?

1. Abrí SQL Server Management Studio.
2. Ejecutá el archivo `schema.sql` para crear las tablas.
3. Cargá datos de prueba con `sample_data.sql`.
4. Probá consultas con `queries_examples.sql`.

## 📄 Consultas de ejemplo

```sql
-- Obtener todos los países y sus capitales
SELECT c.name AS country, ca.name AS capital
FROM countries c
JOIN capitals ca ON c.country_id = ca.country_id;

-- Idiomas oficiales de Argentina
SELECT l.name
FROM languages l
JOIN country_languages cl ON l.language_id = cl.language_id
JOIN countries c ON c.country_id = cl.country_id
WHERE c.name = 'Argentina' AND cl.is_primary = 1;
