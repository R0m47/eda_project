# Exploratory Data Analysis (EDA) Project

Proyecto enfocado en aplicar técnicas basicas de **análisis con SQL** sobre un pequeño **Data Warehouse** en SQL Server. Incluye la creación de la base de datos, carga de datos desde CSV o backup, y un set de consultas para exploración, métricas clave, agregaciones y ranking.

> **Disclaimer / Créditos**  
> Las bases de datos (estructura/tablas) y la base conceptual de varias consultas están inspiradas en el proyecto de **Baraa Khatib**:  
> https://www.datawithbaraa.com/sql-introduction/advanced-sql-analytics-project/

## Requisitos

- **SQL Server** (Developer o Express).
- **SSMS** (SQL Server Management Studio) o **Azure Data Studio**.

## Instalación (tres métodos)

> **Orden recomendado:** intentar primero por **Script**. Si no funciona en tu entorno (por permisos o rutas), usar el **.bak**. Como alternativa, puedes hacer la importación manual con **Flat Files**.

### Método A) Script (recomendado)

1. Abre `scripts/00_init_database.sql` en SSMS.
2. Cambia las rutas de los `BULK INSERT` a donde tengas los CSV por ejemplo:
   ```sql
   BULK INSERT gold.dim_customers
   FROM 'C:\TU_RUTA\gold.dim_customers.csv';
   ```
3. Ejecuta el script completo (Elimina la base `DataWarehouseAnalytics` si existe).
4. Verifica que las tablas estén pobladas (`gold.dim_customers`, `gold.dim_products`, `gold.fact_sales`).

### Método B) Restaurar desde backup `.bak`

1. En SSMS: **Databases** → clic derecho → **Restore Database…**
2. **Device** → **Add…** → selecciona `datasets/bk/DataWarehouseAnalytics.bak`.
3. Asigna el nombre `DataWarehouseAnalytics` y restaura.
4. Comprueba que las tablas existen.

### Método C) Flat Files (Import Wizard)

1. Crea manualmente la base `DataWarehouseAnalytics`.
2. Crea el esquema `gold`:
   ```sql
   CREATE SCHEMA gold;
   ```
3. Crea las tablas con la definición incluida en el script.
4. Usa **Tasks → Import Flat File** en SSMS para cargar cada CSV en su tabla.

## Script de inicialización

El archivo [`scripts/00_init_database.sql`](scripts/00_init_database.sql) incluye:

- Creación de la base de datos.
- Creación del esquema `gold`.
- Definición de las tablas (`dim_customers`, `dim_products`, `fact_sales`).
- Carga de datos vía **BULK INSERT**.

**Advertencia:** El script **elimina** y **recrea** la base si ya existe.

## Notas y buenas prácticas

- Las rutas de `BULK INSERT` deben existir en el **servidor donde corre SQL Server** (no en tu PC local si es remoto).
- Asegúrate de dar permisos de lectura a los archivos CSV para la cuenta del servicio SQL Server.

---

## Créditos

Proyecto educativo inspirado en el trabajo de **Baraa Khatib**  
https://www.datawithbaraa.com/sql-introduction/advanced-sql-analytics-project/
