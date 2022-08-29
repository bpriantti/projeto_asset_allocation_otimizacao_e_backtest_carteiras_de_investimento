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


Stat                 IBOV        Carteira Pesos Iguais    Carteira Mínima Volatilidade    Carteira Máximo Sharpe-Ratio
-------------------  ----------  -----------------------  ------------------------------  ------------------------------
Start                2012-01-02  2012-01-02               2012-01-02                      2012-01-02
End                  2021-12-30  2021-12-30               2021-12-30                      2021-12-30
Risk-free rate       0.00%       0.00%                    0.00%                           0.00%

Total Return         72.89%      315.56%                  266.61%                         340.93%
Daily Sharpe         0.35        0.72                     0.80                            0.74
Daily Sortino        0.56        1.12                     1.23                            1.16
CAGR                 5.63%       15.32%                   13.88%                          16.01%
Max Drawdown         -45.58%     -48.24%                  -40.26%                         -50.54%
Calmar Ratio         0.12        0.32                     0.34                            0.32

MTD                  2.76%       4.17%                    4.00%                           -3.35%
3m                   -5.39%      -4.13%                   4.64%                           -19.56%
6m                   -16.90%     -10.34%                  4.92%                           -20.08%
YTD                  -11.82%     -3.34%                   -1.54%                          -16.25%
1Y                   -11.82%     -3.34%                   -1.54%                          -16.25%
3Y (ann.)            4.68%       18.09%                   13.76%                          14.38%
5Y (ann.)            11.48%      21.37%                   14.13%                          19.38%
10Y (ann.)           5.63%       15.32%                   13.88%                          16.01%
Since Incep. (ann.)  5.63%       15.32%                   13.88%                          16.01%

Daily Sharpe         0.35        0.72                     0.80                            0.74
Daily Sortino        0.56        1.12                     1.23                            1.16
Daily Mean (ann.)    8.51%       17.55%                   15.03%                          18.19%
Daily Vol (ann.)     24.08%      24.42%                   18.72%                          24.54%
Daily Skew           -0.59       -0.87                    -1.24                           -1.14
Daily Kurt           11.55       13.94                    19.62                           17.91
Best Day             13.31%      12.77%                   9.71%                           11.03%
Worst Day            -14.24%     -15.64%                  -14.24%                         -16.58%

Monthly Sharpe       0.34        0.71                     0.88                            0.79
Monthly Sortino      0.56        1.24                     1.47                            1.36
Monthly Mean (ann.)  7.31%       16.82%                   14.56%                          17.61%
Monthly Vol (ann.)   21.51%      23.71%                   16.58%                          22.31%
Monthly Skew         -0.70       -0.62                    -1.08                           -0.86
Monthly Kurt         3.48        4.21                     6.04                            5.90
Best Month           15.77%      21.60%                   14.75%                          19.68%
Worst Month          -29.00%     -31.93%                  -24.15%                         -32.52%

Yearly Sharpe        0.38        0.60                     0.80                            0.95
Yearly Sortino       1.18        4.11                     26.86                           3.25
Yearly Mean          7.55%       17.59%                   13.69%                          17.61%
Yearly Vol           19.79%      29.25%                   17.08%                          18.58%
Yearly Skew          0.30        0.88                     1.45                            -0.29
Yearly Kurt          -1.72       -0.81                    2.02                            0.02
Best Year            36.23%      65.57%                   50.95%                          43.13%
Worst Year           -14.71%     -13.05%                  -1.54%                          -16.25%

Avg. Drawdown        -4.85%      -3.34%                   -2.43%                          -4.19%
Avg. Drawdown Days   70.90       33.51                    29.95                           39.61
Avg. Up Month        4.81%       5.40%                    3.78%                           5.03%
Avg. Down Month      -4.45%      -4.51%                   -3.50%                          -4.18%
Win Year %           55.56%      55.56%                   77.78%                          88.89%
Win 12m %            61.47%      69.72%                   86.24%                          90.83%



IBOV
  Year    Jan    Feb     Mar    Apr     May     Jun    Jul    Aug     Sep    Oct    Nov    Dec     YTD
------  -----  -----  ------  -----  ------  ------  -----  -----  ------  -----  -----  -----  ------
  2012   6.09   4.13   -1.88  -3.97  -11.27   -0.23   3.02   1.62    3.51  -3.38   0.67   5.73    2.7
  2013  -1.86  -3.71   -1.77  -0.74   -4.06  -10.66   1.53   3.45    4.38   3.45  -3.09  -1.75  -14.71
  2014  -7.07  -1.07    6.6    2.26   -0.71    3.54   4.72   9.24  -11.12   0.89   0.06  -8.04   -2.74
  2015  -5.82   9.32   -0.79   9.34   -5.83    0.57  -3.93  -7.84   -3.14   1.68  -1.53  -3.66  -12.5
  2016  -6.32   5.47   15.77   7.24   -9.52    5.91  10.56   0.98    0.76  10.65  -4.43  -2.58   36.23
  2017   7      2.93   -2.4    0.61   -3.92    0.29   4.57   7.11    4.67   0.02  -3.01   5.89   25.49
  2018  10.69   0.64   -0.13   0.85  -10.48   -4.99   8.5   -3.08    3.33   9.79   2.29  -1.74   14.42
  2019  10.43  -1.8    -0.17   0.95    0.68    3.93   0.81  -0.64    3.46   2.29   0.92   6.94   30.81
  2020  -1.85  -8.2   -29      9.82    8.24    8.44   7.99  -3.34   -4.65  -0.67  15.37   9.29    2.8
  2021  -2.69  -5.01    5.83   1.89    6       0.45  -3.85  -2.42   -6.39  -6.55  -1.49   2.76  -11.82


