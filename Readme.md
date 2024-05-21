# <a name="_ge9zg4swd1q"></a>Desenvolvimento e Avaliação de uma Arquitetura Distribuída para o Cadastro Ambiental Rural

## <a name="_g76opdrensik"></a>Arquitetura


Para o projeto, foi adotada uma arquitetura baseada em tecnologias modernas de processamento de Big Data. O Ambiente de Desenvolvimento escolhido foi o **Databricks** e o projeto foi desenvolvido nas etapas "Bronze", "Silver" e "Gold".

Os dados da camada Bronze foram importados para o **Databricks File System (DBFS)** do **Amazon S3** e foram salvos como arquivos Parquet. Como a camada armazena dados brutos, foi focado em escolher uma tecnologia que seria tolerante a falhas e escalável.

Em seguida, nas camadas Silver e Gold, os dados foram armazenados em **Delta Lakes** a fim de otimizar o processamento analítico.

Para as Consultas Analíticas foi utilizado o **Spark SQL**, para catalogação dos metadados, o **Hive.**
## <a name="_f9axk8o6e3ks"></a>Tratamento dos Dados
- Remoção de duplicatas:
  - Foram removidas 4 linhas
- Remoção de 4 colunas não utilizadas: 
  - data\_alteracao\_condicao\_cadastro
  - modulos\_fiscais
  - area\_reserva\_legal\_averbada
  - area\_reserva\_legal\_aprovada\_nao\_averbada
- Remoção de nulos da coluna data\_inscricao:
  - Foram removidas 12 linhas

## <a name="_h8v0otnsmw91"></a>Particionamento
Na camada Silver, a estratégia de particionamento foi projetada visando uma distribuição eficiente dos dados e otimização das consultas. 

temas\_ambientais: Particionado por 'uf' e 'ano\_inscricao', permitindo consultas por unidade federativa e ano de inscrição.

Essa estratégia de particionamento foi escolhida com base nos requisitos de consultas analíticas esperadas, priorizando a eficiência e a otimização do desempenho das consultas.

## <a name="_ill63m4cvkfm"></a>Consultas Analíticas

Na camada Gold, foram criadas duas tabelas para suportar análises mais detalhadas e específicas:

1. temas\_ambientais\_por\_regiao: Essa tabela foi criada para segmentar os dados pelas regiões do Brasil, permitindo análises regionais específicas.
1. propriedades\_area\_nativa\_uf: Essa tabela concentra informações sobre propriedades com área remanescente de vegetação nativa, o que é fundamental para análises ambientais.

Além disso, foram realizadas consultas analíticas diversas, incluindo cálculos de áreas, contagens, médias e comparações entre diferentes conjuntos de dados, proporcionando insights valiosos para a tomada de decisões.


