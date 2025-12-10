# Predicción del Rendimiento Azucarero mediante Machine Learning

## 📋 Descripción del Proyecto

Este proyecto implementa modelos de **regresión** y **clasificación** para predecir y categorizar el rendimiento de cultivos de caña de azúcar en el Ingenio Providencia. El objetivo es proporcionar herramientas analíticas que permitan tomar decisiones más informadas sobre la planificación y manejo de cultivos.

## 🎯 Objetivos

### Parte 1: Modelos de Regresión
Predecir dos variables clave de rendimiento:
- **TCH (Toneladas de Caña por Hectárea)**: Indicador de productividad de la tierra
- **%Sac.Caña (Porcentaje de Sacarosa)**: Medida de calidad de la caña y cantidad de azúcar extraíble

### Parte 2: Modelos de Clasificación
Categorizar los registros en tres niveles de desempeño (Alto, Medio, Bajo) para:
- **TCH**: Niveles de productividad
- **%Sac.Caña**: Niveles de sacarosa

## 📊 Datasets Utilizados

- **HISTORICO_SUERTES.xlsx**: Datos históricos para modelos de regresión
- **BD_IPSA_1940.xlsx**: Datos para modelos de clasificación

## 🔬 Metodología

### Parte 1: Análisis de Regresión

#### 1. Análisis Exploratorio de Datos (EDA)
- Exploración inicial del dataset (shape, tipos de datos, valores faltantes)
- Detección de outliers y valores atípicos
- Visualización de distribuciones mediante histogramas
- Análisis de correlaciones entre variables

#### 2. Limpieza y Preprocesamiento
- **Eliminación de columnas con >50% de valores nulos**
- **Manejo de data leakage**: Eliminación de variables que representan resultados futuros:
  - Variables post-cosecha: `TCHM`, `TAH`, `TAHM`, `KATRHM`
  - Variables ambiguas: `Producto`, `%Sac.Caña`, `%Sac.Muestreadora`, `%ATR`, `%Fibra Caña`, `%AR Jugo`, `%ME Min`, `%ME Veg`, `%ME Tot`
  - Variables descriptivas: `Nombre`, `Suerte`, `Hacienda`
- **Encoding de variables categóricas** mediante One-Hot Encoding
- **Imputación de valores faltantes** en variables numéricas

#### 3. Desarrollo de Modelos
- Implementación de **Regresión Lineal Multiple**
- Análisis de significancia estadística de variables
- Evaluación de supuestos del modelo:
  - Linealidad
  - Homocedasticidad
  - Normalidad de errores
  - Multicolinealidad (VIF)

#### 4. Validación y Evaluación
- División de datos en entrenamiento y prueba (holdout)
- Métricas calculadas:
  - **R²** (Coeficiente de determinación)
  - **RMSE** (Root Mean Squared Error)
  - **MAE** (Mean Absolute Error)
- Análisis de residuales

### Parte 2: Análisis de Clasificación

#### 1. Creación de Categorías
Se definieron umbrales mediante **cuantiles (terciles)**:

**Para TCH:**
- Bajo: ≤ Percentil 33
- Medio: > Percentil 33 y ≤ Percentil 66
- Alto: > Percentil 66

**Para %Sac.Caña:**
- Bajo: ≤ Percentil 33
- Medio: > Percentil 33 y ≤ Percentil 66
- Alto: > Percentil 66

**Justificación**: Los cuantiles garantizan una distribución equilibrada de las clases y capturan la variabilidad natural de los datos sin requerir conocimiento de dominio específico.

#### 2. Desarrollo de Modelos
- **Regresión Logística** con regularización
- **K-Nearest Neighbors (KNN)**
- Análisis de significancia estadística mediante:
  - Prueba de Wald
  - Valores p (nivel de significancia α = 0.05)
- Identificación de multicolinealidad entre variables (edad, semsmad, vejez)

#### 3. Validación y Evaluación
- **Validación cruzada** (k-fold cross-validation)
- Métricas de clasificación:
  - **Accuracy** (Exactitud general)
  - **Precision** (Precisión por clase)
  - **Recall** (Sensibilidad)
  - **F1-Score** (Media armónica de Precision y Recall)
  - **Kappa de Cohen**
- Matrices de confusión para análisis detallado

## 🛠️ Tecnologías Utilizadas

```python
# Librerías principales
- pandas              # Manipulación de datos
- numpy               # Operaciones numéricas
- matplotlib          # Visualización
- seaborn             # Visualización estadística
- scikit-learn        # Modelos de ML
- statsmodels         # Análisis estadístico
```

## 📈 Resultados Principales

### Modelos de Regresión
- Identificación de variables más significativas para predecir TCH y %Sac.Caña
- Evaluación del poder predictivo mediante métricas R², RMSE y MAE
- Detección y manejo de multicolinealidad

### Modelos de Clasificación
- Categorización efectiva en tres niveles de desempeño
- Variables significativas (p ≤ 0.05): `semsmad`, `edad`, `cortes`, `vejez`
- Comparación de rendimiento entre Regresión Logística y KNN
- Análisis de importancia de características

