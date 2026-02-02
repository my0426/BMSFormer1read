<div align="center">
  <img src="https://img.shields.io/badge/Language-中文-red.svg" alt="Chino">
  <img src="https://img.shields.io/badge/Language-English-blue.svg" alt="Inglés">
  <img src="https://img.shields.io/badge/Language-Español-yellow.svg" alt="Español">
  <img src="https://img.shields.io/badge/Language-Português-green.svg" alt="Portugués">
  <img src="https://img.shields.io/badge/Model-BMSFormer-orange" alt="Modelo">
  <img src="https://img.shields.io/badge/Task-SOH_Estimation-blueviolet" alt="Tarea">
  
  <h1>📚 Notas de Lectura: BMSFormer - Un modelo eficiente de estimación de SOH para BMS con recursos limitados</h1>
  <p>Paper: BMSFormer: An efficient deep learning model for online state-of-health estimation of lithium-ion batteries under high-frequency early SOC data with strong correlated single health indicator</p>
  
  <div style="margin: 10px 0;">
    <a href="./" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">简体中文</a> | 
    <a href="README_en.html" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">English</a> | 
    <a href="#readme" style="padding: 5px 10px; background: #333; border-radius: 4px; text-decoration: none; color: #fff; font-weight: bold;">Español</a> | 
    <a href="README_pt.html" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">Português</a>
  </div>
</div>

> **Título del Artículo**: BMSFormer: An efficient deep learning model for online state-of-health estimation...  
> **Revista**: Energy (2024, Vol.313, 134030)  
> **Modelo Principal**: BMSFormer (Atención de Fusión Local-Global + Convolución Separable en Profundidad)  
> **Ventaja Clave**: Mantiene una precisión de predicción SOTA mientras reduce significativamente la complejidad computacional (Complejidad Lineal).

## 🔍 Problemas Centrales
La estimación actual del estado de salud (SOH) de baterías de iones de litio enfrenta un dilema entre "Precisión" y "Eficiencia":
- **Modelos Ligeros Tradicionales** (ej. LSTM, SVM): Bajo costo computacional pero precisión insuficiente para datos no lineales e inestables.
- **Modelos Profundos Modernos** (ej. Transformers, CNNs): Alta precisión pero dependen de estructuras pesadas, lo que dificulta su implementación en Sistemas de Gestión de Baterías (BMS) con recursos limitados.
- **El Cuello de Botella Softmax**: La autoatención tradicional de Transformer tiene una complejidad computacional de $O(N^2)$, extremadamente lenta para secuencias largas.

## 💡 Solución Innovadora: BMSFormer
El artículo propone un modelo de aprendizaje profundo ligero y de alta eficiencia llamado **BMSFormer**. El flujo de trabajo incluye: Adquisición de datos de segmentos de alta frecuencia -> Ingeniería de características (Extracción de HI) -> Entrenamiento del modelo -> Evaluación.

> 📊 **Resumen de la Metodología BMSFormer**
> ![Diagrama de Flujo](assets/fig1.jpg)
> *Esta figura ilustra el ciclo completo desde la Adquisición de Datos (Paso 1), Ingeniería de Características (Paso 2), Entrenamiento (Paso 3), hasta la Evaluación (Paso 4). El núcleo implica extraer Indicadores de Salud (HIs) altamente correlacionados de segmentos de carga/descarga.*

### Módulos Técnicos Principales
1.  **Módulo LGFA (Atención de Fusión Local-Global)**:
    -   **Innovación**: Reemplaza la Atención Softmax tradicional con Atención Lineal basada en ReLU.
    -   **Efecto**: Reduce la complejidad computacional de $O(N^2)$ a $O(N)$, acelerando significativamente el procesamiento de secuencias largas.
    -   **Fusión**: Integra el módulo DSConv-S para mejorar la sensibilidad a características locales.

> 📊 **Comparación de Mecanismos de Atención**
> ![Comparación de Atención](assets/fig6.jpg)
> *La comparación muestra (a) Atención Global Softmax Tradicional, (b) Atención Lineal, y (c) El módulo LGFA propuesto. LGFA logra una fusión de complejidad lineal de características locales y globales.*

2.  **Convolución Separable en Profundidad Multiescala (DSConv)**:
    -   Diseño de módulos **DSConv-S** (núcleo pequeño) y **DSConv-L** (núcleo grande).
    -   Reduce significativamente los parámetros y FLOPs comparado con la convolución estándar.

> 📊 **Arquitectura de BMSFormer**
> ![Arquitectura del Modelo](assets/fig4.jpg)
> *Ilustración detallada de la estructura BMSFormer, incluyendo el módulo LGFA, módulo DSConv-L y el apilamiento de bloques.*

## 📈 Experimentos y Resultados
El artículo validó el modelo en tres conjuntos de datos públicos principales: **Oxford**, **NASA** y **CALCE**.

- **Mejora de Precisión**: Comparado con CNN-Transformer, LSTM, etc., BMSFormer tiene el mejor rendimiento en métricas RMSE, MAE y MAPE.
- **Eficiencia Impresionante**:
    -   Tiempo de entrenamiento reducido aproximadamente un **21.37%**.
    -   Huella de almacenamiento extremadamente baja y estable.

> 📊 **Comparación de Tamaño de Almacenamiento**
> ![Comparación de Almacenamiento](assets/fig8.jpg)
> *Esta figura muestra que bajo varias combinaciones de hiperparámetros, BMSFormer (Rojo) mantiene consistentemente el tamaño de almacenamiento más bajo y estable en comparación con otros.*

## 📚 Referencias
- **Cita**: X. Li, M. Zhao, S. Zhong, et al. BMSFormer: An efficient deep learning model for online state-of-health estimation of lithium-ion batteries under high-frequency early SOC data with strong correlated single health indicator[J]. Energy, 2024, 313: 134030.
- **Fuentes de Datos**: Oxford Battery Dataset, NASA Prognostics Repository, CALCE Battery Group.
- **PDF del artículo**: <a href="pdf/BMSFormer_Lee2_pure.pdf" style="color: #0078d4; text-decoration: none; font-weight: 500;">📄 BMSFormer_Lee2_pure.pdf</a> (Haz clic para ver/descargar)

<br>

<div align="center">
  <p>© 2026 Tech Blog Notes | Fuente: <a href="https://doi.org/10.1016/j.energy.2024.134030">Elsevier Energy</a></p>
  <br>
  <a href="./">简体中文</a> | 
  <a href="README_en.html">English</a> | 
  <a href="#readme">Español</a> | 
  <a href="README_pt.html">Português</a>
</div>
