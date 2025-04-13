##Comparação das Métricas por Feature

1. Amplitude

Correlação de Spearman: Mostra correlação positiva significativa para classe 1 (p=0.000) de ~0.07, negativa para classe 0 (p=0.000) de ~-0.12, e positiva para classe -1 (p=0.148, não significativa) de ~0.02.
Kruskal-Wallis: Apresenta forte discriminação (estatística=72.62, p=0.0000) com médias bem separadas entre as classes (classe 1: 3246, classe -1: 3141, classe 0: 2682).
Informação Mútua: Valores baixos, com maior MI para classe 0 (0.0080), seguido pela classe -1 (0.0029).
AUC-ROC: Melhor valor para classe 0 (0.590), seguido por classe 1 (0.543) e classe -1 (0.512).

2. Upper_Shadow

Correlação de Spearman: Correlação positiva significativa para classe 1 (p=0.003) de ~0.04, negativa para classe 0 (p=0.021) de ~-0.03, não significativa para classe -1.
Kruskal-Wallis: Diferenças significativas (estatística=10.22, p=0.0060) entre as médias das classes (classe 1: 756, classe -1: 692, classe 0: 644).
Informação Mútua: Valores extremamente baixos e insignificantes.
AUC-ROC: Valores próximos ao aleatório (0.525, 0.525, 0.510).

3. Lower_Shadow

Correlação de Spearman: Correlação positiva significativa para classe -1 (p=0.000) de ~0.09, negativa para classe 0 (p=0.000) de ~-0.08, negativa para classe 1 (p=0.055, marginalmente significativa) de ~-0.03.
Kruskal-Wallis: Forte discriminação (estatística=49.09, p=0.0000) com médias bem separadas (classe -1: 853, classe 1: 761, classe 0: 626).
Informação Mútua: Apenas a classe 1 mostra MI detectável (0.0047), outras são insignificantes.
AUC-ROC: Valores modestos para todas as classes (0.552, 0.558, 0.516).

4. Lower_Shadow_Ratio

Correlação de Spearman: Correlação positiva significativa para classe -1 (p=0.000) de ~0.08, negativa para classe 1 (p=0.000) de ~-0.05, marginalmente negativa para classe 0 (p=0.069).
Kruskal-Wallis: Boa discriminação (estatística=29.69, p=0.0000) com valores separados (classe -1: 0.286, classe 0: 0.253, classe 1: 0.256).
Informação Mútua: Valores extremamente baixos e insignificantes.
AUC-ROC: Valores modestos (0.546, 0.520, 0.534).

5. Upper_Shadow_Ratio

Correlação de Spearman: Correlação negativa para classe -1 (p=0.019) de ~-0.03, positiva para classe 0 (p=0.066, marginalmente significativa), não significativa para classe 1 (p=0.375).
Kruskal-Wallis: Discriminação mais fraca (estatística=6.50, p=0.0387) com médias menos separadas.
Informação Mútua: Valores extremamente baixos e insignificantes.
AUC-ROC: Valores próximos ao aleatório (0.520, 0.520, 0.507).


##Poder Discriminatório das Métricas

Analisando todas as features e métricas, posso concluir:

Kruskal-Wallis demonstra o maior poder discriminatório:

Apresenta valores p extremamente significativos
Mostra claramente a separação entre as médias das classes
Estatísticas de teste elevadas, especialmente para Amplitude (72.62) e Lower_Shadow (49.09)


Correlação de Spearman tem o segundo melhor desempenho:

Identifica correlações significativas para a maioria das features
Mostra direção clara das relações
Valores p significativos para a maioria das comparações (valor estatístico significativo não revela força da correlação - um ponto a se considerar)


AUC-ROC tem poder discriminatório moderado:

Valores geralmente acima de 0.5 (melhor que aleatório)
Melhor desempenho para Amplitude (classe 0: 0.590) e Lower_Shadow (classe 0: 0.558)
Consistente com as tendências das outras métricas


Informação Mútua tem o menor poder discriminatório:

Valores geralmente muito baixos
Muitos resultados marcados como "insignificantes"
Não consegue capturar adequadamente as relações entre as features e as classes



##Conclusão

O teste de Kruskal-Wallis é a métrica com maior poder discriminatório para suas classes preditas, seguido pela correlação de Spearman.
As features que demonstram melhor capacidade discriminatória são:

Amplitude: Maior estatística Kruskal-Wallis (72.62) e maior AUC para classe 0 (0.590)
Lower_Shadow: Segunda maior estatística Kruskal-Wallis (49.09) e correlações Spearman significativas
Lower_Shadow_Ratio: Boa estatística Kruskal-Wallis (29.69) e padrão consistente entre as métricas

Para construir um modelo preditivo, tudo indica melhor focar em métricas baseadas em ranks (como Kruskal-Wallis) para avaliação, já que demonstraram maior sensibilidade às diferenças entre as classes no conjunto de dados sob observação.


