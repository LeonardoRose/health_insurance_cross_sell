# Projeto: Health Insurance CrossSell
Este repositório contém todos os arquivos do projeto Health Insurance CrossSell, onde foi realizado a previsão da propensão de compra de cada clientes através de algoritmos de classificação.

# 1. Problema de Negócio
A empresa fictícia Security&Safe é uma empresa dos Estados Unidos que atua em todo o território americano e apesar de ser o principal player do mercado de seguros automotivos, está perdendo  ano a ano o seu market share e faturamento e se nada mudar, logo será ultrapassada pela sua principal concorrente. 

Para reverter essa situação e voltar a ser a empresa referencia do setor, a diretoria está executando algumas mudanças, como:
1. Corte do quadro de funcionários
2. Expansão do time Dados com foco em profissionais com conhecimento de Ciências de Dados e Machine Learning
3. Expansão do portfólio de seguros com o lançamento de um novo produto: Seguro de Vida
   
A respeito do lançamento de novos produtos, antes das mudanças a área de Suporte a Vendas era responsável por ligar para toda a sua base de clientes oferecendo o novo produto, porém essa área teve seu quadro de funcionários reduzido para 40%, tornando a estratégia antiga inviável, mas isso não é desculpa para a Diretoria, eles querem os mesmos resultados ou até mesmo resultados melhores que antes da mudança!

Com os novos Cientista de Dados no time, a proposta para solução desse problema é que seja criado um modelo de Machine Learning que atribua a propensão de compra (score) de cada cliente e que após atríbuido o score, o time de Suporte a Vendas ligue para os 40% de clientes mais propensos, de modo que capture o máximo dos clientes compradores possível!

# 2. Premissas
Para conseguir mensurar o impacto financeiro da adoção do modelo Machine Learning, foi estimado alguns valores fictícios como:
1. Custo da ligação para clientes
2. Lucro por seguro de vida vendido
3. Total de Clientes
4. % de Clientes Compradores   

# 3. Produto Final
O produto final será um Google Sheets onde será preenchido os dados do clientes e retornará o respectivo score do cliente.

# 4. Estratégia da Solução

![This is an image](https://miro.medium.com/v2/resize:fit:640/0*tA5OjppLK627FfFo)

A solução seguirá as etapas do framework CRISP-DM, que é composta por seis fases sequenciais e de modo ciclico: 
  1. Entendimento do problema de negócios
  2. Entendimento dos dados disponíveis
  3. Preparação dos dados
  4. Modelagem de dados
  5. Avaliação do modelo
  6. Deploy do modelo

Para a seleção do modelo de machine learning mais adequado, priorizaremos a métrica de Recall. Nosso principal objetivo é maximizar a identificação dos casos positivos, ou seja, dos potenciais compradores. No entanto, considerando o contexto de negócio, sobre a redução do quadro de funcionários para 40% e os contatos com os potenciais compradores são realizados por meio de chamadas telefônicas, limitando o alcance da equipe de Suporte a Vendas a apenas 40% da base, avaliaremos o Recall com base nos 40% dos clientes mais propensos. Esses 40% serão definidos como os clientes com os maiores scores atribuídos pelo modelo de machine learning. Durante a construção do modelo, referiremos a essa métrica como recall_at_k, sendo K=40%.
Para agregar na explicabilidade do problema, iremos usar a Curva Lift, que indica quantas vezes melhor o modelo está performando em relação a um modelo aleatório, que é exatamente a atual estratégia da empresa, onde são feitas ligações de modo aleatório para sua base de clientes oferecendo os produtos.

# 5. Desempenho dos Modelos de Machine Learning

  No primeiro ciclo do CRISP foi testado 4 algoritmos com o objetivo de encontrar o modelo com a melhor performance. Usou-se como Baseline o cenário atual, que é um cenário sem Machine Learning, onde as ligações são aleatórias, portanto se 40% dos clientes forem contactados, é esperado que dessa lista, 40% sejam compradores.
  Após os testes foram obtidos os seguintes resultados para cada modelo:
  
  | Modelo | Recall at 40% | Curva Lift | 
  | ------ | ------ | ------ | 
  | Gradient Boosting Classifier |93.04%|2.33|
  | XGBoost Classifier	 |92.95%|2.32|
  | Linear Regression	 |91.83%|2.29|
  | K-Nearest Neighbors |91.71%|2.27|
  | Baseline - Cenário Atual: Sem ML |40.00%|1|
  
# 6. Modelo Final e Performance

Avaliando a métrica Recall, o modelo que teve melhor performance foi o Gradient Boosting Classifier, cujo Recall foi de 93.04%, em outras palavras, 93% dos compradores estavam entre os 40% clientes com maior score. A curva Lift teve um valor de 2.33, indicando que enquanto um modelo aleatório teria identificado 1 cliente comprados, o nosso modelo de ML teria indicado 2.33 clientes. Abaixo podemos ver graficamente ambas as métricas.

## 6.1. Recall at 40% - Gradient Boosting Classifier
![This is an image](https://imgur.com/AugqyLw.png)

## 6.2. Curva Lift - Gradient Boosting Classifier
![This is an image](https://i.imgur.com/bD3NSI8.png)

# 7. Resultado de Negócios
Quais são os benefícios para a empresa adotar o modelo de machine learning para atribuir scores aos clientes? Para isso, devemos traduzir o desempenho do modelo para o idioma dos negócios, que é dinheiro. Ou seja, qual é meu lucro esperado sem o modelo? E com o modelo? Para isso, iremos adotar as seguintes premissas:

| Premissa | Valor | 
| ------ | ------ |
| Base Clientes | 1000 |
| % Compradores | 10% |
| Compradores | 100 |

# 7.1. Cenário Baseline - Sem Machine Learning

| Entrada / Saída | Quantidade | Valor Unitário | Valor Total | 
| ------ | ------ | ------ | ------ |
| Custo Ligação | 400 | -5 | -2000 |  
| Lucro por Venda | 40 | 2000 | 80000 | 

# 8. Entregando o Produto Final



