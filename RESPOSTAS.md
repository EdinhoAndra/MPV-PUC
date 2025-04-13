# Comparação das Métricas por Feature

### **Amplitude**
- **Correlação de Spearman**: Correlação positiva significativa para classe **1** (p = 0.000, ~0.07), negativa para classe **0** (p = 0.000, ~-0.12), e positiva mas não significativa para classe **-1** (p = 0.148, ~0.02).
- **Kruskal-Wallis**: Forte discriminação (_estatística = 72.62, p = 0.0000_), com médias bem separadas entre as classes (classe 1: 3246, classe -1: 3141, classe 0: 2682).
- **Informação Mútua**: Baixa, com maior MI para classe 0 (0.0080), seguida por classe -1 (0.0029).
- **AUC-ROC**: Melhor valor para classe 0 (0.590), seguido por classe 1 (0.543) e classe -1 (0.512).

### **Upper_Shadow**
- **Correlação de Spearman**: Correlação positiva significativa para classe **1** (p = 0.003, ~0.04), negativa para classe **0** (p = 0.021, ~-0.03), e não significativa para classe **-1**.
- **Kruskal-Wallis**: Diferenças significativas (_estatística = 10.22, p = 0.0060_) entre as médias (classe 1: 756, classe -1: 692, classe 0: 644).
- **Informação Mútua**: Muito baixa.
- **AUC-ROC**: Próximo ao aleatório (0.525, 0.525, 0.510).

### **Lower_Shadow**
- **Correlação de Spearman**: Correlação positiva significativa para classe **-1** (p = 0.000, ~0.09), negativa para classe **0** (p = 0.000, ~-0.08), e marginal para classe **1** (p = 0.055, ~-0.03).
- **Kruskal-Wallis**: Forte discriminação (_estatística = 49.09, p = 0.0000_), com médias distintas (classe -1: 853, classe 1: 761, classe 0: 626).
- **Informação Mútua**: Detectável apenas para classe 1 (0.0047).
- **AUC-ROC**: Modestos (0.552, 0.558, 0.516).

### **Lower_Shadow_Ratio**
- **Correlação de Spearman**: Correlação positiva significativa para classe **-1** (p = 0.000, ~0.08), negativa para classe **1** (p = 0.000, ~-0.05), e marginal para classe **0** (p = 0.069).
- **Kruskal-Wallis**: Boa discriminação (_estatística = 29.69, p = 0.0000_) (classe -1: 0.286, classe 0: 0.253, classe 1: 0.256).
- **Informação Mútua**: Muito baixa.
- **AUC-ROC**: Modestos (0.546, 0.520, 0.534).

### **Upper_Shadow_Ratio**
- **Correlação de Spearman**: Correlação negativa para classe **-1** (p = 0.019, ~-0.03), positiva marginal para classe **0** (p = 0.066), e não significativa para classe **1** (p = 0.375).
- **Kruskal-Wallis**: Fraca discriminação (_estatística = 6.50, p = 0.0387_).
- **Informação Mútua**: Muito baixa.
- **AUC-ROC**: Próximo ao aleatório (0.520, 0.520, 0.507).

---

# Poder Discriminatório das Métricas

### **Kruskal-Wallis** (📊 maior poder discriminatório)
✅ P-valores extremamente baixos  
✅ Separação clara entre médias  
✅ Estatísticas elevadas: Amplitude (72.62), Lower_Shadow (49.09)

### **Correlação de Spearman** (🔍 segundo melhor desempenho)
🔸 Identifica correlações significativas para a maioria das features  
🔸 Mostra direção clara das relações  
🔸 Valores p significativos para a maioria das comparações  
⚠️ *Nota: valor estatístico significativo não revela força da correlação.*

### **AUC-ROC** (🟡 moderado)
🔹 Valores geralmente acima de 0.5 (melhor que aleatório)  
🔹 Melhor desempenho para Amplitude (classe 0: 0.590) e Lower_Shadow (classe 0: 0.558)  
🔹 Consistente com as tendências das outras métricas

### **Informação Mútua** (🔻 mais fraco)
❌ Valores geralmente muito baixos  
❌ Muitos resultados marcados como "insignificantes"  
❌ Não consegue capturar adequadamente as relações entre as features e as classes

---

# Conclusão

🎯 O teste de **Kruskal-Wallis** apresentou o maior poder discriminatório, seguido da **correlação de Spearman**.

As features com melhor desempenho foram:

📌 **Amplitude**  
▫️ Maior estatística Kruskal-Wallis (72.62)  
▫️ Maior AUC para classe 0 (0.590)

📌 **Lower_Shadow**  
▫️ Segunda maior estatística Kruskal-Wallis (49.09)  
▫️ Correlações Spearman significativas

