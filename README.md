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

__Project Steps:__

1 - import database:

> Para esse projeto utilizaremos todos os ativos listados no indice bovespa inicialmente vamos realizar um web-scrapping do site da b3 para extrair a lista de ativos:

   > <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_1.png?raw=true"  width="800" height = "270">


   > <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_2.png?raw=true">

   > <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_3.png?raw=true">
   > <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_4.png?raw=true">
   > <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_5.png?raw=true">
   > <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_7.png?raw=true">
   > <img src="https://github.com/bpriantti/projeto_asset_allocation_otimizacao_e_backtest_carteiras_de_investimento/blob/main/files_/image_6.png?raw=true">

