# Pipeline-de-dados-no-Telegram

## Contexto
O projeto visa analisar dados de chatbots do Telegram, extraindo insights estratégicos para melhorar a experiência do usuário. Utiliza um pipeline ETL para processar mensagens de forma escalável com AWS Lambda, S3 e EventBridge.

## Arquitetura
O fluxo é dividido em duas partes:

Transacional: O bot do Telegram envia mensagens via AWS API Gateway, armazenadas no S3.
Analítica: Um processo ETL diário converte os dados, otimizando consultas no AWS Athena.

## Dados
As mensagens captadas pelo bot são salvas em JSON, contendo informações como usuário, chat, data e conteúdo. O processo de data wrangling transforma esses dados semiestruturados em um formato padronizado.

## Ingestão
Um AWS Lambda recebe as mensagens via API Gateway e as salva no S3. Um webhook no Telegram direciona as mensagens automaticamente para esse pipeline.

## ETL
Diariamente, um AWS Lambda processa os arquivos JSON do dia anterior, transforma e compacta os dados no formato Parquet, armazenando-os em um bucket S3 de dados enriquecidos.

## Apresentação

## Análise
Uma explanação detalhada dos dados de acordo com as consultas no AWS Athena.

## Conclusões
Observações sobre os insights e sugestões de diretrizes a serem tomadas.
