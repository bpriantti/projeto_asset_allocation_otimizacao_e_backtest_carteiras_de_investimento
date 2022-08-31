# Projeto Asset Allocation Otimização e Backtest de Carteiras de Investimento (Markowitz)

__Bussines Problem:__

> Durante a rotina de asset allocation torna-se importante a composicao de portifolios de ativos, estes que correspodem a unniao de ativos para a diversificacao de risco, no entanto torna-se importante o uso de metodos para a minimizacao de volatilidade ou aumento de retorno, para isso é importante o conceito de otimizacao backtest(teste no passado) de portifolios e tabem estimacao de maximo drawdown utilziando metodo de monte carlo.

__Objetivo:__

> Desenvolver uma ferramenta que tenha a capacidade de receber a série histórica de ativos listados no índice Ibovespa - IBOV e implemente a otimização utilizando a teoria moderna de montagem de portfólios por Markowitz em seguida realizar otimizações para mínima volatilidade e máximo índice de sharpe, posteriormente o backtest utilizando o método de walk-forward.

__Autor:__  
   - Bruno Priantti.
    
__Contato:__  
  - bpriantti@gmail.com

__Encontre-me:__  
   -  https://www.linkedin.com/in/bpriantti/  
   -  https://github.com/bpriantti
   -  https://www.instagram.com/brunopriantti/
   
__Frameworks Utilizados:__

- Numpy: https://numpy.org/doc/  
- Pandas: https://pandas.pydata.org/
- Matplotlib: https://matplotlib.org/ 
- Seaborn: https://seaborn.pydata.org/  
- Plotly: https://plotly.com/  
- Scikit learn: https://scikit-learn.org/stable/index.html
- Statsmodels: https://www.statsmodels.org/stable/index.html
- Fin Quant: https://pypi.org/project/FinQuant/
- BackTest: https://pypi.org/project/bt/
___

### __Project Steps:__

#### 1 - import database:

   > Para esse projeto utilizaremos todos os ativos listados no indice bovespa inicialmente vamos realizar um web-scrapping do site da b3 para extrair a lista de ativos e seguida realizou-se a conexao em api com os dados da yfinance para obter series historicas dos tickers(ativos) extraidos do site da b3, visualmente verificou-se defeitos de marketdata na base tornan-do necessesario um wralling da base.

<p align="center">
   <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_2.png?raw=true" height = 400>
   
#### wralling database:
   
- __Removendo Nan's:__

   > Inicialmente verificou-se a quantidade de dados faltantes na base de dados, utilizando o metodo de heatmap por nan's e foram removidas as colunas com o dados faltantes, como ilustrado abaixo:
   
<p align="center">
   <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_1.png?raw=true"  width="800" height = "220">

- __Removendo Tickers Com Defeito de Market Data:__

   > Normalmente visualizamos spikes de preços excessivos no momento em que o provedor de dados atualiza bases que estavam desatualizadas a dias, vamos verificar isso com um boxplot do retorno de todas as ações da base:
   
<p align="center">
   <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_3.png?raw=true" height = 400>
   
   > Verificou-se na base defeitos de dias seguidos, sabemos que por características das ações em momentos de baixa volatilidade os preços tendem a oscilar menos no entanto o defeito de dias seguidos pode ser definido com um range alto de dias por exemplo 20 dias sem atualizações de preço, isso provavelmente pode ser um defeito de market data, portanto desenvolveu-se uma função para verificar essas ocorrências e mostra-se o resultado na figura abaixo:
   
<p align="center">
   <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_4.png?raw=true" height = 400>

tickers removidos por defeito de market data:
   > Removidos:  ['ENGI11', 'GGBR4', 'PCAR3', 'SUZB3', 'TAEE11', 'UGPA3']
   
#### Implementando Janelas de Otimizacao:
   
   > Para o projeto em questao utilizaremos a biblioteca em python chamada - finquant (links abaixo), realizou-se a sepracao dos dados em janelas, realizando a otimizacao para minima volatilidade e depois para maximo sharpe-ratio, armazenando os dados em um dicionario para posterior backtest das carteiras, a biblioteca, optou-se por realizar a otimizacao pela fronteira eficiente da teoria moderna de alocacao de portigolios indealizada por markowitz.

<p align="center">
   <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_8.PNG?raw=true" height = 280e>
    
         
