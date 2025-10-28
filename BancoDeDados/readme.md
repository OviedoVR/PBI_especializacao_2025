# Varejista global de eletrônicos (Global Electronics Retailer)

Dados de vendas para um varejista global de eletrônicos (fictício), incluindo tabelas
contendo informações sobre transações, produtos, clientes, lojas e taxas de câmbio.

## Análises recomendadas

1. Que tipos de produtos a empresa vende, quantos produtos ela tem por subcategoria e onde os clientes estão localizados?
2. Há algum padrão ou tendência sazonal para volume de pedidos ou receita?
3. Qual é o tempo médio de entrega em dias? Isso mudou ao longo do tempo?
4. Em que cagetoria e subcategoria os clientes gastam? (adicione um filtro por filial)

## Origem da base de dados

Neste caso, vamos subir os dados para o Google Cloud Platform (GCP) e criar um
banco de dados utilizando o Google BigQuery. A ideia é conectar o Power BI
ai banco de dados criado, já que temos múltiplas tabelas.

## Passos no GCP e no BigQuery:

1. Criar projeto no GCP
2. Acessar BigQuery
3. Criar pasta no banco de dados
4. Subir tabelas (com opção "detectar schema")
5. Conectar os dados no Power BI (pode ser via import direto ou query)


## DAX utilizada na conversão de moeda (padronização em USD)

```
Revenue_USD = SWITCH(
    TRUE(),
    sales[Currency Code] <> "USD",
    sales[Revenue] * RELATED(exch_avg_period[Avg_rate]),
    sales[Revenue]
)
```

Lógica (neste casso podemos utiliza várias condições, se necessário):

```
Revenue_USD = SWITCH(
    TRUE(),
    <expressao>, 
    <resultado>,
    <else>
)
```