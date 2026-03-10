# Prediccion de Precios de Bitcoin a 7 Dias — Time Series Forecasting

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![yfinance](https://img.shields.io/badge/data-yfinance-orange)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.0%2B-blue)

## Descripcion

Proyecto de series temporales para predecir el precio de cierre de Bitcoin
(BTC-USD) a 7 dias vista, utilizando exclusivamente datos historicos OHLCV
diarios descargados desde Yahoo Finance (2015–2025).

**Objetivo principal:**
Evaluar si es posible superar baselines simples (Naive forecasting) en un
activo de alta volatilidad y fuerte persistencia como Bitcoin, y entender
los limites reales del forecasting en mercados de criptomonedas.

---

## Resultados

| Modelo | MAE (USD) | RMSE (USD) | R² |
|---|---|---|---|
| **Naive shift-7** | **4,582** | **6,240** | **0.9141** |
| Media Movil 30 dias | — | — | 0.8895 |
| XGBoost (lags + features) | — | — | -0.47 |

**Conclusion principal:**
En horizontes cortos (7 dias) y con solo datos de precio/volumen, la
persistencia simple domina completamente en Bitcoin. El modelo Naive
shift-7 explica el 91% de la varianza en el conjunto de test.

XGBoost con rezagos y features derivadas obtiene R² negativo (-0.47),
lo que significa que es peor que predecir la media — un hallazgo relevante
sobre los limites del ML en activos de alta autocorrelacion y volatilidad.

---

## Metodologia

### 1. Datos
- Fuente: Yahoo Finance via yfinance
- Periodo: 2015–2025
- Dataset original: 4.069 dias → 3.497 dias limpios para modelado
- Variables: Open, High, Low, Close, Volume (OHLCV)

### 2. EDA
- Retornos logaritmicos y distribucion por año
- Volatilidad rolling (ventanas multiples)
- Analisis de volumen vs precio
- Deteccion y tratamiento de valores anomalos

### 3. Feature Engineering
- Lags de precio, retornos y volatilidad (1–30 dias)
- Features calendarias
- Division temporal: 85% train / 15% test (test: sep 2023 – feb 2025)

### 4. Modelos evaluados
- Naive shift-7 (baseline — prediccion = precio de hace exactamente 7 dias)
- Media Movil 30 dias
- XGBoost con lags y features derivadas

### 5. Metricas
- MAE (Mean Absolute Error)
- RMSE (Root Mean Squared Error)
- R² (coeficiente de determinacion)

---

## Estructura del Repositorio

```
bitcoin-7day-forecast-naive-wins/
├── notebooks/
│   └── bitcoin_forecast_7days.ipynb   # Notebook principal completo
├── requirements.txt
├── README.md
└── images/
```

---

## Instalacion

```bash
# Crear entorno virtual
python -m venv venv
source venv/bin/activate        # Linux/macOS
# venv\Scripts\activate         # Windows

# Instalar dependencias
pip install -r requirements.txt
```

---

## Insight clave

Bitcoin presenta alta autocorrelacion en horizontes cortos — el precio
de hoy se parece mucho al de hace 7 dias. Esto hace que modelos mas
sofisticados no logren superar al Naive porque agregan ruido sin capturar
señal adicional con solo datos OHLCV.

Este proyecto es un caso de estudio realista sobre la importancia de
definir baselines fuertes antes de invertir en modelos complejos, y sobre
la honestidad en la comunicacion de resultados.

---

## Proximos Pasos

- Incorporar datos externos (sentimiento de mercado, indices macro)
- Evaluar modelos de series temporales especializados (ARIMA, Prophet)
- Probar horizontes de prediccion mas cortos (1–3 dias)
- Analisis de regimenes de mercado (bull/bear) como variable de contexto

---

## Tecnologias

Python 3.10+ · pandas · numpy · matplotlib · seaborn ·
yfinance · XGBoost · scikit-learn · Jupyter Notebook

---

## Licencia

MIT License — libre para uso, modificacion y distribucion (atribucion apreciada).
Pull requests y sugerencias son bienvenidos.

### Estructura del repositorio
bitcoin-price-forecast-7d/
├── notebooks/
│   └── bitcoin_forecast_7days.ipynb     # Notebook principal completo
├── requirements.txt
├── README.md
└── images/
