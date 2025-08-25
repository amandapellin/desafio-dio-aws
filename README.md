# RELATÓRIO DE IMPLEMENTAÇÃO DE SERVIÇOS AWS

Data: 25 de Agosto de 2025<br>
Empresa: Abstergo Industries<br> 
Responsável: Amanda Talita P. Pellin

## Introdução
Este relatório apresenta o processo de implementação de ferramentas na empresa Abstergo Industries, realizado por Amanda Pellin. O objetivo do projeto foi elencar 3 serviços da Amazon Web Services (AWS), com a finalidade de realizar uma diminuição de custos imediatos e otimizar a comunicação com empresas e farmácias parceiras. A implementação destes serviços visa modernizar a infraestrutura de TI, tornando-a mais elástica, escalável e com um custo operacional reduzido. Uma análise detalhada do impacto financeiro, que projeta uma economia de até 64%, pode ser encontrada na Planilha de Estimativa de Custos (Anexo 1).

## Descrição do Projeto
O projeto de implementação de ferramentas foi dividido em 3 etapas, cada uma focada em um serviço específico da AWS para abordar diferentes frentes de otimização de custos e eficiência operacional. O Diagrama da Arquitetura Proposta (Anexo 2) ilustra visualmente como estes três serviços se integram para criar um fluxo de trabalho coeso e automatizado. A descrição detalhada do fluxo da arquitetura pode ser consultado no Anexo 2.1. A seguir, serão descritas as etapas do projeto:

### Etapa 1: Otimização de Comunicação Assíncrona com Filas de Mensagens

- **Nome da ferramenta:** Amazon SQS (Simple Queue Service)
- **Foco da ferramenta:** Desacoplamento de sistemas e processamento de pedidos. O Amazon SQS é um serviço de enfileiramento de mensagens totalmente gerenciado que permite o desacoplamento e a escalabilidade de microsserviços, sistemas distribuídos e aplicativos sem servidor. A principal vantagem é a transição de um modelo de custo fixo com servidores de mensagens para um modelo de pagamento por uso, eliminando custos com recursos ociosos.
- **Descrição de caso de uso:** Atualmente, a Abstergo Industries processa um grande volume de pedidos de diversas farmácias e empresas parceiras. Cada pedido inicia uma série de processos internos, como verificação de estoque, faturamento e logística. Com o SQS, cada pedido recebido via API ou portal B2B será colocado em uma fila como uma mensagem. Sistemas distintos e independentes podem então consumir essas mensagens para realizar suas tarefas específicas no seu próprio ritmo. Isso garante que nenhum pedido seja perdido durante picos de demanda e elimina a necessidade de manter servidores robustos (e caros) ligados 24/7 para processar essas solicitações, gerando uma redução de custos imediata com poder computacional.

### Etapa 2: Execução de Código sob Demanda sem Servidores

- **Nome da ferramenta:**  AWS Lambda
- **Foco da ferramenta:** Redução de custos computacionais e automação de processos. O AWS Lambda é um serviço de computação sem servidor que executa código em resposta a eventos e gerencia automaticamente os recursos computacionais subjacentes. A vantagem principal é pagar apenas pelo tempo de computação consumido, em milissegundos, em vez de pagar por servidores inteiros.
- **Descrição de caso de uso:** Diversas rotinas da Abstergo Industries, como a geração de relatórios de vendas para parceiros, a atualização de status de pedidos ou a validação de dados recebidos, não necessitam de um servidor dedicado operando continuamente. Com o AWS Lambda, essas tarefas podem ser reestruturadas como "funções". Por exemplo, uma função Lambda pode ser acionada automaticamente toda vez que um novo pedido é adicionado à fila do SQS (da Etapa 1) para iniciar o processo de validação de estoque. Outra função pode ser executada diariamente para consolidar os dados de vendas e enviá-los por e-mail aos parceiros. Isso elimina os custos associados a servidores que ficariam a maior parte do tempo ociosos, aguardando por essas tarefas.

### Etapa 3: Armazenamento Inteligente e Automatizado de Dados
- **Nome da ferramenta:**  Amazon S3 Intelligent-Tiering
- **Foco da ferramenta:** Otimização automática de custos de armazenamento de dados. O S3 é um serviço de armazenamento de objetos, e a classe de armazenamento "Intelligent-Tiering" monitora os padrões de acesso aos dados e move automaticamente os objetos entre diferentes camadas de acesso (de acesso frequente para acesso infrequente) para otimizar os custos de armazenamento sem impacto no desempenho ou sobrecarga operacional.
- **Descrição de caso de uso:** A Abstergo Industries armazena um grande volume de dados, como notas fiscais, receitas médicas digitalizadas, históricos de pedidos e contratos com parceiros. Muitos desses documentos são acessados frequentemente nos primeiros meses, mas depois raramente são consultados, sendo mantidos apenas por questões de conformidade e histórico. Utilizando o S3 Intelligent-Tiering, a empresa pode armazenar todos esses documentos em um único local. O serviço irá, de forma automática e sem necessidade de intervenção manual, mover os documentos mais antigos e menos acessados para uma camada de armazenamento de custo mais baixo. Isso resulta em uma economia significativa e contínua nos custos de armazenamento, especialmente à medida que o volume de dados cresce.


## Conclusão
A implantação das ferramentas AWS na empresa Abstergo Industries tem como esperado uma drástica redução nos custos operacionais, maior escalabilidade para suportar o crescimento e um aumento geral na eficiência. Embora todo projeto tecnológico apresente desafios, os principais riscos foram identificados e endereçados na Matriz de Riscos e Plano de Mitigação (Anexo 3), garantindo uma transição segura e controlada. Recomenda-se, portanto, a aprovação e continuidade do projeto, bem como a busca por novas tecnologias que possam melhorar ainda mais os processos da empresa.

## Anexos

- Anexo 1: *[Planilha de Estimativa de custos](/assets/Planilha%20de%20estimativa%20de%20custos%20AWS.xlsx)*
- Anexo 2: *[Diagrama da Arquitetura Proposta](/assets/diagrama_infra_aws.png)*
- Anexo 2.1: *[Descrição de Fluxo da Arquitetura Proposta](/assets/descricao_infra_aws.md)*
- Anexo 3: *[Matriz de Riscos e Plano de Mitigação](/assets/Matriz%20de%20Riscos%20e%20Plano%20de%20Mitigação.xlsx)*

Assinatura do Responsável pelo Projeto:

Amanda Talita P. Pellin

