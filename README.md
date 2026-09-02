# 📊 People Analytics com Python e Pandas

Projeto de análise e tratamento de dados desenvolvido em Python e Pandas, aplicado a um contexto de **People Analytics / Gente & Gestão**.

O projeto parte de uma base inicial de colaboradores, realiza etapas de exploração, tratamento, transformação e análise dos dados e, ao final, exporta uma nova base tratada em Excel.

> **Fluxo do projeto:**  
> `analise_funcionarios.xlsx` → Python + Pandas → Tratamento e Análise → `Analise_Final_Tratada.xlsx`

---

## 🎯 Objetivo

O objetivo deste projeto é aplicar conceitos de **Python, Pandas e Análise de Dados** em uma situação relacionada à área de Recursos Humanos.

A análise busca transformar uma base de colaboradores em informações mais organizadas e úteis para explorar questões relacionadas a:

- Perfil dos colaboradores
- Distribuição por departamento
- Remuneração
- Faixa salarial
- Desempenho
- Avaliação de desempenho
- Satisfação
- Desligamentos
- Motivos de desligamento
- Relações entre diferentes variáveis

Além da parte técnica, o projeto busca desenvolver uma visão de análise orientada a perguntas de negócio.

---

## 📂 Arquivos do projeto

### Base original
**`analise_funcionarios.xlsx`**
Arquivo utilizado como **entrada do projeto**. Essa é a base inicial dos colaboradores, que foi importada para o Python para realização das etapas de exploração e tratamento.

### Base final
**`Analise_Final_Tratada.xlsx`**
Arquivo **exportado ao final do processo de tratamento e análise**. Ele representa o resultado do processamento realizado em Python/Pandas. O arquivo final contém informações tratadas e organizadas para facilitar análises posteriores.

---

## 🐍 Tecnologias utilizadas

- Python
- Pandas
- NumPy
- Jupyter Notebook
- Microsoft Excel
- Matplotlib

---

## 🔎 Fluxo da análise

O projeto foi desenvolvido seguindo um fluxo de análise de dados:

```text
1. Base original
       ↓
analise_funcionarios.xlsx
       ↓
2. Importação com Pandas
       ↓
3. Exploração dos dados
       ↓
4. Identificação de problemas
       ↓
5. Tratamento dos dados
       ↓
6. Criação de novas variáveis
       ↓
7. Análise dos indicadores
       ↓
8. Exportação
       ↓
Analise_Final_Tratada.xlsx
```

### 📥 1. Importação dos dados
A base original foi importada para o Python utilizando a biblioteca Pandas.

```python
import pandas as pd

df = pd.read_excel("analise_funcionarios.xlsx")
```
O arquivo `analise_funcionarios.xlsx` representa o ponto inicial da análise.

### 🔍 2. Exploração inicial
Após a importação, foram utilizadas funções do Pandas para compreender a estrutura da base.

```python
df.head()
df.info()
df.shape
df.columns
df.isnull().sum()
```

Essas funções permitiram verificar:
- Primeiros registros da base
- Quantidade de linhas e colunas
- Nomes das variáveis
- Tipos de dados
- Valores ausentes
- Estrutura geral do DataFrame

Essa etapa foi importante para entender os dados antes de realizar qualquer transformação.

### 🧹 3. Tratamento dos dados
Durante a exploração foram identificadas informações ausentes e valores representados por textos, como:
- Não Informado
- Não informado
- Indisponível

Esses casos foram analisados antes de qualquer alteração. A decisão adotada foi preservar os registros e tratar as informações ausentes de maneira adequada para cada análise. Os valores ausentes não foram simplesmente excluídos da base.

### 🔢 4. Tratamento de variáveis numéricas
Algumas variáveis apresentavam informações numéricas misturadas com textos indicando ausência de informação. Por exemplo:
- Idade
- Desempenho

Para as análises numéricas, os valores não informados foram tratados como ausentes na camada analítica. Isso permitiu calcular médias e outros indicadores sem transformar valores desconhecidos em números artificiais.

### 📌 5. Criação da variável de avaliação
A partir da variável `Desempenho`, foi criada uma nova variável chamada `Avaliação`. Foi utilizado o método `apply()` do Pandas juntamente com uma função condicional:

