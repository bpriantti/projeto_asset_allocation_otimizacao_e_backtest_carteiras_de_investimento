# Projeto Asset Allocation Otimização e Backtest de Carteiras de Investimento (Markowitz)

__Bussines Problem:__

> Durante a rotina de asset allocation torna-se importante a composicao de portifolios de ativos, estes que correspodem a unniao de ativos para a diversificacao de risco, no entanto torna-se importante o uso de metodos para a minimizacao de volatilidade ou aumento de retorno, para isso é importante o conceito de otimizacao backtest(teste no passado) de portifolios e tabem estimacao de maximo drawdown utilziando metodo de monte carlo.

__Objetivo:__

> Desenvolver uma ferramente que tenha a capacidade de receber a serie historica de ativos listados no indice Ibovespa - IBOV e implemente a otimizacao utilizando a teoria moderna de montagem de portifolios por Markovitz em seguida realizar otimizacoes para minima volatilidade e maximo indice de sharpe, posteriormente o backtest utlizando o metodo de walk-foward e estimacao de maximo drawdown pelo metodo de monte carlo.

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

> Para esse projeto utilizaremos todos os ativos listados no indice bovespa inicialmente vamos realizar um web-scrapping do site da b3 para extrair a lista de ativos:

<p align="center">
   <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_2.png?raw=true" height = 420>
   
#### wralling database:
   
__Removendo Nan's:__

<p align="center">
   <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_1.png?raw=true"  width="800" height = "270">

__Removendo Tickers Com Defeito de Market Data:__

<p align="center">
   <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_3.png?raw=true" height = 420>

<p align="center">
   <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_4.png?raw=true" height = 420>

Removidos:  ['ENGI11', 'GGBR4', 'PCAR3', 'SUZB3', 'TAEE11', 'UGPA3']
   
#### Implementando Janelas de Otimizacao e Backtest:
      
<p align="center">
   <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_5.png?raw=true" height = 320>
   
<p align="center">
   <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_7.png?raw=true" height = 320>
   
<p align="center">
   <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_6.png?raw=true" height = 420>
   
### Estatisticas Carteiras:  

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
