📊 People Analytics com Python, Pandas e Dashboard Interativo

Projeto de análise e tratamento de dados desenvolvido em Python e Pandas, aplicado a um contexto de People Analytics / Gente & Gestão.

O projeto parte de uma base inicial de colaboradores, realiza etapas de exploração, tratamento, transformação e análise dos dados, exporta uma nova base tratada em Excel e, como etapa final, transforma os resultados em um dashboard web interativo e responsivo.

Fluxo do projeto:
analise_funcionarios.xlsx → Python + Pandas → Tratamento e Análise → Analise_Final_Tratada.xlsx → Dashboard Interativo

🎯 Objetivo

O objetivo deste projeto é aplicar conceitos de Python, Pandas e Análise de Dados em uma situação relacionada à área de Recursos Humanos.

A análise busca transformar uma base de colaboradores em informações mais organizadas e úteis para explorar questões relacionadas a:

Perfil dos colaboradores

Distribuição por departamento

Remuneração

Faixa salarial

Desempenho

Avaliação de desempenho

Satisfação

Desligamentos

Motivos de desligamento

Relações entre diferentes variáveis

Além da parte técnica, o projeto busca desenvolver uma visão de análise orientada a perguntas de negócio e apresentar os resultados em uma interface visual que facilite a exploração dos indicadores.

📂 Arquivos do projeto

Base original

analise_funcionarios.xlsx
Arquivo utilizado como entrada do projeto. Essa é a base inicial dos colaboradores, que foi importada para o Python para realização das etapas de exploração e tratamento.

Base final

Analise_Final_Tratada.xlsx
Arquivo exportado ao final do processo de tratamento e análise. Ele representa o resultado do processamento realizado em Python/Pandas. O arquivo final contém informações tratadas e organizadas para facilitar as análises posteriores.

Notebook

analise.ipynb
Notebook responsável pelas etapas de exploração, tratamento, transformação e análise dos dados com Python e Pandas.

Dashboard final

People_Analytics_Dashboard_Final.html
Arquivo HTML que representa a etapa final do projeto, reunindo os principais indicadores e análises em uma interface interativa e responsiva.

🐍 Tecnologias utilizadas

Python

Pandas

NumPy

Jupyter Notebook

Microsoft Excel

Matplotlib

HTML

CSS

JavaScript

Plotly.js

Git / GitHub

Claude — apoio na geração inicial da interface do dashboard

ChatGPT — apoio no refinamento, interatividade, validação e correções do dashboard

🔎 Fluxo da análise

O projeto foi desenvolvido seguindo um fluxo de análise de dados:

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
       ↓
9. Construção do dashboard
       ↓
10. Refinamento e interatividade
       ↓
11. Validação dos indicadores
       ↓
People_Analytics_Dashboard_Final.html

📥 1. Importação dos dados

A base original foi importada para o Python utilizando a biblioteca Pandas.

import pandas as pd

df = pd.read_excel("analise_funcionarios.xlsx")

O arquivo analise_funcionarios.xlsx representa o ponto inicial da análise.

🔍 2. Exploração inicial

Após a importação, foram utilizadas funções do Pandas para compreender a estrutura da base.

df.head()
df.info()
df.shape
df.columns
df.isnull().sum()

Essas funções permitiram verificar:

Primeiros registros da base

Quantidade de linhas e colunas

Nomes das variáveis

Tipos de dados

Valores ausentes

Estrutura geral do DataFrame

Essa etapa foi importante para entender os dados antes de realizar qualquer transformação.

🧹 3. Tratamento dos dados

Durante a exploração foram identificadas informações ausentes e valores representados por textos, como:

Não Informado

Não informado

Indisponível

Esses casos foram analisados antes de qualquer alteração. A decisão adotada foi preservar os registros e tratar as informações ausentes de maneira adequada para cada análise. Os valores ausentes não foram simplesmente excluídos da base.

🔢 4. Tratamento de variáveis numéricas

Algumas variáveis apresentavam informações numéricas misturadas com textos indicando ausência de informação. Por exemplo:

Idade

Desempenho

Para as análises numéricas, os valores não informados foram tratados como ausentes na camada analítica. Isso permitiu calcular médias e outros indicadores sem transformar valores desconhecidos em números artificiais.

📌 5. Criação da variável de avaliação

A partir da variável Desempenho, foi criada uma nova variável chamada Avaliação. Foi utilizado o método apply() do Pandas juntamente com uma função condicional:

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

A classificação utilizada foi:

Desempenho

Avaliação

≥ 9

Excelente Desempenho

≥ 7 e < 9

Bom Desempenho

< 7

Desempenho Insatisfatório

Não informado

Não Avaliado

👥 6. Classificação do status

A variável Status foi derivada a partir de Motivo_Desligamento. A regra utilizada foi:

