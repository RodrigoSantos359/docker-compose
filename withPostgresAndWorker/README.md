## Sobre este setup

Este compose foi projetado para executar o n8n em um ambiente mais avançado, escalável e preparado para alta carga, utilizando PostgreSQL, Redis, workers dedicados e runners externos.

Diferente de instalações simples, este modelo utiliza o modo `queue` do n8n, permitindo separar a interface principal da execução dos workflows. Isso melhora desempenho, estabilidade e capacidade de processamento em ambientes com muitas execuções simultâneas.

O ambiente é dividido em múltiplos serviços especializados:

* PostgreSQL para persistência dos dados
* Redis para gerenciamento da fila de execuções
* n8n principal para interface e gerenciamento
* Workers dedicados para processar workflows em paralelo
* Runners externos para isolamento das execuções

### Principais objetivos deste setup

* Utilizar PostgreSQL como banco principal
* Utilizar Redis para gerenciamento de filas
* Executar workflows em modo distribuído (`queue mode`)
* Separar interface da execução dos workflows
* Melhorar desempenho em ambientes com alta carga
* Permitir múltiplos workers no futuro
* Melhorar estabilidade e tolerância a falhas
* Preparar ambiente para escalabilidade horizontal
* Reduzir impacto de workflows pesados na interface principal

### Estrutura dos serviços

#### PostgreSQL

Responsável pelo armazenamento persistente dos dados do n8n.

#### Redis

Gerencia as filas de execução dos workflows no modo queue.

#### n8n

Container principal responsável pela interface web, APIs e gerenciamento dos workflows.

#### n8n-worker

Worker dedicado para processar workflows em segundo plano.

#### n8n-runner

Executa workflows do container principal utilizando runners externos.

#### n8n-worker-runner

Executa workflows do worker utilizando runners externos.

### Benefícios deste modelo

* Melhor desempenho em execuções simultâneas
* Interface do n8n mais responsiva
* Maior estabilidade em workflows pesados
* Melhor aproveitamento de CPU e memória
* Escalabilidade horizontal com múltiplos workers
* Melhor isolamento entre interface e processamento
* Ideal para automações com IA e processamento intensivo
* Estrutura mais adequada para produção avançada

### Recursos utilizados

* PostgreSQL
* Redis
* Queue Mode
* Workers dedicados
* Runners externos
* Volumes persistentes Docker

### Indicado para

* Ambientes de produção avançados
* Alto volume de workflows
* Processamento paralelo
* Integrações com IA
* Grandes volumes de webhooks
* Execuções simultâneas intensivas
* Ambientes multiusuário
* Infraestruturas escaláveis


# n8n com PostgreSQL e Worker

Inicia o n8n com PostgreSQL como banco de dados, Redis para gerenciamento de filas e um Worker como um contêiner separado. Contêineres auxiliares para execução de tarefas estão incluídos para executar nós de código (JavaScript/Python), conforme exigido pelo n8n 2.0+.

## Iniciar

Para iniciar o n8n, basta executar o docker-compose com o seguinte comando na pasta atual.

**IMPORTANTE:** Mas antes disso, altere os usuários, senhas e tokens padrão no arquivo [`.env`](.env)!

``` docker compose up -d
```

Para interromper o processo, execute:

``` docker compose stop
```

## Configuração

O nome padrão do banco de dados, o usuário e a senha do PostgreSQL podem ser alterados no arquivo [`.env`](.env) no diretório atual.

O `RUNNERS_AUTH_TOKEN` no arquivo [`.env`](.env) é um segredo compartilhado usado para autenticação entre o n8n e os contêineres do executor de tarefas. Gere um valor aleatório seguro para uso em produção.