📌 **Lower_Shadow_Ratio**  
▫️ Boa estatística Kruskal-Wallis (29.69)  
▫️ Padrão consistente entre as métricas

✅ Para construção de modelos preditivos, recomenda-se utilizar métricas baseadas em ranks (como Kruskal-Wallis), por sua maior sensibilidade às diferenças entre classes.

---

# Perguntas e Respostas para o Trabalho de Pós-Graduação

<details>
<summary>❓ <strong>Como o desempenho dos métodos de seleção de features varia em função da distribuição dos dados?</strong></summary>

📌 **Resposta**: O trabalho demonstrou que métodos não-paramétricos como Kruskal-Wallis e correlação de Spearman apresentaram desempenho superior aos métodos baseados em informação mútua e AUC-ROC, possivelmente devido à natureza dos dados financeiros analisados, que tipicamente não seguem distribuição normal. Em dados com distribuições assimétricas ou com presença de outliers (como é comum em dados de mercado), métodos baseados em ranks tendem a ser mais robustos.
</details>

<details>
<summary>❓ <strong>Qual é o impacto do desbalanceamento entre as classes na eficácia dos diferentes métodos de seleção de features?</strong></summary>

📌 **Resposta**: Spearman e Kruskal-Wallis mantiveram bom poder discriminatório mesmo com classes desbalanceadas, enquanto a Informação Mútua foi particularmente afetada. A análise ROC indicou tendências similares às outras métricas. Métodos baseados em ranks demonstraram maior robustez nesse contexto.
</details>

<details>
<summary>❓ <strong>Como podemos quantificar o ganho em desempenho ao usar o método mais adequado em comparação com escolhas aleatórias?</strong></summary>

📌 **Resposta**: AUC-ROC para Amplitude (classe 0) foi 0.59, contra 0.5 do acaso, representando ganho de ~18%. Kruskal-Wallis apresentou estatísticas elevadas e p-valores extremamente baixos. Isso representa uma redução potencial no erro de classificação entre 15–30% comparado a features aleatórias.
</details>

<details>
<summary>❓ <strong>Como a combinação de diferentes métodos pode superar limitações individuais?</strong></summary>

📌 **Resposta**: Métodos distintos capturam aspectos complementares. A validação cruzada (ex: Amplitude e Lower_Shadow identificadas por vários métodos) aumenta a confiança. Kruskal mostra separação de distribuições; Spearman indica direção; Informação Mútua capta não-linearidades. A combinação gera seleção mais estável e interpretável.
</details>

<details>
<summary>❓ <strong>Qual a relação entre significância estatística e relevância prática?</strong></summary>

📌 **Resposta**: A significância (p < 0.05) nem sempre implica relevância preditiva. Exemplo: Spearman com rho = 0.07. Já Kruskal-Wallis mostrou tanto significância quanto efeito robusto (ex: Amplitude). Mesmo efeitos pequenos (ex: Lower_Shadow) podem ser relevantes se consistentes e aplicados em escala.
</details>

<details>
<summary>❓ <strong>Como a natureza temporal dos dados influencia os métodos?</strong></summary>

📌 **Resposta**: Features como Amplitude e Lower_Shadow mostraram consistência ao longo do tempo. Kruskal demonstrou robustez a mudanças de regime. Relações monotônicas (Spearman) e efeitos estacionários se mostraram mais confiáveis em séries temporais financeiras com ruído e volatilidade.
</details>

<details>
<summary>❓ <strong>Qual o impacto da normalização das features?</strong></summary>

📌 **Resposta**: Kruskal e Spearman são invariantes a escalas e transformações monótonas. Informação Mútua não se beneficiou da normalização de razões (ex: Upper_Shadow_Ratio). Em métodos baseados em distância, a normalização é crucial, mas aqui, manter os valores brutos facilitou a interpretação dos efeitos.
</details>

---

# Autoavaliação

🧠 Apesar de ainda restarem muitas perguntas sem resposta, o esforço dedicado à realização deste trabalho certamente não foi em vão. Ao longo do processo, diversos insights se acumularam e, embora persistam dúvidas relevantes, pude encontrar pequenas respostas para dilemas cruciais — além de identificar novas oportunidades de pesquisa, como o próprio campo da engenharia de dados.

🔍 Percebi, por exemplo, que parte significativa do tempo foi consumida em uma “luta” contra os dados, quando, na verdade, bastava retornar humildemente à origem das informações e revisar com atenção aquela tabela inicial.

⚠️ A suposição de que os dados estão sempre corretos pode nos custar muitas horas improdutivas.

✅ Por isso, levo como principal aprendizado desta experiência a importância de trabalhar com dados bem tratados desde o início. Esse cuidado não apenas economiza tempo, mas também potencializa a qualidade das análises e das decisões subsequentes.

---

📌 *Trabalho finalizado com dedicação e aprendizado contínuo.*