Funcionário Ativo → Ativo

Demais motivos → Desligado

Essa transformação permitiu separar os registros entre colaboradores ativos e registros classificados como desligados. A mesma regra foi preservada na camada analítica do dashboard.

📊 7. Principais indicadores

Após o tratamento dos dados, foram analisados indicadores relacionados ao quadro de colaboradores.

Indicadores gerais

Indicador

Resultado

Total de registros

179

Colaboradores ativos

144

Registros classificados como desligados

35

Proporção de desligados

19,55%

Salário médio

R$ 5.946,96

Menor salário

R$ 2.419,64

Maior salário

R$ 12.018,65

Desempenho médio

6,47

Idade média

41,05 anos

💰 8. Análise de remuneração

A análise de remuneração buscou compreender a distribuição dos salários entre os colaboradores. Foram observados:

Salário mínimo

Salário máximo

Salário médio

Salário total

Faixas salariais

Distribuição salarial por departamento

Essas informações permitem explorar diferenças de remuneração dentro da estrutura analisada.

📈 9. Análise de desempenho

A variável Desempenho foi utilizada para analisar o desempenho dos colaboradores. Foram explorados:

Desempenho médio

Maior desempenho

Menor desempenho

Distribuição das avaliações

Desempenho por departamento

Relação entre desempenho e satisfação

O objetivo foi identificar padrões nos dados e não estabelecer relações de causa e efeito.

😊 10. Análise de satisfação

A variável Satisfacao foi utilizada para explorar o nível de satisfação dos colaboradores. Foram analisadas possibilidades como:

Distribuição dos níveis de satisfação

Satisfação por departamento

Satisfação em relação ao desempenho

Satisfação em relação à avaliação

Essas análises são de caráter exploratório e descritivo.

🚪 11. Análise de desligamentos

A partir da variável Motivo_Desligamento, foram identificados os registros classificados como desligados. Os principais motivos encontrados foram:

Motivo

Quantidade

Reestruturação

10

Pedido de demissão

9

Desempenho

8

Proposta externa

4

Fim de contrato

4

Também foram exploradas relações entre:

Departamento × Desligamento

Faixa salarial × Desligamento

Avaliação × Desligamento

Motivo de desligamento × Departamento

⚠️ Sobre o turnover

Um cuidado importante durante o projeto foi não classificar automaticamente os 35 registros desligados entre os 179 registros da base como uma taxa de turnover. A base não possui informações temporais suficientes, como:

Data de admissão

Data de desligamento

Período de análise

Histórico do quadro de colaboradores

Por isso, o indicador foi interpretado como o percentual de registros classificados como desligados sobre o total da base, e não como uma taxa temporal de turnover.

📊 Análises exploratórias

O projeto também buscou analisar possíveis associações entre variáveis:

Departamento × Desligamento: Permite identificar a concentração de registros desligados entre os departamentos.

Faixa Salarial × Desligamento: Permite observar a distribuição dos registros desligados entre diferentes faixas salariais.

Satisfação × Desempenho: Permite explorar se existem padrões de associação entre satisfação e desempenho.

Avaliação × Desligamento: Permite observar a distribuição dos desligamentos de acordo com a classificação de desempenho.

Nota: Essas análises são descritivas e exploratórias. Uma associação observada entre duas variáveis não significa que uma variável seja responsável pela outra.

💾 12. Exportação dos dados tratados

Após as etapas de tratamento e análise, os dados foram exportados novamente para Excel. O arquivo gerado foi o Analise_Final_Tratada.xlsx. Esse arquivo representa o resultado final do processamento realizado em Python/Pandas, mantendo a base original intacta.

🖥️ Dashboard interativo

Após a conclusão da análise e da exportação da base tratada, o projeto avançou para uma etapa de visualização de dados, transformando os resultados em um dashboard web interativo.

O dashboard foi construído a partir dos indicadores e regras definidos durante a análise em Python. A primeira versão da interface foi gerada com apoio do Claude e, posteriormente, passou por diferentes etapas de refinamento com o ChatGPT, preservando os dados, cálculos, metodologia e regras de negócio do projeto.

O objetivo dessa etapa foi transformar a análise já realizada em uma interface capaz de facilitar a leitura dos indicadores e permitir diferentes recortes da base.

🧭 Estrutura do dashboard

O dashboard final foi dividido em cinco páginas:

1. Visão Geral

Apresenta os principais KPIs e uma visão resumida da composição da base, incluindo:

Total de registros

Ativos e desligados

Proporção de desligados

Salário médio

Desempenho médio

Idade média

Distribuição por departamento

Distribuição por faixa salarial

Avaliação de desempenho

2. Remuneração

Página voltada para a análise salarial, contendo:

Distribuição dos salários

Salário médio por departamento

Distribuição por faixa salarial

Composição das faixas salariais por departamento

