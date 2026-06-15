# Olist Decision Science

Projeto de análise exploratória e investigação de negócio utilizando a base pública **Brazilian E-Commerce Public Dataset by Olist**, disponível no Kaggle.

A base contém aproximadamente 100 mil pedidos realizados entre 2016 e 2018 em marketplaces no Brasil, com informações de pedidos, clientes, sellers, produtos, pagamentos, entregas, avaliações e geolocalização. Fonte: Kaggle/Olist.

## Objetivo do projeto

O objetivo deste projeto é entender o comportamento da base da Olist a partir de uma visão de negócio e Decision Science.

Algumas perguntas iniciais:

* Um cliente pode comprar de mais de um seller?
* Um pedido pode ter mais de um seller?
* A baixa recorrência de clientes representa comportamento real ou fragmentação da base?
* A análise de recorrência deve ser feita no nível cliente, seller ou cliente-seller?
* Quais variáveis podem explicar recompra, atraso, satisfação e comportamento dos pedidos?

## Como baixar os dados

Os arquivos originais não estão versionados neste repositório para evitar subir bases grandes no GitHub.

A base deve ser baixada diretamente pelo Kaggle:

**Dataset:** Brazilian E-Commerce Public Dataset by Olist
**Link:** https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce/data

### Opção 1 — Download manual

1. Acesse o link do dataset no Kaggle.
2. Faça login na sua conta Kaggle.
3. Clique no botão **Download**.
4. Extraia o arquivo `.zip`.
5. Coloque os arquivos `.csv` dentro da pasta:

```bash
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

## Estrutura do projeto

```text
olist-decision-science/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── data/
│   └── raw/
│
├── notebooks/
│   ├── 01_entendimento_dados.ipynb
│   ├── 02_analise_recorrencia_clientes.ipynb
│   └── 03_analise_sellers_pedidos.ipynb
│
├── src/
│   ├── __init__.py
│   ├── data_cleaning.py
│   ├── feature_engineering.py
│   └── analysis.py
│
├── reports/
│   └── figures/
│
└── docs/
    └── perguntas_negocio.md
```

## Primeiras análises previstas

1. Entendimento das tabelas e relacionamentos.
2. Validação da granularidade da base.
3. Análise de clientes recorrentes.
4. Análise da relação entre clientes, pedidos e sellers.
5. Análise de pedidos com múltiplos sellers.
6. Análise de atraso de entrega.
7. Análise de satisfação dos clientes via reviews.
8. Construção de hipóteses de negócio.

## Fonte dos dados

Dataset original:

Brazilian E-Commerce Public Dataset by Olist — Kaggle
https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce/data

A base foi publicada pela Olist e contém dados públicos de pedidos realizados no Brasil entre 2016 e 2018.
