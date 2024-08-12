## Projeto Databricks: Ingestão + Análise de Vendas de uma loja de Eletrônicos
#### Schema das Tabelas do Projeto
<img src="https://github.com/marcelmarujo/Databricks-Vendas-Loja-Eletronicos/blob/master/Schema%20-%20Vendas%20Eletr%C3%B4nicos.jpeg?raw=true" alt="Schema do Projeto" width="500" />

### Passo a Passo da Execução:

1. **Inicialização e Configuração**
   - Inicia uma `SparkSession` com o nome "Exemplo de Dataset".
   - Importa funções necessárias do PySpark para manipulação de dados e criação de funções definidas pelo usuário (UDF).

2. **Criação e Manipulação do DataFrame de Vendas**
   - Define um conjunto de dados de exemplo contendo informações sobre vendas em uma loja.
   - Cria um DataFrame `df_Vendas_Loja1` a partir dos dados fornecidos.
   - Adiciona uma coluna `preco_total` que calcula o valor total da transação multiplicando a quantidade pelo preço unitário.
   - Adiciona uma coluna `País_cliente` com um país aleatório para cada linha usando uma função UDF.
   - Adiciona uma coluna `Atualizacao` com a data e hora atual no formato "yyyy-MM-dd HH:mm:ss".

3. **Persistência dos Dados**
   - Cria um banco de dados SQL `BD_ELETRONICOS_VENDAS` se ele não existir.
   - Salva o DataFrame `df_Vendas_Loja1` como uma tabela Delta chamada `Vendas_Eletronicos_Loja1` no banco de dados.

4. **Criação da Tabela de Dimensão de Clientes**
   - Define listas de IDs e nomes de clientes e cria um DataFrame `df_clientes`.
   - Salva o DataFrame `df_clientes` como uma tabela Delta chamada `CLIENTES`, substituindo qualquer tabela existente com o mesmo nome.

5. **Análise dos Dados**
   - Descobre o produto mais vendido agrupando os dados de vendas por produto e somando a quantidade vendida.
   - Descobre o produto que mais trouxe faturamento somando o valor total de vendas por produto.
   - Identifica o dia de maior faturamento somando o valor total de vendas por data.

6. **Detalhamento do Dia de Maior Faturamento**
   - Coleta os dados do dia de maior faturamento e filtra as vendas realizadas nesse dia.
   - Calcula a quantidade total, valor total e preço médio dos produtos vendidos no dia de maior faturamento.
   - Exibe os detalhes dos produtos vendidos nesse dia.

7. **Mescla de Tabelas**
   - Lê as tabelas `CLIENTES` e `Vendas_Eletronicos_Loja1` do banco de dados.
   - Faz uma mescla (left join) das tabelas `Vendas_Eletronicos_Loja1` e `CLIENTES` com base no `cliente_id`.
   - Exibe o DataFrame resultante da mescla.

8. **Identificação do Cliente Mais Rentável**
   - Agrupa os dados mesclados por nome do cliente e calcula o valor total gasto por cada cliente.
   - Ordena os clientes pelo valor total gasto e exibe os resultados, mostrando o cliente que mais consumiu.
