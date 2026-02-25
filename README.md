# Predicción de Precios de Bitcoin a 7 días – Time Series Forecasting

Proyecto de series temporales para predecir el precio de cierre de Bitcoin (BTC-USD) a **7 días** vista, utilizando **solo datos históricos OHLCV** de Yahoo Finance (2015–2025).

**Objetivo principal**  
Evaluar si es posible superar baselines extremadamente simples (Naive forecasting) en un activo de alta volatilidad y fuerte persistencia como Bitcoin.

### Resultados clave

- **Mejor modelo encontrado**: **Naive shift-7** (predicción = precio de cierre de hace exactamente 7 días)  
  - MAE: 4,582 USD  
  - RMSE: 6,240 USD  
  - **R² = 0.9141** (explica ~91% de la varianza en el conjunto de test)

- Otros modelos evaluados (todos inferiores al baseline):
  - Media Móvil 30 días → R² 0.8895
  - EMA 7 días → resultados cercanos o ligeramente mejores que naive (pendiente de detalle final)
  - EMA 14 días → intermedio
  - XGBoost con lags y features derivadas → R² negativo (-0.47)

**Conclusión principal**  
En horizontes cortos (7 días) y con solo datos de precio/volumen, **la persistencia simple domina completamente** en Bitcoin. Modelos de machine learning estándar no logran aportar valor predictivo adicional significativo con este enfoque.

### Tecnologías utilizadas

- Python 3.10+
- pandas, numpy, matplotlib, seaborn, yfinance, xgboost, scikit-learn

### Estructura del repositorio
bitcoin-price-forecast-7d/
├── notebooks/
│   └── bitcoin_forecast_7days.ipynb     # Notebook principal completo
├── requirements.txt
├── README.md
└── images/