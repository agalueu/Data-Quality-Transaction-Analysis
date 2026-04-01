# 📊 Data Quality & Transaction Analysis (Python)

## 🧠 Contexto de negocio

La empresa recibe un archivo diario de transacciones desde múltiples fuentes.
Actualmente, los datos presentan problemas de calidad que afectan:

* Reportes financieros
* Dashboards
* Monitoreo de riesgo
* Toma de decisiones

---

## 🎯 Objetivo del proyecto

Diseñar un pipeline en Python que permita:

* Limpieza de datos
* Validación mediante reglas de negocio
* Detección de anomalías
* Generación de datasets confiables para análisis

---

## 📦 Dataset

Archivo: `transactions_raw.csv`

Columnas principales:

* transaction_id
* user_id
* transaction_date
* amount
* status
* country
* created_at
* source_system

---

## ⚙️ Proceso aplicado

### 1. Exploración de datos (EDA)

* Identificación de nulos, duplicados y errores de formato
* Detección de inconsistencias en montos y fechas

---

### 2. Normalización

* Conversión de tipos (`amount`, fechas)
* Estandarización de categorías (`status`)

---

### 3. Validación de reglas de negocio

Se definen reglas como:

* IDs obligatorios
* Fechas válidas
* Montos coherentes
* No duplicados

Se generan flags por regla y una columna final:

```python
is_valid
```

---

### 4. Dataset limpio

Se construye un dataset con solo transacciones válidas:

```python
valid_df = df[df["is_valid"]]
```

---

### 5. Detección de anomalías

Se identifican outliers usando percentiles:

* Regla: `amount > 3 * P75`
* Generación de flag: `flag_amount_outlier`

---

### 6. Outputs del pipeline

Se generan tres datasets:

* ✅ `reporting_df` → datos listos para BI
* ⚠️ `anomalies_df` → monitoreo de riesgo
* 🔍 `audit_df` → trazabilidad completa

---

### 7. KPIs de calidad de datos

Se calculan métricas como:

* Total registros
* Registros válidos / inválidos
* % calidad de datos
* Fallas por regla

---

## 📊 Resultado clave

* Total registros: 21
* Registros inválidos: 10
* **Data Quality Score: 52.38%**

👉 Casi la mitad de los datos presentan problemas de calidad.

---

## 🧠 Insights relevantes

* Duplicados afectan métricas financieras
* Fechas inválidas rompen análisis temporal
* Montos inconsistentes implican riesgo operativo
* Outliers detectados en transacciones válidas

---

## 🚀 Tecnologías utilizadas

* Python
* Pandas
* Jupyter Notebook

---

## 📁 Estructura del proyecto

```
project/
│
├── data/
│   └── transactions_raw.csv
│
├── notebooks/
│   └── data_quality_analysis.ipynb
│
├── outputs/
│   ├── transactions_reporting.csv
│   ├── transactions_anomalies.csv
│
└── README.md
```

---

## 📌 Próximos pasos

* Automatización del pipeline
* Integración con Power BI
* Alertas automáticas de calidad
* Escalabilidad para múltiples datasets

---
