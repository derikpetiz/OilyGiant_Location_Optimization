# 🛢️ Projeto de Otimização de Margem de Lucro: Seleção de Regiões para Poços de Petróleo (OilyGiant)

---

## 📌 1. Apresentação e Contexto de Negócio
A empresa petrolífera **OilyGiant** busca identificar a melhor região para o desenvolvimento de **200 novos poços de petróleo**. O orçamento total alocado para a operação é de **$100.000.000** ($100 milhões de dólares), com dados disponíveis em três regiões distintas (Região 0, Região 1 e Região 2).

### 💡 Premissas Financeiras e Regras de Negócio:
* **Investimento total:** $100.000.000 (para 200 poços).
* **Custo por poço:** $500.000 ($100M / 200 poços).
* **Receita por unidade de volume:** $4.500 por unidade de volume (1 unidade = 1.000 barris).
* **Critério de Governança de Risco:** A região escolhida deve apresentar um risco de prejuízo financeiro **inferior a 2,5%**.

---

## 📐 2. Cálculo do Ponto de Equilíbrio (Break-Even Point)

Para que o investimento não gere prejuízo:

$$\text{Volume Total Necessário} = \frac{\$100.000.000}{\$4.500} = 22.222,22 \text{ unidades}$$

$$\text{Volume Médio Mínimo por Poço} = \frac{22.222,22}{200} = 111,11 \text{ unidades (mil barris)}$$

### 🔎 Análise Crítica Populacional:
* **Região 0:** Média populacional de ~92,50 mil barris/poço.
* **Região 1:** Média populacional de ~68,72 mil barris/poço.
* **Região 2:** Média populacional de ~95,00 mil barris/poço.

**Conclusão de Negócio:** Nenhuma região atinge a média mínima exigida de 111,11 mil barris via amostragem aleatória. Torna-se indispensável o desenvolvimento de um modelo preditivo de **Regressão Linear** para selecionar cirurgicamente os 200 poços com maior potencial produtivo em cada região.

---

## 🛠️ 3. Tecnologias e Metodologia Utilizada

* **Linguagem:** Python 3.x
* **Manipulação e Análise de Dados:** Pandas, NumPy
* **Visualização:** Matplotlib, Seaborn
* **Machine Learning:** Scikit-Learn (`LinearRegression`, `StandardScaler`, `train_test_split`)
* **Validação Estatística de Risco:** Amostragem por Bootstrap (1.000 reamostragens com reposição)

---

## 📊 4. Desempenho dos Modelos por Região

Os dados de cada região foram divididos na proporção de **75% Treino / 25% Validação**, aplicando `StandardScaler` (sem *Data Leakage*):

| Região | Volume Médio Previsto (mil barris) | RMSE do Modelo | Desempenho Preditivo |
|:---:|:---:|:---:|:---:|
| **Região 0** | 92,59 | 37,58 | Alta variabilidade |
| **Região 1** | 68,73 | **0,89** | **Exatidão preditiva cirúrgica** |
| **Região 2** | 94,97 | 40,03 | Maior incerteza amostral |

---

## 🎲 5. Análise de Risco com Bootstrapping (1.000 Reamostragens)

Para simular o cenário real de exploração (onde 500 poços são mapeados e os 200 melhores são escolhidos preditivamente), aplicamos o método estatístico de **Bootstrap**:

| Região | Lucro Médio Líquido (USD) | Intervalo de Confiança (95%) | Risco de Prejuízo | Status de Risco |
|:---:|:---:|:---:|:---:|:---:|
| **Região 0** | US$ 3.816.285,42 | [-US$ 974.513,12 ; US$ 8.785.099,43] | 7,30% | ❌ Reprovado (> 2,5%) |
| **Região 1** | **US$ 4.545.975,29** | **[+US$ 242.137,45 ; US$ 8.701.936,76]** | **2,30%** | **✅ APROVADO (< 2,5%)** |
| **Região 2** | US$ 4.125.023,03 | [-US$ 1.086.948,55 ; US$ 9.436.797,26] | 6,10% | ❌ Reprovado (> 2,5%) |

---

## 🎯 6. Conclusão Executiva e Recomendação

1. **Reprovação das Regiões 0 e 2:** Apresentam riscos de prejuízo de **7,30%** e **6,10%**, excedendo o limite de segurança da empresa (2,5%), além de possuírem limites inferiores negativos no intervalo de confiança.
2. **Aprovação da Região 1:** É a única região que cumpre rigorosamente os critérios de governança, apresentando apenas **2,30% de risco de prejuízo** e mantendo o intervalo de confiança de 95% 100% no campo positivo (lucro mínimo estatístico garantido de US$ 242.137,45).
3. **Importância da Simulação Preditiva:** Embora a Região 1 possua a menor média populacional bruta, a acurácia quase perfeita do seu modelo de Regressão Linear (RMSE ~0,89) permite filtrar com precisão máxima os poços mais rentáveis.

💡 **Recomendação Final:** Investimento e perfuração concentrados na **REGIÃO 1**.
