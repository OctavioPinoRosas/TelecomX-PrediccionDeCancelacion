# Telecom X Predicción de Cancelación (Churn)
## 🧭 Misión
Desarrollar modelos predictivos capaces de prever qué clientes tienen mayor probabilidad de cancelar sus servicios. Este repositorio contiene el pipeline de modelado, evaluación e interpretación de resultados que continúa el trabajo de limpieza y EDA realizado en la [Parte 1](https://github.com/OctavioPinoRosas/ChallengeTelecomX.git).

## 🎯 Objetivos
- Preparar los datos para el modelado (tratamiento, codificación, normalización cuando aplique).
- Realizar análisis de correlación y selección de variables.
- Entrenar múltiples modelos de clasificación (baseline, Árbol de Decisión y Random Forest).
- Evaluar el rendimiento con métricas y matrices de confusión.
- Interpretar resultados: importancia de variables y principales factores que influyen en la cancelación.
- Elaborar conclusiones y una estrategia de retención basada en los hallazgos.

## 📦 Datos (Entrada)
Fuente: [archivo CSV](https://github.com/OctavioPinoRosas/ChallengeTelecomX/blob/main/DataBase/TelecomXData.csv) tratado en la Parte 1 (limpio, columnas relevantes y estandarizadas).  
Ruta sugerida: `DataBase/TelecomXData.csv`  
Target: columna binaria de cancelación (por ej., Churn = 0/1).  

🛠️ Preparación de los datos
- Extracción: carga del CSV tratado (uso de pandas).
- Eliminación de columnas irrelevantes: IDs u otros identificadores sin valor predictivo.
- Transformaciones: manejo de nulos, tipos y estandarización cuando aplique.
- Encoding: variables categóricas → numéricas con `pd.get_dummies(drop_first=True)`.
- Balance de clases: análisis de proporciones; aplicación de oversampling (SMOTE) cuando corresponde.
- Separación de datos: `train_test_split` (80/20) con `stratify`.

## 📈 Correlación y Análisis Dirigido
- Matriz y mapa de calor de correlación para variables numéricas.
- Análisis dirigido de relaciones con churn, ejemplos:
- Tiempo de contrato × Cancelación
- Gasto total × Cancelación
- Visualizaciones (boxplots / scatter) para patrones y tendencias.

## 🧪 Modelos de  Machine Learnong
1. Baseline (Dummy)
Modelo de referencia para contextualizar mejoras. Métricas: accuracy, precision, recall, F1 y matriz de confusión.
2. Decision Tree Classifier
Configuraciones: versión sin balanceo y con balanceo (Oversampling `SMOTE`).
Búsqueda de hiperparámetros y validación cruzada.
Matriz de confusión e interpretación de errores.
3. RandomForestClassifier
Configuraciones: versión sin balanceo y con balanceo (Oversampling `SMOTE`)
Búsqueda de hiperparámetros y validación cruzada.
Matriz de confusión e interpretación de errores.

## 🔍 Mejores Hiperparámetros (ejemplos obtenidos)
Los mejores parámetros pueden variar según la semilla y el preprocesamiento. A continuación, ejemplos registrados durante los experimentos:
1. Modelo DecisionTreeClassifier
    - Modelo con datos no balanceados
        ```
        {
        'max_depth': 5
        }
        ```
        - Modelo con datos balanceados
        ```
        {
        'max_depth': 11
        }
        ```
2. RandomForestClassifier
    - Modelo con datos no balanceados
        ```
        {
        'max_depth': 10,
        'max_features': 'sqrt',
        'min_samples_leaf': 4,
        'min_samples_split': 10,
        'n_estimators': 200,
        }
        ```
    - Modelo con datos no balanceados
        ```
        {
        'max_depth': None,
        'max_features': 'sqrt',
        'min_samples_leaf': 2,
        'min_samples_split': 2,
        'n_estimators': 300,
        }
        ```
## 📊 Resultados (Test)

Resumen por escenario (clase positiva = churn = 1):

|Modelo	      |Balanceo |Presicion |Accuracy |Recall (clase 1) | F1 (clase 1)|
|-------------|---------|----------|---------|-----------------|-------------|        
|DecisionTree | No      || 0.78	  |0.52	            |0.55 |
|DecisionTree |	Sí      || 0.73	  |0.65	            |0.55|
|RandomForest |	No      || 0.80	  |0.51	            |0.57|
|RandomForest |	Sí      || 0.78	  |0.63	            |0.59|