Janelas temporal - train-opt-test:  
   
         {2011: <finquant.portfolio.Portfolio at 0x7f206b6e3690>,
          2012: <finquant.portfolio.Portfolio at 0x7f206b6e34d0>,
          2013: <finquant.portfolio.Portfolio at 0x7f206b74ad50>,
          2014: <finquant.portfolio.Portfolio at 0x7f206b6e33d0>,
          2015: <finquant.portfolio.Portfolio at 0x7f20683e1650>,
          2016: <finquant.portfolio.Portfolio at 0x7f2068c57c10>,
          2017: <finquant.portfolio.Portfolio at 0x7f206879ffd0>,
          2018: <finquant.portfolio.Portfolio at 0x7f206b74ac90>,
          2019: <finquant.portfolio.Portfolio at 0x7f20683ea8d0>,
          2020: <finquant.portfolio.Portfolio at 0x7f2068681110>,
          2021: <finquant.portfolio.Portfolio at 0x7f2068579710>}
 
> obs: estabeleceu-se um limite para o peso de um ativo na carteira no valor de __peso_min = 0.001__

__Otimizacao de carteira para minima volatilidade:__

- script calculo composicao de pesos da carteira, minima volatilidade:

         pesos_min_vol = pd.DataFrame(index=database.index, columns=database.columns)

         for ano in optbase.keys():
             pesos_min_vol.loc[pesos_min_vol.index.year == (ano+1),:] =  optbase[ano].ef_minimum_volatility().T.values

         #---
         pesos_min_vol.dropna(inplace=True)
         pesos_min_vol.where(pesos_min_vol > peso_min, 0, inplace=True)

         pesos_min_vol.head()
   
- verificando quantidade de ativos ao decorrer do tempo de teste a carteira de __minima volatilidade__:

   <p align="center">
      <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_5.png?raw=true" height = 300>

__Otimizacao de carteira para maximo sharp-ratio:__

- script calculo composicao de pesos da carteira, maximo sharp-ratio:

         pesos_max_sr = pd.DataFrame(index=database.index, columns=database.columns)

         for ano in optbase.keys():
             pesos_max_sr.loc[pesos_max_sr.index.year == (ano+1),:] = optbase[ano].ef_maximum_sharpe_ratio().T.values

         pesos_max_sr.dropna(inplace=True)
         pesos_max_sr.where(pesos_max_sr > peso_min, 0, inplace=True)

         pesos_max_sr.head()

- verificando quantidade de ativos ao decorrer do tempo de teste a carteira de __maximo sharp-ratio__:

   <p align="center">
   <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_7.png?raw=true" height = 300>

### backtest e comparacao das carteiras otimizadas com o benckmark:

> Apos a otimizacoes realizou-se o backtest das carteiras para cada intervalo de tempo utilizando o biblio, backtest, verificando o resultado do backtest e comparando as carteiras com o benchmark idice ibovespa e uma carteira com pesos iguais, analisando a tabela abaixo observamos que abordagem foi vencedora ao longo do periodo de backtest ultrapassando o benchmark e tambem a carteira de pesos iguais, analizando as estatisticas observamos que a carteira de minima volatilidade obteve um drawdown inferior as demais, e a carteira com maximo sharpe-ratio obteve a melhor rentabilidade entre as carterias sendo este o nosso objetivo.
   
- Estatisticas Carteiras:  

Stat                | IBOV        |Carteira Pesos Iguais   | Carteira Mínima Volatilidade   | Carteira Máximo Sharpe-Ratio
------------------- | ----------  |----------------------- | ------------------------------ | ------------------------------
Start               | 2012-01-02  |2012-01-02              | 2012-01-02                     | 2012-01-02
End                 | 2021-12-30  |2021-12-30              | 2021-12-30                     | 2021-12-30
Risk-free rate      | 0.00%       |0.00%                   | 0.00%                          | 0.00%
Total Return        | 72.89%      |315.56%                 | 266.61%                        | 340.93%
Daily Sharpe        | 0.35        |0.72                    | 0.80                           | 0.74
Daily Sortino       | 0.56        |1.12                    | 1.23                           | 1.16
CAGR                | 5.63%       |15.32%                  | 13.88%                         | 16.01%
Max Drawdown        | -45.58%     |-48.24%                 | -40.26%                        | -50.54%
Calmar Ratio        | 0.12        |0.32                    | 0.34                           | 0.32
   
___

<p align="center">
   <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_6.png?raw=true" height = 400>

__Verificando Correlacao das Carteiras:__

> Podemos observar que as a correlacao das carteiras pelo hearmap abaixo, obviamente as carteiras sao altamente correlacionadas pois derivam do mesmo mercado, poderiamos montar em um trabalho futuro a asset allocation, em carteiras com mercados minimamente descorrelacionados.

<p align="center">
   <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_9.png?raw=true" height = 400>
