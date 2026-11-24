# PREDICCION_COMBUSTIBLE_RD

## Descripción del proyecto

**Repositorio:**
https://github.com/michaelventura01/PREDICCION_COMBUSTIBLE_RD\
**Dominio:** Energía y combustibles\
**Enfoque propuesto:** Ciencia de Datos, Machine Learning y análisis
predictivo\
**Contexto geográfico:** República Dominicana

## 1. Resumen ejecutivo

PREDICCION_COMBUSTIBLE_RD es un proyecto orientado al análisis y la
predicción dentro del sector de combustibles de la República Dominicana.
El problema puede abordarse desde distintas perspectivas: pronóstico de
precios, estimación del consumo o análisis de la demanda de
combustibles.

La definición exacta de la variable objetivo es esencial para
interpretar el proyecto. La predicción de precios y la predicción de
consumo son problemas diferentes, con fuentes de datos, variables
explicativas, modelos y métricas de evaluación particulares.

**Alcance de esta descripción:** este documento es una descripción
preliminar basada en el nombre del repositorio y en el contexto del
proyecto. No se ha podido inspeccionar el código, los notebooks, los
datos ni los resultados internos. Por tanto, los elementos descritos
como recomendaciones no deben interpretarse como funcionalidades ya
implementadas.

## 2. Objetivos potenciales

Una solución de predicción de combustibles puede perseguir los
siguientes objetivos, según la variable objetivo que realmente utilice
el proyecto:

-   Analizar el comportamiento histórico de los precios o del consumo.
-   Identificar tendencias, patrones temporales y variaciones.
-   Construir modelos para estimar valores futuros.
-   Comparar diferentes enfoques estadísticos y de Machine Learning.
-   Evaluar la precisión y estabilidad de las predicciones.
-   Generar información que apoye el análisis y la toma de decisiones.

## 3. Posibles enfoques de predicción

### 3.1 Predicción de precios

Si el objetivo es pronosticar los precios de combustibles, pueden
estudiarse variables como:

-   Historial de precios nacionales por tipo de combustible.
-   Cotizaciones internacionales del petróleo, como WTI y Brent.
-   Precios internacionales de productos refinados.
-   Tipo de cambio USD/DOP.
-   Impuestos, márgenes y componentes de la estructura de precios.
-   Fechas de publicación y vigencia de los precios oficiales.

### 3.2 Predicción de consumo o demanda

Si el objetivo es estimar consumo o demanda, pueden ser relevantes:

-   Consumo histórico por tipo de combustible.
-   Frecuencia temporal de los registros.
-   Actividad económica y movilidad.
-   Estacionalidad, días festivos y patrones de calendario.
-   Variables sectoriales o regionales, si están disponibles y son
    confiables.

Estos dos enfoques no deben mezclarse sin una definición clara del
objetivo y de la unidad de análisis.

## 4. Fuentes de datos que conviene considerar

Para un estudio enfocado en República Dominicana, se recomienda
investigar fuentes oficiales y documentadas:

-   **Ministerio de Industria, Comercio y Mipymes (MICM):**
    publicaciones y referencias oficiales sobre precios de combustibles.
-   **Fuentes internacionales de energía:** series de referencia para
    petróleo y productos derivados.
-   **Fuentes cambiarias:** tasas históricas USD/DOP.
-   **Fuentes estadísticas nacionales:** indicadores económicos y
    demográficos que puedan explicar la demanda.

Cada fuente debe documentarse con su URL, frecuencia, fecha de
actualización, unidad de medida, cobertura histórica y condiciones de
uso. No se debe asumir que todas estas fuentes forman parte del
repositorio actual.

## 5. Metodología de Ciencia de Datos recomendada

1.  **Comprensión del problema:** definir si se predicen precios,
    consumo o demanda; especificar combustible, región, frecuencia y
    horizonte.
2.  **Adquisición de datos:** recopilar datos históricos y registrar la
    procedencia de cada variable.
3.  **Preparación y calidad:** validar tipos, unidades, fechas,
    duplicados, valores faltantes y cambios metodológicos.
4.  **Análisis exploratorio (EDA):** estudiar tendencias,
    estacionalidad, volatilidad, correlaciones y anomalías.
5.  **Feature Engineering:** construir variables de calendario, rezagos
    (*lags*) y promedios móviles utilizando únicamente información
    disponible en el momento de cada predicción.
6.  **Entrenamiento:** establecer un modelo base y comparar modelos
    adecuados al tipo de problema.
7.  **Validación temporal:** evaluar con particiones cronológicas y,
    cuando corresponda, validación de origen móvil (*walk-forward
    validation*).
8.  **Comunicación:** presentar pronósticos, errores, limitaciones e
    incertidumbre de manera comprensible.

## 6. Modelos que podrían evaluarse

La selección depende de la variable objetivo, la cantidad de datos y la
frecuencia temporal.

  -----------------------------------------------------------------------
  Modelo                  Uso posible             Consideraciones
  ----------------------- ----------------------- -----------------------
  Naive / Seasonal Naive  Línea base              Es indispensable para
                                                  comprobar que un modelo
                                                  complejo aporta valor

  Linear Regression       Regresión con variables Sencillo e
                          explicativas            interpretable

  Random Forest Regressor Datos tabulares y       Requiere ingeniería de
                          relaciones no lineales  variables temporales

  XGBoost / Gradient      Predicción tabular      Puede capturar
  Boosting                                        interacciones; requiere
                                                  ajuste y validación
                                                  cuidadosos

  ARIMA / SARIMA          Series temporales       Útil para patrones
                                                  temporales y
                                                  estacionales

  Prophet                 Series con tendencia y  Debe compararse con una
                          estacionalidad          línea base y otros
                                                  métodos
  -----------------------------------------------------------------------