```python
def avaliar_desempenho(desempenho):
    if pd.isna(desempenho):
        return "Não Avaliado"
    elif desempenho >= 9:
        return "Excelente Desempenho"
    elif desempenho >= 7:
        return "Bom Desempenho"
    else:
        return "Desempenho Insatisfatório"

df["Avaliação"] = df["Desempenho"].apply(avaliar_desempenho)
```

A classificação utilizada foi:

| Desempenho | Avaliação |
| :--- | :--- |
| ≥ 9 | Excelente Desempenho |
| ≥ 7 e < 9 | Bom Desempenho |
| < 7 | Desempenho Insatisfatório |
| Não informado | Não Avaliado |

### 👥 6. Classificação do status
A variável `Status` foi derivada a partir de `Motivo_Desligamento`. A regra utilizada foi:
- Funcionário Ativo → Ativo
- Demais motivos → Desligado

Essa transformação permitiu separar os registros entre colaboradores ativos e registros classificados como desligados.

### 📊 7. Principais indicadores
Após o tratamento dos dados, foram analisados indicadores relacionados ao quadro de colaboradores.

#### Indicadores gerais

| Indicador | Resultado |
| :--- | :--- |
| Total de registros | 179 |
| Colaboradores ativos | 144 |
| Registros classificados como desligados | 35 |
| Salário médio | R$ 5.946,96 |
| Menor salário | R$ 2.419,64 |
| Maior salário | R$ 12.018,65 |
| Desempenho médio | 6,47 |
| Idade média | 41,05 anos |

### 💰 8. Análise de remuneração
A análise de remuneração buscou compreender a distribuição dos salários entre os colaboradores. Foram observados:
- Salário mínimo
- Salário máximo
- Salário médio
- Salário total
- Faixas salariais
- Distribuição salarial por departamento

Essas informações permitem explorar diferenças de remuneração dentro da estrutura analisada.

### 📈 9. Análise de desempenho
A variável `Desempenho` foi utilizada para analisar o desempenho dos colaboradores. Foram explorados:
- Desempenho médio
- Maior desempenho
- Menor desempenho
- Distribuição das avaliações
- Desempenho por departamento
- Relação entre desempenho e satisfação

O objetivo foi identificar padrões nos dados e não estabelecer relações de causa e efeito.

### 😊 10. Análise de satisfação
A variável `Satisfacao` foi utilizada para explorar o nível de satisfação dos colaboradores. Foram analisadas possibilidades como:
- Distribuição dos níveis de satisfação
- Satisfação por departamento
- Satisfação em relação ao desempenho
- Satisfação em relação à avaliação

Essas análises são de caráter exploratório e descritivo.

### 🚪 11. Análise de desligamentos
A partir da variável `Motivo_Desligamento`, foram identificados os registros classificados como desligados. Os principais motivos encontrados foram:

| Motivo | Quantidade |
| :--- | :--- |
| Reestruturação | 10 |
| Pedido de demissão | 9 |
| Desempenho | 8 |
| Proposta externa | 4 |
| Fim de contrato | 4 |

Também foram exploradas relações entre:
- Departamento × Desligamento
- Faixa salarial × Desligamento
- Avaliação × Desligamento
- Motivo de desligamento × Departamento

#### ⚠️ Sobre o turnover
Um cuidado importante durante o projeto foi não classificar automaticamente os 35 registros desligados entre os 179 registros da base como uma taxa de turnover. A base não possui informações temporais suficientes, como:
- Data de admissão
- Data de desligamento
- Período de análise
- Histórico do quadro de colaboradores

Por isso, o indicador foi interpretado como o **percentual de registros classificados como desligados sobre o total da base**, e não como uma taxa temporal de turnover.

#### 📊 Análises exploratórias
O projeto também buscou analisar possíveis associações entre variáveis:
- **Departamento × Desligamento:** Permite identificar a concentração de registros desligados entre os departamentos.
- **Faixa Salarial × Desligamento:** Permite observar a distribuição dos registros desligados entre diferentes faixas salariais.
- **Satisfação × Desempenho:** Permite explorar se existem padrões de associação entre satisfação e desempenho.
- **Avaliação × Desligamento:** Permite observar a distribuição dos desligamentos de acordo com a classificação de desempenho.

