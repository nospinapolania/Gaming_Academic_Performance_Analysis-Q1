<div align="center">

<img src="assets/header_banner.svg" alt="Gaming Academic Performance Dashboard" width="100%"/>

# Gaming Academic Performance - Student Behavior Intelligence

**Analisis SQL de habitos de gaming, estudio, descanso y rendimiento academico**  
*Proyecto finalizado: Power Query - Excel - MySQL - SQL Analytics - Power BI*

<br/>

[![Power Query](https://img.shields.io/badge/Power%20Query-ETL%20Cleaning-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)](https://powerquery.microsoft.com/)
[![SQL](https://img.shields.io/badge/SQL-MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://www.mysql.com/)
[![DAX](https://img.shields.io/badge/DAX-Power%20BI%20Measures-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://learn.microsoft.com/power-bi/transform-model/desktop-quickstart-learn-dax-basics)
[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard%20Interactivo-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)

<br/>

**Languages / Query Languages:** SQL · DAX · Power Query M

<br/>

> "No todas las horas de pantalla pesan igual: el valor analitico esta en entender cuando el gaming compite con el estudio, el sueño y la asistencia."

</div>

---

## Contexto del Proyecto

Una institucion academica quiere entender como los habitos digitales de sus estudiantes se relacionan con el rendimiento. El dataset combina horas de gaming, horas de estudio, sueño, asistencia, uso de dispositivos, tiempo de reaccion, nivel de estres y calificaciones.

El proyecto transforma un CSV crudo en un flujo analitico reproducible: limpieza en Power Query, dataset final en Excel, consultas SQL reutilizables en MySQL y un dashboard interactivo de cuatro paginas en Power BI para explorar gaming, estudio y rendimiento academico.

---

## Como se divide el proyecto

Este repositorio presenta un caso completo de portafolio con sus dos fases finalizadas:

| Fase | Entregable | Estado | Enfoque |
|------|------------|--------|---------|
| **Proyecto 1** | SQL Analytics | Finalizado | Consultas, KPIs, segmentacion, correlaciones y vistas |
| **Proyecto 2** | Dashboard Power BI | Finalizado | Medidas DAX, cuatro paginas, filtros y navegacion |

El **Proyecto 1** no es otro repositorio separado. Es la parte SQL de este mismo caso: el archivo `SQL/gaming_academic_queries.sql`, apoyado por el dataset limpio, el diccionario de datos y esta documentacion.

El **Proyecto 2** utiliza las vistas SQL mediante una conexion ODBC e incluye medidas DAX, filtros y botones de navegacion entre las cuatro paginas. El alcance de esta entrega se da por cerrado.

---

## Dashboard en Power BI - Proyecto 2

| Pagina | Nombre | Pregunta que responde |
|--------|--------|-----------------------|
| **P1** | Executive | ¿Cómo se distribuye el rendimiento academico general? |
| **P2** | Trade-Off | ¿Cómo se relacionan las bandas de gaming y estudio con las notas, el riesgo y la excelencia? |
| **P3** | Behavior | ¿Cómo varia el rendimiento segun sueño, estres y tiempo de reaccion? |
| **P4** | Risk | ¿Cómo se distribuyen los segmentos y el riesgo academico segun asistencia y estudio? |

<br/>

<div align="center">
<img src="assets/dashboard_executive.png" alt="Captura real de la pagina Executive del dashboard en Power BI" width="100%"/>
<br/><sub><i>Captura real de la pagina Executive en Power BI: indicadores, habitos de gaming y estudio, correlaciones y segmentos de riesgo.</i></sub>
</div>

---

## Arquitectura

```text
FUENTE DE DATOS
   data/gaming_academic_performance.csv
   8,000 estudiantes - 14 variables originales
           |
           v
LIMPIEZA / TRANSFORMACION
   Power Query
   PowerQuery/gaming_academic_cleaning.pq
   - normalizacion de texto
   - correccion de valores fuera de rango
   - columnas derivadas para segmentacion
           |
           v
DATASET FINAL
   data/Desempeño_académico_limpio.xlsx
   8,000 estudiantes - 19 columnas limpias
           |
           v
ALMACENAMIENTO ANALITICO
   MySQL
   SQL/gaming_academic_queries.sql
   - 14 queries analiticas
   - 3 vistas para Power BI
           |
           v
VISUALIZACION
   Power BI / Excel
   - KPIs
   - segmentos
   - ranking
   - correlaciones
```

<br/>

<div align="center">
<img src="assets/project_workflow.svg" alt="Project Analytics Workflow" width="90%"/>
<br/><sub><i>Flujo del proyecto: CSV original, limpieza en Power Query, dataset limpio, SQL Analytics y dashboard en Power BI.</i></sub>
</div>


---

## Datos

Esta seccion resume los dos archivos de datos usados en el proyecto.

| Archivo | Descripcion | Filas | Columnas |
|---------|-------------|------:|---------:|
| `data/gaming_academic_performance.csv` | Dataset original sin transformar | 8,000 | 14 |
| `data/Desempeño_académico_limpio.xlsx` | Dataset limpio y transformado en Power Query | 8,000 | 19 |

Flujo de datos:

```text
gaming_academic_performance.csv
        |
        v
Power Query
        |
        v
Desempeño_académico_limpio.xlsx
```

---

## Limpieza y Transformacion

La limpieza principal fue realizada en **Power Query**. El archivo con los pasos en lenguaje M queda en:

```text
PowerQuery/gaming_academic_cleaning.pq
```

Resumen del proceso:

| Paso | Resultado |
|------|-----------|
| Carga del CSV original | 8,000 filas y 14 columnas |
| Revision de nulos | 0 valores nulos |
| Configuracion regional | En Power Query se uso **Decimal Number** con configuracion regional **English (United States)** para leer correctamente los decimales |
| Limpieza de texto | Normalizacion de `gender`, `stress_level` y conservacion de siglas `FPS` / `RPG` |
| Renombrado de columna | `attendance` pasa a llamarse `attendance (%)` en el archivo limpio de Power Query |
| Correccion de `grades` | Valores acotados al rango 0-100 |
| Correccion de `addiction_score` | Valores negativos acotados a 0 |
| Columnas agregadas | `gaming_band`, `study_band`, `sleep_band`, `performance_band`, `risk_flag` |
| Dataset final | 8,000 filas y 19 columnas |

---

## Diccionario de Columnas

El detalle completo de columnas, tipos sugeridos, valores categoricos, reglas de limpieza y columnas derivadas esta documentado en [`data/data_dictionary.md`](data/data_dictionary.md).

Resumen rapido:

| Elemento | Detalle |
|----------|---------|
| Columnas originales | 14 |
| Columnas finales | 19 |
| Columna renombrada | `attendance` pasa a `attendance (%)` en Power Query / Excel |
| Columnas derivadas | `gaming_band`, `study_band`, `sleep_band`, `performance_band`, `risk_flag` |

---

## Metricas Implementadas

| Metrica | Definicion | Uso en dashboard |
|---------|------------|------------------|
| **Grade Average** | Promedio de calificaciones limpias | KPI principal de rendimiento |
| **At-Risk Students** | Estudiantes con `grades < 60` | Seguimiento academico |
| **Excellent Students** | Estudiantes con `grades >= 90` | Identificacion de mejores practicas |
| **Gaming Hours** | Horas diarias de gaming | Intensidad de juego |
| **Study Hours** | Horas diarias de estudio | Disciplina academica |
| **Sleep Hours** | Horas diarias de sueño | Balance de rutina |
| **Attendance** | Porcentaje de asistencia, columna `attendance (%)` en Power Query | Compromiso academico |
| **Addiction Score** | Indice de dependencia al gaming | Riesgo conductual |
| **Device Usage** | Uso diario de dispositivos | Exposicion digital |
| **Reaction Time** | Tiempo de reaccion en milisegundos | Indicador cognitivo operativo |

---

## SQL Analytics - 14 Queries Analiticas + 3 Vistas para Power BI

Esta es la fase principal del **Proyecto 1**. Incluye preguntas analiticas, consultas SQL, segmentacion de estudiantes, calculo de KPIs y las vistas utilizadas por el dashboard en Power BI.

```sql
-- Ejemplo: calificacion promedio por banda de gaming
SELECT
    gaming_band,
    COUNT(*) AS students,
    ROUND(AVG(grades), 2) AS avg_grade,
    ROUND(AVG(study_hours), 2) AS avg_study_hours,
    ROUND(AVG(addiction_score), 2) AS avg_addiction_score
FROM gaming_academic_performance
GROUP BY gaming_band
ORDER BY FIELD(gaming_band, '0-2h', '2-4h', '4-6h', '6-8h');
```

| Seccion SQL | Queries | Tecnicas utilizadas |
|-------------|---------|---------------------|
| KPIs Ejecutivos | Q1-Q4 | `AVG`, `COUNT`, `CASE WHEN`, agregaciones condicionales |
| Rendimiento Academico | Q5-Q8 | segmentacion, ranking, performance bands |
| Inteligencia de Comportamiento | Q9-Q12 | correlaciones calculadas, `NTILE`, agregaciones |
| Riesgo y Segmentacion | Q13-Q14 | segmentos accionables, riesgo por asistencia y estudio |
| ETL Views | 3 vistas | `CREATE OR REPLACE VIEW`, tablas listas para dashboard |

Nota: en el archivo limpio de Power Query la columna aparece como `attendance (%)`. En el script SQL se usa `attendance` como nombre tecnico para evitar espacios y parentesis en las consultas.

---

## Estructura del Repositorio

```text
Gaming_Academic_Performance_Analysis-Q1/
|
|-- data/
|   |-- gaming_academic_performance.csv
|   |-- Desempeño_académico_limpio.xlsx
|   `-- data_dictionary.md
|
|-- SQL/
|   `-- gaming_academic_queries.sql
|
|-- PowerQuery/
|   `-- gaming_academic_cleaning.pq
|
|-- PowerBI/
|   |-- measures.dax
|   `-- Dashboard Gaming/
|       |-- Dashboard Gaming.pbip
|       |-- Dashboard Gaming.Report/
|       |-- Dashboard Gaming.SemanticModel/
|       `-- .gitignore
|
|-- assets/
|   |-- header_banner.svg
|   `-- dashboard_executive.png
|
|-- .gitignore
`-- README.md
```

---

## Como Reproducir

### 1. Generar dataset limpio en Power Query

1. Abrir Excel o Power BI.
2. Importar `data/gaming_academic_performance.csv`.
3. Entrar a **Power Query**.
4. Aplicar los pasos documentados en `PowerQuery/gaming_academic_cleaning.pq`.
5. Cargar la tabla limpia como `data/Desempeño_académico_limpio.xlsx`.

### 2. Crear tabla en MySQL

🗄️ Crear la tabla con el script de setup en `SQL/gaming_academic_queries.sql`.

📄 El dataset limpio esta en `data/Desempeño_académico_limpio.xlsx`. Para importarlo en MySQL, exportar la hoja limpia como CSV con el nombre:

```text
data/gaming_academic_performance_clean.csv
```

📥 Importar el CSV con **Table Data Import Wizard** en MySQL Workbench:

1. Abrir MySQL Workbench.
2. Conectarse a la base de datos.
3. Ir a **Schemas**.
4. Seleccionar la base de datos del proyecto.
5. Clic derecho en **Tables**.
6. Elegir **Table Data Import Wizard**.
7. Seleccionar el CSV exportado: `data/gaming_academic_performance_clean.csv`.
8. Importar los datos en la tabla `gaming_academic_performance`.

Antes de importar el CSV, revisar que los numeros decimales usen **punto (`.`)** y no **coma (`,`)** como separador decimal.

Ejemplo esperado para MySQL:

```text
91.44
```

No:

```text
91,44
```

Esto fue necesario porque MySQL puede generar error al leer valores numericos con coma decimal durante la importacion.

### 3. Abrir el dashboard en Power BI

1. Ejecutar las consultas y crear las tres vistas del archivo `SQL/gaming_academic_queries.sql` en MySQL.
2. Configurar el controlador ODBC de MySQL y un origen de datos (DSN) llamado `mysql_powerbi`. El modelo guardado usa la base de datos `repositorios`.
3. Abrir [`Dashboard Gaming.pbip`](PowerBI/Dashboard%20Gaming/Dashboard%20Gaming.pbip) en Power BI Desktop, conservando a su lado las carpetas `.Report` y `.SemanticModel`.
4. Configurar las credenciales locales y actualizar los datos. Si se usan otro DSN o base de datos, ajustar el origen de las consultas en Power Query.
5. Explorar las paginas **Executive**, **Trade-Off**, **Behavior** y **Risk**.

El modelo utiliza las vistas `vw_kpis_academicos`, `vw_student_segments` y `vw_behavior_dashboard`. Las medidas y la configuracion del modelo estan incluidas en el proyecto. La conexion y las credenciales de MySQL deben configurarse en cada equipo; los archivos locales de cache `.pbi` no forman parte del repositorio.

---

## Checklist de Cierre del Proyecto

- [x] Tabla `gaming_academic_performance` creada en MySQL.
- [x] Dataset limpio importado correctamente.
- [x] Q1-Q14 ejecutadas sin errores.
- [x] Vistas `vw_kpis_academicos`, `vw_student_segments` y `vw_behavior_dashboard` creadas correctamente.
- [x] Insights clave revisados contra los resultados reales de SQL.
- [x] README actualizado con contexto, datos, metodologia, consultas e insights.
- [x] Dashboard de cuatro paginas construido en Power BI con medidas DAX.
- [x] Filtros y botones de navegacion entre paginas implementados.
- [x] Proyecto editable de Power BI y captura real del dashboard incluidos en el repositorio.

---

## Insights Clave del Analisis

- El dataset fuente contiene **8,000 estudiantes**, **14 columnas** y no presenta valores nulos.
- La limpieza en Power Query genera un archivo limpio de **19 columnas** sin eliminar filas.
- Despues de la limpieza, `grades` queda dentro del rango **0-100** y `addiction_score` queda con minimo **0**.
- Las **horas de estudio** son la variable con relacion positiva mas fuerte frente a calificaciones (`corr = 0.733`).
- Las **horas de gaming** muestran una relacion negativa relevante con calificaciones (`corr = -0.552`).
- Estudiantes con **0-2h de gaming** tienen calificacion promedio de **82.02**, frente a **49.38** en el grupo de **6-8h**.
- Estudiantes con **8-10h de estudio** alcanzan promedio de **88.66**, frente a **44.91** en el grupo de **1-3h**.
- Hay **3,131 estudiantes en riesgo academico** (`grades < 60`) y **1,375 estudiantes excelentes** (`grades >= 90`).

---

## Autor

**Nicolás Ospina Polanía**  
Data Analyst Jr. en formacion

**Stack principal:** Power Query - Excel - SQL/MySQL - Power BI

---

<div align="center">

*Proyecto construido como repositorio de portafolio por fases a partir de un unico dataset CSV.*

</div>

