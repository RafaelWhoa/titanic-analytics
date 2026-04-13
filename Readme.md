# Análise Exploratório e Pré-processamento do Dataset Titanic

## Introdução

Este projeto tem como objetivo realizar uma **análise exploratória de dados (EDA)** e aplicar técnicas de **pré-processamento** no dataset do Titanic, amplamente utilizado em estudos de ciência de dados e aprendizado de máquina.  

A análise busca identificar padrões e relações entre as características dos passageiros que possam explicar suas chances de sobrevivência durante o desastre do Titanic.

O dataset utilizado é o **Titanic: Machine Learning from Disaster**, disponível no Kaggle.

---

# 1. Definição do Problema

## Descrição do Problema

O objetivo deste projeto é analisar os dados dos passageiros do Titanic para compreender quais fatores podem ter influenciado suas chances de sobrevivência.  

A partir das informações disponíveis, busca-se identificar padrões e relações entre variáveis como sexo, idade, classe do passageiro e estrutura familiar.

Além disso, o conjunto de dados é preparado para possível utilização futura em **modelos de aprendizado de máquina capazes de prever a sobrevivência de passageiros com base em suas características**.

---

## Tipo de Problema

Este é um **problema de aprendizado supervisionado de classificação**, pois o objetivo é prever a variável **Survived**:


Onde:

- **0** → passageiro não sobreviveu  
- **1** → passageiro sobreviveu

---

## Hipóteses Investigadas

Durante a análise exploratória foram levantadas as seguintes hipóteses:

1. **O sexo do passageiro e a classe podem influenciar a sobrevivência?**  
   Historicamente, houve prioridade para mulheres e crianças no acesso aos botes salva-vidas.

2. **A idade pode influenciar a sobrevivência?**  
   Crianças podem ter recebido prioridade durante a evacuação.

3. **O número de familiares a bordo pode influenciar a sobrevivência?**  
   Passageiros viajando com familiares podem ter tido vantagens ou dificuldades durante a evacuação.

---

## Restrições ou Condições do Dataset

Algumas limitações do dataset foram consideradas:

- Nem todas as informações dos passageiros estão disponíveis.
- Algumas variáveis apresentam **valores faltantes**, como `Age` e `Cabin`.
- Certos atributos, como `Name` e `Ticket`, possuem pouca relevância para análise preditiva e foram removidos durante o pré-processamento.

---

## Descrição dos Atributos

| Atributo | Descrição |
|--------|--------|
PassengerId | Identificador único do passageiro |
Survived | Indica se o passageiro sobreviveu (0 = não, 1 = sim) |
Pclass | Classe do passageiro (1ª, 2ª ou 3ª classe) |
Name | Nome do passageiro |
Sex | Sexo do passageiro |
Age | Idade do passageiro |
SibSp | Número de irmãos/cônjuges a bordo |
Parch | Número de pais/filhos a bordo |
Ticket | Número do ticket |
Fare | Tarifa paga pela passagem |
Cabin | Número da cabine |
Embarked | Porto de embarque |

---

# 2. Análise de Dados

## Estatísticas Descritivas

O dataset de treinamento contém:

- **891 instâncias**
- **12 atributos**

### Tipos de Dados

Os atributos incluem:

- Variáveis **numéricas** (`Age`, `Fare`, `SibSp`, `Parch`)
- Variáveis **categóricas** (`Sex`, `Embarked`)
- Variáveis **identificadoras** (`PassengerId`, `Ticket`, `Name`)

---

### Valores Faltantes

Durante a análise foram identificados valores faltantes nas seguintes variáveis:

| Variável | Valores faltantes |
|--------|--------|
Age | 177 |
Cabin | 687 |
Embarked | 2 |

---

### Resumo Estatístico

Foi realizado um resumo estatístico das variáveis numéricas, incluindo:

- média
- mediana
- desvio padrão
- valores mínimos e máximos

Essa análise permitiu identificar:

