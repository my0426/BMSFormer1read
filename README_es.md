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

> [cite_start]**Título del Artículo**: BMSFormer: An efficient deep learning model for online state-of-health estimation... [cite: 6]  
> [cite_start]**Revista**: Energy (2024, Vol.313, 134030) [cite: 2]  
> [cite_start]**Modelo Principal**: BMSFormer (Atención de Fusión Local-Global + Convolución Separable en Profundidad) [cite: 21, 22]  
> [cite_start]**Ventaja Clave**: Mantiene una precisión de predicción SOTA mientras reduce significativamente la complejidad computacional (Complejidad Lineal)[cite: 24].

## 🔍 Problemas Centrales
La estimación actual del estado de salud (SOH) de baterías de iones de litio enfrenta un dilema entre "Precisión" y "Eficiencia":
- [cite_start]**Modelos Ligeros Tradicionales** (ej. LSTM, SVM): Bajo costo computacional pero precisión insuficiente para datos no lineales e inestables[cite: 33].
- [cite_start]**Modelos Profundos Modernos** (ej. Transformers, CNNs): Alta precisión pero dependen de estructuras pesadas, lo que dificulta su implementación en Sistemas de Gestión de Baterías (BMS) con recursos limitados[cite: 34, 76].
- [cite_start]**El Cuello de Botella Softmax**: La autoatención tradicional de Transformer tiene una complejidad computacional de $O(N^2)$, extremadamente lenta para secuencias largas[cite: 565].

## 💡 Solución Innovadora: BMSFormer
El artículo propone un modelo de aprendizaje profundo ligero y de alta eficiencia llamado **BMSFormer**. El flujo de trabajo incluye: Adquisición de datos de segmentos de alta frecuencia -> Ingeniería de características (Extracción de HI) -> Entrenamiento del modelo -> Evaluación.

> 📊 **Resumen de la Metodología BMSFormer**
> 
> *(Inserte aquí la **Fig. 1** del artículo: Flowchart of developed SOH estimation approach)*
> ![Diagrama de Flujo](assets/fig1.jpg)
> *Esta figura ilustra el ciclo completo desde la Adquisición de Datos (Paso 1), Ingeniería de Características (Paso 2), Entrenamiento (Paso 3), hasta la Evaluación (Paso 4). [cite_start]El núcleo implica extraer Indicadores de Salud (HIs) altamente correlacionados de segmentos de carga/descarga.* [cite: 89]

### Módulos Técnicos Principales
1.  [cite_start]**Módulo LGFA (Atención de Fusión Local-Global)**[cite: 21, 530]:
    -   **Innovación**: Reemplaza la Atención Softmax tradicional con Atención Lineal basada en ReLU.
    -   **Efecto**: Reduce la complejidad computacional de $O(N^2)$ a $O(N)$, acelerando significativamente el procesamiento de secuencias largas.
    -   **Fusión**: Integra el módulo DSConv-S para mejorar la sensibilidad a características locales.

> 📊 **Comparación de Mecanismos de Atención**
> 
> *(Inserte aquí la **Fig. 6** del artículo: Difference between traditional Softmax...)*
> ![Comparación de Atención](assets/fig6.jpg)
> *La comparación muestra (a) Atención Global Softmax Tradicional ($O(N^2)$), (b) Atención Lineal, y (c) El módulo LGFA propuesto. [cite_start]LGFA logra una fusión de complejidad lineal de características locales y globales.* [cite: 641]

2.  [cite_start]**Convolución Separable en Profundidad Multiescala (DSConv)**[cite: 22, 428]:
    -   Diseño de módulos **DSConv-S** (núcleo pequeño) y **DSConv-L** (núcleo grande).
    -   Reduce significativamente los parámetros y FLOPs comparado con la convolución estándar.

> 📊 **Arquitectura de BMSFormer**
> 
> *(Inserte aquí la **Fig. 4** del artículo: Framework of BMSFormer)*
> ![Arquitectura del Modelo](assets/fig4.jpg)
> [cite_start]*Ilustración detallada de la estructura BMSFormer, incluyendo el módulo LGFA, módulo DSConv-L y el apilamiento de bloques.* [cite: 480]

## 📈 Experimentos y Resultados
[cite_start]El artículo validó el modelo en tres conjuntos de datos públicos principales: **Oxford**, **NASA** y **CALCE**[cite: 23].

- [cite_start]**Mejora de Precisión**: Comparado con CNN-Transformer, LSTM, etc., BMSFormer tiene el mejor rendimiento en métricas RMSE, MAE y MAPE[cite: 686].
- **Eficiencia Impresionante**:
    -   [cite_start]Tiempo de entrenamiento reducido aproximadamente un **21.37%**[cite: 905].
    -   Huella de almacenamiento extremadamente baja y estable.

> 📊 **Comparación de Tamaño de Almacenamiento**
> 
> *(Inserte aquí la **Fig. 8** del artículo: Storage size of five models...)*
> ![Comparación de Almacenamiento](assets/fig8.jpg)
> [cite_start]*Esta figura muestra que bajo varias combinaciones de hiperparámetros, BMSFormer (Rojo) mantiene consistentemente el tamaño de almacenamiento más bajo y estable en comparación con otros.* [cite: 948]

## 📚 Referencias
- **Cita**: Li, X., Zhao, M., et al. "BMSFormer: An efficient deep learning model for online state-of-health estimation..." Energy 313 (2024): 134030.
- **Fuentes de Datos**: Oxford Battery Dataset, NASA Prognostics Repository, CALCE Battery Group.

<br>

<div align="center">
  <p>© 2026 Tech Blog Notes | Fuente: <a href="https://doi.org/10.1016/j.energy.2024.134030">Elsevier Energy</a></p>
  <br>
  <a href="./">简体中文</a> | 
  <a href="README_en.html">English</a> | 
  <a href="#readme">Español</a> | 
  <a href="README_pt.html">Português</a>
</div>
