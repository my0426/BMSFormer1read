<div align="center">
  <img src="https://img.shields.io/badge/Language-中文-red.svg" alt="Chinês">
  <img src="https://img.shields.io/badge/Language-English-blue.svg" alt="Inglês">
  <img src="https://img.shields.io/badge/Language-Español-yellow.svg" alt="Espanhol">
  <img src="https://img.shields.io/badge/Language-Português-green.svg" alt="Português">
  <img src="https://img.shields.io/badge/Model-BMSFormer-orange" alt="Modelo">
  <img src="https://img.shields.io/badge/Task-SOH_Estimation-blueviolet" alt="Tarefa">
  
  <h1>📚 Notas de Leitura: BMSFormer - Um Modelo Eficiente de Estimativa de SOH para BMS com Recursos Limitados</h1>
  <p>Paper: BMSFormer: An efficient deep learning model for online state-of-health estimation of lithium-ion batteries under high-frequency early SOC data with strong correlated single health indicator</p>
  
  <div style="margin: 10px 0;">
    <a href="./" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">简体中文</a> | 
    <a href="README_en.html" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">English</a> | 
    <a href="README_es.html" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">Español</a> | 
    <a href="#readme" style="padding: 5px 10px; background: #333; border-radius: 4px; text-decoration: none; color: #fff; font-weight: bold;">Português</a>
  </div>
</div>

> [cite_start]**Título do Artigo**: BMSFormer: An efficient deep learning model for online state-of-health estimation... [cite: 6]  
> [cite_start]**Revista**: Energy (2024, Vol.313, 134030) [cite: 2]  
> [cite_start]**Modelo Principal**: BMSFormer (Atenção de Fusão Local-Global + Convolução Separável em Profundidade) [cite: 21, 22]  
> [cite_start]**Vantagem Chave**: Mantém precisão de previsão SOTA enquanto reduz significativamente a complexidade computacional (Complexidade Linear)[cite: 24].

## 🔍 Problemas Centrais
A estimativa atual do estado de saúde (SOH) de baterias de íon-lítio enfrenta um dilema entre "Precisão" e "Eficiência":
- [cite_start]**Modelos Leves Tradicionais** (ex: LSTM, SVM): Baixo custo computacional, mas precisão insuficiente para dados não lineares e instáveis[cite: 33].
- [cite_start]**Modelos Profundos Modernos** (ex: Transformers, CNNs): Alta precisão, mas dependem de estruturas pesadas, dificultando a implementação em Sistemas de Gerenciamento de Baterias (BMS) com recursos limitados[cite: 34, 76].
- [cite_start]**O Gargalo Softmax**: A autoatenção tradicional do Transformer tem complexidade computacional de $O(N^2)$, extremamente lenta para sequências longas[cite: 565].

## 💡 Solução Inovadora: BMSFormer
O artigo propõe um modelo de aprendizado profundo leve e de alta eficiência chamado **BMSFormer**. O fluxo de trabalho inclui: Aquisição de dados de segmentos de alta frequência -> Engenharia de recursos (Extração de HI) -> Treinamento do modelo -> Avaliação.

> 📊 **Visão Geral da Metodologia BMSFormer**
> 
> *(Insira aqui a **Fig. 1** do artigo: Flowchart of developed SOH estimation approach)*
> ![Fluxograma da Metodologia](assets/fig1.jpg)
> *Esta figura ilustra o ciclo completo desde a Aquisição de Dados (Etapa 1), Engenharia de Recursos (Etapa 2), Treinamento (Etapa 3), até a Avaliação (Etapa 4). [cite_start]O núcleo envolve extrair Indicadores de Saúde (HIs) altamente correlacionados de segmentos de carga/descarga.* [cite: 89]

### Módulos Técnicos Principais
1.  [cite_start]**Módulo LGFA (Atenção de Fusão Local-Global)**[cite: 21, 530]:
    -   **Inovação**: Substitui a Atenção Softmax tradicional por Atenção Linear baseada em ReLU.
    -   **Efeito**: Reduz a complexidade computacional de $O(N^2)$ para $O(N)$, acelerando significativamente o processamento de sequências longas.
    -   **Fusão**: Integra o módulo DSConv-S para aumentar a sensibilidade a características locais.

> 📊 **Comparação de Mecanismos de Atenção**
> 
> *(Insira aqui a **Fig. 6** do artigo: Difference between traditional Softmax...)*
> ![Comparação de Atenção](assets/fig6.jpg)
> *A comparação mostra (a) Atenção Global Softmax Tradicional ($O(N^2)$), (b) Atenção Linear, e (c) O módulo LGFA proposto. [cite_start]LGFA alcança fusão de complexidade linear de características locais e globais.* [cite: 641]

2.  [cite_start]**Convolução Separável em Profundidade Multiescala (DSConv)**[cite: 22, 428]:
    -   Design de módulos **DSConv-S** (núcleo pequeno) e **DSConv-L** (núcleo grande).
    -   Reduz significativamente os parâmetros e FLOPs em comparação com a convolução padrão.

> 📊 **Arquitetura do BMSFormer**
> 
> *(Insira aqui a **Fig. 4** do artigo: Framework of BMSFormer)*
> ![Arquitetura do Modelo](assets/fig4.jpg)
> [cite_start]*Ilustração detalhada da estrutura BMSFormer, incluindo o módulo LGFA, módulo DSConv-L e o empilhamento de blocos.* [cite: 480]

## 📈 Experimentos e Resultados
[cite_start]O artigo validou o modelo em três principais conjuntos de dados públicos: **Oxford**, **NASA** e **CALCE**[cite: 23].

- [cite_start]**Melhoria de Precisão**: Comparado com CNN-Transformer, LSTM, etc., o BMSFormer tem o melhor desempenho nas métricas RMSE, MAE e MAPE[cite: 686].
- **Eficiência Impressionante**:
    -   [cite_start]Tempo de treinamento reduzido em aproximadamente **21.37%**[cite: 905].
    -   Uso de armazenamento extremamente baixo e estável.

> 📊 **Comparação de Tamanho de Armazenamento**
> 
> *(Insira aqui a **Fig. 8** do artigo: Storage size of five models...)*
> ![Comparação de Armazenamento](assets/fig8.jpg)
> [cite_start]*Esta figura mostra que, sob várias combinações de hiperparâmetros, o BMSFormer (Vermelho) mantém consistentemente o menor e mais estável tamanho de armazenamento em comparação com outros.* [cite: 948]

## 📚 Referências
- **Citação**: Li, X., Zhao, M., et al. "BMSFormer: An efficient deep learning model for online state-of-health estimation..." Energy 313 (2024): 134030.
- **Fontes de Dados**: Oxford Battery Dataset, NASA Prognostics Repository, CALCE Battery Group.

<br>

<div align="center">
  <p>© 2026 Tech Blog Notes | Fonte: <a href="https://doi.org/10.1016/j.energy.2024.134030">Elsevier Energy</a></p>
  <br>
  <a href="./">简体中文</a> | 
  <a href="README_en.html">English</a> | 
  <a href="README_es.html">Español</a> | 
  <a href="#readme">Português</a>
</div>
