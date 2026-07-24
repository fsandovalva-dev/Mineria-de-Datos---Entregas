# Minería de Datos: Análisis y Predicción de Salarios

Este repositorio contiene el proyecto de evaluación de Minería de Datos, enfocado en descubrir patrones y predecir sueldos utilizando el "Job Salary Prediction Dataset" obtenido desde Kaggle[cite: 7]. El proyecto abarca el ciclo completo de vida de los datos, desde la limpieza y el análisis exploratorio hasta la implementación de algoritmos descriptivos y predictivos de Machine Learning[cite: 7].

## Sobre el Dataset
El conjunto de datos procesado consta de variables categóricas y numéricas que describen diversos perfiles profesionales[cite: 7]. Las principales variables analizadas incluyen: rol del trabajo (`job_title`), años de experiencia (`experience_years`), nivel educativo (`education_level`), industria (`industry`), tamaño de la empresa (`company_size`), modalidad de trabajo (`remote_work`), y número de certificaciones (`certifications`), entre otras[cite: 7].

## Arquitectura y Preprocesamiento de Datos
Para preparar los datos para el modelado algorítmico, se aplicaron las siguientes técnicas de ingeniería de características:
* **Manejo de Alta Cardinalidad:** Se implementó Binary Encoding mediante `category_encoders` en variables como la ubicación y el cargo para evitar la dispersión excesiva de la matriz y optimizar el rendimiento[cite: 7].
* **Variables Categóricas Nominales/Ordinales:** Se aplicó One-Hot Encoding a características como la industria, modalidad de trabajo, nivel educativo y tamaño de la empresa[cite: 7].
* **Tratamiento de Outliers:** Se utilizó Winsorización (Capping) basado en los límites del Rango Intercuartílico (IQR) para controlar los salarios gerenciales extremos sin eliminar información valiosa de los altos cargos[cite: 7].
* **Escalamiento:** Se estandarizaron las variables numéricas utilizando `StandardScaler` para garantizar un peso equitativo en los algoritmos que calculan distancias[cite: 7].

## Modelado y Resultados

### 1. Modelado Descriptivo (Clustering)
* Se implementó el algoritmo K-Means para descubrir segmentaciones naturales y perfiles dentro del mercado laboral[cite: 7].
* Mediante la aplicación del Método del Codo y el cálculo del Índice de Silhouette, se determinó que el número óptimo de agrupaciones es K=3[cite: 7].
* Se utilizó PCA (Análisis de Componentes Principales) para reducir la dimensionalidad y lograr proyectar visualmente los clústeres en un espacio 2D[cite: 7].

### 2. Modelado Predictivo (Regresión)
Se entrenaron y compararon dos algoritmos de naturaleza distinta para predecir el salario en USD:
* **Regresión Lineal Múltiple:** Utilizado como modelo base (Baseline) para evaluar relaciones lineales directas[cite: 7].
* **Árbol de Regresión (CART):** Seleccionado como el modelo definitivo[cite: 7].
* **Resultados de Inferencia:** El modelo CART superó ampliamente a la Regresión Lineal, logrando un Coeficiente de Determinación ($R^2$) superior al 81% en la fase de prueba[cite: 7]. Esto demostró que el salario se define por "bandas" salariales condicionales más que por incrementos puramente lineales[cite: 7]. Además, se validó la ausencia de Overfitting al someter el modelo a pruebas de estabilidad con particiones Holdout del 20%, 30% y 40%[cite: 7].

## Conclusiones Clave del Negocio
A partir de la Matriz de Correlación de Pearson y el análisis de Importancia de Variables del Árbol CART, se extrajeron los siguientes insights:
* **Principales Predictores:** Los años de experiencia y el tamaño de la corporación son los factores matemáticamente más determinantes para asegurar un sueldo alto[cite: 7].
* **El impacto de las certificaciones:** La cantidad de habilidades técnicas abstractas o el número de certificaciones extra presentan una correlación sorprendentemente débil o casi nula con el aumento salarial directo[cite: 7].
* **Modalidad de trabajo:** Trabajar de forma remota, híbrida o completamente presencial no presenta una relación lineal que castigue o beneficie la remuneración final[cite: 7].

## Integración y Escalabilidad (Bonus)
Para demostrar la capacidad del proyecto de ser integrado en entornos reales de producción, se desarrollaron componentes avanzados:
* **Inferencia Web en Tiempo Real (Scraping):** Un pipeline automatizado con `BeautifulSoup` que extrae ofertas de trabajo web reales, aplica las transformaciones de escala y procesa las inferencias de salario utilizando el Árbol CART[cite: 7].
* **Serialización:** El modelo predictivo ganador y el transformador de escalas fueron exportados en formato `.pkl` usando `joblib`, permitiendo que la inteligencia artificial sea consumida por una API REST en Flask sin necesidad de reentrenamiento[cite: 7].
* **Inteligencia de Negocios:** Se consolidó una exportación del dataset final estructurado específicamente para tableros de visualización en Power BI, incorporando los clústeres detectados y las proyecciones salariales completas[cite: 7].

---
*Proyecto de carácter académico desarrollado por Francisco Sandoval y Nicko Cortes.*
