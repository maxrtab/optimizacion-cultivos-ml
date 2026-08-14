# Modelado Predictivo para la Optimización de Cultivos Agrícolas

El objetivo de este proyecto es determinar la variable edafoclimática del suelo con mayor capacidad predictiva individual para clasificar **22 tipos de cultivo** mediante **Regresión Logística multiclase**. El estudio busca ayudar a los agricultores a tomar decisiones informadas sobre la selección de cultivos cuando cuentan con recursos o presupuestos limitados para análisis de laboratorio.


### Herramientas y tipo de proyecto

<p align="left">
  <img src="https://img.shields.io/badge/PYTHON-f4ebe1?style=flat&logo=python&logoColor=000000" alt="Python" />
  <img src="https://img.shields.io/badge/PANDAS-f4ebe1?style=flat&logo=pandas&logoColor=000000" alt="Pandas" />
  <img src="https://img.shields.io/badge/SCIKIT--LEARN-f4ebe1?style=flat&logo=scikit-learn&logoColor=000000" alt="Scikit-Learn" />
  <img src="https://img.shields.io/badge/LOGISTIC_REGRESSION-f4ebe1?style=flat&logoColor=000000" alt="Logistic Regression" />
  <img src="https://img.shields.io/badge/ANÁLISIS_EXPLORATORIO-f4ebe1?style=flat&logoColor=000000" alt="EDA" />
  <img src="https://img.shields.io/badge/EVALUACIÓN_DE_FEATURES-f4ebe1?style=flat&logoColor=000000" alt="Features" />
  <img src="https://img.shields.io/badge/MODELADO_PREDICTIVO-f4ebe1?style=flat&logoColor=000000" alt="Modelado" />
  <img src="https://img.shields.io/badge/APRENDIZAJE_SUPERVISADO-f4ebe1?style=flat&logoColor=000000" alt="Supervisado" />
</p>

## Preguntas clave

1. ¿Cuál es la distribución y balanceo de las categorías de cultivos en el conjunto de datos?
2. De las cuatro variables del suelo ($N$, $P$, $K$, $ph$), ¿cuál posee el mayor poder predictivo univariado para clasificar los cultivos?
3. ¿Qué métrica de evaluación refleja de mejor manera el rendimiento de un modelo multiclase balanceado?


## Metodología

* **Análisis Exploratorio de Datos (EDA):** Verificación de ausencia de valores nulos en los 2,200 registros y confirmación de un balance de clases perfecto (100 observaciones por cada uno de los 22 cultivos).
* **División del conjunto de datos:** Separación en conjuntos de entrenamiento (80%) y prueba (20%) con `random_state = 42` para asegurar la reproducibilidad de los resultados.
* **Modelado univariado:** Entrenamiento de cuatro modelos independientes de `LogisticRegression` (algoritmo multinomial, `max_iter = 200`), uno por cada característica química/física del suelo.
* **Evaluación de desempeño:** Cálculo del $F_1$-score ponderado (*weighted F1-score*) sobre el conjunto de prueba para evaluar la precisión discriminatoria individual de cada variable.



## Conclusiones y recomendaciones

#### Rendimiento univariado de características:
* **Capacidad predictiva por variable:** La evaluación del $F_1$-score ponderado identificó diferencias significativas en el impacto de cada parámetro del suelo:
  * **Potasio ($K$):** $0.2511$ *(Mayor poder predictivo univariado)*.
  * **Fósforo ($P$):** $0.1360$.
  * **Nitrógeno ($N$):** $0.0946$.
  * **pH ($ph$):** $0.0453$.
* **Característica determinante:** El potasio ($K$) se consolidó como la variable de mayor relevancia en el conjunto de datos (`best_predictive_feature = {'K': 0.25109}`).

#### Relevancia técnica y comercial:
* **Optimización de costos en campo:** Si un agricultor cuenta con presupuesto limitado y solo puede medir una propiedad química del suelo, se recomienda priorizar el **potasio ($K$)**, ya que ofrece casi el doble de capacidad discriminatoria que el fósforo.
* **Implementación práctica:** Priorizar la medición de potasio permite realizar una preselección eficiente del cultivo idóneo antes de realizar inversiones mayores en análisis químicos completos.



## Diccionario de datos
El conjunto de datos `soil_measures.csv` contiene **2,200 observaciones** de propiedades del suelo y los cultivos correspondientes:

* **N:** Contenido de Nitrógeno en el suelo (ratio).
* **P:** Contenido de Fósforo en el suelo (ratio).
* **K:** Contenido de Potasio en el suelo (ratio).
* **ph:** Valor del pH del suelo (escala de 0 a 14).
* **crop:** Tipo de cultivo idóneo (Variable objetivo categórica con 22 clases, ej. arroz, maíz, manzana, café, etc.).
