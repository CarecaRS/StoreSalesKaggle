
### <img src="https://github.com/CarecaRS/TCC_USP/blob/master/caution.png" width="48"> This profile is no longer maintained here on GitHub, it has been migrated to [Codeberg.org](https://codeberg.org/twerminghoff/). <img src="https://github.com/CarecaRS/TCC_USP/blob/master/caution.png" width="48">


# Desafio Store Sales

#### Link do desafio: https://www.kaggle.com/competitions/store-sales-time-series-forecasting/

## Contextualização do desafio
Através de análise temporal, os participantes devem calcular a quantidade de vendas prevista ('sales') para uma rede de mercados do Equador por um período de 15 dias - previsão individual e específica para cada uma das 54 lojas e para cada uma das 33 categorias de produtos disponíveis à venda.

Os resultados disponíveis no site da Kaggle na data de referência (30/05) tem como pior score o resultado 4.37970 e o melhor estava em 0.37768, com 671 participantes na data de referência. Esse resultado é calculado através de RMSLE (_Root Mean Squared Logarithmic Error_), ou seja, quanto menor, melhor.

## Objetivos específicos

Após uma breve modelagem naive praticamente sem manipulação alguma dos dados, obtive o resultado 2.94770. Sendo assim, estabeleci duas metas para este desafio: a meta base é reduzir esse score em, no mínimo, um ponto inteiro e a meta avançada é reduzir esse score em pelo menos dois pontos inteiros.

## Data wrangling

Minha primeira abordagem foi unir os datasets extras (como registro dos feriados ou do tipo da loja, por exemplo) aos datasets de treino e de teste de forma independente, o que foi feito de forma rápida e simples. Imediatamente depois já realizei alguns processos de feature engeneering, criando variáveis que identificassem, por exemplo, finais de semana ou sazonalidade mensal, também criando um indicador ordinal regressivo discreto dos dias de pagamento.

## EDA

Comecei então o trabalho de EDA com a matriz de correlação das variáveis, também identificando visualmente alguns outliers com auxílio dos gráficos gerados com esse fim específico. Após tratamento, criei uma seção específica para normalização dos dados através tanto de Z-Score como de Log. Como este procedimento é rápido, gosto de testar ambos métodos para selecionar o melhor durante a modelagem (se existente).

## Modelagem
Para a modelagem propriamente dita foram testados alguns regressores do pacote Scikit-Learn (HistGradientBoostRegressor, SGDRegressor, DecisionTree, entre outros), o pacote Darts, o pacote LightGBM e o pacote XGBoost. Os melhores resultados individuais, mesmo antes de ajuste fino da modelagem, foram todos com o pacote XGBoost.

Durante o processo de modelagem foram testados vários pré-processamentos do banco de dados, como normalização através de dois padrões diferentes e detecção de outliers, criação de dummies para variáveis categóricas, além de várias alterações nos hiperparâmetros dos regressores com o objetivo do melhor score possível no resultado final. 

## Sobre resultados e características dos modelos

A maior parte dos modelos gerados (independente de resultado ou de quaisquer um dos parâmetros) encontra-se catalogada no arquivo 'registros.txt', discriminadas por nome e data individualmente, além da descrição de variáveis, scores obtidos, níveis de significância de variáveis, hiperparâmetros utilizados em cada modelo, dentre várias outras informações. UPDATE: cada modelo realiza o registro em arquivo específico (a modelagem XGB continua registrando em 'registros.txt'), modelos ensemble também têm registro em arquivo próprio.

## Resultados dos objetivos específicos

Consegui reduzir meu primeiro score de 2.94770 para um mínimo de 1.50040 com modelagem independente e única (sem ensemble), logrando êxito na meta base com certa folga, mas infelizmente sem conseguir bater minha meta avançada de atingir um score abaixo de 1. UPDATE: Com metodologia ensemble, consegui reduzir o score ainda um pouco mais, para 1.43196.

Após várias modelagens com pacotes diferentes, janelas de tempo diferentes, hiperparâmetros diferentes, criação/exclusão de N variáveis do dataset, os scores ficaram estagnados na faixa de 1.50-1.60 nas modelagens individuais, o que me leva a concluir que não é necessariamente a modelagem ou o tunning dos modelos que estão pecando (minha hipótese original e persistente), e sim minha abordagem que encontra-se ineficaz.

## Considerações finais
Boa parte do código está inibido pois não é necessário para cada remodelagem nas etapas de fine-tuning do sistema.

Este estudo ficará em standby por pelo menos 6 meses e no máximo 1 ano, de modo a que em uma próxima oportunidade e depois de seguir trabalhando no campo de data science eu consiga abordar o problema de formas diferentes e inovadoras, de modo a conseguir um score e colocação melhor no desafio.