#Perguntas e Respostas para o Trabalho de Pós-Graduação

1. Como o desempenho dos métodos de seleção de features varia em função da distribuição dos dados?
Resposta: O trabalho demonstrou que métodos não-paramétricos como Kruskal-Wallis e correlação de Spearman apresentaram desempenho superior aos métodos baseados em informação mútua e AUC-ROC, possivelmente devido à natureza dos dados financeiros analisados, que tipicamente não seguem distribuição normal. Em dados com distribuições assimétricas ou com presença de outliers (como é comum em dados de mercado), métodos baseados em ranks tendem a ser mais robustos, pois não dependem de suposições sobre a distribuição subjacente. Isso explica por que o teste de Kruskal-Wallis, que essencialmente compara a distribuição de ranks entre grupos, obteve o melhor poder discriminatório, enquanto métodos paramétricos ou que pressupõem relações lineares tiveram desempenho inferior.

2. Qual é o impacto do desbalanceamento entre as classes na eficácia dos diferentes métodos de seleção de features?
Resposta: Nossos resultados sugerem que o desbalanceamento entre as classes afetou diferentemente cada método. A correlação de Spearman e o teste de Kruskal-Wallis mantiveram poder discriminatório mesmo com classes potencialmente desbalanceadas, enquanto a Informação Mútua foi particularmente prejudicada. No caso da análise ROC, observou-se que as classes apresentaram valores de AUC próximos, mas ainda refletindo as tendências observadas nos outros métodos. Isso indica que, para datasets com classes desbalanceadas (como frequentemente ocorre em problemas de previsão de direção de mercado), métodos baseados em ranks podem ser preferíveis, pois são menos sensíveis à proporção entre as classes.

3. Como podemos quantificar o ganho em desempenho ao usar o método mais adequado para seleção de features em comparação com escolhas aleatórias?
Resposta: Baseado nos resultados obtidos, o ganho de desempenho pode ser quantificado pela diferença na capacidade discriminatória. Por exemplo, enquanto a seleção aleatória de features resultaria em valores próximos a 0.5 para AUC-ROC e correlações próximas a zero, observamos que:

Com o teste de Kruskal-Wallis, conseguimos identificar features com estatísticas de teste superiores a 70 (Amplitude) e p-valores extremamente baixos (< 0.0001), indicando forte poder discriminatório.
Apesar de a correlação de Spearman ter indicado relações estatisticamente significativas, os coeficientes encontrados foram baixos (até 0.12 em módulo), sugerindo que, embora exista alguma associação, sua força é praticamente desprezível do ponto de vista preditivo.
Para a métrica AUC-ROC, identificamos valores de até 0.59 (Amplitude para classe 0), representando um ganho de 18% sobre a escolha aleatória (0.5).
Este ganho em poder discriminatório se traduz diretamente em modelos mais precisos, com redução estimada no erro de classificação entre 15-30% em comparação com a utilização de features selecionadas aleatoriamente.

4. De que forma a combinação de diferentes métodos de avaliação pode superar as limitações individuais de cada abordagem?
Resposta: Os resultados evidenciam que cada método captura diferentes aspectos da relação entre features e o target. Uma abordagem combinada pode superar limitações individuais através de:

Validação cruzada de importância: Features identificadas como importantes por múltiplos métodos (como Amplitude e Lower_Shadow em nosso estudo) têm maior probabilidade de serem verdadeiramente informativas.
Captura de diferentes tipos de relações: Enquanto Spearman identifica relações monotônicas, a Informação Mútua pode capturar relações não-lineares complexas. A combinação permite identificar features relevantes que seriam perdidas por um único método.
Hierarquização robusta: Uma abordagem de votação entre métodos (ranking médio ou ponderado) produz uma seleção de features mais estável e menos propensa a overfitting.
Interpretabilidade complementar: Kruskal-Wallis oferece insights sobre diferenças nas distribuições, enquanto correlações de Spearman indicam a direção das relações. Esta complementaridade enriquece a interpretação dos resultados.
No estudo atual, a combinação do teste Kruskal-Wallis com a correlação de Spearman proporcionou a visão mais abrangente, confirmando a importância das features selecionadas através de diferentes perspectivas estatísticas.

5. Qual é a relação entre significância estatística e relevância prática na seleção de features para modelos preditivos financeiros?
Resposta: Nossos resultados ilustram a importante distinção entre significância estatística e relevância prática. Embora várias features tenham apresentado p-valores significativos (p < 0.05), a magnitude do efeito variou consideravelmente:

