# Decision Science aplicado ao Marketplace Olist

## 1. Contexto do projeto

Este projeto tem como objetivo aplicar técnicas de **Decision Science**, **Analytics Engineering** e **Ciência de Dados** para investigar fatores que influenciam a satisfação dos clientes em um marketplace brasileiro.

A base utilizada é o **Brazilian E-Commerce Public Dataset by Olist**, um conjunto de dados público com informações sobre pedidos, clientes, vendedores, produtos, pagamentos, avaliações e localização.

Atualmente a Olist é um ERP, no entanto, os dados apresentam um comportamento de:

* um pedido pode conter múltiplos itens;
* um pedido pode envolver mais de um vendedor;
* um cliente pode comprar de diferentes vendedores;

Entenderemos os dados como de Marketplace para essa análise.

---

## 2. Como obter os dados

Os dados utilizados neste projeto são públicos e estão disponíveis no Kaggle:

**Brazilian E-Commerce Public Dataset by Olist**

### Observação importante

A pasta `data/raw/` está no `.gitignore` para evitar que os dados sejam enviados ao GitHub.

Isso mantém o repositório mais leve, organizado e reproduzível.

### Download manual

1. Acesse o dataset **Brazilian E-Commerce Public Dataset by Olist** no Kaggle.
2. Faça o download dos arquivos `.csv`.
3. Extraia os arquivos.
4. Coloque todos os arquivos dentro da pasta:

```text
data/raw/
```

A estrutura esperada é:

```text
data/
└── raw/
    ├── olist_customers_dataset.csv
    ├── olist_geolocation_dataset.csv
    ├── olist_order_items_dataset.csv
    ├── olist_order_payments_dataset.csv
    ├── olist_order_reviews_dataset.csv
    ├── olist_orders_dataset.csv
    ├── olist_products_dataset.csv
    ├── olist_sellers_dataset.csv
    └── product_category_name_translation.csv
```

<<<<<<< HEAD
## Estrutura do projeto
=======
---

## 3. Objetivo principal

Responder à seguinte pergunta central:

> Quais fatores operacionais e comerciais estão associados à satisfação do cliente?

A satisfação do cliente será analisada principalmente a partir da variável `review_score`, presente na tabela de avaliações.

---

## 4. Linhas de análise do projeto

O projeto será dividido em três grandes blocos:

### 4.1 Análise principal: satisfação do cliente

Nesta etapa, o objetivo é entender como diferentes fatores se relacionam com a avaliação dada pelo cliente.

Perguntas principais:

* Qual é a distribuição das avaliações dos clientes?
* Qual percentual de pedidos recebe notas baixas?
* O tempo de entrega influencia a nota?
* O valor do frete está associado a piores avaliações?
* Pedidos com múltiplos sellers possuem pior experiência?
* Algumas categorias possuem satisfação média menor?
* Existem estados ou regiões com maior incidência de avaliações negativas?

Principais variáveis analisadas:

* `review_score`
* `order_status`
* `order_purchase_timestamp`
* `order_delivered_customer_date`
* `order_estimated_delivery_date`
* `price`
* `freight_value`
* `product_category_name`
* `seller_id`
* `customer_state`
* `seller_state`

Métricas derivadas:

* dias de entrega;
* dias de atraso;
* flag de pedido atrasado;
* valor total do pedido;
* percentual do frete sobre o valor do produto;
* quantidade de itens por pedido;
* quantidade de sellers por pedido.

---

### 4.2 Modelo explicativo: regressão

Nesta etapa, o objetivo é construir um modelo explicativo para entender quais fatores estão mais associados à nota de avaliação do cliente.

A ideia não é apenas prever a nota, mas interpretar os fatores que ajudam a explicar avaliações melhores ou piores.

Perguntas principais:

* Quais variáveis estão mais associadas ao `review_score`?
* O atraso na entrega continua relevante mesmo controlando por frete, categoria e seller?
* Quanto a nota média tende a cair quando o pedido atrasa?
* O percentual de frete sobre o pedido possui relação negativa com a avaliação?
* Pedidos com múltiplos sellers apresentam pior nota mesmo controlando outras variáveis?

Possíveis abordagens:

* regressão linear;
* regressão ordinal;
* regressão logística para classificar avaliação ruim vs boa;
* análise de coeficientes;
* comparação entre modelos;
* validação de premissas básicas.

Exemplo de variável-alvo:

```text
review_score
```

Ou uma versão binária:

```text
avaliacao_ruim = 1 se review_score <= 2
avaliacao_ruim = 0 se review_score >= 4
```

Possíveis variáveis explicativas:

```text
dias_entrega
dias_atraso
pedido_atrasado
freight_value
frete_percentual
valor_total_pedido
qtd_itens
qtd_sellers
product_category_name
customer_state
seller_state
```

---

### 4.3 Segmentação: clusterização de sellers

Nesta etapa, o objetivo é segmentar vendedores com base em seu comportamento operacional e impacto na experiência do cliente.

