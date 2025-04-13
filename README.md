# MPV-PUC
🎯 Objetivo do Trabalho
Este projeto tem como foco avaliar e comparar o poder discriminatório de diferentes métodos estatísticos na seleção de features contínuas voltadas para a predição de alvos categóricos no contexto de dados financeiros.
O estudo busca responder a questões centrais sobre a eficácia de cada abordagem estatística na construção de modelos preditivos robustos.

📌 Metas Específicas
Comparar métodos estatísticos — Investigar qual método apresenta maior capacidade discriminatória para selecionar features preditivas relevantes:

Correlação de Spearman

Teste de Kruskal-Wallis

Informação Mútua

Curva ROC (AUC)

Avaliar atributos derivados de preços — Identificar quais variáveis como:

Amplitude do candle

Sombras superiores e inferiores

Razões entre corpo e sombras
possuem maior poder preditivo para movimentos significativos de preço.

Relacionar tipos de variáveis — Analisar como diferentes métodos capturam relações entre features contínuas e um target categórico multinível:

-1: Candle de Venda (≤ -400 pontos)

0: Candle Neutro (entre -400 e 400 pontos)

1: Candle de Compra (≥ 400 pontos)

Estabelecer critérios objetivos — Refletir sobre os critérios mais eficazes para seleção de features em modelos preditivos, considerando:

Significância estatística

Relevância prática

Construir uma metodologia sistemática — Desenvolver uma abordagem reutilizável de avaliação e seleção de features com aplicação em modelos de trading algorítmico e sistemas de suporte à decisão.