Tabela para consulta dos registros

3. Desempenho

Página dedicada à análise de desempenho:

Distribuição das notas

Avaliações de desempenho

Desempenho médio por departamento

Cruzamento entre avaliação e departamento

Consulta dos registros

4. Satisfação

Página utilizada para explorar:

Distribuição dos níveis de satisfação

Desempenho médio por nível de satisfação

Relação entre satisfação e avaliação

Tabela analítica

As relações apresentadas permanecem descritivas e exploratórias, sem afirmações de causalidade.

5. Desligamentos

Página voltada aos registros classificados como desligados:

Motivos de desligamento

Proporção de desligados por departamento

Desligamentos por faixa salarial

Comparação entre ativos e desligados por faixa salarial

Perfil dos registros desligados

📊 Visualizações utilizadas

Foram utilizados diferentes tipos de gráficos de acordo com a finalidade da análise:

Gráficos de barras horizontais

Histogramas

Gráficos de rosca (donut)

Gráficos 100% empilhados

Heatmaps

Dot plots

Tabelas analíticas

A diversificação das visualizações buscou evitar o uso repetitivo de um único formato e facilitar a interpretação de diferentes tipos de informação.

🎛️ Filtros e interatividade

A versão final do dashboard possui recursos de exploração semelhantes aos encontrados em ferramentas de BI:

Filtros por departamento

Filtros por status

Filtros específicos de cada página

Filtros por intervalo de idade

Filtros por intervalo salarial

Filtros por intervalo de desempenho

Cross-filter por clique nos gráficos

Chips para visualização dos filtros ativos

Opção para remover filtros individualmente

Alternância entre Quantidade e Percentual

Ordenação de rankings

KPIs interativos quando aplicável

Tooltips com informações analíticas

Busca, ordenação e paginação nas tabelas

Atualização dinâmica dos indicadores de acordo com o recorte selecionado

📱 Responsividade

O dashboard também foi desenvolvido para funcionar em diferentes tamanhos de tela.

Foram realizados ajustes para:

Desktop

Notebook

Tablet

Smartphone

No mobile, a navegação lateral passa a funcionar como um menu expansível, os gráficos são reorganizados em uma única coluna quando necessário e as tabelas possuem rolagem horizontal.

O objetivo foi manter a legibilidade e a capacidade de interação tanto por clique quanto por toque.

🤖 Uso de IA no desenvolvimento do dashboard

Ferramentas de Inteligência Artificial foram utilizadas como apoio ao desenvolvimento da camada visual.

O fluxo foi:

Análise e tratamento em Python/Pandas
              ↓
Indicadores e regras validados
              ↓
Estrutura inicial do dashboard com Claude
              ↓
Redesign visual
              ↓
Refinamento com ChatGPT
              ↓
Responsividade e cross-filter
              ↓
Validação matemática
              ↓
Correção de bugs
              ↓
Dashboard final

A primeira versão da interface foi gerada com apoio do Claude. O ChatGPT foi utilizado posteriormente para apoiar o processo de revisão técnica e visual, implementação de novas interações, responsividade, validação dos indicadores e correção de problemas identificados durante os testes.

A utilização dessas ferramentas não substituiu o processo de análise dos dados. A base tratada, os indicadores, as regras de classificação e as limitações metodológicas permaneceram vinculados ao trabalho realizado em Python/Pandas.

<details>
<summary><strong>📝 Resumo dos prompts utilizados</strong></summary>

1. Construção inicial

Foi solicitada a criação de um dashboard de People Analytics a partir da análise já realizada, preservando os indicadores, categorias e regras de negócio da base tratada.

2. Redesign visual

A interface foi refinada para um estilo dark profissional, utilizando maior hierarquia visual, diferentes tipos de gráficos e uma estrutura responsiva.

3. Interatividade

Foram solicitados recursos como cross-filter, filtros ativos, filtros numéricos, KPIs clicáveis, busca e paginação nas tabelas e alternância entre quantidade e percentual.

4. Refinamento

Os prompts seguintes focaram na melhoria dos tooltips, valores exatos, experiência mobile e comportamento dos gráficos após aplicação dos filtros.

5. Correções e validação

A etapa final concentrou-se na validação matemática dos percentuais, preservação dos 179 registros, revisão dos indicadores e correção de bugs específicos dos gráficos de rosca.

Os prompts completos foram iterativos e extensos. Por isso, este README registra apenas os objetivos principais de cada etapa.

</details>

🔬 Validação do dashboard

Antes da conclusão do projeto, os principais indicadores foram comparados com a base tratada.

Foram preservados:

179 registros

144 ativos

35 desligados

Salário médio ≈ R$ 5.946,96

Desempenho médio ≈ 6,47

Idade média ≈ 41,05 anos

