# Resumen Ejecutivo – Predicción de Precios de Bitcoin a 7 días

**Problema**  
Predecir el precio de cierre de Bitcoin (BTC-USD) a 7 días vista usando exclusivamente datos históricos OHLCV diarios (2015–2025).

**Enfoque**  
- Descarga limpia vía yfinance → 4.069 días originales → 3.497 limpios para modelado  
- EDA exhaustivo: retornos log, volatilidad rolling, volumen vs precio, distribución por año  
- Features: lags de precio, retornos y volatilidad (1–30 días) + calendáricas  
- División temporal: 85% train / 15% test (2023-09 a 2025-02)  
- Modelos evaluados: Naive, MA30, EMA 7/14, XGBoost

**Resultados principales**  
- **Ganador absoluto**: Naive shift-7  
  MAE: 4,582 USD | RMSE: 6,240 USD | **R² = 0.9141**  
- EMA 7/14: resultados cercanos o marginalmente mejores (pendiente detalle)  
- XGBoost con rezagos: R² negativo (-0.47) → peor que predecir la media

**Insight clave**  
En horizontes cortos y sin datos externos, **la persistencia simple es prácticamente imbatible** en Bitcoin debido a su alta autocorrelación y volatilidad extrema. Modelos más sofisticados añaden ruido sin mejorar la predicción.

**Valor del proyecto**  
Caso de estudio realista sobre límites del forecasting en cripto, importancia de baselines fuertes y honestidad en resultados.