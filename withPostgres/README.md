## Sobre este setup

Este compose foi pensado para executar o n8n com PostgreSQL em um ambiente mais estável e preparado para produção, substituindo o SQLite padrão por um banco de dados dedicado.

O ambiente separa os serviços principais em containers independentes:

* PostgreSQL para persistência dos dados
* n8n para interface e gerenciamento dos workflows
* n8n Runners para execução externa dos fluxos

Esse modelo melhora confiabilidade, desempenho e escalabilidade em comparação com instalações simples usando apenas SQLite.

### Principais objetivos deste setup

* Utilizar PostgreSQL como banco principal do n8n
* Melhorar estabilidade e desempenho dos workflows
* Separar execução dos workflows usando runners externos
* Facilitar crescimento futuro da aplicação
* Persistir dados usando volumes Docker
* Preparar ambiente para automações mais pesadas
* Facilitar deploy em VPS com Docker Compose

### Estrutura dos serviços

#### PostgreSQL

Responsável pelo armazenamento dos workflows, credenciais, execuções e configurações do n8n.

#### n8n

Container principal da aplicação, responsável pela interface web e gerenciamento das automações.

#### n8n Runner

Executa workflows externamente, reduzindo carga no container principal e melhorando desempenho em execuções simultâneas ou tarefas pesadas.

### Benefícios deste modelo

* Mais confiável que SQLite
* Melhor desempenho em ambientes com muitos workflows
* Maior estabilidade em reinícios e atualizações
* Melhor suporte para automações com IA e processamento pesado
* Facilita futura escalabilidade horizontal
* Organização mais adequada para produção

### Indicado para

* Ambientes de produção
* VPS dedicadas
* Workflows intensivos
* Integrações com IA
* Ambientes com muitos webhooks
* Uso simultâneo por múltiplos usuários


## Iniciar

Para iniciar o n8n com o PostgreSQL, basta executar o comando a seguir no diretório atual:

**IMPORTANTE:** Mas antes disso, altere os usuários e senhas padrão no arquivo [`.env`](.env)!

```
docker-compose up -d
```

Para interromper o processo, execute:

```
docker-compose stop
```

## Configuração

O nome do banco de dados, o usuário e a senha padrão do PostgreSQL podem ser alterados no arquivo [`.env`](.env) no diretório atual.