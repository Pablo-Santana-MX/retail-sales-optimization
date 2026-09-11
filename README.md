# 🛒 RETAIL SALES OPTIMIZATION & INVENTORY DECISION ENGINE
### Motor de Optimización de Ventas Minoristas y Asignación Prescriptiva de Inventarios

<p align="center">
  <img src="reports/figures/banner_showcase.gif" alt="Retail Sales Optimization Pipeline Banner" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10%2B-blue.svg" alt="Python 3.10+">
  <img src="https://img.shields.io/badge/License-MIT-purple.svg" alt="License: MIT">
  <img src="https://img.shields.io/badge/Framework-XGBoost%20%7C%20SHAP%20%7C%20PuLP-7F26D9.svg" alt="Frameworks">
  <img src="https://img.shields.io/badge/Architecture-End--to--End%20Pipeline-2626D9.svg" alt="Pipeline">
</p>

---

## 📌 1. Resumen Ejecutivo / Executive Summary

**🇬🇧 English:** This enterprise-grade portfolio project implements an end-to-end analytical framework for a major retail and self-service store chain (**cadena de autoservicio**). Spanning across **420,000+ historical multi-department transactions** calibrated for the **2023–2025 fiscal horizon**, the system bridges diagnostic business intelligence, gradient-boosted demand forecasting, and constrained operations research. The primary objective is to eliminate stockouts, prevent dead inventory, and maximize gross operating margin under strict physical warehouse footprint and working capital limitations.

**🇲🇽 Español:** Este proyecto de portafolio de nivel corporativo implementa un marco analítico integral para una importante **cadena de tiendas de autoservicio**. Abarcando más de **420,000 transacciones históricas multidepartamentales** calibradas para el **horizonte fiscal 2023–2025**, el sistema conecta inteligencia diagnóstica de negocio, pronóstico de demanda con ensambles de árboles e investigación de operaciones con restricciones lineales. El objetivo central es mitigar quiebres de inventario, evitar acumulación de stock inmovilizado y maximizar el margen operativo bruto bajo restricciones estrictas de presupuesto de capital y capacidad física de almacén.

---

## 🏗️ 2. Arquitectura del Sistema / System Pipeline

| Directorio / Recurso | Módulos & Artefactos Clave | Propósito Operativo |
| :--- | :--- | :--- |
| **`notebooks/`** | `01_EDA_and_Engineering.ipynb`<br>`02_Predictive_Models.ipynb`<br>`03_Prescriptive_Analytics.ipynb` | Pipeline analítico secuencial: exploración diagnóstica, pronósticos supervisados y optimización prescriptiva. |
| **`data/`** | `raw/`, `processed/` | Ingesta transaccional unificada y almacenamiento estructurado final (`retail_data_processed.csv`). |
| **`reports/figures/`** | Visualizaciones (`.png`), `banner_showcase.gif` | Diagnósticos de estacionalidad multianual, impacto marginal SHAP y reporte visual para portafolio. |
| **`src/`** | `data_processing.py`<br>`model_training.py`<br>`optimization.py` | Lógica modular de nivel de producción exportable a pipelines automatizados. |
| **Entorno & Setup** | `requirements.txt`, `make_banner.py` | Configuración determinista de librerías y script de renderizado dinámico del banner. |

---

## 🔬 3. Analytical Pipeline & Milestones / Fases del Proyecto

### Phase 01: Diagnostic Analytics & Feature Engineering (`01_EDA_and_Engineering.ipynb`)
* **Relational Harmonization / Armonización Relacional:** * 🇬🇧 Multi-table relational schema integrating transactional sales, store metadata, and macroeconomic indicators (CPI, Unemployment, Fuel Price).  
  * 🇲🇽 Fusión relacional multivariable integrando registros transaccionales, metadatos operativos e indicadores macroeconómicos exógenos (INPC, Desempleo, Precio de Combustible).
* **Sparsity & Imputation Protocols / Protocolo de Imputación y Densidad:** * 🇬🇧 Domain-informed treatment of structural zero-sales and promotional clearance vectors (`MarkDown1-5`).  
  * 🇲🇽 Tratamiento matemático y funcional de vectores dispersos en descuentos promocionales dinámicos (`MarkDown1-5`).
* **Temporal Horizon Calibration / Descomposición Temporal Estratégica:** * 🇬🇧 Cyclic Fourier/calendar decomposition across the modernized **2023–2025 fiscal horizon**, isolating macro-holiday demand spikes (Thanksgiving, Christmas, Super Bowl).  
  * 🇲🇽 Descomposición cíclica y de calendario sobre el horizonte activo **2023–2025**, aislando choques de estacionalidad festiva crítica.

### Phase 02: Predictive Intelligence & Explainability (`02_Predictive_Models.ipynb`)
* **Forecasting Engine / Motor de Pronóstico Algorítmico:** * 🇬🇧 Gradient Boosted Decision Trees (**XGBoost**) calibrated to handle non-linear elasticities, cross-department interactions, and trend shifts.  
  * 🇲🇽 Ensambles de árboles de decisión no lineales (**XGBoost**) optimizados para capturar elasticidades complejas e interacciones multidepartamentales.