## 📁 Estructura del Repositorio

```
Lab1Repo/
├── Consigna.md                              # Descripción del laboratorio
├── Parte1_Lab_1_APO_III-TERMINADO.ipynb    # Análisis de regresión
├── Lab1_Parte2_final.ipynb                 # Análisis de clasificación
├── README.md                               # Este archivo
└── HISTORICO_SUERTES.xlsx                  # Dataset (no incluido en repo público)
└── BD_IPSA_1940.xlsx                       # Dataset (no incluido en repo público)
```

## 🔑 Hallazgos Clave

1. **Data Leakage Prevention**: Se identificaron y eliminaron variables que representaban información futura o resultados post-cosecha, evitando sobreajuste artificial

2. **Multicolinealidad**: Se detectó alta correlación entre `edad`, `semsmad` y `vejez`, requiriendo técnicas de regularización

3. **Variables Significativas**: 
   - Para TCH: edad del cultivo, número de cortes, condiciones climáticas
   - Para clasificación: semsmad, cortes, vejez mostraron significancia estadística

4. **Balance de Clases**: El uso de terciles garantizó distribuciones equilibradas en las categorías

## 👥 Autores

**Equipo de Desarrollo**
- Juan Pablo Parra Bernal

**Curso**: APO III - Séptimo Semestre  
**Institución**: [Tu Universidad]  
**Fecha**: Diciembre 2025

## 📝 Notas

- Los datasets no están incluidos en el repositorio público por políticas de privacidad
- El código está completamente documentado en los notebooks Jupyter
- Se siguieron buenas prácticas de ciencia de datos y machine learning

## 🚀 Cómo Usar

1. Clonar el repositorio
```bash
git clone https://github.com/Juanpapb0401/Prediccion-Rendimiento-Azucar-ML.git
```

2. Instalar dependencias
```bash
pip install pandas numpy matplotlib seaborn scikit-learn statsmodels openpyxl
```

3. Abrir los notebooks Jupyter
```bash
jupyter notebook Parte1_Lab_1_APO_III-TERMINADO.ipynb
jupyter notebook Lab1_Parte2_final.ipynb
```

## 📊 Visualizaciones Incluidas

- Histogramas de distribución de variables
- Matrices de correlación
- Gráficos de dispersión
- Análisis de residuales
- Matrices de confusión
- Importancia de características

## 🎓 Conceptos Aplicados

- Regresión Lineal Múltiple
- Regresión Logística
- K-Nearest Neighbors
- Validación Cruzada
- Regularización
- Análisis de Multicolinealidad (VIF)
- Pruebas de Hipótesis
- Ingeniería de Características
- Manejo de Datos Faltantes

## 📋 Resumen de la Consigna

El laboratorio consistió en desarrollar modelos predictivos para el Ingenio Providencia con dos objetivos principales:

### 1. Regresión (HISTORICO_SUERTES.xlsx)
Predecir:
- **Toneladas de caña por hectárea (TCH)**: Productividad de la tierra
- **Porcentaje de sacarosa (%Sac.Caña)**: Calidad de la caña

### 2. Clasificación (BD_IPSA_1940.xlsx)
Crear categorías de desempeño (Alto, Medio, Bajo) para TCH y %Sac.Caña

### Criterios de Evaluación:
- ✅ Claridad y rigor en el análisis exploratorio
- ✅ Correcta implementación de modelos de regresión y clasificación
- ✅ Validación adecuada y uso de métricas apropiadas
- ✅ Comunicación clara de resultados
- ✅ Propuestas de mejora e innovación

## 💡 Cómo lo Solucioné

### Enfoque de Regresión (Parte 1):
1. **EDA Exhaustivo**: Análisis profundo de distribuciones, correlaciones y valores faltantes
2. **Preprocesamiento Riguroso**: 
   - Eliminé columnas con >50% de valores nulos
   - Identifiqué y eliminé variables de "data leakage" (TCHM, TAH, variables post-cosecha)
   - Apliqué One-Hot Encoding a variables categóricas
3. **Modelado**: Regresión lineal múltiple con validación de supuestos
4. **Evaluación**: Métricas R², RMSE, MAE y análisis de residuales

### Enfoque de Clasificación (Parte 2):
1. **Categorización Inteligente**: Uso de terciles para garantizar balance de clases
2. **Análisis Estadístico**: Prueba de Wald y valores p para identificar variables significativas
3. **Modelos Comparativos**: Regresión Logística vs KNN
4. **Validación Robusta**: Validación cruzada y múltiples métricas (Accuracy, Precision, Recall, F1, Kappa)

### Decisiones Clave:
- **Prevención de Data Leakage**: Eliminación de variables futuras como `Producto`, `%Sac.Caña`, `%Sac.Muestreadora`
- **Manejo de Multicolinealidad**: Identificación de correlación entre edad, semsmad y vejez
- **Terciles para Categorización**: Decisión fundamentada en distribución equilibrada de datos
- **Variables Significativas**: Selección basada en valores p (α = 0.05)

---

**Nota**: Este proyecto fue desarrollado con fines académicos como parte del Laboratorio 1 del curso APO III.