Carteira Pesos Iguais
  Year    Jan    Feb     Mar    Apr     May    Jun    Jul    Aug     Sep    Oct    Nov    Dec     YTD
------  -----  -----  ------  -----  ------  -----  -----  -----  ------  -----  -----  -----  ------
  2012   5.03   7.86    1.74  -0.31   -8.12   2.29   1.79   2.65    3.64   0.14  -0.08   4.04   21.72
  2013   1.79  -0.88   -1.65   0.6    -1.43  -8.4    1.23   1.6     5.44   3.69  -2.23  -1.25   -2.15
  2014  -7.25  -1.21    6.29   0.96    0.68   5.02   1.98   9.82  -11.2   -0.46   0.67  -7.64   -4.3
  2015  -8.74   8.04    0.25   8.54   -3.49   0.84  -5.22  -8.88   -2.42   4.17  -1.31  -3.87  -13.05
  2016  -7.47   7.48   21.6    8.41   -8.83   9.65  15.5    1.66   -0.69  11.17  -5.11  -0.4    60.55
  2017   9.32   4.93   -1.88   1.53   -4.83   0.31   6.13   8.38    3.91   0.09  -2.96   6.72   35.17
  2018   8.39  -0.08   -2.2    0.6   -11.3   -5.21   9.36  -4       1.36  15.24   3.17   0.14   13.51
  2019  14.58  -0.76    0.88   3.15    2.77   4.61   6      1.46    3.24   2.15   4.58   9.75   65.57
  2020   2.37  -7.98  -31.93  11.96    9.44   8.71   9.67  -4.3    -5.18  -1.19  16.62   8.58    6.36
  2021  -5.49  -2.02    8.66   2.42    6.73  -1.99  -3.02  -1.16   -2.43  -7.46  -0.56   4.17   -3.34


Carteira Mínima Volatilidade
  Year    Jan    Feb     Mar    Apr    May    Jun    Jul    Aug    Sep    Oct    Nov    Dec    YTD
------  -----  -----  ------  -----  -----  -----  -----  -----  -----  -----  -----  -----  -----
  2012   0.21   6.2     6.23   1.9   -3.21   3.05   2.14  -0.13   2.42   1.05  -0.1    3.56  25.48
  2013   3.16   1.27   -1.71   0.15   1.66  -4.66   1.31  -0.5    2.93   1.05   1.88  -2.55   3.73
  2014  -5.58   3.27    4.56   0.41   3.9    4.67  -1.87   7.17  -5.22   4.61   2.78  -2.7   16.08
  2015  -5.81   4.36    4.04   4.39   2.98   5.51  -0.73  -6.49  -3.66   2.77   1.46  -1.11   6.95
  2016  -3.56   4.29    7.78   1.45  -2.56   0.23   8.44   3.29   0.68   5.71  -6.15  -1.44  18.44
  2017   4.56   1.59   -0.99   5.76   2.47   0.25   3.99   3.6    1.27   0.09  -3      5.38  27.55
  2018   3.89   0.93    0.09   0.31  -8.49  -4.34   5.12  -2.84  -1.03   3.29   5.4   -1.7   -0.31
  2019  13.54  -2.02   -0.36   3.66   2.91   0.03   7.08  -1.89   4.83  -0.09   5.14  10.3   50.95
  2020   1.85  -7.36  -24.15   7.67   7.48   5.56   6.52  -5.54  -6.01  -0.58  14.75   7.44   1.35
  2021  -3.92  -4.23    4.03   0.34   3.27  -5.38  -1.18   2.75  -1.25   1.42  -0.79   4     -1.54


Carteira Máximo Sharpe-Ratio
  Year    Jan    Feb     Mar    Apr    May    Jun    Jul    Aug    Sep    Oct    Nov    Dec     YTD
------  -----  -----  ------  -----  -----  -----  -----  -----  -----  -----  -----  -----  ------
  2012   0.14   8.68    3.13   5.02  -8.73   0.48   0.95   3.59  -7.71   1.35   5.39   2.1    13.77
  2013   5.4    2.63   -3.02   0.07   0.71  -5.21  -0.68   1.18   2.42   0.09   3.65  -1.44    5.46
  2014  -5.08   0.2     6.52   2.26   5.54   7.44  -2.81   5.06  -3.88   6.99   2.4   -6.75   17.79
  2015  -2.22   2.85   -0.53   6.9    3.18  11.1    1.96  -6.13  -0.56  -2.39   0.73  -3.98   10.15
  2016   0.65   2.31    0.51   1.33  -5.49  -0.16   4.18  -0.71   2.74  13.34  -2.63   1.8    18.15
  2017   6.53   6.22   -3.95  12.85  -0.08  -3.27   7.35   9.26  -0.06   2.18  -6.01   7.25   43.13
  2018   4.21  -4.34   -1.67   7.57  -9.41  -2.28   6.25   0.73   2.11   8.43  -3.45   1.87    8.76
  2019  12.59  -2.53   -0.31   1.15   4.95   0.46   4.74   2.38   0.5   -0.4   -0.53  12.06   39.61
  2020   7.55  -8.21  -32.52  19.68  11.73  13.5   13.19  -3.36  -5.66  -0.82  15.42  10.26   31.71
  2021   3.01  -2.07    2.69   4.13  -2.62  -0.24   4.9   -7.57   2.46  -9.37  -8.17  -3.35  -16.25