* **Leakage-Free Validation / Validación Temporal Rigurosa:** * 🇬🇧 Rolling out-of-time (OOT) evaluation framework (Train < 2025 \| Test $\ge$ 2025) benchmarked via **MAE**, **RMSE**, and **$R^2$**.  
  * 🇲🇽 Partición temporal fuera de muestra (Train < 2025 \| Test $\ge$ 2025) sin filtración prospectiva de información (*data leakage*).
* **Explainable AI (XAI) / Explicabilidad Teórico-Juegos:** * 🇬🇧 Local and global attribution using **SHAP (Shapley Additive Explanations)** to transform opaque tree ensembles into transparent business drivers.  
  * 🇲🇽 Deconstrucción del impacto marginal mediante valores **SHAP**, otorgando interpretabilidad y gobernanza analítica al negocio.

### Phase 03: Prescriptive Analytics & Operations Research (`03_Prescriptive_Analytics.ipynb`)
* **Optimization Framework / Optimización Prescriptiva Matemática:**
  * 🇬🇧 Constrained **Integer Linear Programming (ILP)** implemented in `PuLP` and solved via Branch-and-Cut (CBC Solver).
  * 🇲🇽 Formulación de **Programación Lineal Entera Mixta (ILP)** en `PuLP` resuelta mediante algoritmos exactos Branch-and-Cut.
* **Objective Function / Función Objetivo:**
  $$\max \sum_{i \in \text{Depts}} (\text{Price}_i - \text{Cost}_i) \cdot x_i$$
* **Operational Constraints / Restricciones Operativas:**
  * 💰 **Working Capital Cap / Techo Presupuestal:** $\sum (\text{Cost}_i \cdot x_i) \le \$450{,}000\text{ USD}$
  * 📦 **Physical Footprint / Huella Cúbica:** $\sum (\text{Volume}_i \cdot x_i) \le 1{,}000\text{ m}^3$
  * 🎯 **Demand Saturation / Techo de Demanda:** $x_i \le \hat{y}_i\quad (\text{Predicted Demand})$

---

## 🛠️ 4. Tech Stack & Corporate Visual Design / Tecnologías y Diseño Visual

| Dimension / Dimensión | Core Libraries / Tecnologías | Operational Scope / Propósito Técnico |
| :--- | :--- | :--- |
| **Data Architecture** | `Python 3.10+`, `Pandas`, `NumPy` | Vectorized pipelines, temporal data manipulation, and curation. |
| **Machine Learning** | `XGBoost`, `Scikit-Learn` | Gradient boosting regression with cross-validation. |
| **Explainability (XAI)** | `SHAP` | Game-theoretic marginal feature attribution. |
| **Operations Research** | `PuLP` (COIN-OR CBC Engine) | Constrained discrete integer optimization. |
| **Diagnostic Graphics** | `Matplotlib`, `Seaborn` | Publication-ready scientific reporting artifacts. |

**Standardized Analogous Palette / Sistema Cromático Cohesivo:**
* `Primary Focus / Foco Primario:` **`#7F26D9`** (Deep Royal Purple)
* `Accent / Contraste Secundario:` **`#D926D9`** (Magenta Highlight)
* `Technical / Capa Estructural:` **`#2626D9`** (Enterprise Cobalt Blue)
* `Constraints / Línea Base:` **`#B0BEC5`** (Slate Grey / Neutral Reference)

---

## ⚡ 5. Reproducibility Protocol / Guía de Reproducción

```bash
# 1. Clone repository / Clonar el repositorio
git clone [https://github.com/Pablo-Santana-MX/retail-sales-optimization.git](https://github.com/Pablo-Santana-MX/retail-sales-optimization.git)
cd retail-sales-optimization

# 2. Initialize isolated virtual environment / Crear entorno virtual
python3 -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate

# 3. Provision validated dependencies / Instalar dependencias
pip install --upgrade pip
pip install -r requirements.txt

# 4. Sequential Pipeline Execution / Ejecución secuencial de notebooks
# -> notebooks/01_EDA_and_Engineering.ipynb
# -> notebooks/02_Predictive_Models.ipynb
# -> notebooks/03_Prescriptive_Analytics.ipynb
---
```
## 👨‍💻 6. Strategic Leadership & Authorship / Autoría y Liderazgo

**Pablo Alberto Santana Flores, PhD**  
*Data Scientist | PhD in Marine Sciences | Quantitative Strategy & Advanced Analytics*

* 🌐 **LinkedIn:** [linkedin.com/in/pablo-santana-mx](https://mx.linkedin.com/in/pablo-santana-mx)
* 🐙 **GitHub:** [github.com/Pablo-Santana-MX](https://github.com/Pablo-Santana-MX)
* 📧 **Portfolio Inquiries:** Professional contact via LinkedIn or GitHub issues.
```