A clusterização será utilizada para identificar perfis de sellers dentro do marketplace, permitindo recomendações mais acionáveis para o negócio.

Pergunta central:

> Existem grupos de sellers com padrões diferentes de desempenho operacional, satisfação e volume de vendas?

Perguntas secundárias:

* Quais sellers possuem maior volume de pedidos?
* Quais sellers possuem maior taxa de atraso?
* Quais sellers possuem melhor avaliação média?
* Existem sellers com alto volume e baixa satisfação?
* Existem sellers pequenos com excelente desempenho?
* Existem sellers com alto frete médio ou maior complexidade logística?
* Quais clusters deveriam ser priorizados para ações operacionais?

Possíveis features para clusterização:

```text
qtd_pedidos
receita_total
ticket_medio
frete_medio
frete_percentual_medio
review_score_medio
taxa_avaliacao_ruim
taxa_atraso
dias_entrega_medio
dias_atraso_medio
qtd_categorias
qtd_estados_atendidos
qtd_clientes_unicos
```

Possíveis clusters esperados:

```text
Sellers grandes e confiáveis
Sellers grandes com problemas operacionais
Sellers pequenos bem avaliados
Sellers pequenos com alto atraso
Sellers de alto ticket e baixa satisfação
Sellers com maior complexidade logística
```

---

## 5. Estrutura analítica esperada

O projeto seguirá uma jornada estruturada:

```text
Entendimento do negócio
↓
Entendimento dos dados
↓
Modelagem dimensional
↓
Construção da base analítica
↓
Análise exploratória
↓
Testes estatísticos
↓
Modelo explicativo
↓
Clusterização de sellers
↓
Recomendações de negócio
```

---

## 6. Etapas do projeto

### Etapa 1 — Data Understanding

Objetivo:

Entender a estrutura dos dados, a granularidade das tabelas e as relações entre clientes, pedidos, itens, sellers e avaliações.

Perguntas respondidas nesta etapa:

* O que representa uma linha em `orders`?
* O que representa uma linha em `order_items`?
* Qual a diferença entre `customer_id` e `customer_unique_id`?
* Um pedido pode ter mais de um seller?
* Um cliente pode comprar de mais de um seller?
* Qual a melhor unidade de análise para o projeto?

Entregáveis:

* notebook `00_data_understanding.ipynb`;
* documentação inicial das tabelas;
* primeiras conclusões sobre a estrutura do marketplace.

---

### Etapa 2 — Modelagem dos dados

Objetivo:

Criar uma estrutura organizada para análise, separando dados crus, staging, dimensões, fatos e marts analíticos.

Camadas propostas:

```text
raw_olist
staging_olist
dw_olist
mart_olist
```

Possíveis tabelas finais:

```text
dim_customers
dim_sellers
dim_products
dim_dates
fact_order_items
fact_reviews
fact_payments
mart_customer_satisfaction
mart_seller_performance
```

Entregáveis:

* scripts SQL de criação dos schemas;
* scripts SQL de criação das tabelas;
* carga dos dados no PostgreSQL;
* documentação da modelagem.

---

### Etapa 3 — Construção da base analítica de satisfação

Objetivo:

Criar uma base consolidada para análise da satisfação do cliente.

A base deverá conter, no mínimo:

```text
order_id
customer_unique_id
seller_id
product_id
product_category_name
customer_state
seller_state
order_status
order_purchase_timestamp
order_delivered_customer_date
order_estimated_delivery_date
review_score
price
freight_value
dias_entrega
dias_atraso
pedido_atrasado
qtd_itens
qtd_sellers
valor_total_pedido
frete_percentual
```

Entregáveis:

* tabela `mart_customer_satisfaction`;
* validações de qualidade;
* documentação das variáveis criadas.

---

### Etapa 4 — Análise exploratória

Objetivo:

Explorar os dados e identificar padrões iniciais relacionados à satisfação do cliente.

Perguntas respondidas:

* Como as avaliações estão distribuídas?
* Qual a nota média geral?
* Qual a nota média de pedidos atrasados vs pedidos no prazo?
* Qual o comportamento da nota por faixa de atraso?
* Quais categorias possuem menor satisfação?
* Quais sellers possuem maior volume e menor nota média?
* O frete alto parece estar associado a avaliações menores?

Entregáveis:

* notebook exploratório;
* gráficos;
* tabelas-resumo;
* primeiros insights de negócio.

---

### Etapa 5 — Testes estatísticos

Objetivo:

Validar se algumas diferenças observadas na análise exploratória são estatisticamente relevantes.

Hipóteses iniciais:

#### H1 — Atraso e satisfação

> Pedidos atrasados possuem avaliações menores do que pedidos entregues no prazo.

Possíveis testes:

```text
Mann-Whitney
t-test
```

#### H2 — Frete e satisfação

> Pedidos com frete proporcionalmente alto possuem avaliações menores.

Possíveis métodos:

```text
Correlação de Spearman
Comparação por faixas de frete percentual
```