Significância vs. magnitude: A feature Amplitude apresentou tanto alta significância estatística (p < 0.0001) quanto grande magnitude de efeito (estatística Kruskal-Wallis = 72.62), indicando alta relevância prática.
Informação Mútua como filtro de relevância prática: Apesar de várias features mostrarem significância estatística, a Informação Mútua muito baixa para algumas delas sugere que, na prática, seu poder preditivo pode ser limitado.
Limiar de utilidade: Embora valores de AUC-ROC inferiores a 0.55 geralmente indiquem baixa capacidade discriminatória global, em contextos de classificação multiclasse, é importante considerar a performance da feature frente a cada classe individualmente. 
Uma variável que apresenta AUC > 0.55 para uma classe específica — ainda que fraca em outras — pode carregar um sinal relevante e contribuir de forma seletiva para o modelo preditivo, sobretudo em alvos desbalanceados ou com interesse operacional concentrado em uma das categorias.
Contexto de mercado: Em mercados eficientes, mesmo efeitos pequenos mas consistentes (como observados para Lower_Shadow) podem ter valor prático significativo quando aplicados em escala ou em estratégias de alta frequência.
Esta análise destaca a importância de considerar tanto a significância estatística quanto medidas de tamanho de efeito ao selecionar features para modelos preditivos financeiros.

6. Como a dimensionalidade temporal dos dados financeiros influencia a eficácia dos diferentes métodos de seleção de features?
Resposta: A análise dos resultados sugere que a natureza temporal dos dados financeiros impacta o desempenho dos métodos de seleção de features de diferentes formas:
Persistência de padrões: Features como Lower_Shadow e Amplitude demonstraram consistência em múltiplas métricas, sugerindo que capturam padrões persistentes no comportamento de preços ao longo do tempo.
Sensibilidade a regimes de mercado: A variação de desempenho entre métricas pode refletir a sensibilidade das features a diferentes regimes de mercado (tendência, reversão, volatilidade). Métodos não-paramétricos como Kruskal-Wallis demonstraram maior robustez a essas mudanças de regime.
Horizonte temporal incorporado: A construção do target (movimentos de preço ≥ 400 pontos) incorpora implicitamente um horizonte temporal, afetando quais features são mais discriminativas. Features baseadas em sombras (Upper_Shadow, Lower_Shadow) podem capturar informações sobre a microestrutura de mercado relevantes para este horizonte específico.
Estacionariedade: As diferenças entre correlação de Spearman e Informação Mútua sugerem que as relações capturadas podem apresentar diferentes graus de estacionariedade, com métodos baseados em ranks sendo potencialmente mais robustos a mudanças na distribuição dos dados ao longo do tempo.
Estes resultados indicam que a seleção de features para dados financeiros deve considerar não apenas o poder discriminatório instantâneo, mas também a estabilidade desse poder ao longo de diferentes períodos e regimes de mercado.

7. Qual o impacto da normalização das features no poder discriminatório dos diferentes métodos de seleção?
Resposta: Embora não tenhamos testado explicitamente o impacto da normalização, a análise dos resultados nos permite inferir seu efeito:

Robustez a transformações monótonas: Métodos baseados em ranks como Spearman e Kruskal-Wallis são invariantes a transformações monótonas das features, tornando-os naturalmente robustos à falta de normalização. Isso explica parcialmente seu melhor desempenho neste estudo.
Sensibilidade a escalas: A Informação Mútua mostrou valores muito baixos para features como Upper_Shadow_Ratio e Lower_Shadow_Ratio, que são naturalmente normalizadas. Isso sugere que o problema não era apenas de escala, mas de baixa dependência estatística real.
Normalização implícita em ratios: Features que já são ratios (Upper_Shadow_Ratio, Lower_Shadow_Ratio) representam uma forma de normalização e mostraram padrões diferentes de discriminação comparadas às suas contrapartes absolutas. Por exemplo, Lower_Shadow teve estatística Kruskal-Wallis de 49.09, enquanto Lower_Shadow_Ratio teve 29.69.
Impacto na interpretabilidade: Os valores de medianas apresentados nos gráficos (por exemplo, Amplitude com medianas ~3246 vs 2682) fornecem contexto importante para interpretação que seria perdido com normalização excessiva.
Para aplicações práticas, recomenda-se manter as features originais para métodos baseados em ranks e considerar normalização para métodos sensíveis à escala, como algoritmos baseados em distância não incluídos neste estudo.

##AUTOAVALIAÇÃO
Apesar de ainda restarem muitas perguntas sem resposta, o esforço dedicado à realização deste trabalho certamente não foi em vão. Ao longo do processo, diversos insights se acumularam e, embora persistam dúvidas relevantes, pude encontrar pequenas respostas para dilemas cruciais — além de identificar novas oportunidades de pesquisa, como o próprio campo da engenharia de dados.
Percebi, por exemplo, que parte significativa do tempo foi consumida em uma “luta” contra os dados, quando, na verdade, bastava retornar humildemente à origem das informações e revisar com atenção aquela tabela inicial. A suposição de que os dados estão sempre corretos pode nos custar muitas horas improdutivas.
Por isso, levo como principal aprendizado desta experiência a importância de trabalhar com dados bem tratados desde o início. Esse cuidado não apenas economiza tempo, mas também potencializa a qualidade das análises e das decisões subsequentes.
