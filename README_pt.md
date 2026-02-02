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

> **Título do Artigo**: BMSFormer: An efficient deep learning model for online state-of-health estimation...  
> **Revista**: Energy (2024, Vol.313, 134030)  
> **Modelo Principal**: BMSFormer (Atenção de Fusão Local-Global + Convolução Separável em Profundidade)  
> **Vantagem Chave**: Mantém precisão de previsão SOTA enquanto reduz significativamente a complexidade computacional (Complexidade Linear).

## 🔍 Problemas Centrais
A estimativa atual do estado de saúde (SOH) de baterias de íon-lítio enfrenta um dilema entre "Precisão" e "Eficiência":
- **Modelos Leves Tradicionais** (ex: LSTM, SVM): Baixo custo computacional, mas precisão insuficiente para dados não lineares e instáveis.
- **Modelos Profundos Modernos** (ex: Transformers, CNNs): Alta precisão, mas dependem de estruturas pesadas, dificultando a implementação em Sistemas de Gerenciamento de Baterias (BMS) com recursos limitados.
- **O Gargalo Softmax**: A autoatenção tradicional do Transformer tem complexidade computacional de $O(N^2)$, extremamente lenta para sequências longas.

## 💡 Solução Inovadora: BMSFormer
O artigo propõe um modelo de aprendizado profundo leve e de alta eficiência chamado **BMSFormer**. O fluxo de trabalho inclui: Aquisição de dados de segmentos de alta frequência -> Engenharia de recursos (Extração de HI) -> Treinamento do modelo -> Avaliação.

> 📊 **Visão Geral da Metodologia BMSFormer**
> ![Fluxograma da Metodologia](assets/fig1.jpg)
> *Esta figura ilustra o ciclo completo desde a Aquisição de Dados (Etapa 1), Engenharia de Recursos (Etapa 2), Treinamento (Etapa 3), até a Avaliação (Etapa 4). O núcleo envolve extrair Indicadores de Saúde (HIs) altamente correlacionados de segmentos de carga/descarga.*

### Módulos Técnicos Principais
1.  **Módulo LGFA (Atenção de Fusão Local-Global)**:
    -   **Inovação**: Substitui a Atenção Softmax tradicional por Atenção Linear baseada em ReLU.
    -   **Efeito**: Reduz a complexidade computacional de $O(N^2)$ para $O(N)$, acelerando significativamente o processamento de sequências longas.
    -   **Fusão**: Integra o módulo DSConv-S para aumentar a sensibilidade a características locais.

> 📊 **Comparação de Mecanismos de Atenção**
> ![Comparação de Atenção](assets/fig6.jpg)
> *A comparação mostra (a) Atenção Global Softmax Tradicional, (b) Atenção Linear, e (c) O módulo LGFA proposto. LGFA alcança fusão de complexidade linear de características locais e globais.*

2.  **Convolução Separável em Profundidade Multiescala (DSConv)**:
    -   Design de módulos **DSConv-S** (núcleo pequeno) e **DSConv-L** (núcleo grande).
    -   Reduz significativamente os parâmetros e FLOPs em comparação com a convolução padrão.

> 📊 **Arquitetura do BMSFormer**
> ![Arquitetura do Modelo](assets/fig4.jpg)
> *Ilustração detalhada da estrutura BMSFormer, incluindo o módulo LGFA, módulo DSConv-L e o empilhamento de blocos.*

## 📈 Experimentos e Resultados
O artigo validou o modelo em três principais conjuntos de dados públicos: **Oxford**, **NASA** e **CALCE**.

- **Melhoria de Precisão**: Comparado com CNN-Transformer, LSTM, etc., o BMSFormer tem o melhor desempenho nas métricas RMSE, MAE e MAPE.
- **Eficiência Impressionante**:
    -   Tempo de treinamento reduzido em aproximadamente **21.37%**.
    -   Uso de armazenamento extremamente baixo e estável.

> 📊 **Comparação de Tamanho de Armazenamento**
> ![Comparação de Armazenamento](assets/fig8.jpg)
> *Esta figura mostra que, sob várias combinações de hiperparâmetros, o BMSFormer (Vermelho) mantém consistentemente o menor e mais estável tamanho de armazenamento em comparação com outros.*

## 📚 Referências
- **Citação**: X. Li, M. Zhao, S. Zhong, et al. BMSFormer: An efficient deep learning model for online state-of-health estimation of lithium-ion batteries under high-frequency early SOC data with strong correlated single health indicator[J]. Energy, 2024, 313: 134030.
- **Fontes de Dados**: Oxford Battery Dataset, NASA Prognostics Repository, CALCE Battery Group.
- **PDF do artigo**: <a href="pdf/BMSFormer_Lee2_pure.pdf" style="color: #0078d4; text-decoration: none; font-weight: 500;">📄 BMSFormer_Lee2_pure.pdf</a> (Clique para visualizar/baixar)

<br>

<div align="center">
  <p>© 2026 Tech Blog Notes | Fonte: <a href="https://doi.org/10.1016/j.energy.2024.134030">Elsevier Energy</a></p>
  <br>
  <a href="./">简体中文</a> | 
  <a href="README_en.html">English</a> | 
  <a href="README_es.html">Español</a> | 
  <a href="#readme">Português</a>
</div>
