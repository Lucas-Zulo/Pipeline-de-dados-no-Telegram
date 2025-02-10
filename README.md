# Pipeline-de-dados-no-Telegram

## Contexto
O projeto visa analisar dados de chatbots do Telegram, extraindo insights estratégicos para melhorar a experiência do usuário. Utiliza um pipeline ETL para processar mensagens de forma escalável com AWS Lambda, S3 e EventBridge.

## Arquitetura
O fluxo é dividido em duas partes:

Transacional: O bot do Telegram envia mensagens via AWS API Gateway, armazenadas no S3 em formato JSON.
Analítica: Um processo ETL diário converte os dados em Parquet, otimizando consultas no AWS Athena.

## Dados
As mensagens captadas pelo bot são salvas em JSON, contendo informações como usuário, chat, data e conteúdo. O processo de data wrangling transforma esses dados semiestruturados em um formato padronizado.

## Ingestão
Um AWS Lambda recebe as mensagens via API Gateway e as salva no S3. Um webhook no Telegram direciona as mensagens automaticamente para esse pipeline.

## ETL
Diariamente, um AWS Lambda processa os arquivos JSON do dia anterior, transforma e compacta os dados no formato Parquet, armazenando-os em um bucket S3 de dados enriquecidos.

## Apresentação
6.1. No AWS Athena, que se conecta aos dados armazenados no AWS S3, foi criada uma tabela para facilitar a consulta dos dados. O Athena permite análise direta dos dados no S3 sem necessidade de transferência.

6.2. O comando MSCK REPAIR TABLE foi utilizado para carregar as partições da tabela, garantindo que o Athena reconheça corretamente a estrutura dos dados armazenados.

6.3. Foi executado o comando SELECT * FROM telegram LIMIT 10, que retorna as 10 primeiras linhas da tabela, permitindo uma visualização inicial dos dados carregados.

## Análise
Quantidade de mensagens por dia: Consulta realizada para identificar o volume de mensagens enviadas em cada dia.
Quantidade de mensagens por usuário por dia: Permite entender quais usuários são mais ativos diariamente.
Média do tamanho das mensagens por usuário por dia: Mede a extensão média das mensagens, revelando padrões de comunicação.
Quantidade de mensagens por hora/dia da semana/número da semana: Analisa os horários e dias da semana com maior atividade no grupo.
Storytelling
A análise revelou padrões de comportamento dos usuários, identificando frequência de mensagens, horários preferidos e temas recorrentes. Alguns insights importantes:

Todas as mensagens analisadas foram enviadas no dia 07/02/2025.
O comprimento médio das mensagens variou entre 11 e 52 caracteres.
Lucas enviou tanto a mensagem mais curta quanto a mais longa.
Todas as mensagens foram enviadas na sexta-feira, com pico de atividade às 18h.
As palavras mais recorrentes incluem "API", "integração", "analítica" e "bots", sugerindo que o grupo tem um foco profissional/tecnológico.
Não foram identificados bots enviando mensagens, indicando que a comunicação é predominantemente humana.

## Conclusões
Pico de mensagens às 18h pode indicar um evento específico ou um padrão noturno dos usuários.
Tópicos frequentes ligados à tecnologia sugerem um ambiente profissional/estudantil.
Diferença no tamanho das mensagens pode refletir diferentes estilos de comunicação (saudações curtas vs. instruções mais detalhadas).
Predomínio de mensagens de um único usuário pode indicar baixa participação no grupo.
Atividade concentrada na sexta-feira sugere que o grupo tem uma interação semanal e pode necessitar de acompanhamento em outros dias.
Esse tipo de análise pode ser aprimorado com mais dados ao longo do tempo, permitindo uma visão mais robusta do comportamento dos participantes. 🚀