Também foram revisados os percentuais apresentados nos gráficos e o comportamento dos indicadores após aplicação de filtros.

▶️ Como abrir o dashboard

O arquivo final é:

People_Analytics_Dashboard_Final.html

Para visualizar:

Baixe o arquivo HTML.

Abra-o em um navegador moderno, como Chrome, Edge ou Firefox.

Mantenha conexão com a internet, pois o dashboard utiliza recursos externos como Plotly.js e a fonte Inter.

Utilize os filtros ou clique nos gráficos para explorar diferentes recortes dos dados.

Limpe os filtros para retornar à visão completa da base.

🧠 Principais aprendizados

Durante o desenvolvimento deste projeto, pratiquei conceitos importantes de Python e Pandas, incluindo:

Importação de arquivos: Leitura de arquivos Excel.

Manipulação de DataFrames: Criação e alteração de tabelas.

Exploração de dados: Uso de head(), info(), shape e columns.

Identificação de ausentes: Localização de valores nulos ou vazios.

Tratamento de dados: Limpeza e conversão de tipos de dados.

Novas variáveis: Criação de colunas e uso do método apply().

Lógica condicional: Aplicação de regras de negócio em funções.

Agrupamento de dados: Agregações e resumos estatísticos.

Análise exploratória: Investigação e cruzamento de variáveis.

Exportação de dados: Gravação de DataFrames de volta para Excel.

Interpretação de indicadores: Leitura crítica dos resultados obtidos.

Visualização de dados: Escolha de gráficos de acordo com o tipo de análise.

Interatividade: Uso de filtros e cross-filter para exploração dos dados.

Validação: Conferência de cálculos e percentuais após aplicação dos filtros.

Responsividade: Adaptação de uma interface analítica para diferentes dispositivos.

Uso de IA: Utilização de ferramentas generativas como apoio técnico, mantendo a validação dos dados e resultados.

Além dos conhecimentos técnicos, o projeto ajudou a desenvolver uma visão analítica voltada para People Analytics, focando em quais perguntas de negócio podem ser respondidas através dos dados de Gente & Gestão e em como apresentar essas respostas de maneira visual.

⚠️ Limitações do projeto

Durante a análise, foram identificadas as seguintes limitações na base de dados:

Ausência de ID único: A base não possui matrícula. Nomes repetidos não foram tratados automaticamente como duplicatas.

Sem dados temporais: Ausência de datas de admissão e desligamento, impedindo o cálculo da taxa temporal de turnover.

Valores ausentes: Algumas variáveis possuem campos não preenchidos, que precisaram ser preservados na análise.

Falta de histórico: Os dados representam um retrato estático, sem histórico de movimentações dos colaboradores no tempo.

Associação não implica causalidade: As relações entre variáveis apresentadas no projeto possuem caráter exploratório.

Escopo acadêmico: A base de dados foi utilizada estritamente para fins de estudo e desenvolvimento técnico.

📂 Estrutura do projeto

Sugestão de organização de pastas e arquivos para o repositório:

people-analytics-pandas/
│
├── data/
│   ├── analise_funcionarios.xlsx
│   └── Analise_Final_Tratada.xlsx
│
├── notebooks/
│   └── analise.ipynb
│
├── dashboard/
│   └── People_Analytics_Dashboard_Final.html
│
├── README.md
│
└── requirements.txt

Fluxo dos arquivos de dados

data/
│
├── analise_funcionarios.xlsx  ➔ Base original de entrada
│
└── Analise_Final_Tratada.xlsx ➔ Base exportada após tratamento em Python
                                      ↓
                         Dashboard interativo HTML

🚀 Próximos passos

O dashboard planejado inicialmente como próxima etapa foi concluído. Com isso, o fluxo principal deste projeto está encerrado.

Como possíveis evoluções futuras, uma base com mais informações permitiria desenvolver análises como:

Turnover por período

Evolução do quadro de colaboradores ao longo do tempo

Tempo médio de permanência

Admissões e desligamentos por período

Análise de coortes

Comparações temporais entre departamentos

Evolução histórica de remuneração, satisfação e desempenho

Essas análises dependem de informações temporais e identificadores que não estão disponíveis na base atual.

📌 Status do projeto

🟢 Análise e tratamento dos dados — Concluído

🟢 Exportação da base final — Concluído

🟢 Dashboard interativo — Concluído

🟢 Responsividade e interatividade — Concluído

🟢 Validação e refinamento final — Concluído

Projeto concluído e pronto para portfólio.

👨‍💻 Sobre mim

Sou estudante de Data Science, desenvolvendo competências técnicas em:

Python & Pandas

Análise de Dados

SQL

Microsoft Excel

Power BI

People Analytics

Este projeto faz parte do meu portfólio profissional, representando a aplicação prática de conhecimentos em tratamento, limpeza, interpretação e visualização de dados.
