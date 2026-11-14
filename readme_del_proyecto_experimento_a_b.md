# 📊 Evaluación de Experimento A/B en Landing Page

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter Notebook](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=Jupyter&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?style=for-the-badge&logo=scipy&logoColor=white)
![Statsmodels](https://img.shields.io/badge/Statsmodels-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c?style=for-the-badge&logo=python&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-3776AB?style=for-the-badge&logo=python&logoColor=white)

Análisis estadístico y de negocio para evaluar el desempeño de dos versiones de una página de inicio (**Landing A vs. Landing B**) durante una ventana de 28 días, con el objetivo de respaldar decisiones estratégicas basadas en datos.

---

## 🎯 Objetivo del Proyecto
Determinar qué versión de la *landing page* genera mayor valor comercial para el negocio analizando tanto la **tasa de conversión** como el **gasto promedio por usuario convertido**, además de evaluar el impacto de variables segmentadoras como la fuente de tráfico y el tipo de usuario.

---

## 📁 Estructura de los Datos
El conjunto de datos (`landing_experiment.csv`) cuenta con **40,000 registros únicos** (sin valores nulos ni duplicados) recopilados entre el `2026-01-01` y el `2026-01-28`:

* `user_id`: Identificador único del usuario.
* `date`: Fecha de exposición a la página.
* `landing`: Versión de la página mostrada (`A` o `B`).
* `region`: Región geográfica del usuario (*Norte, Centro, Sur, Occidente, Oriente*).
* `dispositivo`: Dispositivo de acceso (*Mobile, Desktop*).
* `traffic_source`: Canal de adquisición (*Organic, Ads, Email, Referral*).
* `user_type`: Historial del usuario (*Nuevo, Recurrente*).
* `converted`: Indicador binario de conversión (`1` = convirtió, `0` = no convirtió).
* `gasto`: Monto gastado por el usuario (`0` si no hubo conversión).

---

## 🛠️ Metodología y Herramientas

### Stack Tecnológico
* **Lenguaje:** Python 3
* **Manipulación de datos:** `pandas`, `numpy`
* **Visualización:** `matplotlib`, `seaborn`
* **Pruebas estadísticas:** `scipy.stats`, `statsmodels`

### Flujo de Análisis
1. **Validación y Limpieza (EDA):** Verificación de tipos de datos, integridad muestral y distribuciones.
2. **Evaluación de Monetización (Gasto Promedio):** Prueba de Levene para homocedasticidad ($p < 0.05$) seguida de una **prueba t de Welch** (`equal_var=False`) para comparar el ticket promedio entre versiones.
3. **Evaluación de Conversión:** **Prueba Z de dos proporciones** para contrastar la efectividad de conversión entre la versión A y B.
4. **Análisis de Segmentación:** **Pruebas Chi-Cuadrado de independencia** ($\chi^2$) para evaluar la relación entre conversión y variables categóricas (`traffic_source` y `user_type`).
5. **Storytelling y Visualización:** Gráficos de distribución (histogramas, *boxplots*) y proporciones (barras agrupadas y apiladas al 100%).

---

## 💡 Hallazgos Principales (Insights)

1. **Superioridad de la Landing B en Conversión y Ticket Promedio:**
   * **Tasa de conversión:** La versión B alcanzó un **15.96%** frente al **12.57%** de la versión A (+3.4 puntos porcentuales; $Z = -9.68$, $p = 3.76 \times 10^{-22}$).
   * **Gasto promedio:** Los usuarios convertidos en B gastaron en promedio **$68.75** frente a **$61.09** en A (+12.5%; $t = -9.48$, $p < 0.001$).
2. **Significancia Estadística vs. Impacto Práctico en Canales de Tráfico:**
   * Aunque la prueba Chi-cuadrado detectó asociación ($p = 0.034$) debido al gran tamaño muestral, la brecha real de conversión entre canales es mínima (**14% a 15%**). El volumen bruto de ventas depende principalmente del alcance de adquisición liderado por *Organic* y *Ads*.
3. **Neutralidad del Tipo de Usuario:**
   * No existe evidencia estadística de diferencia en la conversión entre usuarios *Nuevos* y *Recurrentes* ($\chi^2 = 0.513$, $p = 0.474$), manteniendo ambos una tasa cercana al **14%**.

---

## 🚀 Recomendaciones de Negocio

* **Despliegue definitivo de la Landing B:** Implementar la versión B como página principal para maximizar tanto el volumen de clientes adquiridos como el ingreso por transacción.
* **Optimización de Adquisición basada en CAC:** Priorizar la escalabilidad de tráfico en canales de alto volumen (*Organic* y *Ads*) cruzando futuros análisis con el Costo de Adquisición de Clientes (CAC) y el ROI.
* **Mejora transversal del embudo:** Enfocar los esfuerzos de UX/UI en la propuesta de valor y el proceso de *checkout* de manera general, en lugar de diseñar flujos separados por antigüedad de usuario.
* **Métricas futuras:** Incorporar el seguimiento del **ingreso por usuario expuesto** (*ARPU*) y el **Valor de Vida del Cliente (LTV)** en próximos experimentos.

---

## ⚠️ Limitaciones del Estudio
* El análisis cubre una ventana temporal acotada de 28 días.
* El dataset no incluye costos de pauta o adquisición (CAC) para calcular rentabilidad neta por canal.

---
*Proyecto desarrollado como parte del bootcamp de Análisis de Datos en **TripleTen**.*