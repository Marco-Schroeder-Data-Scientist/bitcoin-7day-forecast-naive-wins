RESUMEN EJECUTIVO
Prediccion de Precios de Bitcoin a 7 Dias — Time Series Forecasting
====================================================================

PROBLEMA
--------
Predecir el precio de cierre de Bitcoin (BTC-USD) a 7 dias vista usando
exclusivamente datos historicos OHLCV diarios (2015–2025), y determinar
si modelos de ML pueden superar baselines simples en un activo de alta
volatilidad.


DATOS
-----
- Fuente:          Yahoo Finance via yfinance
- Periodo:         2015–2025
- Dataset original: 4.069 dias
- Dataset limpio:   3.497 dias para modelado
- Variables:        Open, High, Low, Close, Volume (OHLCV)
- Division:         85% train / 15% test (test: sep 2023 – feb 2025)


METODOLOGIA
-----------
EDA:
  - Retornos logaritmicos y distribucion por año
  - Volatilidad rolling en ventanas multiples
  - Analisis de volumen vs precio
  - Deteccion y tratamiento de valores anomalos

Feature Engineering:
  - Lags de precio, retornos y volatilidad (1–30 dias)
  - Features calendarias (dia de semana, mes)

Modelos evaluados:
  - Naive shift-7 (baseline fuerte)
  - Media Movil 30 dias
  - XGBoost con lags y features derivadas

Metricas utilizadas:
  - MAE, RMSE, R²


RESULTADOS
----------
Modelo                      MAE (USD)   RMSE (USD)   R²
--------------------------  ----------  -----------  --------
Naive shift-7               4,582       6,240        0.9141
Media Movil 30 dias         —           —            0.8895
XGBoost (lags + features)   —           —           -0.47

Ganador absoluto: Naive shift-7
  - Explica el 91.4% de la varianza en el conjunto de test
  - MAE de 4,582 USD sobre un activo que puede valer 60,000–90,000 USD

XGBoost: R² negativo (-0.47)
  - Peor que predecir la media
  - Causa: el modelo captura ruido en lugar de señal con solo datos OHLCV


INSIGHT CLAVE
-------------
Bitcoin presenta alta autocorrelacion en horizontes cortos — el precio
de hoy se parece mucho al de hace exactamente 7 dias. Esto hace que
modelos mas sofisticados no logren superar al Naive porque agregan ruido
sin capturar señal adicional con solo datos de precio y volumen.

Conclusion practica: antes de usar ML en forecasting financiero, siempre
definir un baseline fuerte. Si el Naive no puede ser superado, el problema
requiere datos adicionales (sentimiento, macro) o un enfoque diferente.


VALOR DEL PROYECTO
------------------
- Caso de estudio realista sobre limites del forecasting en criptomonedas
- Demostracion de la importancia de baselines fuertes en ML
- Honestidad en comunicacion de resultados — incluye resultados negativos
- Pensamiento critico aplicado: XGBoost falla y se explica por que


PROXIMOS PASOS
--------------
- Incorporar datos externos (sentimiento, indices macro)
- Evaluar ARIMA y Prophet como modelos especializados en series temporales
- Probar horizontes mas cortos (1–3 dias)
- Analisis por regimenes de mercado (bull/bear)


TECNOLOGIAS UTILIZADAS
----------------------
Python 3.10+ · pandas · numpy · matplotlib · seaborn ·
yfinance · XGBoost · scikit-learn · Jupyter Notebook