- presença de **outliers**, principalmente na variável `Fare`
- grande variação de valores entre os atributos

---

# 3. Visualizações

Diversas visualizações foram utilizadas para compreender melhor o comportamento dos dados.

## Distribuição das Classes

Foi utilizado um **countplot** para analisar a distribuição da variável `Survived`.

A análise mostrou que:

- o número de passageiros que **não sobreviveram é maior** que o número de sobreviventes
- o dataset apresenta **desbalanceamento de classes**

---

## Média das Variáveis Numéricas

Foi utilizado um **barplot** para representar a média das variáveis:

- Age
- Fare
- SibSp
- Parch

Esse gráfico permite comparar rapidamente os valores médios entre diferentes variáveis.

---

## Desvio Padrão das Variáveis

Um **barplot** também foi utilizado para visualizar o **desvio padrão** dessas mesmas variáveis.

Essa análise ajuda a compreender a **dispersão dos dados** em relação à média.

---

## Distribuição da Tarifa (Fare)

Um **histograma** foi utilizado para analisar a distribuição da variável `Fare`.

Observou-se que:

- a maioria das tarifas está concentrada entre **5 e 20**
- existem valores muito altos, indicando **presença de outliers**
- a distribuição apresenta **assimetria à direita**

---

## Tarifa por Classe

Foi utilizado um **boxplot** para analisar a distribuição de `Fare` em relação à variável `Pclass`.

A análise mostrou que:

- passageiros da **1ª classe pagaram tarifas significativamente maiores**
- há maior variabilidade de preços na primeira classe
- foram observados diversos **outliers**, especialmente nas classes primeira e terceira

---

## Matriz de Correlação

Uma **matriz de correlação** foi utilizada para identificar relações entre as variáveis numéricas.

Algumas correlações relevantes foram observadas:

- correlação negativa entre **Sex e Survived**
- correlação negativa entre **Pclass e Survived**
- correlação positiva entre **Fare e Survived**

Esses resultados indicam que fatores sociais e econômicos podem ter influenciado a sobrevivência.

---

# 4. Pré-processamento de Dados

## Tratamento de Valores Faltantes

As seguintes estratégias foram aplicadas:

| Variável | Tratamento |
|--------|--------|
Age | substituição pela mediana |
Embarked | substituição pela moda |
Cabin | remoção da coluna |

---

## Remoção de Variáveis Irrelevantes

Algumas variáveis foram removidas por apresentarem baixa relevância para análise preditiva:

- `Name`
- `Ticket`
- `Cabin`

---

## Codificação de Variáveis Categóricas

A variável `Sex` foi convertida para valores numéricos:

- **female** → 0
- **male** → 1


Essa transformação facilita a utilização do dataset em algoritmos de aprendizado de máquina.

---

## Padronização dos Dados

As variáveis numéricas contínuas **Age** e **Fare** foram padronizadas utilizando a técnica de **Standardization**, que transforma os dados de modo que:

- a média seja aproximadamente **0**
- o desvio padrão seja aproximadamente **1**

Essa etapa é importante para algoritmos de aprendizado de máquina que são sensíveis à escala dos dados.

---

# Conclusão

A análise exploratória e o pré-processamento do dataset Titanic permitiram identificar padrões importantes relacionados à sobrevivência dos passageiros.

Entre os principais fatores observados estão:

- **Sexo do passageiro**, com maior taxa de sobrevivência entre mulheres
- **Classe social**, com passageiros da primeira classe apresentando maiores taxas de sobrevivência
- **Estrutura familiar**, indicando que passageiros viajando em pequenos grupos familiares podem ter tido maiores chances de sobreviver

Esses resultados demonstram como técnicas de análise exploratória podem revelar padrões relevantes nos dados e preparar o dataset para futuras aplicações de **modelos de aprendizado de máquina**.

---

# Tecnologias Utilizadas

- Python
- Pandas
- Seaborn
- Matplotlib
- Scikit-learn
- Google Colab