#### H3 — Complexidade do pedido e satisfação

> Pedidos com múltiplos sellers possuem avaliações menores.

Possíveis testes:

```text
Mann-Whitney
Análise por grupos
```

Entregáveis:

* notebook de testes estatísticos;
* interpretação dos resultados;
* conclusões em linguagem de negócio.

---

### Etapa 6 — Modelo explicativo

Objetivo:

Construir um modelo para entender quais fatores estão associados à avaliação do cliente.

Possíveis modelos:

```text
Regressão linear
Regressão logística
Regressão ordinal
```

Perguntas respondidas:

* O atraso na entrega é um dos principais fatores associados à nota?
* O frete percentual influencia a avaliação?
* O número de sellers no pedido afeta a experiência?
* Algumas categorias possuem efeito relevante na satisfação?
* O efeito do atraso permanece mesmo controlando outras variáveis?

Entregáveis:

* notebook de modelagem;
* comparação entre modelos;
* interpretação dos coeficientes;
* principais fatores associados à satisfação.

---

### Etapa 7 — Clusterização de sellers

Objetivo:

Segmentar sellers em grupos com características semelhantes para apoiar recomendações estratégicas.

Possíveis etapas:

```text
1. Construção da base agregada por seller
2. Seleção de features
3. Padronização das variáveis
4. Escolha do número de clusters
5. Aplicação do K-Means ou algoritmo similar
6. Interpretação dos clusters
7. Recomendações de negócio
```

Perguntas respondidas:

* Quantos perfis de sellers existem?
* Quais sellers combinam alto volume com baixa satisfação?
* Quais sellers possuem maior risco operacional?
* Quais clusters deveriam ser priorizados pela Olist?
* Quais clusters representam oportunidades de crescimento?

Entregáveis:

* tabela `mart_seller_performance`;
* notebook de clusterização;
* descrição dos clusters;
* recomendações por grupo de sellers.

---

## 7. Tecnologias utilizadas

* Python
* Pandas
* NumPy
* PostgreSQL
* SQL
* SQLAlchemy
* Jupyter Notebook
* Matplotlib
* SciPy
* Statsmodels
* Scikit-learn
* Git e GitHub
* VSCode

---

## 8. Estrutura do repositório
>>>>>>> 4d126b5 (ajuste readme e avanço na analise)

```text
olist-decision-science/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── notebooks/
│   ├── 00_data_understanding.ipynb
│   ├── 01_exploratory_analysis.ipynb
│   ├── 02_statistical_tests.ipynb
│   ├── 03_regression_model.ipynb
│   └── 04_seller_clustering.ipynb
│
├── sql/
│   ├── 00_create_schemas.sql
│   ├── 01_raw_tables.sql
│   ├── 02_staging.sql
│   ├── 03_dw.sql
│   └── 04_marts.sql
│
├── src/
│   ├── config.py
│   ├── ingest_raw.py
│   └── utils.py
│
├── images/
│
├── reports/
│
├── .env.example
├── .gitignore
├── requirements.txt
└── README.md
```

<<<<<<< HEAD
## Primeiras análises previstas
=======
---

## 9. Orientações metodológicas

Este projeto não tem como objetivo apenas treinar modelos, mas sim construir uma análise orientada à tomada de decisão.

Por isso, cada etapa seguirá a lógica:

```text
Pergunta de negócio
↓
Hipótese
↓
Métrica
↓
Método
↓
Resultado
↓
Interpretação
↓
Recomendação
```

Sempre que possível, os resultados técnicos serão traduzidos para linguagem de negócio.

Exemplo:
>>>>>>> 4d126b5 (ajuste readme e avanço na analise)

```text
Resultado técnico:
Pedidos atrasados possuem review_score médio inferior e diferença estatisticamente significativa.

Interpretação de negócio:
Atrasos na entrega estão associados a uma pior experiência do cliente e devem ser monitorados como um indicador operacional crítico.
```

---

## 10. Resultados esperados

Ao final do projeto, espera-se entregar:

* uma base modelada em PostgreSQL;
* um processo organizado de ingestão e transformação dos dados;
* uma análise exploratória da satisfação do cliente;
* testes estatísticos sobre atraso, frete e complexidade do pedido;
* um modelo explicativo dos fatores associados à nota;
* uma clusterização de sellers;
* recomendações estratégicas para melhoria da experiência no marketplace.

---

## 11. Possíveis recomendações de negócio

Algumas recomendações esperadas ao final do projeto podem envolver:

* priorização de sellers com alta taxa de atraso;
* monitoramento preventivo de pedidos próximos ao prazo estimado;
* identificação de categorias com maior risco de avaliação negativa;
* criação de políticas específicas para sellers com alto volume e baixa satisfação;
* melhoria da comunicação com clientes em pedidos com risco de atraso;
* revisão de estratégia logística para clusters de sellers com pior desempenho operacional.

---

## 12. Status do projeto

Projeto em desenvolvimento.

Etapa atual:

```text
Data Understanding
```