No se afirma que estos algoritmos estén implementados actualmente en el
repositorio; son candidatos para una evaluación metodológica.

## 7. Métricas de evaluación

Para pronósticos numéricos pueden utilizarse:

-   **MAE:** error absoluto medio, expresado en la unidad de la variable
    objetivo.
-   **RMSE:** penaliza con mayor intensidad los errores grandes.
-   **MAPE:** expresa el error porcentual, pero puede ser inestable
    cuando los valores reales son cero o cercanos a cero.
-   **sMAPE o WAPE:** alternativas porcentuales que pueden ser más
    apropiadas en ciertos conjuntos de datos.

Las métricas deben calcularse sobre períodos futuros no utilizados para
entrenar o seleccionar el modelo. En una predicción de precios, el error
puede expresarse en DOP por unidad de combustible; en una predicción de
consumo, debe conservarse la unidad de volumen correspondiente.

## 8. Riesgos técnicos que deben auditarse

### Fuga de información (*Data Leakage*)

Las variables rezagadas, promedios móviles y transformaciones deben
construirse sin utilizar datos futuros. Los escaladores, imputadores y
demás transformaciones deben ajustarse únicamente con los datos de
entrenamiento.

### Validación incorrecta

Una partición aleatoria puede mezclar pasado y futuro y producir
resultados poco realistas. Para series temporales, debe respetarse el
orden cronológico.

### Cambios estructurales

Los precios y el consumo pueden verse afectados por cambios
regulatorios, impuestos, shocks internacionales, variaciones cambiarias
y eventos extraordinarios. El modelo debe evaluarse también en períodos
de alta volatilidad.

### Disponibilidad de variables

Una variable explicativa solo es válida si sus valores estaban
disponibles en el momento en que se habría generado el pronóstico. Por
ejemplo, no debe utilizarse una cotización o publicación que se conoció
después de la fecha de predicción.

## 9. Arquitectura de referencia

Una arquitectura posible para evolucionar el proyecto sería:

``` text
Fuentes de datos
  ├── Precios oficiales de combustibles
  ├── Indicadores internacionales de energía
  ├── Tipo de cambio
  └── Variables económicas
          |
          v
Ingesta y almacenamiento
          |
          v
Limpieza y validación de datos
          |
          v
Análisis exploratorio (EDA)
          |
          v
Feature Engineering temporal
          |
          v
Entrenamiento y validación temporal
          |
          v
Evaluación y selección del modelo
          |
          v
Pronósticos, visualizaciones e informes
```

Esta arquitectura es una propuesta de referencia, no una descripción
confirmada de la implementación actual.

## 10. Aplicaciones potenciales

Dependiendo del alcance real del proyecto, los resultados podrían
apoyar:

-   El seguimiento de tendencias de precios de combustibles.
-   La planificación y el análisis de escenarios.
-   La comprensión de la relación entre variables internacionales y
    precios nacionales.
-   La estimación de necesidades de consumo.
-   La comunicación de tendencias y riesgos a través de dashboards e
    informes.

Las predicciones deben presentarse como estimaciones sujetas a
incertidumbre y no como precios oficiales ni garantías de comportamiento
futuro.

## 11. Plan de auditoría del repositorio

Para completar una revisión técnica es necesario inspeccionar los
archivos y reproducir los experimentos. La auditoría debería cubrir:

  -----------------------------------------------------------------------
  Área                                Revisión
  ----------------------------------- -----------------------------------
  Estructura                          Carpetas, notebooks, scripts,
                                      documentación y dependencias

  Datos                               Origen, cobertura, frecuencia,
                                      unidades y calidad

  EDA                                 Distribuciones, tendencias,
                                      estacionalidad y anomalías

  Features                            Rezagos, ventanas móviles y
                                      disponibilidad temporal

  Modelos                             Algoritmos, parámetros, línea base
                                      y reproducibilidad

  Validación                          Separación cronológica y
                                      backtesting

  Métricas                            MAE, RMSE, MAPE y análisis de
                                      residuos

  Resultados                          Comparación con modelos base y
                                      análisis por horizonte

  Entrega                             Visualizaciones, instrucciones y
                                      limitaciones
  -----------------------------------------------------------------------

## 12. Conclusión

PREDICCION_COMBUSTIBLE_RD representa una línea de trabajo con potencial
para aplicar Ciencia de Datos y modelos predictivos al sector energético
dominicano. Su valor dependerá de una definición precisa del objetivo,
de la calidad y trazabilidad de los datos y de una validación que
reproduzca las condiciones reales de predicción.

La prioridad de la auditoría debe ser determinar qué variable predice
realmente el proyecto ---precio, consumo o demanda--- y comprobar si sus
resultados superan una línea base sencilla en períodos futuros no
utilizados durante el entrenamiento.

------------------------------------------------------------------------

**Nota de alcance:** descripción preliminar. El código fuente, los
notebooks, el dataset, los modelos entrenados y sus métricas no han sido
inspeccionados para elaborar este documento. Las fuentes, modelos,
variables y arquitectura mencionados son recomendaciones para orientar
la revisión y no afirmaciones sobre componentes ya presentes en el
repositorio.
