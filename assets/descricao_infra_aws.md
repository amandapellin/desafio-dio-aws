
## Descrição do Fluxo da Arquitetura
Este modelo de arquitetura sem servidor (serverless) foi projetado para ser altamente escalável, resiliente e com custo-efetivo, processando os pedidos dos parceiros de forma assíncrona.

**1. Recebimento do Pedido (Entrada):**

- Um Parceiro B2B (ex: uma rede de farmácias) envia um novo pedido através de uma chamada de API segura.

- O Amazon API Gateway atua como a porta de entrada. Ele recebe a requisição, a autentica e a valida, garantindo que apenas parceiros autorizados possam enviar pedidos.

**2. Enfileiramento e Desacoplamento:**

- Em vez de processar o pedido imediatamente (o que poderia sobrecarregar o sistema em horários de pico), o API Gateway simplesmente publica os dados do pedido como uma mensagem na fila do Amazon SQS (Simple Queue Service).

- **Vantagem de Custo:** Isso desacopla o sistema de recebimento do sistema de processamento. A empresa não precisa manter servidores caros esperando por pedidos; a fila armazena os pedidos de forma segura e barata até que possam ser processados.

**3. Processamento Sob Demanda:**

- A chegada de uma nova mensagem na fila do SQS aciona automaticamente uma função no AWS Lambda.

- **Vantagem de Custo:** O código da função Lambda só é executado quando há um pedido para processar. A Abstergo Industries paga apenas pelos milissegundos de computação utilizados, eliminando 100% do custo com recursos ociosos.

**4. Execução da Lógica de Negócio:**

- A função Lambda contém a lógica de negócio: ela lê os dados do pedido da mensagem, interage com o Banco de Dados Existente para verificar o estoque, validar informações do cliente e processar o faturamento.

**5. Armazenamento de Documentos:**

- Após o processamento, a função Lambda gera os documentos necessários, como a Nota Fiscal Eletrônica (NF-e) ou uma confirmação de pedido em PDF.

- Esses documentos são salvos diretamente no Amazon S3, utilizando a classe de armazenamento Intelligent-Tiering.

- **Vantagem de Custo:** O S3 Intelligent-Tiering move automaticamente os documentos para camadas de armazenamento mais baratas à medida que se tornam menos acessados, otimizando os custos de armazenamento a longo prazo sem nenhuma gestão manual.
  
Este design garante que a "Abstergo Industries" possa lidar com qualquer volume de pedidos, desde um até milhões por dia, pagando estritamente pelo que usa e garantindo que nenhum pedido seja perdido.