*Nota: Essas análises são descritivas e exploratórias. Uma associação observada entre duas variáveis não significa que uma variável seja responsável pela outra.*

### 💾 12. Exportação dos dados tratados
Após as etapas de tratamento e análise, os dados foram exportados novamente para Excel. O arquivo gerado foi o `Analise_Final_Tratada.xlsx`. Esse arquivo representa o resultado final do processamento realizado em Python/Pandas, mantendo a base original intacta.

---

## 🧠 Principais aprendizados

Durante o desenvolvimento deste projeto, pratiquei conceitos importantes de Python e Pandas, incluindo:
- **Importação de arquivos:** Leitura de arquivos Excel.
- **Manipulação de DataFrames:** Criação e alteração de tabelas.
- **Exploração de dados:** Uso de `head()`, `info()`, `shape` e `columns`.
- **Identificação de ausentes:** Localização de valores nulos ou vazios.
- **Tratamento de dados:** Limpeza e conversão de tipos de dados.
- **Novas variáveis:** Criação de colunas e uso do método `apply()`.
- **Lógica condicional:** Aplicação de regras de negócio em funções.
- **Agrupamento de dados:** Agregações e resumos estatísticos.
- **Análise exploratória:** Investigação e cruzamento de variáveis.
- **Exportação de dados:** Gravação de DataFrames de volta para Excel.
- **Interpretação de indicadores:** Leitura crítica dos resultados obtidos.

Além dos conhecimentos técnicos, o projeto ajudou a desenvolver uma visão analítica voltada para **People Analytics**, focando em quais perguntas de negócio podem ser respondidas através dos dados de Gente & Gestão.

---

## ⚠️ Limitações do projeto

Durante a análise, foram identificadas as seguintes limitações na base de dados:
- **Ausência de ID único:** A base não possui matrícula. Nomes repetidos não foram tratados automaticamente como duplicatas.
- **Sem dados temporais:** Ausência de datas de admissão e desligamento, impedindo o cálculo da taxa temporal de turnover.
- **Valores ausentes:** Algumas variáveis possuem campos não preenchidos, que precisaram ser preservados na análise.
- **Falta de histórico:** Os dados representam um retrato estático, sem histórico de movimentações dos colaboradores no tempo.
- **Escopo acadêmico:** A base de dados foi utilizada estritamente para fins de estudo e desenvolvimento técnico.

---

## 📂 Estrutura do projeto

Sugestão de organização de pastas e arquivos para o repositório:

```text
people-analytics-pandas/
│
├── data/
│   ├── analise_funcionarios.xlsx
│   └── Analise_Final_Tratada.xlsx
│
├── notebooks/
│   └── analise_people_analytics.ipynb
│
├── outputs/
│
├── README.md
│
└── requirements.txt
```

### Fluxo dos arquivos de dados

```text
data/
│
├── analise_funcionarios.xlsx  ➔ Base original de entrada
│
└── Analise_Final_Tratada.xlsx ➔ Base exportada após tratamento em Python
```

---

## 🚀 Próximos passos

Como evolução deste projeto, o objetivo é desenvolver uma etapa de visualização e construção de um **Dashboard de People Analytics**. A proposta é transformar as análises em uma interface interativa contendo:
- Indicadores gerais de colaboradores.
- Visões específicas de remuneração e desempenho.
- Gráficos de satisfação e análise de desligamentos.
- Filtros dinâmicos por departamento e por status do funcionário.
- Análises cruzadas e correlações entre variáveis.

---

## 📌 Status do projeto

- 🟢 **Análise e tratamento dos dados** — Concluído
- 🟢 **Exportação da base final** — Concluído
- 🔵 **Dashboard interativo** — Próximo passo

---

## 👨‍💻 Sobre mim

Sou estudante de **Data Science**, desenvolvendo competências técnicas em:
- Python & Pandas
- Análise de Dados
- SQL
- Microsoft Excel
- Power BI
- People Analytics

Este projeto faz parte do meu portfólio profissional, representando a aplicação prática de conhecimentos em tratamento, limpeza e interpretação de dados.