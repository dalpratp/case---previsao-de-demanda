Case realizado para conclusão da Capacitação em Ciência de Dados, promovida pela VAI Academy em parceria com a americanas s.a.

São disponibilizadas 3 bases de dados: informações estáticas sobre lojas, como tamanho e tipo, dados de vendas semanais segmentadas por loja e departamento ao longo de 2,5 anos e fatores externos, como preços de combustíveis, IPC e taxa de desemprego.

A proposta consistiu em, com base nos dados disponíveis, prever a venda semanal segmentada por loja para os 6 meses seguintes.

O trabalho foi realizado em grupo de 5 pessoas ao longo de 3 semanas, com período de 1 semana para esclarecer dúvidas com um time de negócios simulado.

Feita a EDA, foram criadas features tradicionais de time series (lag features, médias rolantes, diferenciações etc.) e também diversas clusterizações das lojas a partir de features e conjuntos de features distintos, buscando fornecer ao modelo final informações de contexto.

O modelo final adotado foi um LGBM devido à capacidade de encontrar relações não lineares entre as variáveis, sua robustez e capacidade de receber entradas categóricas e nulas sem processamento adicional (embora esse tenha sido testado) e, principalmente, sua agilidade em iterar novos conjuntos de hiperparâmetros. Além disso, é amplamente difundida a noção de que ensembles de árvores de decisão com boosting, como XGBoost e LGBM, tem boa performance para dados tabulares, sendo frequentes em soluções vencedoras em competições de Machine Learning com esse tipo de dados.

A estratégia utilizada foi uma previsão Multi-Shot, em que todas as datas do conjunto de previsão são obtidas simultaneamente utilizando todo o conjunto de dados disponíveis. Evitando assim de ter um modelo para cada loja ou para cada período de previsão, é possível traçar conclusões mais assertivas sobre as features que mais influenciam o modelo, suas limitações e suas vantagens.

Foi realizada também a seleção de variáveis usando Recursive Feature Elimination e removendo as variáveis menos importantes, obtidas a partir do método feature_importances_ da instância LGBM.

O scoring utilizado para avaliar o modelo foi o WMAPE por conciliar a necessidade de compreensão no contexto de negócios sem as desvantagens da métrica MAPE, em que divisões por números muito pequenos ou zero podem afetar a avaliação do score final. Um score de 10% como meta de erro máximo foi definido com base em pesquisas realizadas pelo grupo.

Foi implementado também um loop criando modelos ARIMA de maneira automatizada para cada loja para se ter um baseline e poder comparar se o modelo final foi adequado para o problema proposto.

A conclusão final é que os objetivos foram atingidos e que a baseline foi superada com um modelo explicável e com tempo de treino e previsão adequados para a tarefa proposta. Foram obtidos insights relevantes para o negócio quanto a lojas com comportamentos interessantes, que podem ser estudados e potencialmente replicados em outras lojas, e efeitos de sazonalidade que podem ser investigados. Atenção especial foi dada para as épocas com maiores picos de vendas, sendo elas Black Friday, Natal e as duas semanas que precedem o Natal, e os resultados obtidos foram considerados apropriados.

Apenas uma loja não obteve erro dentro do esperado, sendo feita a recomendação de que se estude se esse comportamento é inerente à loja ou se é devido a alguma anomalia que não deve se repetir. Esse estudo, também, poderia tornar o modelo mais robusto.
 
